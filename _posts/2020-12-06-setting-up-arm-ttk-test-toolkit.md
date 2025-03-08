---
id: 679
title: 'Setting up ARM-TTK test toolkit'
date: '2020-12-06T23:30:00+11:00'
author: 'Fernando Rolnik'
layout: post
guid: 'https://azuretar.com/?p=679'
permalink: /setting-up-arm-ttk-test-toolkit/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - ARM
    - Automation
    - Azure
    - DevOps
---

Azure Resource Manager templates allow you to build resources in Azure in a repeatable way, many times you need, but while writing this resource, how can you ensure the code has no errors before you apply? How can you check if good practices are in place? How can you test it before the deployment? Azure Resource Manager Template Toolkit (ARM-TTK) can spot errors and bad practices. It acts as a linter for ARM templates. Today we have our Azuretar contributor Microsoft Azure MVP [Tao Yang](https://twitter.com/MrTaoYang) to introduce ARM-TTK, and of course, we have a demo!

<div class="wp-block-group is-layout-flow wp-block-group-is-layout-flow"><div class="wp-block-group__inner-container"></div></div><figure class="wp-block-embed-youtube alignleft wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/w3Ic7ZsYi70?feature=oembed" title="Setting up ARM TTK test toolkit" width="500"></iframe></div></div></figure>You can get ARM-TTK from Azure’s Github at <https://github.com/Azure/arm-ttk> ARM-TTK is also availiable on [GitHub Super Linter.](https://github.com/github/super-linter) Run ARM-TTK linter on your current folder using the Super Linter container on PowerShell with the following command:

`docker run -e RUN_LOCAL=true -v $pwd`:/tmp/lint github/super-linter`

From Linux bash run with:

`docker run --rm -e RUN_LOCAL=true -v $(pwd):/tmp/lint github/super-linter`

  
Stay tuned for the next videos.

**Follow us on Twitter**

[@azuretar](https://twitter.com/azuretar)[ ](https://twitter.com/drii_cavalcanti)[@MrTaoYang ](https://twitter.com/MrTaoYang)[@JorgeArteiro](https://twitter.com/JorgeArteiro) [@FernandoRolnik](https://twitter.com/fernandorolnik)

Subscribe the [Azuretar YouTube Channel](https://www.youtube.com/channel/UC3FS96NUdoR3DwkaDwiLdRw)