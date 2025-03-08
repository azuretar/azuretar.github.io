---
id: 443
title: '[Portuguese] Criar o menu do KDE Fedora Remix na barra de tarefa do Windows'
date: '2020-07-05T14:47:12+10:00'
author: 'Rodrigo Lira'
layout: post
guid: 'https://azuretar.com/?p=443'
permalink: /criar-o-menu-do-kde-fedora-remix-na-barra-de-tarefa-do-windows/
site-sidebar-layout:
    - default
site-content-layout:
    - default
theme-transparent-header-meta:
    - default
categories:
    - '- Blogs in Portuguese'
    - Linux
    - Windows
    - WSL
tags:
    - Fedora
    - 'Fedora Remix'
    - KDE
    - Linux
    - Windows
    - 'Windows 10'
    - WSL
    - WSL2
---

Salve Salve Pessoal!  
Nesse post vou mostrar como podemos criar o menu do **KDE** do nosso **Fedora Remix** na barra de tarefas do Windows.  
Se você não leu o meu post sobre **[Windows 10 + WSL2 + Fedora Remix + KDE + X410](https://azuretar.com/portuguese-windows-10-wsl2-fedora-remix-kde-x410/)** eu sugiro que leia, pois esse post é basicamente uma continuação dele.

Nesse post do link acima mostrei como podemos fazer a instalação do ambiente gráfico do **KDE** no **Fedora Remix**, porém para abrir uma aplicação com ambiente gráfico é necessário abrir todo o ambiente gráfico do KDE.  
Para resolver esse problema existe um projeto chamado **WSL Windows Toolbar Launcher**.  
Esse script cria um menu na **Barra de Tarefas do Windows** baseado no **Menu do KDE**, como na imagem abaixo:

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/001.png)</figure></div>Vamos logo ao que interessa! 😀  
Inicie seu Fedora Remix com o KDE instalado e digite o seguinte comando:

```
# pip install wsl-windows-toolbar CairoSVG
```

Agora precisamos executar o script:

```
# wsl-windows-toolbar
```

Por padrão ele procura o menu do gnome e acaba apresentando um erro, como na imagem abaixo:

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/002.png)</figure></div>Então precisamos informar o caminho completo para nosso menu KDE, é basicamente o mesmo:

```
# wsl-windows-toolbar -f /etc/xdg/menus/applications.menu
```

Apos executar o comando pressione **ENTER** para continuar.

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/003.png)</figure></div>Ao final do processo ele informa o procedimento para criação do menu no windows, como mostra a imagem abaixo.

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/004.png)</figure></div>No Windows clique com o botão direito na **barra de tarefas**, depois navegue até **Barra de ferramentas** &gt; **Nova barra de ferramentas**.

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/005.png)</figure></div>Na janela que se abre só digitar o seguinte caminho.

```
%USERPROFILE%\.config\wsl-windows-toolbar-launcher\menus\WSL
```

E depois clicar em **Selecionar pasta**.

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/006-1200x549.png)</figure></div>Pronto, o menu é criado automaticamente na barra de tarefas do Windows, agora só se divertir com essa facilidade.

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/007.png)</figure></div>Abrindo o **Konsole** por exemplo ele só abrirá a janela dele sem precisar abrir todo o KDE, vejam a imagem abaixo:

<div class="wp-block-image"><figure class="aligncenter size-large">![](https://azuretar.com/wp-content/uploads/2020/07/008.png)</figure></div>**OBSERVAÇÕES:**  
Lembre-se que seu **servidor X** tem que estar em execução, no meu caso o **X410**.  
Para esse modo de usabilidade deixo o **X410** com a opção **Windowed Apps** definida por padrão.  
Pronto, espero que tenham gostado!  
Até o próximo post.  
😀  
Referência:  
<https://pypi.org/project/wsl-windows-toolbar/>