---
layout: post
title:  "Texto com imagem animada usando CSS3"
date:   2016-09-02 19:37:09 -0300
categories: css3 animacao efeitos
tags: css3 efeitos animacao texto
images: 
    - url: ../foto_home.jpg

lang: pt
ref: text-image-animation
---

Nos últimos dias andei olhando alguns efeitos que eu poderia por em títulos só com CSS3, sem ter que usar JavaScript. Fiz algumas pens e fui testando combinações de efeitos, transforms e animações para criar diferentes efeitos. Até que cheguei nessa combinação aqui, que me deixou completamente apaixonada:

<br>
<p data-height="335" data-theme-id="0" data-slug-hash="jrOkBQ" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/jrOkBQ/">Animate text image fill</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
<br>

O resultado final vem da junção de duas coisas muito bacanas: animações em CSS3 com `keyframes` e o `background-clip`. Separadas, as duas já conseguem criar coisas muito legais e bonitas, mas nesse exemplo a junção das duas deu um efeito ainda mais legal, como se as árvores tivessem crescendo, sei lá.

Observação: o `background-clip` só é suportado por browsers que usam o `webkit` (então não funciona no Firefox e no IE). Mas no final dei algumas opções que podem ser usadas como alternativas para esses browsers.

<br>
O HTML é bem simples:

```html
<div class="container-text">
  Nature
</div>
```

Temos o div, onde colocaremos a imagem como plano de fundo e o texto que exibiremos. Isso é legal porque o texto continua selecionável, conseguimos copiar e colar pra onde quisermos :)

<br>
A magia acontece no CSS! Vamos por partes: 

```css
.container-text {
  background-image: url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);
  -webkit-text-fill-color: transparent;
  color: #FFFFFF;
  -webkit-background-clip: text;
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
}
```

Até aqui, temos um texto preenchido com a imagem, mas sem a animação. Para fazer isso, colocamos a imagem como background do div, colocamos a cor do texto como transparente, e usamos o `-webkit-background-clip` para que a imagem seja "cortada" de acordo com os limites do texto. Colocamos estilos de tamanho, padding e fonte para deixar tudo mais bonitinho e pronto! Temos um texto preenchido pela imagem. Observação: Para browsers que usam o webkit, então não faz diferença usar `-webkit-text-fill-color` ou `color`. Esses browsers vão olhar primeiro o `-webkit-text-fill-color` e caso ele não exista, olhar o `color`. Essa parte fica mais clara ao explicar as alternativas ao final do post.

<br>
Agora vamos adicionar a animação à nossa imagem!

```css
@keyframes filling {
  from{
    background-position: center 25%;
  }
  to {
    background-position: center 50%;
  }
}

.container-text {
  background-image: url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);
  -webkit-text-fill-color: transparent;
  color: #FFFFFF;
  -webkit-background-clip: text;
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
  animation: filling 3s ease forwards;
}
```

Primeiro usamos a regra `@keyframe` para criar uma animação. Nesse caso, dei o nome de filling para a animação, que vai do CSS presente em "from" pro CSS presente em "to". Nesse caso, a variação acontece no eixo Y do plano de fundo. A animação começa com o plano de fundo posicionado em 25% no Y (se a imagem tem 100px de altura, o fundo começa em 25px) e vai até 50%. Essa variação de posicionamento dá a impressão de estar descendo na imagem.

Depois, atribuimos a animação ao div que contém a imagem como plano de fundo. Usando o atributo `animation` chamamos a animação pelo nome definido, passamos o tempo que ela vai durar, a curva de velocidade e o estado do elemento quando a animação tá inativa. Nesse caso, a animação dura 3s e o valor `ease` indica que ela começa devagar, acelera um pouco e depois diminui a sua velocidade. O valor `forwards` define que a animação deve, ao final, ficar da maneira como terminou. 

TCHARAAAAN! TERMINAMOS! Fácil né?

<br>
Agora vamos ver nossas opções quanto aos browsers que não usam o `webkit`. Nesses browsers o "corte" do plano de fundo pelo texto não funciona, então de todo jeito seu texto ficará de uma cor só, e não será preenchido pela imagem. Então aqui, sem usar JavaScript, temos duas opções:

<br>
####Opção 1:
__Browsers com webkit:__ efeito e animação como no exemplo <br>
__Browsers sem webkit:__ texto de cor única com background do div animado

Nesse caso, o código fica como está. Nos browsers sem suporte teremos um texto de cor única e o backgorund vai preencher o div e ser animado por trás do texto. Fica bem legal dependendo de onde o texto vai ficar. Abaixo uma simulação de como ficaria:

<br>
<p data-height="265" data-theme-id="0" data-slug-hash="WGNLwR" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/WGNLwR/">Animate text image fill - simulation for non Webkit browsers</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<br>

####Opção 2:
__Browsers com webkit:__ imagem preenche o texto, mas sem animação <br>
__Browsers sem webkit:__ texto de cor única sem background no div

Caso não seja possível ter a imagem ocupando div inteiro, a solução seria fazer com que o plano de fundo só fosse aplicado em browsers que usam o webkit. Para isso, colocamos '-webkit-linear-gradient(transparent, transparent)' antes da url do background. Assim, o browser entende o plano de fundo como um gradiente, que só é suportado no webkit, e portanto ignora. Nesse caso, ao ignorar os outros atributos webkit, teremos apenas um texto com a cor definida em `color`. O problema dessa opção é que gradientes não podem ser animados. Nesse caso então, teríamos que abrir mão da animação e posicionar o plano de fundo em um ponto só. O CSS ficaria o seguinte:

```css
.container-text {
  background-image: -webkit-linear-gradient(transparent, transparent), url(https://static.pexels.com/photos/4827/nature-forest-trees-fog.jpeg);  /* vai ser ignorado pelos browsers sem webkit */
  -webkit-text-fill-color: transparent;  /* vai ser ignorado pelos browsers sem webkit */
  -webkit-background-clip: text;  /* vai ser ignorado pelos browsers sem webkit */
  color: #FFFFFF;  /* cor a ser usada nos browsers sem webkit */
  padding-top: 20px;
  font-size: 170px;
  font-family: 'Bungee', cursive;
}
```

Acho que é isso! Efeito bem bacana, pena que tem algumas limitações quanto aos browsers. Mas acho que dá pra fazer alternativas que ficam legais também né?
