---
layout: post
title:  "Usando a API do Google para fazer gráficos responsivos"
date:   2016-10-27 20:20:00 -0300
categories: js css html dicas bibliotecas
tags: js css html dicas bibliotecas 
images: 
    - url: ../assets/google_charts.tiff

lang: pt
ref: google-vis-api-responsive
---

Quando o assunto é visualização de dados, o que não faltam são alternativas bacanas e visualizações diferentes para serem usadas. Com bibliotecas como [D3.js](https://d3js.org), usamos a ferramenta incrível que é o SVG para criar visualizações com um pouco de abstração. Mas e quando precisamos de ainda mais abstração? Ou se queremos algum boilerplate, alguma coisa que seja mais simples de configurar? Daí, uma boa opção é a __API de Visualização do Google__.

Com diversos modelos de gráficos e visualizações, a API do Google traz justamente isso: simplicidade. Também através do SVG, a API do Google faz com que não seja necessário criar várias linhas de código para exibir um eixo ou uma fatia do gráfico de pizza. Só precisamos definir os dados, estilizar como quisermos e mandar desenhar o gráfico.

Mas como toda coisa boa, temos um tradeoff. Em comparação com o uso de bibliotecas como o D3.js, por exemplo, os gráficos do Google são menos personalizáveis, então alterações muito específicas podem ser difíceis de alcançar. Por outro lado, acredito que o nível de configurações possíveis dos gráficos é excelente, e deve atender a maioria das pessoas.

<br>

## Então, mão na massa!

<hr>
Para começar, [aqui](https://developers.google.com/chart/interactive/docs/reference) está a referência da API. Tudo que precisar saber, configurar, consultar, o link é esse!

<br>

### Os dados do gráfico

Vamos começar pelos dados que vão preencher o gráfico. Para todos os gráficos do Google os dados tem que estar em um objeto da classe javascript `DataTable`. Um objeto dessa classe consiste em uma tabela bidimensional (linhas e colunas), onde as colunas tem obrigatoriamente um tipo e um ID ou rótulo opcionais.

Considerando a tabela a seguir, vamos ver o código de duas maneiras de transformá-la no nosso objeto `DataTable`.

| Escolaridade | Anos |
| --- | :---:  |
| Primário | 9 |
| Ensino Médio | 3 |
| Faculdade | 4 |
| Mestrado | 2 |
| Doutorado | 4 |

<br>

```javascript
var dados = new google.visualization.DataTable();
  dados.addColumn('string', 'Escolaridade');
  dados.addColumn('number', 'Anos');
  dados.addRows([
    ['Primário', 9],
    ['Ensino Médio', 3],
    ['Faculdade', 4], 
    ['Mestrado', 2],
    ['Doutorado', 4]
]);
```
Nessa primeira forma, instanciamos o objeto e adicionamos as colunas passando seu tipo (que é obrigatório) e o rótulo (opcional). Depois adicionamos as linhas, onde cada linha é um vetor composto pelos valores de cada coluna. Nesse caso adicionamos todas as linhas num vetor e adicionamos todas de uma vez ao `DataTable` usando o método `addRows`. Podemos também adicionar uma a uma através do método `addRow`.


```javascript
var vetor_dados = [
  ['Escolaridade', 'Anos'],
  ['Primário', 9],
  ['Ensino Médio', 3],
  ['Faculdade', 4], 
  ['Mestrado', 2],
  ['Doutorado', 4]
];

var dados = google.visualization.arrayToDataTable(vetor_dados,false);
```
Nessa segunda forma, temos um vetor javascript com os dados e passamos ele para a função `arrayToDataTable`, que converte um vetor para um objeto `DataTable`. Nesse exemplo, ele infere o tipo das colunas, já que não especificamos, e o valor `false` é passado para indicar que a primeira linha são as colunas e não compõem os dados. Essa forma pode ser bem útil quando os dados vem de outro lugar, ou são gerados por exemplo.

<br>

### Configurações do gráfico

Agora vamos configurar algumas coisinhas do gráfico. As possibilidades são inúmeras, então tem que ir olhando na referência de acordo com o que você precisar. Mas vamos ao básico: título, largura e altura.

```javascript
var opcoes = {'title':'Quantidade de anos em cada período escolar',
              'width':400,
              'height':300};
```

Podemos definir também outras coisas como o texto dos eixos, cores, legendas e etc. Aí só olhar a sintaxe correta mesmo, porque cada configuração tem sua chave específica, como `title` no exemplo.

<br>

### Dependências

Primeiro, no nosso HTML, devemos adicionar o script responsáel por carregar os pacotes da API:

```html
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
```

Ele deve ser chamado apenas uma vez. No começo do nosso script, devemos adicionar o pacote dos gráficos básicos do Google, e podemos chamá-lo quantas vezes quisermos, alterando os pacotes a serem incluídos de acordo com a necessidade.

```javascript
google.charts.load('current', {'packages':['corechart']});
```

Se quisermos adicionar um gráfico que não é de um dos tipos básicos, adicionamos no lugar de `corechart`. (Os nomes dos gráficos de tipo básico são: *bar, column, line, area, stepped area, bubble, pie, donut, combo, candlestick, histogram, scatter*). Se quisermos fazer um diagrama Sankey por exemplo:

```javascript
google.charts.load('current', {'packages':['sankey']});
```

<br>

### Desenhando o gráfico

Para esse exemplo, vamos criar um gráfico de colunas com os dados e configurações já definidos. O código completo fica assim:

```javascript
//carrega pacote dos gráficos basicos
google.charts.load('current', {'packages':['corechart']});

//definimos a funcao de desenhar como callback do carregamento do pacote
google.charts.setOnLoadCallback(desenha_grafico);

//funcao que configura e desenha grafico
function desenha_grafico(){

    //cria dataTable com os dados
    var dados = new google.visualization.DataTable();
      dados.addColumn('string', 'Escolaridade');
      dados.addColumn('number', 'Anos');
      dados.addRows([
        ['Primário', 9],
        ['Ensino Médio', 3],
        ['Faculdade', 4], 
        ['Mestrado', 2],
        ['Doutorado', 4]
    ]);

    //configurações do grafico
    var opcoes = {'title':'Quantidade de anos em cada período escolar',
                  'width':600,
                  'height':250};

    //define grafico como gráfico de colunas a ser incluido no elemento de id grafico_div
    var grafico = new google.visualization.ColumnChart(document.getElementById('grafico_div'));

    //desenha gráfico com dados e configuraçoes definidas
    grafico.draw(dados, opcoes);
}
```
Aqui, envolvemos a definição do `DataTable` e das opções em uma função, assim como as duas útlimas linhas, que são responsáveis por definir o elemento ao qual o gráfico será adcionado e desenhar o gráfico propriamente dito. O objetivo aqui é que a função só seja executada após os pacotes terem sido carregados. Pra conseguir isso, adicionamos também a linha `google.charts.setOnLoadCallback(desenha_grafico);`, onde passamos essa função como callback para o carregamento do pacote de gráficos.


Você ver o código funcionando abaixo, e se quiser editar é só clicar em [aqui](http://codepen.io/csbatista/pen/ozRwgk) ou em __Edit on Codepen__
<p data-height="320" data-theme-id="0" data-slug-hash="ozRwgk" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/ozRwgk/">ozRwgk</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<br>

### Responsividade

Se você redimensionar a janela vai ver que o gráfico que temos até agora não está responsivo. Em uma janela com largura menor que 600 ou altura menor que 250, o que estiver sobrando vai ser escondido e adicionado barra de rolagem. Os gráficos do Google não são naturalmente responsivos, mas podemos contornar a situação de uma maneira bem simples.

Pense assim: nós definimos nas opcções quais são as dimensões do gráfico. E se falássemos novas dimensões caso a tela fosse redimensionada? Só alterar as dimensões, porém, não vai surtir nenhum efeito. É preciso redesenhar o gráfico para que ele receba as novas dimensões e seja criado de acordo com elas. 

Primeiro então, vamos definir a largura e altura iniciais de acordo com o tamanho da tela.

```javascript
var altura = 250;

var largura = 600;
if (document.getElementById('grafico_div').offsetWidth < 600){
  largura = document.getElementById('grafico_div').offsetWidth;
}

//configurações do grafico
var opcoes = {'title':'Quantidade de anos em cada período escolar',
              'width':largura,
              'height':altura};
```
No fim das contas, as configurações de largura e altura vão depender do seu gráfico e dos seus dados. Cada caso vai ter suas limitações. Nesse caso aqui, não me preocupei com a altura, pois como o gráfico é de colunas e o intervalo vertical não é muito grande, ele não precisa de mais que isso (e é um tamanho que não fica ruim em celulares). A largura eu defini como a largura do div de id `grafico_div`, mas caso a largura dele seja maior que 600, limitamos o gráfico a 600.

Agora, vamos atualizar os valores quando a janela for redimensionada. Para isso, vamos adicionar um evento ao redimensionamento da janela, assim toda vez que a janela for redimensionada, nossa função será chamada.

```javascript
window.addEventListener('resize', desenha_grafico);
```

Essa linha conecta nossa função com a ação de redimensionar a janela. Agora o código fica assim:

```javascript
//carrega pacote dos gráficos basicos
google.charts.load('current', {'packages':['corechart']});

//definimos a funcao de desenhar como callback do carregamento do pacote
google.charts.setOnLoadCallback(desenha_grafico);

//funcao que configura e desenha grafico
function desenha_grafico(){

    //cria dataTable com os dados
    var dados = new google.visualization.DataTable();
      dados.addColumn('string', 'Escolaridade');
      dados.addColumn('number', 'Anos');
      dados.addRows([
        ['Primário', 9],
        ['Ensino Médio', 3],
        ['Faculdade', 4], 
        ['Mestrado', 2],
        ['Doutorado', 4]
    ]);

    var altura = 250;

    var largura = 600;
    if (document.getElementById('grafico_div').offsetWidth < 600){
      largura = document.getElementById('grafico_div').offsetWidth;
    }

    //configurações do grafico
    var opcoes = {'title':'Quantidade de anos em cada período escolar',
                  'width':largura,
                  'height':altura};

    //define grafico como gráfico de colunas a ser incluido no elemento de id grafico_div
    var grafico = new google.visualization.ColumnChart(document.getElementById('grafico_div'));

    //desenha gráfico com dados e configuraçoes definidas
    grafico.draw(dados, opcoes);
}

window.addEventListener('resize', desenha_grafico);
```

Agora quando redimensionamos a janela, o gráfico se adapta! Bem fácil né? Como eu disse, a quantidade de manipulação das alturas e larguras vai depender do tipo de visualização e dos dados, mas a lógica é essa. Obter as dimensões atuais, atualizar as opções do gráfico e redesenhá-lo. Ah! Uma dica importante é usar sempre o div onde está o gráfico e não a janela toda! Porque aí fica fácil separar as configurações do gráfico com os estilos dos elementos, e você pode mexer com o CSS da página a vontade sem se preocupar com o gráfico :)

O resultado tá aqui, e é o mesmo esquema, se quiser editar é só clicar em [aqui](http://codepen.io/csbatista/pen/VKOWPr) ou em __Edit on Codepen__

<p data-height="320" data-theme-id="0" data-slug-hash="VKOWPr" data-default-tab="result" data-user="csbatista" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/csbatista/pen/VKOWPr/">Responsive Google chart</a> by Carolina Santos Batista (<a href="http://codepen.io/csbatista">@csbatista</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<br>

A API tem MUITAS visualizações disponíveis, tudo MUITO bem documentado e intuitivo. Tem que ir explorando e testando novas coisas mesmo. Já revirei essa API de ponta a cabeça, então se tiverem alguma dúvida posso tentar ajudar também :)

"Isso é tudo pessoal!", abraços e até a próxima!
