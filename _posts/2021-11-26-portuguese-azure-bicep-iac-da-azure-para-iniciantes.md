---
id: 787
title: '[Portuguese] Azure Bicep IaC da Azure para iniciantes'
date: '2021-11-26T23:56:36+11:00'
author: 'Edinaldo Oliveira'
layout: post
guid: 'https://azuretar.com/?p=787'
permalink: /portuguese-azure-bicep-iac-da-azure-para-iniciantes/
categories:
    - '- Blogs in Portuguese'
tags:
    - azure
    - iac
    - 'visual studio code'
---

Nesta postagem, iremos dar um *start* na utilização de Infraestrutura como Código, utilizando o Azure Bicep, para despertar a necessidade de utilização da IaC em ambientes de nuvem, no nosso caso, Microsoft Azure.

No vídeo abaixo, neste primeiro passo, iremos demonstrar a preparação de um ambiente de trabalho, para que possamos utilizar o Azure Bicep, com o Microsoft Visual Studio Code.

No segundo vídeo, falaremos sobre insfraestrutura como código (IaC) e faremos uma implementação prática, a partir do ambiente que preparamos no primeiro vídeo.

Preparando seu ambiente para IaC com Azure Bicep:

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/R-cWIzqCQ1Q?feature=oembed" title="Bicep - IaC na Azure - Ambiente de Desenvolvimento" width="500"></iframe></div></div></figure><span class="has-inline-color has-ast-global-color-0-color">**Links Utilizados:**</span>

- Microsoft Visual Studio Code: https://code.visualstudio.com/
- Azure Bicep: https://github.com/azure/bicep/releases
    - Observação: Podemos instalar o azure bicep via CLI, com os comandos:

*az bicep install  
az bicep upgrade*

- CLI: https://docs.microsoft.com/pt-br/cli/azure/install-azure-cli-windows?tabs=azure-cli
- Comandos az bicep: https://docs.microsoft.com/en-us/cli/azure/bicep?view=azure-cli-latest

**<span class="has-inline-color has-ast-global-color-0-color">Algun</span>**<span class="has-inline-color has-ast-global-color-0-color">**s comandos:**</span>

Instalação bicep via CLI:

*az bicep install  
az bicep upgrade*

No visual studio, para ativar extensão Bicep:  
*crtl+k crtl+m e escolher bicep*

**CONVERTER BICEP TO JSON**  
:entrar na pasta do bicep  
:az bicep build –file .\\arm.bicep

**Convert the ARM JSON to Bicep**  
az bicep decompile –file template.json

**IMPLEMENTAR BICEP NO AZURE**

- *abra powershell*
- *az login*
- *az group create -l eastus2 -n azuretarstolab  
    **para ler grupos** az group list –query “\[?location==’eastus2′\]”*
- *az deployment group create –resource-group azuretarstolab –template-file .\\arm.bicep*

Mas o que seria IaC e Bicep? Entenda melhor o assunto:

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><div class="ast-oembed-container " style="height: 100%;"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen="" frameborder="0" height="281" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" src="https://www.youtube.com/embed/2L5r0DlNJ1s?feature=oembed" title="Bicep - IaC na Azure para Iniciantes" width="500"></iframe></div></div></figure>Até a próxima.

<div class="wp-block-image is-style-rounded"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/11/WhatsApp-Image-2021-10-15-at-19.10.57-1-1200x1029.jpeg)<figcaption>**Edinaldo Oliveira** *System Administrator | Azure Administrator | MCT Microsoft*</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.23,5.924c-0.736,0.326-1.527,0.547-2.357,0.646c0.847-0.508,1.498-1.312,1.804-2.27 c-0.793,0.47-1.671,0.812-2.606,0.996C18.324,4.498,17.257,4,16.077,4c-2.266,0-4.103,1.837-4.103,4.103 c0,0.322,0.036,0.635,0.106,0.935C8.67,8.867,5.647,7.234,3.623,4.751C3.27,5.357,3.067,6.062,3.067,6.814 c0,1.424,0.724,2.679,1.825,3.415c-0.673-0.021-1.305-0.206-1.859-0.513c0,0.017,0,0.034,0,0.052c0,1.988,1.414,3.647,3.292,4.023 c-0.344,0.094-0.707,0.144-1.081,0.144c-0.264,0-0.521-0.026-0.772-0.074c0.522,1.63,2.038,2.816,3.833,2.85 c-1.404,1.1-3.174,1.756-5.096,1.756c-0.331,0-0.658-0.019-0.979-0.057c1.816,1.164,3.973,1.843,6.29,1.843 c7.547,0,11.675-6.252,11.675-11.675c0-0.178-0.004-0.355-0.012-0.531C20.985,7.47,21.68,6.747,22.23,5.924z"></path></svg><span class="wp-block-social-link-label screen-reader-text">Twitter</span>](https://twitter.com/Edinaldojr1981)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/edinaldo-oliveira-junior/)