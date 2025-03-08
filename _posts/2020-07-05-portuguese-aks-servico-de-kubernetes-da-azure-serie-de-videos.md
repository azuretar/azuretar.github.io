---
id: 425
title: '[Portuguese] AKS (Serviço de Kubernetes da Azure) série de videos'
date: '2020-07-05T01:47:52+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=425'
permalink: /portuguese-aks-servico-de-kubernetes-da-azure-serie-de-videos/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - '- Blogs in Portuguese'
    - Azure
    - Containers
    - Kubernetes
---

Nesta série de videos Fernando Rolnik vai descomplicar o Kubernetes usando o [AKS (Serviço de Kubernetes da Azure)](https://azure.microsoft.com/pt-br/services/kubernetes-service/). Teremos introdução, deployment do AKS usando o portal Azure e a Azure Cli, tudo com a conta grátis da Azure. Depois teremos deployment de pods e serviços com comando, arquivo YAML, e em breve videos mais avançados.

## Parte 1 – Introdução ao AKS

<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow"><figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/CuRuKI0GaTs?feature=oembed" title="Kubernetes Introdução na Azure AKS Part 1 em Português" width="500"></iframe></div></div></figure>No primeiro vídeo teremos uma introdução ao AKS, incluindo:

- Arquiterura
- Componentes Básicos
- Node pools
- Ferramentas para trabalhar com AKS.

</div></div>## Parte 2 – Instalação do AKS no portal Azure e na CLI

Na segunda parte será feito o deployment do AKS através do portal Azure e da CLI.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/oFCIo_dtiR0?feature=oembed" title="Kubernetes instalação na Azure AKS Part 2 em Português" width="500"></iframe></div></div></figure>Comando para fazer o deploy através da Azure CLI

1. Primeiro crie um grupo de recursos com `az group create --name rg-azuretar-aks --location "Australia East"`
2. Crie o cluster AKS com duas VMs B2s (As mais baratas com 2 vCPU e 4GB RAM) , com monitoramento habilitado `az aks create --resource-group rg-azuretar-aks --name azuretar --node-vm-size Standard_B2s --node-count 2 --enable-addons monitoring --generate-ssh-keys`

## Parte 3 – Deployment na CLI

Agora configuraremos o kubectl e faremos deployment usando a command line

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/IEtSFveveTE?feature=oembed" title="Kubernetes CLI Deployment na Azure AKS Part 3 em Português" width="500"></iframe></div></div></figure>Comandos utilizados no video

1. Conceda as credenciais dos cluster para o kubectl com `az aks get-credentials --resource-group rg-azuretar-aks --name azuretar`
2. Cheque tudo o que o Kubernetes está rodando `kubectl get all`
3. Crie o deployment do http-server `kubectl create deployment http --image=katacoda/docker-http-server:latest`
4. Cheque os deployment que acabou de fazer `kubectl get deployments`
5. Descreva o deployment http `kubectl describe deployment http`
6. Cheque os pods rodando `kubectl get pod`
7. Encaminhe uma porta para testar a aplicação rodando no pod `kubectl port-forward <nome do pod> 5000:80`
8. Exponha o pod com um IP público `kubectl expose deployment http --port=80 --target-port=80 --type=LoadBalancer`
9. Veja o IP externo `kubectl get services`
10. Delete o que criou com `kubectl delete <nome do recurso>`, comece pelos deployments e services.

Aprenda mais sobre Kubernetes usando os tutoriais interativos do [Katakoda](https://www.katacoda.com/courses/kubernetes)

## Parte 4 – Deployment com YAML

A parte 4 mostrará como fazer deployment utilizando arquivo YAML.

Baixe os arquivos no [GitHub do Azuretar](https://github.com/azuretar/aks-video-series) `git clone https://github.com/azuretar/aks-video-series.git`

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/o89IV0LbZo4?feature=oembed" title="Kubernetes YAML Deployment na Azure AKS Part 4 em Português" width="500"></iframe></div></div></figure>Comandos utilizados no video

1. Cheque tudo o que o Kubernetes está rodando `kubectl get all`
2. Deployment do deployment.yaml `kubectl apply -f deployment.yaml`
3. Cheque tudo o que o Kubernetes está rodando novamente `kubectl get all`
4. Deployment do services.yaml `kubectl apply -f services.yaml`
5. Sempre que editar um arquivo YAML use `kubectl apply -f <nome do arquivo yaml>` para aplicar as novas definições.
6. Veja os pods com os nodes que estão rodando `kubectl get pods -o wide`
7. Carregue a pagina na CLI a cada 0.1 segundos `watch -n 0.1 curl http://<Endereço IP>`
8. Veja o status dos nodes `kubectl get nodes`
9. Delete o deployment.yaml `kubectl delete -f deployment.yaml`
10. Delete o services.yaml `kubectl delete -f services.yaml`

Baixe o [guestbook-all-in-one.yaml](https://raw.githubusercontent.com/kubernetes/examples/master/guestbook/all-in-one/guestbook-all-in-one.yaml) e o [azure-vote-all-in-one-redis.yaml](https://raw.githubusercontent.com/Azure-Samples/azure-voting-app-redis/master/azure-vote-all-in-one-redis.yaml).

Em breve novos videos neste post.

#### **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)