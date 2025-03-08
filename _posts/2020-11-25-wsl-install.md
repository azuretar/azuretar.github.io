---
id: 671
title: 'Install WSL2 and Ubuntu on Windows with a single command: wsl install'
date: '2020-11-25T18:00:06+11:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=671'
permalink: /wsl-install/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - Linux
    - Windows
    - WSL
---

We all love WSL2, but the installation process used to have several steps, as we showed here on [Azuretar previously](https://www.youtube.com/watch?v=_V6fStEa4YM). As promised on Microsoft Build 2020 now you can install WSL2 and Ubuntu with a single command. This feature is now available in preview Windows Insider. In the following videos, we will show the `wsl --install` command in action, on Windows Insider, builds 20241 and 20262/

<div class="wp-block-group"><div class="wp-block-group__inner-container is-layout-flow wp-block-group-is-layout-flow">## First attempt on Build 20241

</div></div><figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/MDCcquChxkE?feature=oembed" title="WSL --INSTALL Preview Build 20241+" width="500"></iframe></div></div></figure>In our first attempt, we tried the command on `wsl --install` Windows Insider Build 20241.

 It has enabled WSL2 and installed the Linux Kernel, which was a big improvment but we had to install a distro manually.

## Second attempt on Build 20262

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/XM0MDTyx-qA?feature=oembed" title="WSL --INSTALL Preview Build 20262+" width="500"></iframe></div></div></figure>Eventualy, we got the latest Windows Insider Build 20262, at the recording time and we tested again and it worked.

`wsl --install` enables WSL2, installs the kernel and installs the default distro Ubuntu.

Also, now you can install any distro available on Microsoft store with `wsl --install <distro>`

To check the available distros type `wsl --list --online`

After reboot the computer, type `wsl `on a terminal and wait a few seconds, you will see the distro windows starting the initial setup.

Thanks Microsoft WSL Team to make the WSL install process so easy.

#### **Follow us on Twitter**

[](https://twitter.com/azuretar)[@azuretar](https://twitter.com/azuretar) [](https://twitter.com/jorgearteiro)[@FernandoRolnik](https://twitter.com/fernandorolnik) [@JorgeArteiro](https://twitter.com/jorgearteiro)