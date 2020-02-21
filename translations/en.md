# Javascript
Javascript Games | Code Design Style Guide

![GitHub Logo](https://imgur.com/YzWcKkV.png)


**PDF:** [Download](https://gurigraphics.itch.io/code-design-style-guide)
**GITHUB:** [Download](https://github.com/Gurigraphics/javascript)


## Intro

This style guide is based on several others.
  
However, some additions are original and you will only find them here.

If you work for a large company, it is best to follow the style guide for a large company.

In this guide you can pick up what you think is relevant.
And disregard what you consider irrelevant.

Then you can search for other style guides. And create yours.

One of the advantages of following a style guide is being able to think less and produce more.

Another advantage is to make the code more readable and organized.

You will probably need to read this guide several times.

## Start

Why **Code Design Style Guide** and not just **Style Guide**?

Because I address here issues related to writing code blocks.

And also regarding the organization and structure of the code.

Before starting, it is important to review the meaning of these two concepts:
"classes" and "libraries".

Let's start with the classes.

## Class

A "class" arises from the need for a "classification of things".

In javascript we don't need to create a class itself to classify something.

We can classify things using simple objects that working as "namespaces".
```js
var DATA = {}
DATA.player = {}
DATA.player.score = 0

var PLAYER = {}
PLAYER.getPositionX = () => {}
```
A **class** can be used to agroup different types of **data** and **methods**.

A **namespace** can be used to agroup different **classes**.

A **module** can be used to agroup different groups of **namespaces**.

Confused?

A **name** is used to differentiate one thing or category from another.

A **namespace** serves to define a space or context that guarantees the uniqueness of an object.

In this way, the same **name** can represent different objects in different contexts.

```js
DATA.playerOne.totalScore = 0
DATA.playerTwo.totalScore = 0
```
In javascript there are no namespaces themselves.

So, you can understand this as classification, categorization, modularization ...

The important thing is to separate everything into modules, regions, sectors, groups, classes, families, categories, etc.

That is, keep each type of thing in the proper drawer to be able to find it later.

With that we can now start to realize various patterns.


### 01 - Avoid orphan functions. They don't like to live alone.

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
When something is frequently used the exception is allowed: log (), get (), etc.
We'll see that later.


### 02 - Use capital letters for the names of the main "MODULES"

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
I call this "module". You may prefer to call it "groups", "categories", etc.

What happens is that, as the project escalates, it can really change its status.
```js
PAGE_HOME.events.menu...
PAGE_ABOUT.events.menu...
```
These classifications can also vary if they are driven by data, events, objects, functions, etc.

### 03 - In variable names use lowercase letters

Bad
```js
var Name = ""
var NAME = ""
```

Good
```js
var name = "John Doe"
```


### 04 - In variables and methods that are composed use camelCase

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

### 05 - In acronyms use capital letters

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


### 06 - Const and Let are unnecessary for prototypes, beginners and small teams

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
Just because something is new or recommended by big companies doesn't mean you need it.

Avoid the recommendations of surfers for fashions and hypes.

This will usually disorient, hinder and delay you more than helping.

Only use const and let when this is tremendously necessary, relevant, indispensable.

The exception is valid when something cannot or hardly needs to be changed:
```js
const log = (v) => console.log(v)
const get = (v) => document.querySelector(v)
```


### 07 - Repeat console.log is not necessary

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

### 08 - Learn with Jquery how to use javascript vanilla

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


### 09 - The larger the group the greater the likelihood of mess. Save the data in the appropriate "drawers".
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


### 10 - The fewer items there are in a "drawer" the less time you spend looking for what you need

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

### 11 - Modules with compound names separate with UPPER_SNAKE_CASE

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


### 12 - In the "classes themselves" use PascalCase

Bad
```js
class MYCLASS { constructor() ...
class myClass { constructor() ...

```

Good
```js
class MyClass { constructor() ...
```



### 13 - Avoid starting words with _underline

Bad
```js
var _bad = ""

```

Good
```js
var good = ""
```

### 14 - Avoid multiple __underlines

Bad
```js
var __double__bad = ""

```

Good
```js
var good = ""
```


### 15 - When the project escalates, members need to be promoted to group leaders

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
The guys accustomed to programming a calculator usually call this "over-designing".

So now we need to review the concept of libraries.


## Library

Long ago there were paper books ...

Anyway, you must know what a physical library is.

The organization of a code library follows the same organizing principle.

If I'm looking for a book about the First World War I need to know where to search:

Library -> History -> Wars -> First World War -> Shelf -> Book

It is very relevant to consider this classification when writing the code.

Because within your code, Google will not help you.

This library chat seems basic, simple and obvious, but 99% don't know how to use it.

That's why they waste so much time:

1. looking for things inside your code
2. trying to understand your code
3. renaming things
4. moving things around

In short: refactoring the code

So from the beginning we must already consider that the code always scales.

Therefore, it is much better to put things in the "proper drawers" from the beginning.

Of course, you can do as most do.

And postpone that to refactor later.

However, the common thing is that you end up put all in trash and start over from scratch.

Because there will be many things in the wrong place.

And with inappropriate names and responsibilities.

You won't be able to pay off all the "technical debts" that you didn't even realize you were accumulating.

You will also not be able to reuse the same code in another project.

And the worst is the habit of always working this way.

And I am not exaggerating. Because this occurs in 99% of cases.

It is better to consider what Descartes recommended:
> "Divide the problem into the smallest parts possible"


Now we move on ...
 

### 16 - Avoid repeating context

Bad
```js
PLAYER.addPlayerScore()
```

Good
```js
PLAYER.addScore()
```

### 17 - An action needs a responsible actor

Bad
```js
addPlayer()
```

Good
```js
SCENE.addPlayer()
```


### 18 - Describe the actions in the method names

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

### 19 - Avoid putting "data" and "methods" in the same "drawer".

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

### 20 - Don't get involved in the lives of others. Call the person responsible for the task.

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


### 21 - Avoid unnecessary suffixes and prefixes 

Bad
```js
DATA.isVisibleNow = false
DATA.isNoVisible = false
```

Good
```js
DATA.player.visible = true

```


### 22 - Verbs appear before. Qualifiers appear later.

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

### 23 - Avoid creating subdivisions prematurely.

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



### 24 - Avoid C# style

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



### 25 - Code also needs more space to "breathe"

Bad
```js
GROUP.member=(x,y)=>log(x+y)
```

Good
```js
GROUP.member = (x, y) => log(x + y)
```

### 26 - Avoid spaces in parentheses, braces and brackets

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


### 27 - Using only 2 spaces is enough

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

### 28 - First line after brackets in blank

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

### 29 - Last line of code in blank

Bad
```js
if(true) log("hello") 
```

Bad
```js
if(true) log("hello") 
//it should be blank
```


### 30 - Simplify when possible

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


### 31 - Avoid very long lines

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

### 32 - Forget the semicolon

Bad
```js
log("hello"); 
```

Good
```js
log("hello")
```



### 33 - Use backslash to concatenate strings

Bad
```js
log(part1 + " e " + part2)
```

Good
```js
log(`${part1} e ${part2}`)
```
In other words: use "computed property names"


### 34 - Keep the code in English

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

### 35 - Avoid "sesquipedalianism". Avoid more than four terms in the same word

Bad
```js
var bigNamesNoIsRecomended = ""
```

Good
```js
var avoidBigNames = ""
```

Many terms in the same word are a sign that there are problems with responsibility, modularity or classification.

Codes with this symptom are terrible to understand, research, maintain and scale.

Robert C. Martin of Clean Code presents this rule:
> Functions in small scopes should have long and precise names.

If you want to understand directly from the source how this author thinks (2)

He likes names like this: ** gatherFunctionsAndVariablesFromColumnHeader **

It claims that the function name must be sufficient to understand what it does.

I think differently.

To understand what a function does, in addition to the name, we also need the context.

Furthermore, it is not exactly what a function does that matters.

What matters is the result that a function produces or returns.

That is, we just need the data.

For that we need to know for whom to request this.

Outside of that context, we don't care if the function make a parse or dance.

There may be situations that sesquipedalianism is useful. But, it wasn't this time.

The problem with this: ** gatherFunctionsAndVariablesFromColumnHeader **

Is that: this has many responsibilities.
```js
ColumnHeader.getVars()
ColumnHeader.getFuncs()
```

### 36 - Micro-contexts admit abbreviations

I also disagree with this:
> "Avoid Mental Mapping. Explicit is better than implicit". (By Robert C. Martin)

bad
```js
locations.forEach(l => {
```
good
```js
locations.forEach(location => {
```

This recommendation is useful when a method does more than one thing.
When handling multiple elements and there is a possibility of confusion.
And as we realized, this is not the case.

So I prefer:
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

It is necessary to understand that one rule ends when another starts.

And the other rule is that micro-contexts admit abbreviations.

Another rule is:
> "familiarity admits brevity" (Golang principle)

When something is frequently used we create abbreviations and mnemonics: log (), get (), $ ("# ID"), etc.

The more you need to use a name,
the smaller the "weight" of the name you need to "carry" in your memory.

That's why we don't always need to call everyone by their full name.

For the same reason, mathematicians prefer "+", "-", "/", "x", "y" than:

"quantumSpinLeft" divided by "quantumSpinRight".

### 37 - Avoid "creating" and "using" the code at the same time

The idea here is to differentiate "code designer" from "programmer" and "library" from "context of use"

When you CREATE a "library or class" the code can be organized as follows:
```js
FACTORY.create.actors.inNextRow()
FACTORY.create.tiles.inFirstRow()
FACTORY.create.layers.inLastRow()
```

When you are going to USE the "library or class" you created, you can use an alias:
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

We usually do everything at the same time.

We created the tracks with the train moving.

We need to create the code already thinking about being able to reuse this in another project.

And to think differently when we need to use what we create.

Learning how to separate these two processes is not easy, but it is often possible.


### 38 - When there are less than 10 elements in the same group you still don't need to subdivide

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

In this case the problem was also that a method needs to have a single responsibility.
The "createActorsForNextRow" has two responsibilities.
It is one thing to know the position. Another is to create the actor:
```js
var position = getNextRow()
createActors(position)
```
Or with Method Chaining
```js
SCREEN.getNextRow().createActors(position)
```


### 39 - Something very little used can exceed 10 elements or not be subdivided

Bad
```js
MATH.geometry.getArea()
MATH.arithmetic.multiply()
```
Good
```js
MATH.getArea()
```
And what is never used is better to remove from the code.



### 40 - The best functions have a single responsibility

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
Single responsibility is not to do one thing -> ** hold a spoon **

Single responsibility is to be responsible for a single task -> ** who will make the coffee? **

The end. If you liked it remember to leave a star. :)

### References
1. https://hilton.org.uk/presentations/naming-guidelines
2. http://www.informit.com/articles/article.aspx?p=1323426
3. https://github.com/airbnb/javascript
4. https://google.github.io/styleguide/jsguide.html
5. https://addyosmani.com/blog/essential-js-namespacing/

## Licence
(The MIT License)

Copyright (c) 2020 Gurigraphics

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
