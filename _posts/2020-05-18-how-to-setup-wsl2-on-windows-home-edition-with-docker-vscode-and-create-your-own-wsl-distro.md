---
id: 262
title: 'WSL2 Video Series'
date: '2020-05-18T21:56:53+10:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=262'
permalink: /how-to-setup-wsl2-on-windows-home-edition-with-docker-vscode-and-create-your-own-wsl-distro/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - Windows
    - WSL
---

WSL2 – Windows Subsystem for Linux has finally arrived on Windows 10 Home Edition Build 2004.

The following three videos, presented by [Fernando Rolnik](https://twitter.com/fernandorolnik), [Jorge Arteiro](https://twitter.com/JorgeArteiro) and [Nuno do Carmo](http://twitter.com/nunixtech) will show:

1. How to Install WSL 2 and Windows Terminal on Windows 10 Home Edition
2. Setting up Docker Desktop and VSCode on WSL2 using Windows Home Edition
3. Create your own customized WSL2 Linux distro using Docker desktop on Windows 10 Home Edition

## **Part 1: How to Install WSL 2 and Windows Terminal on Windows 10 Home Edition**

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/_V6fStEa4YM?feature=oembed" title="How to Install WSL 2 and Windows Terminal on Windows 10 Home Edition" width="500"></iframe></div></div></figure>1. Install the new Terminal from Windows Store
2. Turn Windows Features on or off &gt; Enable: Virtual Machine Platform, Windows Hypervisor Platform, Windows Subsystem for Linux
3. Download the and install the [WSL 2 Linux Kernel](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) from [Microsoft](https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel)
4. Set WSL 2 as a default version with the command: wsl.exe –set-default-version 2
5. Install the Linux distro you want from the Windows Store
6. Use the command *wsl.exe –help* to learn more

## **Part 2: Setting up Docker Desktop and VSCode on WSL2 using Windows Home Edition**

This is part 2 of our WSL2 series talking about Setting up Docker Desktop using new WSL2 – Windows Subsystem for Linux and Installing VSCode with WSL2 and Docker extensions to enable WSL2 remote connection.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/1jH3nEzv8zk?feature=oembed" title="Setting up Docker Desktop and VSCode on WSL2 using Windows Home Edition" width="500"></iframe></div></div></figure>1. Download Docker Desktop for Windows from[ Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
2. Install the Docker Desktop for Windows, at the end logout and login in your computer
3. Right-click on the Docker icon by the clock, Resources, WSL Integration and select your Linux Distros
4. Download [Visual Studio Code](https://code.visualstudio.com/download) from [Microsoft](https://code.visualstudio.com/download)
5. When VsCode starts, install the WSL Plugin
6. Connect in your Linux Distro with the button corner left button
7. Install the Docker plugin, using the blocks button on the left bar.

## ****Part 3: Create your own customized WSL2 Linux distro using Docker desktop on Windows 10 Home Edition****

[Nuno “WSL Corsair” do Carmo](https://twitter.com/nunixtech), our Microsoft MVP for Windows insider and Docker Captain join us on part 3 of our WSL2 series with our panel:[ Fernando Rolnik](https://twitter.com/fernandorolnik), Nuno do Carmo and[ Jorge Arteiro](https://twitter.com/nunixtech). Nuno is Deeping dive into WSL2 – Windows Subsystem for Linux with new Windows Terminal and Windows Home Edition. This video will show how to install your own customized WSL2 Linux distro using Docker desktop. As an example, we are using Clear Linux.

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/x43cm7TOKY0?feature=oembed" title="Create your own customized WSL2 Linux distro using Docker desktop on Windows 10 Home Edition" width="500"></iframe></div></div></figure>1. We are working from the directory C:\\wsldistros\\clearlinux
2. Run the container once to load it: *docker run clearlinux*
3. Use the command *docker container ls -a* to see the container name you’ve run
4. Export the container’s rootfs in a tar file: docker export -o clearlinux.tar.gz &lt;container name&gt;
5. Import the Distro to your WSL: wsl –import clearlinux C:\\wsldistros\\clearlinux C:\\wsldistros\\clearlinux\\clearlinux.tar.gz –version 2
6. Check with wsl.exe -l -v
7. To run use wsl.exe -d clearlinux

## **Part 4: Setting up Pengwin Linux on Windows WSL 2**

<figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/ARAXUgTDHB0?feature=oembed" title="Setting up Pengwin Linux on Windows WSL 2" width="500"></iframe></div></div></figure>PengWin is the first Linux distribution made specifically for Windows. It has menus to install and configure the most used Linux applications, organized by categories. It is ultra-intuitive. In this video, Fernando will setup up PengWin showing all intuitive menus while Nuno comments functionalities and interesting facts. Fernando will show how PengWin makes the DevOps life on Windows easy.

Learn more about the PengWin Linux distro on the [Whitewater Foundry Website](https://www.whitewaterfoundry.com/).

####  **Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar) [@fernandorolnik](https://twitter.com/fernandorolnik) [@jorgearteiro](https://twitter.com/jorgearteiro) [@nunixtech](https://twitter.com/nunixtech)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)