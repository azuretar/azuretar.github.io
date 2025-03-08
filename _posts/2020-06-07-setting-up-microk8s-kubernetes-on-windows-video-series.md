---
id: 369
title: 'Setting up MicroK8s Kubernetes on Windows Video Series'
date: '2020-06-07T22:15:28+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=369'
permalink: /setting-up-microk8s-kubernetes-on-windows-video-series/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - Containers
    - Kubernetes
    - Windows
---

In this video series our Docker Captain, Microsoft MVP for Windows insider [Nuno “WSL Corsair” do Carmo](https://twitter.com/nunixtech) will show how to set up the MicroK8s Kubernetes on Windows, together with [Jorge Arteiro](https://twitter.com/jorgearteiro) and [Fernando Rolnik](https://twitter.com/fernandorolnik).

## Part 1 – Install and Config

This first part show how to download, install and config the Microk8s on Windows with Multipass, how to connect to the Kubernetes Dashboard and how to deploy a pod.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/EjZ4onyPXWI?feature=oembed" title="Setting up MicroK8s Kubernetes on Windows Part 1 - Install and Config" width="500"></iframe></div></div></figure>1. [Download](https://github.com/ubuntu/microk8s/releases/download/installer-v2.0.0/microk8s-installer.exe) and install the MicroK8s for Windows, it includes Multipass.
2. Before you create the MicroK8s VM, Open a terminal as administrator and check if your multipass localdriver is hyperv: `multipass get local.driver`
3. If you need to change it use: `multipass set local.driver=hyperv`
4. Use microk8s.exe status to check the status
5. Enable DNS and Dashboard: `microk8s.exe enable dns dashboard`
6. Use `microk8s.exe --help` to see all the commands
7. Connect to the Dashboard with `microk8s.exe dashboard-proxy` and open your browser using the supplied address and token
8. Deploy the microbot `microk8s.exe kubectl create deployment microbot --image=dontrebootme/microbot:v1`
9. Expose the deployment `microk8s.exe kubectl expose deployment microbot --type=LoadBalancer --port 80 --name=microbot-service` and check how to port forward on the next video.

## Part 1.1 – How to connect to a pod

In this 1.1 part, Fernando show how the microk8s.exe act as a proxy for the kubectl inside the Multipass MicroK8s VM and allow you easily port-forward to your pod from your Windows

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/nOdIp9MJ5Qs?feature=oembed" title="Setting up MicroK8s Kubernetes on Windows Part 1.1 - How to connect to a pod" width="500"></iframe></div></div></figure>1. Follow the steps from the previous video and expose the ports usinmg the command `microk8s.exe kubectl port-forward -n default --address 0.0.0.0 service/microbot-service 80:80`
2. Check the microk8s-vm IPv4 `multipass list`
3. Open your browser in `https://<microk8s-mv IPv4>/` to see the robot

## Part 2 – Multi-node

Now, Nuno will show how to deploy a second node on MicroK8s on Windows, using Multipass and cloud-init.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/ApQkX6ra3kM?feature=oembed" title="Setting up MicroK8s Kubernetes on Windows Part 2 - Multi-node" width="500"></iframe></div></div></figure>1. Check you have only one multipass instance: `multipass list`
2. You may use the cloud-init fike showed on the video to create the additional nodes, or you can create it and install manually following the instructions above:
3. Create a new node: `multipass launch --name microk8sNode1 focal`
4. Install Microk8s in the node: `multipass exec microk8sNode1 -- snap install microk8s --classic`
5. Add a node in your Windows Microk8s: `microk8s.exe add-node` and copy the output with the microk8s join command.
6. Run the join command on microk8sNode1: `multipass exec microk8sNode1 -- <Join command copied> `

#### **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik) [@jorgearteiro](https://twitter.com/jorgearteiro) [@nunixtech](https://twitter.com/nunixtech)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)