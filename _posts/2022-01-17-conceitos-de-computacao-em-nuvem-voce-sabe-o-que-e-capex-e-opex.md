---
id: 964
title: '[Portuguese] Conceitos de Computação em Nuvem: Você sabe o que é CaPex e OpEx?'
date: '2022-01-17T12:03:40+11:00'
author: 'Leopoldo Cardoso'
layout: post
guid: 'https://azuretar.com/?p=964'
permalink: /conceitos-de-computacao-em-nuvem-voce-sabe-o-que-e-capex-e-opex/
categories:
    - '- Blogs in Portuguese'
    - Azure
tags:
    - azure
    - nuvem
---

Olá pessoal, espero todos estejam bem.

Prosseguindo com os conceitos de computação em nuvem, tema iniciado no último post, hoje vou falar de um assunto bastante importante na hora de pensar em migrar infraestrutura local (on premisse) para nuvem (cloud).

Quando falamos com o CEO de uma empresa em migrar nossa solução de servidor de arquivos local ou de backup para a nuvem, por exemplo, a primeira pergunta que escutamos é: Quanto isso vai me custar?

Pensando nisso, vou explicar para vocês o que é CapEx e OpEx. Após ler o conceito destes dois termos, vai ficar fácil convencer o seu CEO a migrar algumas soluções para nuvem.

**CAPEX** – **Capital Expenditure**

O Capital Expenditure, ou despesas de capital, representa investimentos ou desembolsos em bens de capital. Ocorre quando a empresa necessita adquirir bens utilizados na produção de outros itens, como equipamentos, máquinas e instalações da empresa. Geralmente o CapEx é pago no ato da compra e existe descontos de tributação a partir da depreciação dos bens. Como exemplo de CapEx podemos citar aquisição de computadores e impressoras.

**Vantagens e desvantagens do CapEx:**

- São compreendidos como investimento.
- Aumento do fluxo de caixa dos ativos.
- Retorno ao longo prazo.
- Depreciação dos bens adquirios.
- Dificuldade na aprovação dos gastos
- Altos custos a curto prazo.

**OpEx** – **Operational Expenditure**

O Operational Expenditure ou despesas operacionais, são pagamentos relativos à atividade de gestão empresaria, e vendas de produtos e serviços. O OpEx relaciona todos os custos operacionais como manutenção, salários dos funcionários, contratação de serviços, despesas de consumos entre outros. Para facilitar o entendimento podemos citar os serviços de assinatura de streaming nos quais os usuários pagam um valor por mês e tem acesso a um acervo de músicas ou filmes, onde o serviço continua ativo enquanto o pagamento é feito.

**Vantagens e desavantagens do OpEx:**

- Dedução na tributação do ano corrente.
- Facilidade de aprovação dos gastos.
- Maior flexibilidade dos custos, sem a necessidade de descapitalização.
- Adaptação a mudanças no mercado.
- São compreendidos como despesas e não investimento.
- Possibilidade de altos custos a longo prazo.
- Maior inconstância.

Trazendo os conceitos do mercado financeiro para o setor de tecnologia, temos os seguintes exemplos:

Quando estamos comprando, um computador para funcionalidade de servidor de arquivos, temos o custo de ***CapEx***, visto que é a compra de um equipamento que com o passar dos anos terá sua depreciação.

Quando contratamos um serviço de manutenção de computadores, temos o custo de ***OpEx*** já que pagamos pelo uso daquele serviço, o técnico vai até a empresa, realiza o reparo, é pago pelo serviço e a empresa só terá este custo novamente caso precise de um novo serviço.

**Modelo baseado em consumo**

Os provedores de serviços de nuvem operam em um modelo base em consumo, o que significa que os usuários finais só pagam pelos recursos que usam. com isso temos:

- Melhor previsão de custos
- São fornecidos os preços para serviços e recurso individuais
- A cobrança é baseada no uso real.

Para exemplificar todo o artigo vamos imaginar o seguinte cenário:

Você tem uma loja online de artigos infantis e historicamente durante os mês de Outubro, devido ao dia das crianças, é o período de maior tráfego de vendas. A infraestrutura do comércio eletrônico de sua loja é em seu data center e você está disposto a comprar mais servidores, já que no último ano você teve problemas com seu site fora do ar. Ao investir em novas máquinas você está tendo um custo de CapEx e após o mês de outubro aqueles computadores serão desligados e provavelmente estarão obsoletos no próximo ano.

Agora vamos imaginar o mesmo cenário, com a diferença que você não tem data center on premisse e toda sua infraestrutura está localizada na nuvem. No mês de Outubro, período de maior tráfego de vendas você pode configurar algumas máquinas sobressalentes para que estas possam ser ligadas automaticamente no momento que seu site de vendas apresentar um fluxo muito grande de acesso, desligando estas máquinas quando o número de requisições do seu site voltar ao fluxo normal. Neste caso você está tendo um custo de OpEx pagando apenas pelo uso nas horas utilizadas.

É isso pessoal, no próximo post continuarei trazendo conceitos de nuvem, falando um pouco dos serviços de nuvem.

Espero que tenham gostado do conteúdo e até o próximo post.

**Referências:**

- Material oficial Microsoft
- meupositivo.com.br
- diferenca.com