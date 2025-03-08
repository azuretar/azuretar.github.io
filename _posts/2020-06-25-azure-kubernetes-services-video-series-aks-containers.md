---
id: 416
title: 'Azure Kubernetes Services Video Series'
date: '2020-06-25T14:40:49+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=416'
permalink: /azure-kubernetes-services-video-series-aks-containers/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - AKS
    - Azure
    - Containers
    - Kubernetes
---

In this video series, [Jorge Arteiro](https://twitter.com/jorgearteiro) will introduce AKS, Azure Kubernetes Services to [Fernando Rolnik](https://twitter.com/fernandorolnik) and will show how to get start with valuable tips.

## Part 1 – Introduction to Azure Kubernetes Services

<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow"><figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/Cap8d3pfK_g?feature=oembed" title="Introduction to AKS Azure Kubernetes Services" width="500"></iframe></div></div></figure>In the first part, Jorge will introduce the Azure Kubernetes Services, including:

- Architecture
- Basic components
- Node pools
- Tools to work with AKS.

</div></div>## Part 2 – How to Install Azure Kubernetes Services including Demo

Part two will show how to create a Kubernetes cluster on Azure, using AKS. Jorge will explore all options on the portal. How to use the kubectl tool, what are namespaces, how to deploy a container, how to forward a port to the container, and how to expose the container with a public IP. When the pods and services start to run, we will check it using the monitoring dashboard.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/AFOSxedJPlU?feature=oembed" title="How to Install AKS Azure Kubernetes Services including Demo" width="500"></iframe></div></div></figure>Commands used on this video:

1. After create the service, get the credentials to your kubectl: `az aks --resource-group <Your Cluster RG> --name <Your Cluster Name>`
2. Check the context: `kubectl config get-contexts`
3. Check nodes: `kubectl get nodes`
4. Create a deployment: `kubectl create deployment microbot --image=dontrebootme/microbot:v1`
5. Check what K8s is running: `kubectl get all`
6. Check what is running on default namespace: `kubectl get all -n default`
7. Port Forward to access to a pod:` kubectl port-forward <Pod name> <LocalPort>:<RemotePort>`
8. Assign a public IP to the deployment:` kubectl expose deployment microbot --port=80 --target-port=80 --type=LoadBalancer`

#### **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik) [@jorgearteiro](https://twitter.com/jorgearteiro)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)