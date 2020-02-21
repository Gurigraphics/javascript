# Javascript
Javascript Games | Code Design Style Guide

![GitHub Logo](https://imgur.com/YzWcKkV.png)


**PDF:** [Download](https://gurigraphics.itch.io/code-design-style-guide)
**GITHUB:** [Download](https://github.com/Gurigraphics/javascript)


## Intro

Este guia de estilo é baseado em vários outros. 
  
Contudo, algumas adições são originais e você só encontrará aqui.

Se você trabalha em uma grande empresa, melhor seguir o guia de estilos de uma grande empresa.

Neste guia você pode aproveitar o que considerar relevante. 
E desconsiderar o que considerar irrelevante.

Depois você pode pesquisar outros guias de estilos. E criar o seu.

Uma das vantagens de seguir um guia de estilos é poder pensar menos e produzir mais.

Outra vantagem é tornar o código mais legível e organizado. 

Provavelmente você precisará ler este guia várias vezes.

## Start

Por que **Code Design Style Guide** e não apenas **Style Guide**?

Porque abordo aqui questões relativas a escrita dos blocos de código.

E também relativas a organização e estrutura do código.

Antes de começar é importante rever o significado deste dois conceitos:
"classes" e "bibliotecas". 

Vamos começar pelas classes.

## Class

Uma **classe** surge da necessidade de uma **classificação de coisas**.

Em javascript não precisamos criar uma classe propriamente dita para classificar algo.

Podemos classificar as coisas utilizando objetos simples que funcionam como **namespaces**.

```js
var DATA = {}
DATA.player = {}
DATA.player.score = 0

var PLAYER = {}
PLAYER.getPositionX = () => {}
```
Uma **class** pode servir para agrupar diferentes tipos ou grupos de **dados** e **métodos**.

Um **namespace** pode servir para agrupar diferentes grupos **classes**.

Um **módulo** pode servir para agrupar diferentes grupos de **namespaces**.

Confuso?

Um **name** serve para diferenciar uma coisa ou categoria de outra.

Um **namespace** serve para definir um espaço ou contexto que garanta a singularidade de um objeto.

Deste forma, um mesmo "name" pode representar diferentes objetos em diferentes contextos.

```js
DATA.playerOne.totalScore = 0
DATA.playerTwo.totalScore = 0
```
Em javascript não há namespaces propriamente ditos.

Então, você pode entender isso como classificação, categorização, modularização...

O importante é separar tudo em módulos, regiões, setores, grupos, classes, familias, categorias, etc.

Ou seja, manter cada tipo de coisa na gaveta adequada para conseguir encontrar isso depois.

Com isso agora podemos começar a perceber diversos padrões.


### 01 - Evite funções orfãs. Elas não gostam de viver sozinhas.

Bad
```js
function player(){

}
```

Good
```js
var PLAYER = {}
PLAYER.getScore = () => {}
```
Quando algo é frequentemente utilizado é permitida a exceção: log(), get(), etc.
Veremos isso depois.


### 02 - Use letras maiúsculas para os nomes dos principais "módulos" 

Bad
```js
var Player = {}
var menu = {}
```

Good
```js
var TEMPLATES = {}
TEMPLATES.getMenu = () => {}

var EVENTS = {}
EVENTS.menu = {}
EVENTS.menu.buttonStart.click = () => {}
EVENTS.menu.buttonCredits.click = () => {}
```
Eu chamo isso de "módulo". Você pode preferir chamar de "grupos", "categorias", etc.

O que ocorre é que, a medida que o projeto escala, isso realmente pode mudar de "status".
```js
PAGE_HOME.events.menu...
PAGE_ABOUT.events.menu...
```
Essas classificações também podem variar se forem orientadas a dados, eventos, objetos, funções, etc.


### 03 - Nos nomes das variáveis use letras minúsculas

Bad
```js
var Name = ""
var NAME = ""
```

Good
```js
var name = "John Doe"
```


### 04 - Em nomes de dados e métodos que sejam compostos use camelCase

Bad
```js
var super_control = ""
var SuperControl = ""
```

Good
```js
DATA.playerName = "John Doe"
PLAYER.getName()
```

### 05 - Em siglas use maiúsculas

Bad
```js
var getId = ""
var getCpf = ""
```

Good
```js
var getID = ""
var getCPF = ""
```


### 06 - Const e Let são desnecessários para protótipos, iniciantes e pequenas equipes 

Bad
```js
const HEIGHT = 680
let width = 680
```

Good
```js
DATA.screen.width = 600
DATA.player.score = 100
```
Só porque algo é novo ou recomendado por grandes empresas não significa que você precise disso.

Evite as recomendações dos surfistas de modinhas e hypes.

Isso geralmente irá mais te desorientar, atrapalhar e atrasar do que ajudar. 

Só use const e let quando isso for tremendamente necessário, relevante, indispensável.

A exceção é válida quando algo não pode ou dificilmente precisará ser alterado:
```js
const log = (v) => console.log(v)
const get = (v) => document.querySelector(v)
```


### 07 - Repetir console.log não é necessário

Bad
```js
console.log(1)
console.log(2)
console.log(3)
console.log(4)
```

Good
```js
const log = (v) => console.log(v)
log(1)
log(2)
log(3)
log(4)
```

### 08 - Aprenda com Jquery como usar javascript vanilla 

Bad
```js
document.getElementsByClassName("class")
document.getElementById("id")
document.getElementsByTagName("body")[0]
document.querySelector("#id")
document.querySelector(".class")
document.querySelector("body")
```

Good
```js
const get = (v) => document.querySelector(v)
get("#id")
get(".class")
get("body")
```


### 09 - Quanto maior o grupo maior a probabilidade de bagunça. Salve os dados nas "gavetas" adequadas.

Bad
```js
PLAYER.score = 100
PLAYER.window = 680
PLAYER.getScore()
```

Good
```js
DATA.screen.width = 600
DATA.player.score = 100
PLAYER.getScore = () => DATA.player.score
```


### 10 - Quanto menos itens há em uma "gaveta" menos você perde tempo procurando o que precisa 

Bad
```js
var player = {}
var menu = {}
var button = {}
var getScore = () => {}
```

Good
```js
var MENU = {}
MENU.button = {}

var PLAYER = {}
PLAYER.getScore = () => {}
```

### 11 - Módulos com nomes compostos separe com UPPER_SNAKE_CASE

Bad
```js
var ABOUTPAGE = {}
var HOMEPAGE = {}

```

Good
```js
var PAGE_HOME = {}
var PAGE_ABOUT = {}
```


### 12 - Nas "classes propriamente ditas" use PascalCase

Bad
```js
class MYCLASS { constructor() ...
class myClass { constructor() ...

```

Good
```js
class MyClass { constructor() ...
```



### 13 - Evite iniciar palavras com _underline

Bad
```js
var _bad = ""

```

Good
```js
var good = ""
```

### 14 - Evite sequencias de __underlines

Bad
```js
var __double__bad = ""

```

Good
```js
var good = ""
```


### 15 - Quando o projeto escala, os membros precisam ser promovidos para líderes do grupo

Bad
```js
var DITATOR_CENTRALIZER = {
  1: players,
  2: enemys,
  3: menus,
  4: buttons
}

```

Good
```js
var CHARS = {}
CHARS.players = {}
CHARS.players.playerOne = {}
CHARS.players.playerTwo = {}

CHARS.enemys = {}
CHARS.enemys.typeOne = {}
CHARS.enemys.typetwo = {}

var SCREEN = {}
SCREEN.MENU = {}
MENU.button = {}
```
A galera acostumada a programar calculadora costuma chamar isso de "over-designing".

Por isso, agora precisamos rever o conceito de bibliotecas.


## Library

Há muito tempo atrás haviam livros de papel...

Enfim, você deve saber o que é uma biblioteca física.

A organização de uma biblioteca de código segue o mesmo princípio de organização.

Se eu procuro por um livro sobre a Guerra dos Farrapos eu preciso saber onde pesquisar:

Biblioteca -> História -> História do Brasil -> História do Rio Grande do Sul -> 
Guerras -> Guerra dos Farrapos -> prateleira -> livro 

É muito relevante considerar essa classificação ao escrever o código.

Porque dentro do seu código o Google não vai te ajudar.

Esse papo de biblioteca parece básico, simples e óbvio, mas 99% não sabem utilizar.

Por isso perdem tanto tempo:

1. procurando coisas dentro do próprio código
2. tentando entender o próprio código
3. renomeando as coisas
4. mudando as coisas de lugar

Em resumo: refatorando o código

Ou seja, desde o princípio nós já devemos considerar que o código sempre escala.

Sendo assim, muito melhor é desde o princípio já colocar as coisas nas "gavetas adequadas".

Claro que, você pode fazer como a maioria faz. 

E adiar isso para refatorar depois.

Porém, o comum é você acabar tendo que jogar tudo fora e recomeçar do zero.

Porque haverá muitas coisas no lugar errado. 

E com nomes e responsabilidades inadequadas.

Você não conseguirá pagar todas as "dívidas técnicas" que você nem percebia que estava acumulando.

Você também não conseguirá reaproveitar o mesmo código em outro projeto.

E o pior é o hábito de sempre trabalhar desta forma.

E eu não estou exagerando. Porque isso ocorre em 99% dos casos.

Melhor é considerar o que o Descartes recomendava: 
> "Dividir o problema nas menores partes possíveis"


Agora seguimos em frente...
 

### 16 - Evite repetição de contexto

Bad
```js
PLAYER.addPlayerScore()
```

Good
```js
PLAYER.addScore()
```

### 17 - Uma ação precisa de um sujeito responsável

Bad
```js
addPlayer()
```

Good
```js
SCENE.addPlayer()
```


### 18 - Descreva as ações nos nomes dos métodos

Bad
```js
PLAYER.myID()
PLAYER.positionX()
PLAYER.score()
```

Good
```js
PLAYER.getID()
PLAYER.getPositionX()
PLAYER.setScore()
```

### 19 - Evite colocar "dados" e "métodos" na mesma gaveta. 

Bad
```js
PLAYER.isVisible = false
PLAYER.getIsVisible()
```

Good
```js
DATA.player.visible = true
DATA.player.created = true
PLAYER.isVisible()
PLAYER.isCreated()
```

### 20 - Não se meta na vida dos outros. Chame o responsável pela tarefa.

Bad
```js
ENEMY.hit = () => DATA.player.life-=1
FRUIT.hit = () => DATA.player.life+=1
```

Good
```js
ENEMY.hit = () => PLAYER.decLife(DATA.enemy.damage)
FRUIT.hit = () => PLAYER.incLife(DATA.fruit.value)
```


### 21 - Evite sufixos e prefixos desnecessários 

Bad
```js
DATA.isVisibleNow = false
DATA.isNoVisible = false
```

Good
```js
DATA.player.visible = true

```


### 22 - Verbos aparecem antes. Qualificadores aparecem depois.

Bad
```js
var canJump = false
var activeControl = false
PLAYER.controlActive()
```

Good
```js
DATA.player.controlsActive = true
PLAYER.activeControls()
```

### 23 - Evite criar subdivisões prematuramente.

Bad
```js
DATA.player.buttons.jump.active()
PLAYER.jump.active()
```

Good
```js
DATA.player.jump = true
PLAYER.activeJump()
PLAYER.desactiveJump()
```



### 24 - Evite C# style

Bad
```js
function child ()
{

}
```

Good
```js
function child() {

}
```



### 25 - Código também precisa de mais espaço para "respirar"

Bad
```js
GROUP.member=(x,y)=>log(x+y)
```

Good
```js
GROUP.member = (x, y) => log(x + y)
```

### 26 - Evite espaços entre parênteses, chaves e colchetes 

Bad
```js
if ( true ) {
  log( array[ { text: "hello" } ] )  
}
```
Good
```js
if (true) {

 log(array[{text: "hello"}]) 
}
```


### 27 - Usar apenas 2 espaços é suficiente

Bad
```js
GROUP.member = () => {
      log("hello")
}
```

Good
```js
GROUP.member = () => {
  log("hello")
}
```

### 28 - Primeira linha após colchetes em branco

Bad
```js
GROUP.member = () => {
  if(true){  
    for(item in items){  
       log(item[item])
    }
  }  
}
```

Good
```js
GROUP.member = () => {

  if (true) {
  
    for (item in items) {
  
       log(item[item])
    }
  }  
}
```

### 29 - Úlima linha do código em branco

Bad
```js
if(true) log("hello") 
```

Bad
```js
if(true) log("hello") 
//it should be blank
```


### 30 - Simplifique quando possível

Bad
```js
if(true){

   log("hello")  
}
```

Good
```js
if (true) log("hello")  

```


### 31 - Evite linhas muito extensas

Bad
```js
compile.then(exec()).then(exec()).then(exec()).then(exec())...
```

Good
```js
compile.then(exec())
  .then(exec())
  .then(exec())
  .then(exec())
```

### 32 - Esqueça o ponto e virgula

Bad
```js
log("hello"); 
```

Good
```js
log("hello")
```



### 33 - Use crase para concatenar strings

Bad
```js
log(part1 + " e " + part2)
```

Good
```js
log(`${part1} e ${part2}`)
```
Em outras palavras: use "computed property names"


### 34 - Mantenha o código em inglês

Bad
```js
ARS_MEMORIAE.método = () => {

  hablar("bruh")
}
```

Good
```js
GROUP.method = () => {

  log("hello")
}
```

### 35 - Evite "sesquipedalianism". Evite mais de quatro termos na mesma palavra

Bad
```js
var bigNamesNoIsRecomended = ""
```

Good
```js
var avoidBigNames = ""
```
Muitos termos na mesma palavra é um sinal de que há problemas com responsabilidade, modularidade ou classificação.

Códigos com este sintoma são péssimos para entender, pesquisar, fazer manutenção e escalar.

Robert C. Martin do Clean Code apresenta esta regra:
> Functions in small scopes should have long and precise names.

Se você quiser entender direto da fonte como este autor pensa (2)

Ele gosta de nomes assim: **gatherFunctionsAndVariablesFromColumnHeader**

Alega que o nome da função deve ser suficiente para entender o que ela faz.

Eu penso diferente. 

Para entender o que uma função faz, além do nome, nós também precisamos do contexto.

Além disso, não é exatamente o que uma função faz o que interessa.

O que interessa é o resultado que uma função produz ou retorna.

Ou seja, eu preciso apenas dos dados. 

Para isso preciso saber para quem solicitar isso.

Fora daquele contexto não me interessa se a função faz um parse ou dance.

Pode haver situações que o sesquipedalianism seja útil. Mas, não foi desta vez.

O problema com isso: **gatherFunctionsAndVariablesFromColumnHeader**

É que isso possui responsabilidades demais.
```js
ColumnHeader.getVars()
ColumnHeader.getFuncs()
```

### 36 - Micro-contextos admitem abreviações

Eu também discordo disso:
> "Avoid Mental Mapping. Explicit is better than implicit". (By Robert C. Martin)

bad
```js
locations.forEach(l => {
```
good
```js
locations.forEach(location => {
```

Essa recomendação é útil quando um método faz mais de uma coisa.
Quando manipula vários elementos e há possibilidade de confusão.
E como percebemos, não é o caso.

Por isso eu prefiro:
> "Avoid Sesquipedalianism when Less is More". (Gurigraphics)

Bad
```js
sesquipedalianisms.forEach(sesquipedalianism => {
document.getterElementByIdentity
console.logger(sesquipedalianisms[sesquipedalianism])
```

Good
```js
items.forEach(i => {
$("#ID")
log(v)
```

É preciso entender que uma regra acaba quando inicia outra.

E a outra regra é que micro-contextos admitem abreviações.
Outra regra é: 
> "familiarity admits brevity"(Golang principle)
Quando algo é frequentemente utilizado criamos abreviações e mnemônicos: log(), get(), $("#ID"), etc.

Quanto mais você precisa usar um nome, 
menor deve ser o "peso" do nome que você precisa "carregar" na sua memória. 

Por isso não precisamos chamar todo mundo sempre pelo nome completo.

Pelo mesmo motivo os matemáticos preferem "+", "-", "/", "x", "y" que:
"quantumSpinLeft" dividido por "quantumSpinRight".

### 37 - Evite "criar" e "utilizar" o código ao mesmo tempo

A ideia aqui é diferenciar "code designer" de "programmer" e "library" de "context of use"

Quando você CRIA uma "library ou class" o código pode ficar organizado desta forma:

```js
FACTORY.create.actors.inNextRow()
FACTORY.create.tiles.inFirstRow()
FACTORY.create.layers.inLastRow()
```

Quando você vai UTILIZAR a "library ou class" que você criou, você pode usar um alias: 
```js
create(entity, mode){
  Factory.create[entity][mode]()
}

create("actors", "inNextRow")
```
Ou
```js
import createActors as createActors from "Factory";
createActors("inNextRow")
```

Geralmente fazemos tudo ao mesmo tempo.
Criamos os trilhos com o trem andando.

Precisamos criar o código já pensando em poder reaproveitar isso em outro projeto.

E pensar de forma diferente quando precisamos utilizar o que criamos.

Aprender a separar estes dois processos não é fácil, mas muitas vezes é possível.


### 38 - Quando há menos de 10 elementos no mesmo grupo você ainda não precisa subdividir

Bad
```js
FACTORY.create.actors.inNextRow()
FACTORY.createActorsForNextRow()
```
Good
```js
SCREEN.getNextRow().addActors(v)
SCREEN.addTiles(SCREEN.getFirstRow())
```

Nesse caso o problema também era que um método precisa ter uma única responsabilidade.
O "createActorsForNextRow" possui duas responsabilidades.
Uma coisa é saber a posição. Outra é criar o actor:
```js
var position = getNextRow()
createActors(position)
```
Ou com Method Chaining
```js
SCREEN.getNextRow().createActors(position)
```


### 39 - Algo muito pouco utilizado pode utrapassar 10 elementos ou nem ser subdividido

Bad
```js
MATH.geometry.getArea()
MATH.arithmetic.multiply()
```
Good
```js
MATH.getArea()
```
E o que nunca é utilizado melhor retirar do código.



### 40 - As melhores funções possuem responsabilidades únicas

Bad
```js
SCREEN.addPlayer = () => {
   
   PLAYER.show()
   PLAYER.setScore(0)
   MENU.show()   
}
```

Good
```js
MENU.start = () => {
   
   MENU.show()
}

PLAYER.start = () => {
   
   PLAYER.show()
   PLAYER.setScore(0)  
}

GAME.start = () => {
   
   MENU.start()
   PLAYER.start()    
}
```
Responsabilidade única não é fazer uma única coisa -> **segurar uma colher**

Responsabilidade única é ser responsável por uma única tarefa -> **quem vai fazer o café?**


The end. Se gostou lembre de deixar uma estrela. :)


### Referências
1. https://hilton.org.uk/presentations/naming-guidelines
2. http://www.informit.com/articles/article.aspx?p=1323426
3. https://github.com/airbnb/javascript
4. https://google.github.io/styleguide/jsguide.html
5. https://addyosmani.com/blog/essential-js-namespacing/

## Licença
(The MIT License)

Copyright (c) 2020 Gurigraphics

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

