---
id: 398
title: 'Using Docker Desktop to run serverless Azure Container Instance ACI in 5 minutes'
date: '2020-07-12T19:11:00+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=398'
permalink: /azure-aci-integration-demo/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - ACI
    - Azure
    - Containers
    - Docker
---

[Fernando Rolnik](https://twitter.com/fernandorolnik) and [Jorge Arteiro](https://twitter.com/jorgearteiro) tried the new Docker functionality that allows running docker containers as Azure Container Instances (ACI) straight from your docker CLI. You only need an [Azure Account](https://azure.microsoft.com/en-us/free/), the [free account](https://azure.microsoft.com/en-us/free/) is suitable to test it.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/toysP8zeEKo?feature=oembed" title="Using Docker Desktop to run serverless Azure Container Instance ACI in 5 minutes" width="500"></iframe></div></div></figure>1. Download and install the latest Docker Desktop Edge (From 19.03.12)
2. `docker version` and check the version and Azure integration
3. `docker login azure` and login to your Azure account in your browser
4. `docker context create aci <context name> `to create your Azure context
5. Select the desired resource group
6. `docker context list `to see all contexts
7. `docker context use <context name>` to use your Azure context
8. From this point, you can run any container on Azure as you run in your machine, eg docker run
9. `docker ps` to check the container and the public IP
10. You can monitor your container from the [Azure Portal on the Container Instances blade](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerInstance%2FcontainerGroups).

#### **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik) [@jorgearteiro](https://twitter.com/jorgearteiro)