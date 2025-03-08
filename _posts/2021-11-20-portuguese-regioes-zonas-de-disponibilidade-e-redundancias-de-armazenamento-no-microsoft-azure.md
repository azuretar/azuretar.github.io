---
id: 763
title: '[Portuguese] Regiões, zonas de disponibilidade e redundâncias de armazenamento no Microsoft Azure'
date: '2021-11-20T10:30:19+11:00'
author: 'Edinaldo Oliveira'
layout: post
guid: 'https://azuretar.com/?p=763'
permalink: /portuguese-regioes-zonas-de-disponibilidade-e-redundancias-de-armazenamento-no-microsoft-azure/
categories:
    - '- Blogs in Portuguese'
    - Azure
tags:
    - armazenamento
    - azure
    - storage
---

Um conceito muito básico, porém, de fundamental importância para quem está iniciando sua jornada na nuvem, e aqui vou focar no Microsoft Azure, é o conceito de regiões, zonas de disponibilidade e as possíveis redundâncias de armazenamento entre elas. Lembrando apenas que estes conceitos se aplicam em outras nuvens, apenas trocando algumas nomenclaturas, mas a base é a mesma.

## **Regiões**

Uma região é tida como um conjunto de data centers implantados em um perímetro definido por latência e conectados por meio de uma rede regional dedicada de baixa latência, ou seja, os data centers possuem uma distância mínima um do outro, ao mesmo tempo, que é interligado por uma rede de baixa latência, com a finalidade de manter a performance de rede entre estes data centers. O Azure oferece a flexibilidade de implantar aplicativos onde você precisa, incluindo entre várias regiões, para fornecer resiliência entre regiões.

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img01.jpg)</figure></div>Verifique as regiões atualizadas aqui: <https://infrastructuremap.microsoft.com/>

## **Zonas de Disponibilidades**

Uma Zona de Disponibilidade é uma oferta de alta disponibilidade que protege aplicativos e dados contra falhas de datacenter. As Zonas de Disponibilidade são locais físicos exclusivos em uma região do Azure. Cada zona é composta por um ou mais datacenters equipados com energia, resfriamento e rede independentes.

Para garantir a resiliência, há um mínimo de três zonas separadas em todas as regiões habilitadas. A separação física das Zonas de Disponibilidade dentro de uma região protege os aplicativos e dados contra falhas do datacenter.

## Relacionando Região x Zona

Observando a imagem abaixo, podemos ver que uma região é composta por zonas, conforme exemplo, na região 1, temos três zonas de disponibilidade (1,2 e 3).

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img02.png)</figure></div>## Qual a importância de escolher a região?

**<u>Principais pontos:</u>**

- **Custo:** o valor dos serviços variam conforme região, então, por exemplo, o custo de armazenamento em uma região, pode ser menor do que em outra. Podemos comparar isto utilizando a calculadora Azure ([clicando aqui](https://azure.microsoft.com/pt-br/pricing/calculator/)) ou utilizando o site [Azure Price](https://azureprice.net/), neste, acho muito legal a função de [cálculo médio por região](https://azureprice.net/region).

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img03.jpg)</figure></div>- **Serviços:** Além dos custos, devemos ficar atentos ao fato de que nem todas as regiões possuem todos os serviços disponíveis. Por exemplo: na região 1, temos tipos de máquinas virtuais que sejam mais específicas, que não vão ser encontradas na região 2, e isso vale para todos os serviços. Você pode consultar a lista de disponibilidade de serviços, por região, [aqui](https://azure.microsoft.com/pt-br/global-infrastructure/services/).
- **Latência:** Outro ponto importante a se considerar seria a latência, que a grosso modo, seria a velocidade de tráfego da sua localidade (seu cliente, por exemplo), para a região/data center escolhido, por exemplo: seu cliente possui sede no Brasil, então, se eu colocar a aplicação do mesmo na região do Brasil, a velocidade (latência), será menor do que colocar a aplicação em alguma região da europa. Podemos comparar as latências no site [Azure Speed ](http://www.azurespeed.com/)(com bastante tipos de testes) e um outro que tira uma média geral, o [Azure Speed Teste 2.0](https://azurespeedtest.azurewebsites.net/). Temos que avaliar os impactos da latência em nossa aplicação.
- **Conformidade:** Por último, temos que avaliar se os dados da nossa aplicação/cliente podem sair do país, então, este fator deve ser considerado.

Neste link, tem um vídeo que exemplifica esses conceitos de região e zonas de disponibilidade: <https://azure.microsoft.com/pt-br/global-infrastructure/availability-zones/#overview>

## Redundância Armazenamento Azure

Finalmente, como estes conceitos de região e zonas de disponibilidade se aplicam na redundância do armazenamento no Azure? Primeiramente, leve em conta os conceitos acima: qual região me dará o menor custo de armazenamento? A região possui todos os tipos de replicação? A latência vai atender? Os dados estão em conformidade?

Verificado estes passos, vamos ver os conceitos de replicação:

### **Redundância na região primária**

Os dados em uma conta de Armazenamento do Azure são sempre replicados três vezes na região primária. O Armazenamento do Azure oferece duas opções de como os dados são replicados na região primária:

O **armazenamento com redundância local (LRS)** copia seus dados de forma síncrona três vezes em um único local físico na região primária. LRS é a opção de replicação menos dispendiosa, mas não é recomendada para aplicativos que exigem alta disponibilidade ou durabilidade. Ou seja, ele replica tudo dentro do mesmo data center.

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img04.png)</figure></div>Verificando a estrutura acima, podemos perceber que no LRS temos três cópias do mesmo dado, DENTRO DO MESMO DATA CENTER. Nesta caso, estaríamos protegidos, por exemplo, para uma eventual queda de um *hack* ou máquina, porém, caso todo o data center/zona fique fora do ar, nossos serviços ficarão indisponíveis.

O LRS é uma boa opção para os seguintes cenários:

- Se seu aplicativo armazenar dados que possam ser facilmente reconstruídos, você pode optar por LRS.
- Se seu aplicativo estiver restrito a replicar dados somente em um país ou região devido a requisitos de governança de dados, você poderá optar pelo LRS.

O **Armazenamento com redundância de zona (ZRS)** copia seus dados de forma síncrona em três zonas de disponibilidade do Azure na região primária. Para aplicativos que exigem alta disponibilidade, a Microsoft recomenda usar o ZRS na região primária e também replicar para uma região secundária.

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img05.png)</figure></div>Já na estrutura acima, podemos notar que temos uma cópia de cada, das três, em um data center/zona separado, o que confere uma alta disponibilidade, pois neste caso, teria que cair toda uma região, para que nossos dados fiquem indisponíveis.

Entretanto, conforme citado acima, o ZRS não pode proteger seus dados contra um desastre regional em que várias zonas permanentemente são afetadas. Para proteção contra desastres regionais, a Microsoft recomenda o uso do [armazenamento com redundância de zona geográfica](https://docs.microsoft.com/pt-br/azure/storage/common/storage-redundancy#geo-zone-redundant-storage) (GZRS), que usa o ZRS na região primária e também replica geograficamente seus dados para uma região secundária.

O **armazenamento com redundância geográfica (GRS)** copia seus dados de forma síncrona três vezes em um único local físico na região primária usando o LRS. Em seguida, ele copia os dados de forma assíncrona para um único local físico na região secundária. Na região secundária, seus dados são copiados de forma síncrona três vezes usando o LRS.

O **armazenamento com redundância de zona geográfica (GZRS)** copia seus dados de forma síncrona em três zonas de disponibilidade do Azure na região primária usando o ZRS. Em seguida, ele copia os dados de forma assíncrona para um único local físico na região secundária. Na região secundária, seus dados são copiados de forma síncrona três vezes usando o LRS.

Com o GRS ou o GZRS, os **dados na região secundária não estão disponíveis para acesso de leitura ou gravação**, a menos que ocorra um failover na região secundária. **Para obter acesso de leitura para a região secundária, configure sua conta de armazenamento para usar o armazenamento com redundância geográfica com acesso de leitura (RA-GRS) ou o armazenamento com redundância de zona com acesso de leitura (RA-GZRS)**.

O diagrama a seguir mostra como os dados são replicados com o GRS ou com o RA-GRS:

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img06.png)</figure></div>O diagrama a seguir mostra como os dados são replicados com o GZRS ou com o RA-GZRS:

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img07.png)</figure></div>Resumindo:

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img08.jpg)</figure></div>É importante lembrar, que para aplicar os conceitos acima, devemos implementar o serviço que suporte tais replicações, conforme tabelas abaixo:

<div class="wp-block-image"><figure class="aligncenter size-full">![](https://azuretar.com/wp-content/uploads/2021/11/img09.jpg)</figure></div>Seguem links que foram fontes de consulta e que recomendo a leitura:

- Redundância do Armazenamento do Azure: https://docs.microsoft.com/pt-br/azure/storage/common/storage-redundancy
- Configurações de carga de trabalho SAP com zonas de disponibilidade do Azure: https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-ha-availability-zones#network-latency-between-and-within-zones
- Regiões e zonas de disponibilidade no Azure: https://docs.microsoft.com/pt-br/azure/availability-zones/az-overview#regions
- Produtos disponíveis por região: https://azure.microsoft.com/pt-br/global-infrastructure/services/

Até a próxima.

<div class="wp-block-image is-style-rounded"><figure class="aligncenter size-large is-resized">![](https://azuretar.com/wp-content/uploads/2021/11/WhatsApp-Image-2021-10-15-at-19.10.57-1-1200x1029.jpeg)<figcaption>**Edinaldo Oliveira** *System Administrator | Azure Administrator | MCT Microsoft*</figcaption></figure></div>- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.23,5.924c-0.736,0.326-1.527,0.547-2.357,0.646c0.847-0.508,1.498-1.312,1.804-2.27 c-0.793,0.47-1.671,0.812-2.606,0.996C18.324,4.498,17.257,4,16.077,4c-2.266,0-4.103,1.837-4.103,4.103 c0,0.322,0.036,0.635,0.106,0.935C8.67,8.867,5.647,7.234,3.623,4.751C3.27,5.357,3.067,6.062,3.067,6.814 c0,1.424,0.724,2.679,1.825,3.415c-0.673-0.021-1.305-0.206-1.859-0.513c0,0.017,0,0.034,0,0.052c0,1.988,1.414,3.647,3.292,4.023 c-0.344,0.094-0.707,0.144-1.081,0.144c-0.264,0-0.521-0.026-0.772-0.074c0.522,1.63,2.038,2.816,3.833,2.85 c-1.404,1.1-3.174,1.756-5.096,1.756c-0.331,0-0.658-0.019-0.979-0.057c1.816,1.164,3.973,1.843,6.29,1.843 c7.547,0,11.675-6.252,11.675-11.675c0-0.178-0.004-0.355-0.012-0.531C20.985,7.47,21.68,6.747,22.23,5.924z"></path></svg><span class="wp-block-social-link-label screen-reader-text">Twitter</span>](https://twitter.com/Edinaldojr1981)
- [<svg aria-hidden="true" focusable="false" height="24" version="1.1" viewbox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M19.7,3H4.3C3.582,3,3,3.582,3,4.3v15.4C3,20.418,3.582,21,4.3,21h15.4c0.718,0,1.3-0.582,1.3-1.3V4.3 C21,3.582,20.418,3,19.7,3z M8.339,18.338H5.667v-8.59h2.672V18.338z M7.004,8.574c-0.857,0-1.549-0.694-1.549-1.548 c0-0.855,0.691-1.548,1.549-1.548c0.854,0,1.547,0.694,1.547,1.548C8.551,7.881,7.858,8.574,7.004,8.574z M18.339,18.338h-2.669 v-4.177c0-0.996-0.017-2.278-1.387-2.278c-1.389,0-1.601,1.086-1.601,2.206v4.249h-2.667v-8.59h2.559v1.174h0.037 c0.356-0.675,1.227-1.387,2.526-1.387c2.703,0,3.203,1.779,3.203,4.092V18.338z"></path></svg><span class="wp-block-social-link-label screen-reader-text">LinkedIn</span>](https://www.linkedin.com/in/edinaldo-oliveira-junior/)