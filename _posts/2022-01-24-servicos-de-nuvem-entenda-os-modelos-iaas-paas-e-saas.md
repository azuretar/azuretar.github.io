---
id: 984
title: '[Portuguese] Serviços de Nuvem: Entenda os modelos IaaS, PaaS e SaaS.'
date: '2022-01-24T13:45:32+11:00'
author: 'Leopoldo Cardoso'
layout: post
guid: 'https://azuretar.com/?p=984'
permalink: /servicos-de-nuvem-entenda-os-modelos-iaas-paas-e-saas/
categories:
    - '- Blogs in Portuguese'
    - Azure
tags:
    - azure
---

Como já sabemos a cloud computing causou e continua causando uma transformação digital em várias empresas, sejam elas de tecnologia ou não.   
  
Apesar de ser bastante usual, a computação em nuvem ainda trás muitas dúvidas, principalmente para profissionais de TI que estão iniciando, já que cloud computing é um assunto grande que possui vários subtemas.

No último post falamos de um dos subtemas que trás dúvidas pra muita gente: CaPex e OpEx.

Neste post falaremos de outro subtema que trás dúvidas para os profissionais e estudantes da área: Modelos de Nuvem.

É comum vermos as siglas IaaS, PaaS e SaaS, mas o que isso significa?

Qual o melhor modelo a ser utilizado? Abaixo trarei uma breve explicação de cada modelo e ao final deste post, você irá decidir qual o melhor modelo para adotar como solução em cloud para sua empresa.

**IaaS – Infrastructure as a Service (Infraestrutura como serviço)**

No modelo IaaS, a empresa “constrói” toda sua infraestrutura de servidores de arquivos, backup, máquinas virtuais, na nuvem.

Imaginemos uma empresa que atualmente tem toda sua infraestrutura on-premises e deseja realizar migração pra nuvem. Na infraestrutura on-premises esta empresa tem as seguintes soluções:

- Servidor de AD;
- File server (servidor de arquivos);
- Servidor de software de gestão; e
- Backup.

Utilizando o modelo IaaS, posso fazer a migração para nuvem de toda essa infraestrutura da mesma forma que funciona on- premises contratando no fornecedor de nuvem que você escolher os seguintes recursos:

- Máquina virtual para instalação do servidor de AD;
- Máquina virtual para instalação e funcionamento do file server (servidor de arquivos);
- Máquina virtual para instalação do servidor do software de gestão; e
- Serviço de backup.

Além dos recursos citados acima toda infraestrutura de redes e sub redes podem e devem ser configuradas utilizando a rede virtual do seu fornecedor de nuvem.

No modelo IaaS, o departamento de TI da empresa que contratou o serviço, é responsável por toda configuração e atualização do sistema operacional e softwares instalados no servidor.

Mas na frente falaremos das responsabilidades de cada modelo.

<a> </a>

<figure class="wp-block-image size-full is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/image.jpg)<figcaption><span class="has-inline-color has-ast-global-color-0-color">\* Imagem material oficial Microsoft</span></figcaption></figure>**PaaS – Platform as a Service (Plataforma como Serviço)**

Neste modelo o seu fornecedor de nuvem oferece um ambiente para criação, teste e implantação de aplicativos de software.

No modelo PaaS o usuário não se preocupa com o gerenciamento de infraestrutura subjacente.

Vamos pensar no seguinte cenário: A empresa XYZ contrata uma equipe de desenvolvedores para desenvolver um aplicativo personalizado para sua empresa que funcionará na nuvem.

Utilizando o modelo PaaS, a equipe de desenvolvimento pode criar, hospedar e gerir esse aplicativo sem preocupações extras como instalação de softwares, atualizações entre outras preocupações do modelo on-premises.

No momento da contratação do modelo você informa qual SO você quer utilizar, qual linguagem de programação será utilizada para desenvolvimento, qual ferramenta será utilizada para gestão deste aplicativo, sem preocupações com updates de software, e outras manutenções que seriam necessárias no modelo on-premises.

<a> </a>

<figure class="wp-block-image size-full is-resized is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/image-1.jpg)<figcaption><span class="has-inline-color has-ast-global-color-0-color">\* Imagem material oficial Microsoft</span></figcaption></figure>**SaaS – Software as a Service (Software como Serviço)**

Neste terceiro modelo, os usuários se conectam e usam aplicativos com base em nuvem pela internet. Toda responsabilidade da infraestrutura por trás dos aplicativos utilizados é do fornecedor de nuvem. Todo usuário conhece, utiliza ou já utilizou SaaS. Usuários de aplicativos como OneDrive, Google Docs e Office 365 usam o modelo de serviço SaaS, já que todos funcionam dessa maneira.

<a> </a>

<figure class="wp-block-image size-full is-resized is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/image-2.jpg)<figcaption><span class="has-inline-color has-ast-global-color-0-color">\* Imagem material oficial Microsoft</span></figcaption></figure>Para facilitar o entendimento, segue imagem do material oficial da Microsoft sobre as responsabilidades de gerenciamento de cada modelo de computação

<figure class="wp-block-image size-large is-resized is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/image-4-1200x675.png)<figcaption><span class="has-inline-color has-ast-global-color-0-color">\* Imagem material oficial Microsoft</span></figcaption></figure>- No modelo on-premises (no local) você é responsável por toda infraestrutura desde o armazenamento, passando por rede, VMs, Sistema Operacional até os dados e acesso de informações.
- No modelo IaaS o provedor da nuvem é responsável pelo gerenciamento do armazenamento, rede e computação. Você gerencia todo o resto
- No modelo PaaS o usuário gerencia aplicativos, dados e acesso. Toda a parte de armazenamento, máquina virtual e sistema operacional é gerenciado pelo provedor de nuvem.
- No modelo SaS o usuário gerencia apenas o acesso.

É isso pessoal, no próximo post trarei informações de como usar portal de nuvem da Microsoft, o Microsoft Azure, o que é necessário para este cadastro, quais recursos são gratuitos e por quanto tempo podem ser utilizados desta forma.

Espero que tenham gostado e até o próximo post.

Fonte: Material oficial Microsoft

Leopoldo Cardoso

Azure Administrator | MCT Microsoft

- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/leopoldopcardoso/)