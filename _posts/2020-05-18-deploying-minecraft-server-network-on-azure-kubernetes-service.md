---
id: 156
title: 'Deploying Minecraft server network on Azure Kubernetes Service'
date: '2020-05-18T20:49:09+10:00'
author: Birkhoff
layout: post
guid: 'https://azuretar.com/?p=156'
permalink: /deploying-minecraft-server-network-on-azure-kubernetes-service/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - AKS
    - Azure
---

## Preface

Minecraft is a popular sandbox creating game that has been growing over the past few years. It is also under very active development and has a large community. We’ll demonstrate a way that deploys a mid-large scale Minecraft server network featuring BungeeCord (reverse proxy) and Paper(Spigot) servers. This blog post includes production-ready Dockerfiles and introductory Kubernetes concepts to help you get started. All of the code and configurations are placed in <https://github.com/azuretar/minecraft-server-on-k8s> and you are welcome to use them at your will. Make sure to clone it now if you want to get started right away.

## Creating Dockerfiles

First of all we need to create the Dockerfiles of the servers. I choose OpenJ9 as our JVM environment as it’s better on GC and crash handling IMHO. I’m also using [Paper](http://papermc.io) for the Minecraft server instead of [Spigot](http://spigotmc.org) because it has overall better performance. Using [gosu](https://github.com/tianon/gosu) here as well to de-elevate the user so we don’t encounter file permissions issues.

```
FROM adoptopenjdk:8-openj9 

ARG PAPER_URL=https://papermc.io/api/v2/projects/paper/versions/1.16.5/builds/446/downloads/paper-1.16.5-446.jar
ENV JAVA_ARGS ""
ENV SPIGOT_ARGS ""
ENV PAPER_ARGS ""

EXPOSE 25565

WORKDIR /data
VOLUME /data

ENV GOSU_VERSION 1.10
RUN set -ex; \
    \
    fetchDeps=' \
        ca-certificates \
        wget \
    '; \
    apt-get update; \
    apt-get install -y --no-install-recommends $fetchDeps; \
    rm -rf /var/lib/apt/lists/*; \
    \
    dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
    wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"; \
    \
    chmod +x /usr/local/bin/gosu; \
# verify that the binary works
    gosu nobody true; \
    wget -O /srv/paper.jar "${PAPER_URL}";

RUN java -jar /srv/paper.jar --version \
    && chmod 0444 /srv/paper.jar

RUN cd /srv \
    && java -jar paper.jar --version \
    && mv cache/patched*.jar paper.jar \
    && rm -rf cache \
    && chmod 444 /srv/paper.jar

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ADD data/* /data/

ENTRYPOINT ["/docker-entrypoint.sh"]
```

Notice that there’s also a `docker-entrypoint.sh` that we can do additional things before actually handing over the container to the Java process.

```
#!/bin/bash

# Ensure the user exists, otherwise creates it
USER_ID=${LOCAL_USER_ID:-9001}
id -u user &>/dev/null || useradd --shell /bin/bash -u $USER_ID -o -c "" -m user

export HOME=/home/user

# Accept Mojang EULA if the environment variable `eula` is true
[[ "$eula" ]] && echo "eula=true" > /data/eula.txt

# Ensure proper file permissions on the server data
chown -R user:user /srv
chown -R user:user /data

# Finally handing over the container to Java, while using gosu to de-elevate
exec /usr/local/bin/gosu user java $JAVA_ARGS -jar /srv/paper.jar $PAPER_ARGS $SPIGOT_ARGS $@
```

There’s a `data` directory too where you can add server configuration files to the image. For BungeeCord it’s basically the same. You can get all the files on our GitHub repository[ Azuretar/minecraft-server-on-k8s](https://github.com/azuretar/minecraft-server-on-k8s).

## Build and push the images to Azure Container Registry

```
$ docker login azuretar.azurecr.io
$ docker build ./bungeecord -t azuretar.azurecr.io/minecraft/bungeecord:latest
$ docker build ./paper -t azuretar.azurecr.io/minecraft/paper:latest
$ docker push azuretar.azurecr.io/minecraft/bungeecord:latest
$ docker push azuretar.azurecr.io/minecraft/paper:latest
$ az acr repository list --name azuretar
```

`minecraft/` here is a Namespace of ACR, you can check the related documentations here: <https://docs.microsoft.com/en-us/azure/container-registry/container-registry-best-practices#repository-namespaces>. TL;DR: it’s basically a prefix so that you can group images together.

You can learn more about how to use ACR at <https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-docker-cli>.

## Creating the Deployment

So, finally Kubernetes! It’s the hardest and most confusing part of this blog post, but I’ll explain how this works underneath the hood. Before showing you how the deployment configuration file looks like, I want to introduce you a couple of core concepts of Kubernetes:

- *Pods* are groups of same-purpose containers or apps. In this case, we will run 2 pods: *BungeeCord* pod and *Paper* pod. Each consists of one instance of the corresponding app. To define a pod, you need to define a `Deployment` in the deployment file, and in that section you can configure what should that pod consist.
- A *service* is where you publish your apps. Say if you’re running a pod that has the *app* label `nginx`, then you need to add another service that **selects** `nginx` app, and expose port `80` in the service config. There are several service types for you to choose for now, see <https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types>.

Either way, each *Pod*, *Service* or *Deployment* gets to have a name, under `metadata` &gt; `name`. Let’s get started.

The configuration file uses YAML, *YAML Ain’t Markup Language*. It’s a language commonly used for describing configurations and it does the job quite well. Let’s start with creating a BungeeCord *Deployment*:

```
---
apiVersion: v1
kind: Service
metadata:
  annotations:
    # https://docs.microsoft.com/en-us/azure/aks/static-ip#apply-a-dns-label-to-the-service
    service.beta.kubernetes.io/azure-dns-label-name: azuretar-minecraft
  name: bungee-lb
spec:
  type: LoadBalancer
  ports:
    - port: 25565
      targetPort: 25577 # On Bungeecord, it's 25577 by default
  selector:
    app: azuretar-bungeecord
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: bungeecord
  labels:
    app: azuretar-bungeecord
spec:
  selector:
    matchLabels:
      app: azuretar-bungeecord
  template:
    metadata:
      labels:
        app: azuretar-bungeecord
    spec:
      containers:
      - name: bungeecord # Pod name
        image: azuretar.azurecr.io/minecraft/bungeecord:latest
        imagePullPolicy: Always # Always re-pull the image when creating container
        tty: true # TTY and STDIN is required if you ever want to attach to the container
        stdin: true
        ports:
          - containerPort: 25565
```

At this point we’ve created a Bungeecord pod, deployment and service. We’re effectively running a load-balancer in front of our Bungeecord instances (pod). Using `service.beta.kubernetes.io/azure-dns-label-name` will allow us later connect to the load balancer on `azuretar-bungee.australiaeast.cloudapp.azure.com`.

Next up we need to run a Minecraft server instance, which I’ll use PaperMC here, a high performance Spigot fork.

```
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: minecraft-data-pvc
spec:
  # For `managed-premium`, check https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes
  storageClassName: managed-premium
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
---
apiVersion: v1
kind: Service
metadata:
  name: paper
spec:
  ports:
  - port: 25565 # Expose 25565 port on Paper container
  selector:
    app: azuretar-paper
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: paper
  labels:
    app: azuretar-paper
spec:
  selector:
    matchLabels:
      app: azuretar-paper
  template:
    metadata:
      labels:
        app: azuretar-paper
    spec:
      volumes:
        # Declare a Volume called `paper-worlds` that asks `minecraft-data-pvc` for a storage
        - name: paper-worlds
          persistentVolumeClaim:
            claimName: minecraft-data-pvc
      containers:
      - name: paper
        image: azuretar.azurecr.io/minecraft/paper:latest
        imagePullPolicy: Always
        tty: true
        stdin: true
        env:
          - name: eula
            value: "true" # Tells docker-entrypoint.sh to make the eula.txt file
        volumeMounts:
          - name: paper-worlds # Uses paper-worlds Volume to store the data in `/data/worlds` persistently
            mountPath: /data/worlds
```

In Kubernetes, if you want to make your data persistent over container life cycles, you need to give them a *VolumeMount*. In order to bind a *Volume* to a specific path on the container, a *Volume* entry in `spec` is required. In there we can specify which *PersistentVolumeClaim* to use. A *PersistentVolumeClaim* is like a Volume pool, you can ask it for a place to store your data if you need to.

Here, we’re making our world data (the map data which includes block, player states and some other things that you may find necessary to make persistent) persistent. Before that there’s an option in `bukkit.yml` that tells the Minecraft server to put all world data in a specific directory instead of spread in the server folder: <https://bukkit.gamepedia.com/Bukkit.yml#world-container>. In `bukkit.yml`, set `world-container` to `worlds` so all the worlds save in `worlds` directory and we can make world data persistent more conveniently.

At this point, if you have had any prior experience of Minecraft server management you might ask where do I edit my plugins/server configuration files? Well, in my humble opinion, we should put them in the images instead of volumes. After that send the image to staging server to test out if it runs properly, and ultimately roll them out to production servers.

## Linking Paper to Bungeecord

In Kubernetes, every Service defined in the Cluster is assigned a DNS name. In our case, the Paper pod DNS name in our cluster is `paper.default.svc.cluster.local`. For more information check out [https://kubernetes.io/docs/concepts/services-networking/dns-pod-service](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/). This is an example Bungeecord configuration:

```
server_connect_timeout: 5000
remote_ping_cache: -1
forge_support: false
player_limit: -1
permissions:
  default:
  - bungeecord.command.server
  - bungeecord.command.list
  admin:
  - bungeecord.command.alert
  - bungeecord.command.end
  - bungeecord.command.ip
  - bungeecord.command.reload
timeout: 30000
log_commands: false
network_compression_threshold: 256
online_mode: true
disabled_commands:
- disabledcommandhere
servers:
  lobby:
    motd: 'Paper Server Pod'
    address: paper.default.svc.cluster.local:25565 # The Paper pod connecting address
    restricted: false
listeners:
- query_port: 25577
  motd: 'Bungeecord - k8s' # The actual MOTD that shows on Minecraft client
  tab_list: GLOBAL_PING
  query_enabled: false
  proxy_protocol: false
  forced_hosts:
    pvp.md-5.net: pvp
  ping_passthrough: false
  priorities:
  - lobby
  bind_local_address: true
  host: 0.0.0.0:25577 # Listen on 0.0.0.0:25577
  max_players: 1
  tab_size: 60
  force_default_server: false
ip_forward: true # Forward IP addresses to backend servers
remote_ping_timeout: 5000
prevent_proxy_connections: false
groups:
  md_5:
  - admin
connection_throttle: 4000
connection_throttle_limit: 3
log_pings: false # this will spam console
```

## Deploy

Put these configuration together in 1 file. I’ll call it `minecraft.yml`. You can use `kubectl` to apply it straight away on AKS since we’ve set up the CLI environment already.

```
$ kubectl apply -f minecraft.yml
```

When running this command, *kubectl* will calculate differences between configuration changes, and send that to the Kubernetes API server. The Kubernetes Control Plane will then apply the changes to your infrastructure.

While the containers are being created, you can check how everything’s going by running:

```
$ kubectl get all
```

You can always get an overview of how your infrastructure is running by using that command. The output should be something like this:

```
NAME                              READY   STATUS    RESTARTS   AGE
pod/bungeecord-675b7dc7c4-c46zj   1/1     Running   0          9h
pod/paper-779c5ff8c-bq6gd         1/1     Running   0          9h

NAME                 TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)           AGE
service/bungee-lb    LoadBalancer   10.0.187.190   20.193.44.182   25565:30385/TCP   11d
service/kubernetes   ClusterIP      10.0.0.1       <none>          443/TCP           11d
service/paper        ClusterIP      10.0.22.61     <none>          25565/TCP         11d

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/bungeecord   1/1     1            1           9h
deployment.apps/paper        1/1     1            1           9h

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/bungeecord-675b7dc7c4   1         1         1       9h
replicaset.apps/paper-779c5ff8c         1         1         1       9h
```

At this point, Azure should’ve already pointed `azuretar-minecraft.australiaeast.cloudapp.azure.com` to the public IP address of our Bungeecord load balancer `20.193.44.182`, and the infrastructure is ready to go.

## Live!

The easiest way to test if everything is working properly is of course spinning up your Minecraft client and connect to it. In this case the address for connecting (i.e. the load balancer’s public host name.) is `azuretar-minecraft.australiaeast.cloudapp.azure.com`. To learn more of how this works, visit <https://docs.microsoft.com/en-us/azure/aks/static-ip#apply-a-dns-label-to-the-service>.

If you prefer CLI, you can use this awesome tool <https://github.com/Dinnerbone/mcstatus> to check the server status.

```
$ python3 -m pip install mcstatus
$ mcstatus azuretar-bungee.australiaeast.cloudapp.azure.com status
```

Congratulations on deploying a Minecraft infrastructure on the Azure Kubernetes Service. This is just the beginning. Kubernetes’ power is way beyond this! There is extensive documentation on Kubernetes concepts and usage on the official website: <https://kubernetes.io/docs>, and if you want to learn more about K8s, you should definitely check it out.