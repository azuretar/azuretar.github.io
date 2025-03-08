---
id: 874
title: '[Portuguese] Azure network security group, nosso pequeno guardião'
date: '2022-01-07T10:09:05+11:00'
author: 'Edinaldo Oliveira'
layout: post
guid: 'https://azuretar.com/?p=874'
permalink: /portuguese-azure-network-security-group-nosso-pequeno-guardiao/
categories:
    - '- Blogs in Portuguese'
    - Azure
tags:
    - azure
    - nsg
---

Um grupo de segurança de rede (ou NSG – Network Security Group) contém regras de segurança que permitem ou negam o tráfego de rede de entrada ou de saída em relação a vários tipos de recursos do Azure, permitindo aos administradores organizar, filtrar e rotear facilmente diferentes tipos de tráfego de rede. Então, qualquer rede virtual do Azure pode ser colocada em um grupo de segurança onde diferentes regras de entrada e saída podem ser configuradas para permitir ou negar certos tipos de tráfego. Para cada regra, você pode especificar origem e destino, porta e protocolo.

Quando estamos trabalhando com nuvens públicas e seus serviços, é de suma importância gerenciar bem este recurso de segurança, que de tão útil, por vezes, é chamado de “mini firewall”.

### Principais pontos referentes ao NSG:

- Limitar o tráfego de rede aos recursos em uma rede virtual
- Contém uma lista de regras de segurança que permitem ou negam tráfego de rede de entrada ou saída
- **<u>Pode ser associado a uma sub-rede ou interface de rede</u> (gravem bem esse ponto!!!)**

A criação do recurso é extremamente simples.

No campo de busca do portal do Azure, digite: network security group, o recomendado é escolher a versão mais atual (a clássica não é mais recomendada, salvo em cenários muito específicos)

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg01.png)</figure></div>Clique em “Create”

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg-2.png)</figure></div>Caso não tenha um grupo de recursos, crie um, clicando em “Create New” e após isto, informe o nome do NSG (aqui escolhemos “nsg-teste”

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg-3.png)</figure></div>Escolha as TAGS (ou deixe em branco)

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg04.png)</figure></div>Após isto, clicar em “Create”

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg05.png)</figure></div>## Regras de grupo de segurança de rede

Depois de criar o NSG, você poderá gerenciar suas regras individuais. Uma regra é usada para definir se o tráfego da rede é seguro e deve ser permitido ou negado pela rede.

Uma regra consiste nos seguintes componentes:

- **Nome –** um nome exclusivo que deve ser fácil para os administradores usarem para encontrar a regra;
- **Prioridade –** é um número inteiro entre 100 e 4096, que deve ser exclusivo. Este valor define a ordem de processamento da regra, com as regras contendo valores mais baixos (prioridade mais alta) sendo executadas primeiro. Ou seja, se uma regra de prioridade 100 permite acesso à porta 80, mesmo tendo uma regra de prioridade 200, negando acesso à porta 80, o acesso será concedido. Pense na prioridade como um lista com nomes de pessoas que vão entrar em uma festa, se ao olhar a lista, iniciando do primeiro nome e for na sequência, assim que encontrar o nome do convidado, o mesmo será autorizado a entrar na festa e o restante da lista não será mais conferido…seria mais ou menos assim que funciona a prioridade. No caso do exemplo da porta 80, se eu inverter a prioridade, no caso, 100 negando acesso à porta 80 e 200 permitindo acesso à porta 80, o acesso seria negado;
- **Origem ou destino –** este campo indica para quais aplicativos ou usuários a regra se aplica. Pode ser um endereço IP, intervalo de endereços IP ou recurso do Azure;
- **Protocolo –** O protocolo TCP, UDP ou ICMP que será analisado;
- **Direção –** indica se o tráfego é de entrada ou saída;
- **Intervalo de portas –** especifica para qual porta ou intervalo de portas a regra se aplica;
- **Ação –** Definir Permitir (o tráfego) ou Negar (e bloquear o tráfego) especificará a ação a ser executada pelo NSG quando o tráfego de rede correspondente à regra for identificado;

A tela inicial do NSG seria essa:

<figure class="wp-block-image size-large is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/nsg06-1200x687.png)</figure>Nestes campos destacados abaixo, podemos inserir as regras de entrada e saída, seguindo as regras mencionadas acima.

<figure class="wp-block-image size-large is-style-default">![](https://azuretar.com/wp-content/uploads/2022/01/nsg07-1200x312.png)</figure>No caso abaixo, estamos permitindo a porta 80, conforme exemplo acima.

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg08.png)</figure></div>No geral, configurar as regras é bastante simples, temos apenas que ficar atentos nas prioridades, para que não impacte no cenário real que desejamos.

Após criar o NSG com todas as suas regras, podemos associar o NSG diretamente na interface de rede de uma VM ou em uma sub-rede inteira. ATENÇÃO!! isto geralmente é questão de prova!! as vezes questionam se podemos associar em uma VNET, e não podemos!

Ainda no tema acima, o que ocorre se tivermos um NSG aplicado em uma sub-rede, com duas VMS, e uma destas VMs tenha um outro NSG associado diretamente na interface de rede?

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg09.png)</figure></div>## **Tráfego de entrada**

Em relação ao tráfego de entrada, o Azure processa as regras em um grupo de segurança de rede associado a uma sub-rede em primeiro lugar, se houver uma, e, em seguida, as regras em um grupo de segurança de rede associado ao adaptador de rede, se houver um.

- **VM1**: as regras de segurança no *NSG1* são processadas, já que estão associadas à *Subnet1* e a *VM1* está na *Subnet1*. A menos que você tenha criado uma regra que permite a entrada pela porta 80, o tráfego será negado pela regra de segurança padrão [DenyAllInbound](https://docs.microsoft.com/pt-br/azure/virtual-network/network-security-groups-overview#denyallinbound) e nunca será avaliado pelo *NSG2*, já que o *NSG2* está associado ao adaptador de rede. Se *NSG1* tem uma regra de segurança que permite a porta 80, o tráfego é processado por *NSG2*. Para permitir a porta 80 para a máquina virtual, tanto *NSG1* quanto *NSG2* devem ter uma regra que permite a porta 80 da Internet.
- **VM2**: as regras no *NSG1* são processadas porque a *VM2* também está na *Subnet1*. Já que a *VM2* têm um grupo de segurança de rede associado a seu adaptador de rede, ela recebe todo o tráfego permitido pelo *NSG1* ou tem todo o tráfego negado por *NSG1* também negado. O tráfego é permitido ou negado para todos os recursos na mesma sub-rede quando um grupo de segurança de rede está associado a uma sub-rede.
- **VM3**: já que não há nenhum grupo de segurança de rede associado à *Subnet2*, o tráfego é permitido para a sub-rede e processado pelo *NSG2*, pois o *NSG2* está associado ao adaptador de rede anexado à *VM3*.
- **VM4**: o tráfego é permitido para a *VM4* porque um grupo de segurança de rede não está associado à *Subnet3* ou ao adaptador de rede na máquina virtual. Todo o tráfego será permitido por meio de um adaptador de rede e sub-rede se não tiver um grupo de segurança de rede associado a eles.

## **Tráfego de saída**

Em relação ao tráfego de saída, o Azure processa as regras em um grupo de segurança de rede associado a um adaptador de rede em primeiro lugar, se houver um, e, em seguida, as regras em um grupo de segurança de rede associado à sub-rede, se houver uma.

- **VM1**: as regras de segurança no *NSG2* são processadas. A menos que você crie uma regra de segurança que nega a porta 80 de saída para a Internet, o tráfego será permitido pela regra de segurança padrão [AllowInternetOutbound](https://docs.microsoft.com/pt-br/azure/virtual-network/network-security-groups-overview#allowinternetoutbound) tanto no *NSG1* quanto no *NSG2*. Se *NSG2* tem uma regra de segurança que nega a porta 80, o tráfego é negado e nunca é avaliado pelo *NSG1*. Para negar a porta 80 na máquina virtual, um ou ambos os grupos de segurança da rede devem ter uma regra que nega a porta 80 para a Internet.
- **VM2**: todo o tráfego é enviado por meio do adaptador de rede na sub-rede, uma vez que o adaptador de rede conectado à *VM2* não tem um grupo de segurança de rede associado a ele. As regras no *NSG1* são processadas.
- **VM3**: se *NSG2* tem uma regra de segurança que nega a porta 80, o tráfego é negado. Se *NSG2* tem uma regra de segurança que permite a porta 80, está tem permissão de saída para a Internet, uma vez que um grupo de segurança de rede não está associado à *Subnet2*.
- **VM4**: todo o tráfego é permitido da *VM4*, pois um grupo de segurança de rede não está associado ao adaptador de rede anexado à máquina virtual, ou para a *Subnet3*.

Então, no caso de NSGs sobrepostos, como no exemplo acima, temos que observar se um deles bloqueia o acesso ou se ambos permitem o acesso…simplificando, seria isso. Por exemplo, no cenário acima: digamos que tenha quatro servidores WEB, na mesma sub-rede, e eu libere a porta 80, no NSG, para esta sub-rede, para que obviamente, consigam acessar o site hospedado nestes quatros servidores. Porém, caso eu queira que apenas um destes servidores para de receber requisições na porta 80, digamos que, para alguma atualização no site, posso implementar um NSG associado diretamente na interface de rede desta VM que hospeda o site, bloqueando a porta 80, e pronto, ninguém terá mais acesso a ela nesta porta.

Abaixo, temos uma questão que pode abordar este tipo de situação:

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg-10.jpg)</figure></div>O cenário acima seria mais ou menos isso (desculpem o desenho):

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg11.jpg)</figure></div>NSG-Subnet1 contém as regras padrões, que são criadas no momento que criamos o NSG. Veja aqui quais são elas: <https://docs.microsoft.com/pt-br/azure/virtual-network/network-security-groups-overview#default-security-rules>

NSG-VM1 possui regras específicas, conforme elencado na questão.

A VM1 contém ip público, então, ao final da questão, de acordo com o cenário, questiona-se se será possível acessar a VM pela porta 3389 (RDP).

Verifiquem que a questão altera as regras padrões do NSG-Subnet1, permitindo o acesso à porta 3389 via protocolo TCP. Neste ponto temos as duas regras permitindo acesso à porta 3389, porém, NSG-Subnet1 utilizando o protocolo TCP (ok neste caso), mas o NSG-VM1 utilizando protocolo UDP (o que não daria acesso), então, se a questão encerrasse desta forma, NÃO IRIÁMOS CONSEGUIR ACESSO RDP, via ip público, na VM. Porém, no final da questão, informa que removemos o NSG-VM1 da interface da VM1, logo, teríamos apenas a regra de entrada, via ip externo, do NSG-Subnet1, logo, iríamos conseguir acessar a VM1 via RDP.

**\*RESPOSTA: SIM\***

Adicionando mais uma informação: neste cenário, poderíamos deixar a regra padrão do NSG-Subnet1, e não teríamos acesso via RDP externo (via ip público), porém, caso existisse outra VM (VM2), dentro da mesma subrede, iríamos conseguir o acesso RDP na VM1 sem problemas, pois a regra AllowVnetInBound permite esse acesso. Fiquem espertos!! Isto pode ser questão de prova.

<div class="wp-block-image is-style-default"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2022/01/nsg12.png)</figure></div>**Referência:**

<https://docs.microsoft.com/pt-br/azure/virtual-network/network-security-groups-overview>

<https://docs.microsoft.com/pt-br/azure/virtual-network/network-security-group-how-it-works>

É isto! Até a próxima!

<div class="wp-block-image is-style-rounded"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/11/WhatsApp-Image-2021-10-15-at-19.10.57-1-1200x1029.jpeg)<figcaption>**Edinaldo Oliveira** *System Administrator | Azure Administrator | MCT Microsoft*</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.23,5.924c-0.736,0.326-1.527,0.547-2.357,0.646c0.847-0.508,1.498-1.312,1.804-2.27 c-0.793,0.47-1.671,0.812-2.606,0.996C18.324,4.498,17.257,4,16.077,4c-2.266,0-4.103,1.837-4.103,4.103 c0,0.322,0.036,0.635,0.106,0.935C8.67,8.867,5.647,7.234,3.623,4.751C3.27,5.357,3.067,6.062,3.067,6.814 c0,1.424,0.724,2.679,1.825,3.415c-0.673-0.021-1.305-0.206-1.859-0.513c0,0.017,0,0.034,0,0.052c0,1.988,1.414,3.647,3.292,4.023 c-0.344,0.094-0.707,0.144-1.081,0.144c-0.264,0-0.521-0.026-0.772-0.074c0.522,1.63,2.038,2.816,3.833,2.85 c-1.404,1.1-3.174,1.756-5.096,1.756c-0.331,0-0.658-0.019-0.979-0.057c1.816,1.164,3.973,1.843,6.29,1.843 c7.547,0,11.675-6.252,11.675-11.675c0-0.178-0.004-0.355-0.012-0.531C20.985,7.47,21.68,6.747,22.23,5.924z"></path></svg><span class="wp-block-social-link-label screen-reader-text">Twitter</span>](https://twitter.com/Edinaldojr1981)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/edinaldo-oliveira-junior/)