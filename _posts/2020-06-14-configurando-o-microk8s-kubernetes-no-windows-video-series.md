---
id: 390
title: '[Portuguese] Configurando o MicroK8s Kubernetes no Windows Video Series'
date: '2020-06-14T00:15:20+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=390'
permalink: /configurando-o-microk8s-kubernetes-no-windows-video-series/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - '- Blogs in Portuguese'
    - Kubernetes
    - Windows
    - WSL
---

Neste vídeo, Fernando Rolnik seguirá os passos do vídeo em inglês com o nosso Capitão [Nuno “WSL Corsair” do Carmo](https://twitter.com/nunixtech) e vai mostrar como instalar, configurar e rodar um pod no Canonical MicroK8s Kubernetes para Windows. A segunda parte mostrará como configurar um segundo node com o Multipass para Windows.

## Parte 1 – Instalando MicroK8s no Windows – Kubernetes deployment demo

Na primeira parte, você vai ver como instalar o MicroK8s para Windows, visualizar o Dashboard e como fazer um deployment.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/VLjPg5XicVI?feature=oembed" title="Instalando MicroK8s no Windows - Kubernetes deployment demo" width="500"></iframe></div></div></figure>1. [Download](https://github.com/ubuntu/microk8s/releases/download/installer-v2.0.0/microk8s-installer.exe) instale o MicroK8s para Windows, que inclui o Multipass.
2. Antes de criar a MicroK8s VM, abra o terminal como a administrator (Clique segurando CTRL + Shift) e verifique se o local driver do Multipass é o HyperV: `multipass get local.driver`
3. Caso precise alterar use: `multipass set local.driver=hyperv`
4. Cheque o status do MicroK8s com `microk8s status`
5. Habilite o DNS e o Dashboard: `microk8s enable dns dashboard`
6. Use `microk8s --help` para ver todos os comandos
7. Conecte ao Dashboard com`microk8s dashboard-proxy` e abra o seu navegador com o endereço e token que aparecerá na tela.
8. Faça o deployment do microbot `microk8s kubectl create deployment microbot --image=dontrebootme/microbot:v1`
9. Esponha o deployment com `microk8s kubectl expose deployment microbot --type=LoadBalancer --port 80 --name=microbot-service`
10. Use o comando `microk8s.exe kubectl port-forward -n default --address 0.0.0.0 service/microbot-service 80:80` para ter acesso ao pod.
11. Verifique o IP da microk8s-vm com `multipass list`
12. Abra o seu browser em` http://<microk8s-vm IP>/` para ver o robô.

## Parte 2 – Multinode MicroK8s Kubernetes Cluster no Windows e introdução ao Multipass

Nesta parte Fernando mostrara como instalar um segundo node MicroK8s usando o Canonical Multipass para Windows

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/VLjPg5XicVI?feature=oembed" title="Instalando MicroK8s no Windows - Kubernetes deployment demo" width="500"></iframe></div></div></figure>1. Verifique as VMs rodando com `multipass list`
2. Instale uma nova VM chamada microk8sn1 com Ubuntu Xenial `multipass launch --name microk8sn1 xenial`
3. Acesse a nova VM com `multipass shell microk8sn1`
4. Instale o Microk8s na VM com sudo snap install microk8s –classic
5. No Windows rode o comando microk8s.exe add-node para obter a credencial para conectar o nó.
6. Copie a linha após o Join Node with:
7. Volte na microk8sn1 e rode o comando copiado.
8. Verifique no Dashboard o novo nó funcionando.

#### **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik) [@jorgearteiro](https://twitter.com/jorgearteiro) [@nunixtech](https://twitter.com/nunixtech)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)