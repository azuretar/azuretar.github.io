---
id: 793
title: '[Portuguese] Suporte ao SFTP (Protocolo FTP Seguro) para Armazenamento de Blobs do Azure, como implementar?'
date: '2021-12-01T12:09:31+11:00'
author: 'Edinaldo Oliveira'
layout: post
guid: 'https://azuretar.com/?p=793'
permalink: /portuguese-suporte-ao-sftp-protocolo-ftp-seguro-para-armazenamento-de-blobs-do-azure-como-implementar/
site-sidebar-layout:
    - ''
site-content-layout:
    - default
ast-main-header-display:
    - ''
ast-hfb-above-header-display:
    - ''
ast-hfb-below-header-display:
    - ''
ast-hfb-mobile-header-display:
    - ''
site-post-title:
    - ''
ast-breadcrumbs-content:
    - ''
ast-featured-img:
    - ''
footer-sml-layout:
    - ''
theme-transparent-header-meta:
    - ''
adv-header-id-meta:
    - ''
stick-header-meta:
    - ''
header-above-stick-meta:
    - ''
header-main-stick-meta:
    - ''
header-below-stick-meta:
    - ''
categories:
    - '- Blogs in Portuguese'
    - Azure
tags:
    - azure
    - sftp
    - storage
---

Olá pessoal!

Hoje vamos fazer a implementação do SFTP, para armazenamento de Blobs do Azure, que é uma excelente solução FTP com segurança.

Documentação oficial sobre SFTP no Azure:

<https://docs.microsoft.com/PT-BR/azure/storage/blobs/secure-file-transfer-protocol-support>

<https://docs.microsoft.com/pt-br/azure/storage/blobs/secure-file-transfer-protocol-support-how-to>

Na primeira etapa, temos que habilitar o recurso, que ainda está em Preview:

<figure class="wp-block-image size-full is-resized is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/1.png)</figure>Selecione a assinatura:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/2.png)</figure>Em settings, escolha Preview features:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/3.png)</figure>Digite na busca SFTP:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/4.png)</figure>Observe que o status está como “Not registered”…marque a caixa de seleção e clique em registrar:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/5.png)</figure>Deve ficar com esse status:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/6.png)</figure>Agora vamos no serviço de Storage:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/7.png)</figure>Crie o Storage:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/8.png)</figure>## Disponibilidade regional

O suporte ao SFTP está disponível nas seguintes regiões:

- Centro-Norte dos EUA
- Leste dos EUA 2
- Leste dos EUA 2 EUAP
- EUA Central EUAP
- Leste do Canadá
- Canadá Central
- Europa Ocidental
- Norte da Europa
- Leste da Austrália
- Norte da Suíça
- Centro-Oeste da Alemanha
- Leste da Ásia
- França Central

Crie o storage, conforme exemplo abaixo e clique em Next:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/9.png)</figure>Marque as duas opções em destaque e clique em Next:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/10.png)</figure>Clique na aba Data Protection e desmarque as duas opções em destaque:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/11.png)</figure>Clique em Review + Create e depois “create”

Vá para o recurso:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/12.png)</figure>Crie um Container:

<figure class="wp-block-image size-large is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/13-1200x576.png)</figure>Vá em SFTP e crie um local user (em username, digite o nome do usuário (não tem vínculo com ad):

<figure class="wp-block-image size-large is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/14-1200x562.png)</figure>> O Armazenamento do Microsoft Azure não dá suporte à SAS (assinatura de acesso compartilhado) nem à autenticação do Azure AD (Azure Active Directory) para acessar o ponto de extremidade do SFTP. Em vez disso, você deve usar uma identidade chamada usuário local que pode ser protegida com uma senha gerada pelo Azure ou um par de chaves SSH (Secure Shell). Para conceder acesso a um cliente que se conecta, a conta de armazenamento deve ter uma identidade associada à senha ou ao par de chaves. Essa identidade é chamada de *usuário local*.

Selecione o container que criamos (ou crie um novo), escolha as permissões e em home directory, coloque o nome da pasta.

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/15.png)</figure>Será gerada uma chave de acesso, que tem que ser copiada agora, pois não aparecerá mais:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/16.png)</figure>Após isto, seu SFTP está criado!

Vamos testar o acesso. Baixe o aplicativo WINSCP:

[https://winscp.net/eng/docs/free\_sftp\_client\_for\_windows](https://winscp.net/eng/docs/free_sftp_client_for_windows)

Efetue a instalação padrão.

Vamos configurar a tela abaixo:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/17.png)</figure>Copie o usuário e cole no WINSCP:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/18.png)</figure>Cole a senha que você salvou anteriormente.

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/19.png)</figure>Clique em Login

Caso apareça a tela abaixo, clique em Yes

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/20.png)</figure>Pronto! Caso de um erro nesse momento, tente novamente a conexão:

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2021/12/21.png)</figure>Podemos conectar via sftp, no terminal também…mais detalhes aqui:

<https://docs.microsoft.com/pt-br/azure/storage/blobs/secure-file-transfer-protocol-support-how-to>

É isto! Até a próxima!

<div class="wp-block-image is-style-rounded"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/11/WhatsApp-Image-2021-10-15-at-19.10.57-1-1200x1029.jpeg)<figcaption>**Edinaldo Oliveira** *System Administrator | Azure Administrator | MCT Microsoft*</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.23,5.924c-0.736,0.326-1.527,0.547-2.357,0.646c0.847-0.508,1.498-1.312,1.804-2.27 c-0.793,0.47-1.671,0.812-2.606,0.996C18.324,4.498,17.257,4,16.077,4c-2.266,0-4.103,1.837-4.103,4.103 c0,0.322,0.036,0.635,0.106,0.935C8.67,8.867,5.647,7.234,3.623,4.751C3.27,5.357,3.067,6.062,3.067,6.814 c0,1.424,0.724,2.679,1.825,3.415c-0.673-0.021-1.305-0.206-1.859-0.513c0,0.017,0,0.034,0,0.052c0,1.988,1.414,3.647,3.292,4.023 c-0.344,0.094-0.707,0.144-1.081,0.144c-0.264,0-0.521-0.026-0.772-0.074c0.522,1.63,2.038,2.816,3.833,2.85 c-1.404,1.1-3.174,1.756-5.096,1.756c-0.331,0-0.658-0.019-0.979-0.057c1.816,1.164,3.973,1.843,6.29,1.843 c7.547,0,11.675-6.252,11.675-11.675c0-0.178-0.004-0.355-0.012-0.531C20.985,7.47,21.68,6.747,22.23,5.924z"></path></svg><span class="wp-block-social-link-label screen-reader-text">Twitter</span>](https://twitter.com/Edinaldojr1981)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/edinaldo-oliveira-junior/)