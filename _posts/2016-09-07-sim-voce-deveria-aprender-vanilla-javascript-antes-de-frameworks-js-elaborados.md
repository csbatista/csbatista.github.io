---
layout: post
title:  "Sim, você deveria aprender vanilla JavaScript antes de frameworks JS elaborados"
date:   2016-09-07 19:37:09 -0300
categories: js frameworks dicas tradução
tags: js frameworks tradução dicas opinião 
images: 
    - url: https://snipcartweb-10f3.kxcdn.com/media/9904/vanilla-js-before-js-frameworks-robot-story.jpg

lang: pt
ref: snipcart-post
---

O ano é 2013. Nosso pequeno time de desenvolvedores está quase lançando um dos seus projetos mais impressionantes ao cliente. Estou na minha mesa, passando pelos meus emails matinais. Meu parceiro entra pela porta do escritório:

"Algo tá errado com nosso app em Angular, cara. Eu recebo o erro _digest is already in progess_ por todo canto e não consigo descobrir o que tá acontecendo", ele diz, visivelmente nervoso.

Mas eu não estou nervoso, nem ao menos estressado. Eu sei exatamente onde começar a olhar, porque eu sei meu JavaScript.

E tudo isso graças a um pequeno robô. Sim, você leu certo: __um robô__.

<hr>

Vamos voltar para 2011.

Nessa época eu ainda era um estudante de engenharia de software com brilho nos olhos, alheio __As__ [urgências de programar no mundo real](https://snipcart.com/blog/guide-choosing-tech-stack-client-work). Eu era apaixonado por desenvolvimento back-end, e não tinha nenhum desejo de aprender vanilla JavaScript ou qualquer coisa relacionada.

Mas meus amigos e eu tivemos que construir um robô de tempo real orientado a tarefas para uma de nossas aulas.

<figure class="pic-post-center">
  <img src="https://snipcartweb-10f3.kxcdn.com/media/9904/vanilla-js-before-js-frameworks-robot-story.jpg" alt="A picture from Transformers movie">
  <figcaption> Nós demos o nome de Optimus Prime pro nosso robô e eventualmente vendemos para o Michael Bay pro seu filme Transformers.</figcaption>
</figure>

Rapidamente encontramos uma coisa nova bem legal chamada Node.js (uma olhada rápida na [documentação na época](https://nodejs.org/docs/v0.4.9/)). Nenhuma dependência elaborada, fácil geração de processos filhos, assíncrono e orientado a eventos... e muitas pessoas online dizendo que era muito f*da. Não tinhamos a menor ideia do que era JavaScript ou V8, mas ainda assim parecia uma boa escolha para o projeto do nosso robô.

Muitas pessoas me falaram para simplesmente achar uma biblioteca decente para meus casos de uso e aplicar um pouco de ctrl+c/ctrl+v para implementar a comunicação via socket. E eu poderia ter feito isso.

Mas eu não fiz. Apesar de não ter percebido na época, essa foi uma das melhores decisões que tomei no princípio da carreira.

Em vez disseo, eu comecei a ler ávidamente. Sobre programação assíncrona, a história do JavaScript, seus prós e contras, tudo. Porque eu queria __dominar os princípios fundamentais da linguagem do meu projeto__. E me tomou bastante tempo, café, cerveja e códigos de teste para chegar lá.

Entre gerenciar a impaciência dos meus colegas e criar uma base de código não tão enxuta mas funcional, __eu aprendi pra caramba__.

<hr>

Então, qual a questão aqui? É que __eu gastei tempo suficiente entendendo os princípios centrais do JavaScript antes de usar os atalhos oferecidos pelos framewords e bibliotecas de JS__. E porque isso é importante? Bem, é sobre isso que esse post quer falar: _não apenas fingir_.

<figure class="pic-post-center">
  <img src="https://snipcartweb-10f3.kxcdn.com/media/9901/pretending-vanilla-javascript-knowledge.jpg" alt="A picture from @iamdevloper">
  <figcaption> Fonte: o sempre engraçado <a href="https://twitter.com/iamdevloper" target="_blank" class="external-link">@iamdevloper</a>.</figcaption>
</figure>

<br>

#### Primeiro, o que quero dizer com "frameworks" JS?
Quando uso _framework_, eu coloco todos os Angular, React, Backbone, Ember, Knockout, Vue, Ext, jQuery, Meteor, Express, Koa, Total, Socket.io, e por aí vai, na mesma caixa. Sim, eu sei que alguns são bem diferentes. Sim, eu sei que alguns "não são bem um framework, mas mais uma biblioteca, e aliás, você viu essa thread no HN?".

Mas por favor, pelo bem desse artigo, vamos declará-los equivalentes em seu objetivo primário.

<br>

#### E para aqueles perguntando "O que é vanilla JavaScript?"

Vou pegar a resposta de [koenpeters no Stack Overflow](http://stackoverflow.com/questions/20435653/what-is-vanillajs):

> "VanillaJS é o nome usado para se referir ao uso de JavaScript puro, sem nenhuma biblioteca adicional como jQuery. As pessoas usam como uma piada para lembrar os outros desenvolvedores que muitas coisas podem ser feitas hoje em dia sem a necessidade de bibliotecas JavaScript adicionais."

Ou, nesse caso, sem frameworks elaborados adicionais.

<br>

#### Porque eu penso que frameworks JavaScript são incríveis

> "Frameworks JS te ajudam ao abstrair código difícil e complexo."

> "Frameworks JS te ajudam a entregar código mais rápido e aumentar a velocidade de desenvolvimento."

> "Frameworks JS te forçam a focar no valor do app ao invés da sua implementação."

Essas razões rapidamente aparecem quando discutimos sobre a popularidade dos frameworks JS. Mas, pra mim, elas são razões mais voltadas ao marketing do que a qualquer outra coisa. E eu não estou protestando contra frameworks aqui. Eu já usei vários deles durante minha carreira (veja a lista na seção anterior).

E eu acredito que o ponto mais valioso nos frameworks JavaScript é a _colaboração_. A interface consistente e seus métodos permitem que desenvolvedores, vamos dizer, do Canadá, Estados Unidos e Brasil possam entender um ao outro e trabalhar em conjunto.

Se você está construindo um app com [insira aqui seu framework favorito], quando chegar a hora, você vai conseguir encontrar um desenvolvedor experiente capaz de entrar no projeto com confiança. Ele ou ela será capaz de se envolver com as ferramentas sem a necessidade de que você explique cada parte da sua arquitetura de software.

Outro motivo chave para o uso de frameworks é _prática_. Eles fazem com que você pratique o tempo inteiro. E isso é bom, de verdade! Prática sempre leva a perfeição, não importa o que você está tentando alcançar.

<br>

#### Porque eu acredito que frameworks JS não TÃO sensacionais assim

Pessoas que trabalham na implementação de frameworks são todas talentosas - pelo menos a grande maioria delas. Eles fazem um trabalho incrível transformando coisas complexas em coisas fáceis (por exemplo fornecendo _router_ de forma incrivelmente simples no lado do cliente no IE6). Mas todos esses níveis de abstração podem se tornar _malvados_ bem rápido.

Em todo desenvolvimento de apps, chega um dia que algo não funciona como esperado, e você não sabe porque. É aí que você tem que começar a escavar. E quando você começar a pesquisar em código puramente JavaScript, mal documentado, complexo e genérico, __você vai precisar de conhecimento aprofundado de JavaScript__ para conseguir descobrir o que quer. Caso contrário, eu posso garantir que você vai perder todo o tempo precioso que você economizou ao usar seu precioso framework. Você pode até precisar comprar uma nova máquina de expresso para cumprir os prazos.

Como eu li em algum lugar uma vez: "Você não é um desenvolvedor Angular ou Express. Você é um __desenvolvedor__."

Claro, frameworks são úteis para pequenos times trabalhando em um mesmo app. Sim, eles vão te economizar um pouco de tempo (a não ser que você seja [viciado em refatoração](https://snipcart.com/blog/tips-on-code-refactoring-from-a-former-addict)). Mas e se você tiver mais de um time trabalhando em mais de um app? Você realmente acha que todos os líderes de projeto vão concordar em um único framework para o grupo inteiro de apps? E se um novo framework "popular" aparecer em 2017?

O problema é: o momento que você decide por um framework, você vai impactar _cada uma de suas futuras decisões de projeto_. E mais, você acorrenta seu time a uma tecnologia que provavelmente vai estar obsoleta logo. Essas coisas piram minha cabeça.

<br>

#### Como que aprender vanilla JavaScript antes de frameworks JS podem - e vão - te ajudar

JavaScript é agora [_a_ linguagem de programação para web](https://w3techs.com/technologies/details/cp-javascript/all/all). Entender seus princípios básicos de engenharia é fundamental se você quiser construir uma carreira em web. Especialmente se você estiver de olho na parte de front-end.

Nos últimos 5 anos, mais de 10 frameworks JS estiveram nas notícias. Adivinhe quantos vão fazer o mesmo nos próximos 5-10 anos? Se você está simplesemente _fingindo_ saber JavaScript, o motor que está por trás dessa revolução na web, como você vai conseguir acompanhar?

Simplesmente pense no que os "desenvolvedores jQuery" estão fazendo hoje: tentando se atualizar com Angular. Amanhã, eles vão estar tentando se atualizar com React. E o triste e depressivo ciclo infinito continua.

<figure class="pic-post-center">
  <img src="https://snipcartweb-10f3.kxcdn.com/media/9902/javascript-frameworks-popularity.png" alt="Tweet from @iamdevloper">
</figure>


Saber vanilla JavaScript vai fazer com que você realmente entenda - e até mesmo contribua para - os frameworks JS, e te ajudar a escolher o certo __quando você precisar__.

Pra mim, trouxe um tanto de coisas positivas:

- Me ajudou a entregar um conjunto de ferramentas ao cliente em um curtíssimo período de tempo para um app em Ember, sem saber nada sobre Ember.
- Consegui uma oferta de trabalho em um dos gigantes da tecnologia por causa de uma biblioteca bem simples que escrevi no meu tempo livre.
- Me ajudou a identificar bugs em implementações de bibliotecas e sugerir sugestões simples bem rápido.

<br>

#### Moral da história: Aprendendo vanilla JavaScript antes de frameworks JS

Então aqui está meu resumo para vocês:

- Se você não sabe os princípios básicos da web, eventualmente você vai acertar uma parede graças __a__ evolução da própria linguagem e a chegada constante de novos frameworks.
- Saber JS puro vai tornar você um engenheiro chave que pode resolver problemas complexos (raciocínio antes de pesquisas frenéticas).
- Vai te deixar versátil e produtivo, tanto no front-end quanto no back-end.
- Vai te dar as ferramentas para inovar, não apenas executar.
- Vai te guiar em quando usar _ou não_ um framework.
- Vai te dar um entendimento geral sobre como browsers e computadores funcionam.

Usar um framework JS com certeza pode te levar a algum lugar rápido. Mas não vai te levar longe se você não entender os conceitos principais por trás. Do mesmo jeito que aprender a tocar Wonderwall no violão não vai te ensinar como compor música, mas vai te dar uma razão para praticar.

E eu acredito fortemente que o principio de "aprender o básico e as raízes primeiro" se aplica para quase tudo em nossa vida. Desde a aprender uma nova linguagem de programação até a começar um novo esporte. Exige muita prática, mas uma vez que você adquire domínio, o que resta a fazer é ser criativo. E é aí que a verdadeira diversão começa.

<br>

#### Um pouco sobre começar com vanilla JS

Eu realmente espero que tenha convencido você a sujar as mãos com JavaScript puro. Então, se você quer ser f*da em desenvolvimento web e fazer isso, aqui está meu conselho:

> Sempre seja curioso, sempre leia o material fonte e sempre tente você mesmo.

E alguns conselhos mais específicos:

- Sempre que um novo framework ou biblioteca JS estiver popular no Echo JS, Hacker News ou GitHub, vai lá e leia os fontes.
- Sempre que você escrever um pedaço de código, tente pensar em uma solução com JavaScript puro que poderia solucionar suas necessidades ao invés de instantaneamente ir buscar uma biblioteca para integrar.
- Vá no Stack Overflow e se desafie a responder perguntas sobre vanilla JavaScript sozinho.

Claro, você deveria se inscrever em canais úteis como [Echo JS](http://www.echojs.com/), [JS news](https://news.js.org/), e [ECMAScript Daily](https://ecmascript-daily.github.io/).

por último mas não menos importante, você deveria também ler sobre a linguagem. Clássicos como [JavaScript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do) e a série de livros [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS) contém toneladas de valores e _insights_.

<br>
<hr>
<br><br>

#### Sobre o post

Essa é uma tradução livre do post ["Yes, You Should Learn Vanilla JavaScript Before Fancy JS Frameworks"](https://snipcart.com/blog/learn-vanilla-javascript-before-using-js-frameworks) publicado em 18 de agosto de 2016 por Francois-Xavier P. Darveau no [blog do Snipcart](https://snipcart.com/blog). 

O objetivo dessa iniciativa é disponibilizar conteúdo interessante de qualidade que existe por aí em português, para que todo mundo possa ter acesso :)














