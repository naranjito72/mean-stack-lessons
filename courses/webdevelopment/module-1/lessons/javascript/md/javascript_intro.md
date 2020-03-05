class: center, middle, inverse

###<img src="https://imgur.com/VJqG5MN.png" width=20% height=20% alt="logo">

---
name: default
layout: true
task: &nbsp;

.task[{{task}}]


---
name:contenido

### Contenido

- [Algoritmos](#algoritmos)
- [Introducción a Javascript](javascript1.html)
- [Funciones](funciones.html)
- [DOM](dom.html)

---
name:algoritmos
task: [<< índice de contenidos >>](#contenido)

## Aprender a programar

Para PODER Programar bien no se necesitas otra cosa que « Tener LÓGICA»

<p style="background-color:rgba(0,0,255,0.3); height:30%; padding-top:30px; padding-left:1em;font-size: 40px;">LA LÓGICA DE LA PROGRAMACIÓN 
= IMAGINA + PIENSA + TRADUCE</p>

---

## Tips para aprender a programar


- __Tip #1__: Despreocúpate del Lenguaje y ocúpate de la __IDEA__…

- __Tip #2__: Ten en cuenta las Diferencias. Lo que se VE en la Pantalla es DIFERENTE al Programa…

- __Tip #3__: Lee, lee, lee y lee !!! Lee todo el código que caiga en tus manos…

- __Tip #4__: Conoce tus Herramientas. Emplea los principios de los Paradigmas de Programación…

- __Tip #5__: Ocúpate (en serio!!!) de la Ortografía. Aplica las reglas léxicas y sintácticas al programar…

- __Tip #6__: Induce !!! Piensa de lo particular a lo general…

- __Tip #7__: Deduce… Divide y Vencerás !!! Piensa de lo General a lo Particular …

- __Tip #9__: Crea los Planos de tus IDEAS. Modela mediante diagramas la «LÓGICA» de tus programas…

- __Tip #10__: Ve más allá de lo Evidente. Comprende totalmente la Lógica de tus programas mediante pruebas y modelos de escritorio…

---

## Análisis del programa

Un de los grandes fallos que se comete cuando se está aprendiendo a programar es que se apresuran a escribir el código fuente sin haberse tomado antes el tiempo necesario para :
  - analizar los objetivos: qué debe hacer el programa
  - y los pasos necesarios para alcanzarlos

El fin es crear un programa robusto: libre de errores.

La fase de análisis es un paso fundamental para obtener una documentación del programa sobre cuya base se comenzará a desarrollar el mismo.

La documentación del programa debe mantenerse actualizada durante todo el ciclo de vida del mismo dejando constancia de todos los cambios realizados, pudiendo así ser consultada en caso de tener que comprobar algo, facilitar la comprensión del mismo por otros programadores que entren a formar parte del proyecto, etc.

---

### Pasos para solucionar un problema

- COMPRENDER EL PROBLEMA
  - Leer el problema varias veces
  - Establecer los datos del problema
  - Aclarar lo que se va a resolver (¿Cuál es la pregunta?)
  - Precisar el resultado que se desea lograr
  - Determinar la incógnita del problema
  - Organizar la información
  - Agrupar los datos en categorías
  - Trazar una figura o diagrama
  
- HACER EL PLAN.
  - Escoger y decidir las operaciones a efectuar
  - Eliminar los datos inútiles
  - Descomponer el problema en otros más pequeños

- EJECUTAR EL PLAN (Resolver)
  - Ejecutar en detalle cada operación
  - Simplificar antes de calcular
  - Realizar un dibujo o diagrama
  
- ANALIZAR LA SOLUCIÓN (Revisar)
  - Dar una respuesta completa
  - Hallar el mismo resultado de otra manera
  - Verificar por apreciación que la respuesta es adecuada

---
## PROBLEMAS DE LÓGICA
En grupo, vamos a intentar resolver algunos problemas de lógica para practicar esta habilidad necesaria para la programación

---
### Problema 1
![](https://imgur.com/jWAFa3P.png);

---
### Problema 2

Tenemos cuatro perros: un galgo, un dogo, un alano y un podenco. Éste último come más que el galgo; el alano come más que el galgo y menos que el dogo, pero éste come más que el podenco. ¿Cuál de los cuatro será más barato de mantener?.

---
### Problema 3

Un explorador cayó en manos de una tribu de indígenas, se le propuso la elección entre morir en la hoguera o envenenado. Para ello, el condenado debía pronunciar una frase tal que, si era cierta, moriría envenenado, y si era falsa, moriría en la hoguera. ¿Cómo escapó el condenado a su funesta suerte?

---

### Problema 4

Un pastor tiene que pasar un lobo, una cabra y una lechuga a la otra orilla de un río, dispone de una barca en la que solo caben el y una de las otras tres cosas. Si el lobo se queda solo con la cabra se la come, si la cabra se queda sola con la lechuga se la come, ¿cómo debe hacerlo?

---
### Problema 5: SILOGISMOS

«Los hombres son mortales, 
Sócrates es hombre. 
Luego, Sócrates es mortal». 
es indudablemente conocido e inevitablemente válido. Qué ocurre con el siguiente: 
 
«Los chinos son numerosos, 
Confucio es chino. 
Luego, Confucio es numeroso».

---

### Cálculo del algoritmo task: [<< índice de contenidos >>](#contenido)

1. Elaborar un Algoritmo para calcular el área de cualquier triángulo
rectángulo y presentar el resultado en pantalla.

2. Modela un algoritmo para jugar a piedra, papel o tijera contra el ordenador.
   
3. Busca el algoritmo para desarrollar un juego en el que el jugador tiene que averiguar cual es el número escondido (del 1 al 10). Tiene 3 intentos. Si acierta el juego se acaba con un mensaje de felicitación. Se puede volver a jugar. 
   
---


## Loops

Los bucles son necesarios cuando queremos ejecutar un determinado código un número de veces definido o indefinido, en este caso hasta que se cumpla una condición de salida. Distintos tipos de bucles:

__`for`__`: bucles que repiten el bloque de código un número determinado de veces`

__`for/in`__`: bucles que recorren les propietats d’un objecte.`

__`while`__`: bucles que repeteixen el bloc de codi mentre la condició de sortida sigui certa.`

__`do/while`__ `el mateix que l’anterior, però la condició de sortida s’avalua al final.`

---

### Bucles for, for/in

La sintaxi bàsica del bucle for és:

```javascript
for ( expressió1; expressió2; expressió3) {
  bloc de codi a executar;
}
```

L’expressió1 s’avalua a l’inici; l’expressió2 és la condició de sortida del bucle; l’expressió3 s’executa a cada volta del bucle. Un exemple típic:


      // taula de multiplicar del 6
      let cad = "";

      for (i = 1; i <= 10; i++) {
        cad += "6 * " + i + " = " + 6 * i + "\n";
      }

      console.log(cad);

I amb dos bucles for niats podem fer totes les taules de multiplicar de l’1 al 10:

    // Taules de multiplicar de l'1 al 10
    let cad;

    for (j = 1; j <= 10; j++) {
      cad = "";
      for (i = 1; i <= 10; i++) {
        cad += j + " * " + i + " = " + j * i + "\n";
      }
      console.log(cad);
    }

---

Les tres expressions dins el for són de fet opcionals. L’única cosa que hem de tenir en compte és de no provocar un bucle sense fi, la qual cosa penjaria el navegador web des del qual estem provant. Per tant, sempre hi haurà d’haver una condició de sortida, i podrem sortir del bucle amb la clàusula break:

    let i = 0;
    for (;;) {
    console.log (i);
    i++;
    if (i>15) break;
    }

---

### Bucles while

El cas més senzill és el bucle `while`. Mentre es compleixi la condició s’executarà el bloc de codi:

    while (condició) {
    bloc de codi
    }

Un exemple que utilitza la funció `charAt()` dels string. Mostrem la part de la cadena str fins que no trobem el caràcter i:

    let str = "That is Javascript";
    let cad = "";
    let i = 0;
    let res = "";

    while (res != 'i') {
    res = str.charAt(i);
    cad += res;
    i++;
    }

    console.log (cad);

---

### Bucle do/while

Una variant és el bucle __`do/while`__. El bloc s’executa com a mínim una vegada. La condició de sortida s’avalua al final, i es va executant el codi fins que no es compleixi la condició de sortida.

    do {
    bloc de codi
    }
    while (condició);
    Per exemple,

    str = "That is Javascript";
    cad = "";
    i = 0;
    res = "";

    do {
    res = str.charAt(i);
    cad += res;
    i++;
    } while (res != 'i')

    console.log (cad);

---

En aquest cas, tant se val avaluar la condició al principi o al final, el resultat és el mateix.

Podem sortir del bucle en qualsevol moment fent un `break`:

    str = "That is Javascript";
    cad = "";
    i = 0;
    res = "";

    while (res != 'i') {
    res = str.charAt(i);
    if (res == 'a') break;
    cad += res;
    i++;
    }

    console.log (cad);

---
## Funciones

Representa la manera de realizar una acción parecida en muchos sitios de nuestro código. Son fragmentos de código reutilizables. 

Creamos una función que se llame `sayHelloWorld` que imprima Hello world.

**Declaración de la función**

    function sayHelloWorld() {
      const whatToSay = 'Hello, World!';
      console.log(whatToSay);
    }

*** ESCRIBIMOS LA FUNCIÓN PERO NO LA EJECUTAMOS


**Invocación de la función**

    sayHelloWorld(); // => Hello, World!
    sayHelloWorld(); // => Hello, World!
    sayHelloWorld(); // => Hello, World!

**EJECUTAMOS LA FUNCIÓN

---

### Sintaxis:
<br><br>

    function <name> ([<argument_list>]) {
      <instructions>

      [return <expression>;]
    }

- `function`: Reserved words and should be typed as it is.      
  - ie: return

- `<something>`: User name. Angle brackets (<, >). 
  - ie: myFunction

- `[something]`: Optional. Square brackets ([, ])

---

???

The HelloWorld program was first coded in 1974 and it’s typically the first program people create when learning a new language. There are Hello World versions in almost every programming language!!

Syntax symbols
function: Reserved words and should be typed as it is. ie: return
<something>: User name. Angle brackets (<, >). ie: myFunction
[something]: Optional. Square brackets ([, ])

To summarize, when declaring a function we have to make sure these exist:

function keyword
the name of the function
parameters (if any, if not then just ())
body of the function - which is all the code between the curly braces {}
// keyword    function   parameters (if any)
// ^           name     _____|   
// |            |      | 
function sayHelloWorld(){
    // the code or so called the body of the function
}
Function Name
The name should describe what the function does clearly.
As a rule of thumb, we will try to use verbs that describe actions
In JavaScript, we prefer to name variables and functions camelCase
addTwoNumbers
sayHello
iKnowYouGetItAlready
weLoveYou
…
Function names always begin with a lowercase letter:
lowerCase :thumbsup:
LowerCase
Function Parameters and Function Arguments
In our previous example, we created a function to sayHelloWorld. That was cool because we could tell the computer to do the exact same thing over and over.

Let’s take a look at these examples. Imagine you want to say hello to your classmates. You could have a lot of functions like these:

function sayHelloMery() {
  console.log('Hello, Mery!');
}
function sayHelloJohn() {
  console.log('Hello, John!');
}
function sayHelloLucy() {
  console.log('Hello, Lucy!');
}
And then, we will have to call every function:

sayHelloMery();
// function will print: "Hello Mery!"
sayHelloJohn();
// function will print: "Hello John!"
sayHelloLucy();
// function will print: "Hello Lucy!"
Can you think of a different solution?

Sometimes we may want to tell the computer to do very similar things, but not exactly the same each time. Here is when parameters come to rescue!

For example, we may want to tell the computer to sayHello to different people each time.

In this example, we could use the same function and pass to the function the name of the person we want to say hello to.

function sayHello(name) {
  console.log(`Hello ${name}!`);
}

sayHello('Mery');
// name = Mery
// function will alert: "Hello Mery!"

sayHello('John');
// name = John
// function will alert: "Hello John!"

sayHello('Lucy');
// name = Lucy
// function will alert: "Hello Lucy!"
We can have as many parameters in a function as we want.

Parameter: the variable name which is part of the function declaration.
Argument is the value passed to function in the moment of its invocation.

function sayHelloManyTimes(name, howManyTimes) {
  for (let i=0; i < howManyTimes; i++) {
    console.log(`Hello ${name}!`);
  }
}


sayHelloManyTimes('Michael', 2);
// => Hello Michael!
// => Hello Michael!

sayHelloManyTimes(3, 'ERROR');
// Will this work?

sayHelloManyTimes(2);
// Will this work?

sayHelloManyTimes('ironBrain');
// Will this work?
Cool huh? :)

JavaScript Callback Functions
When we pass an argument to the function, we can pass any variable type we know, even other functions 😱 They are know as callback functions.

A callback function is a function that is passed to another function as a parameter and will be executed after another function is finished executing, and that’s where the name cames from - “call back”.

Now there can be a question - why would we pass a function as a parameter to the other function?

Let’s create an example:

function eatDinner(){
  console.log("Eating the dinner 🍽");
}

function eatDessert(){
  console.log("Eating the dessert 🍰");
}

eatDinner(); // <== Eating the dinner 🍽
eatDessert(); // <== Eating the dessert 🍰
Great, one function executed and then another so we got the dinner first and then we got the dessert.
But, you know, sometimes the dinner prep can take a reaallllly long time and then if we don’t handle the situation properly, we could be in the situation to get the dessert before the dinner is even served. (Which is not that bad especially if they serve Tiramisu 🥳)
We will simulate this situation just delaying the execution od eatDinner() function for a couple of seconds using the setTimeout() function. We will use setTimeout much later; now we need it just to show what would happen if one of the functions didn’t execute on time.

function eatDinner(){
  setTimeout(function(){
    console.log("Eating the dinner 🍽");
  }, 1000)
}

function eatDessert(){
  console.log("Eating the dessert 🍰");
}

eatDinner(); 
eatDessert(); 

// the console:
// Eating the dessert 🍰
// Eating the dinner 🍽
As we can see, we called first eatDinner() function and then eatDessert() but in the console, the first conole.log is from the second function. This means that JavaScript didn’t wait for the response from the first function, but instead, it moved to the second and then after 1000 milliseconds (that’s the delay we passed to the setTimeout) it executed the first function.

This kind of situations are very often, and you will deal with them especially in the module 2 and 3 when working with some API requests (you will know everything about this, just patience 🙏🏻). Imagine situation where you need a lot of data from some API and then to load the page with that data displayed - if it takes a bit longer time to get the data, and you don’t handle this situation using callbacks or some other approach, you will end up displaying an empty page to users since the page will load before the delayed data arrives.

Do you understand now a bit better why we need callbacks? Yes, correct!

The callbacks are the way to make sure that some piece of code doesn’t execute before some other code hasn’t finished executing.

Now let’s use the knowledge we just got and make sure we get that dinner before the dessert comes.

function eatDinner(callback){
  console.log("Eating the dinner 🍽");
  callback();
}

function eatDessert(){
  console.log("Eating the dessert 🍰");
}

eatDinner(eatDessert); // <== notice that there's NO () when passing a function as argument here

// Eating the dinner 🍽
// Eating the dessert 🍰
:pencil: Time to practice
Play around with the example below and try to understand it:

function functionOne(x) {
  console.log(x);
}

function functionTwo(var1, var2) {
    var2(var1);
}

functionTwo(2, functionOne);
What is printed in the console and why?

Returning values
Functions help us bundle different instructions together, and we can also add parameters to the function so that its behavior will change depending on those parameters. Functions also have an interesting property; they return a value.

It is not mandatory to explicitly return a value in a function, but it is strongly recommended that you do so when it makes sense. Why return a value? Because we can later use that returned value inside an expression, assign it to a variable, etc.

Potential interview question:
A JavaScript function always returns something.
When a returning value is not specified, the function returns undefined.

We already covered undefined as primitive data type but here you can refresh your knowledge.

Example 1:

function printName(name){
  return name;
}

printName("Ana"); 

// console:
// Ana
Example 2:

function calculateTotalPrice(price, taxPercent){
  if(typeof price !== 'number' || typeof taxPercent !== 'number'){
    return `You have to pass number values!`;
  }
  const theTaxPart = price * taxPercent / 100
  return `${price + theTaxPart} €`;
}

calculateTotalPrice(5, 7); // <== 5.35 €
As you can see, one function can have more one return statement. In the previous example, we took care of the edge case if user passed the string or some other type of value and if that would be the case we would return a message to user. This leads us to one more conclusion: there’s nothing after return, that is the last statement in the function. If the user passed a string instead of a number, they would get the message, and the rest of the code would never execute.

Return a function
We can also return another function, let´s see an example:

function anotherFunction(text){
  console.log(`Hello ${text}!`);
}

function oneFunction(name) {
  return anotherFunction(name);
}

oneFunction("Lluis");

// Prints "Hello Lluis"
Random Example
We already covered Math.random() method and here we will play a bit with it and try to apply it in the function.
Math.random() returns a floating-point, pseudo-random number in the range [0, 1) that is, from 0 (inclusive) up to but not including 1 (exclusive).

var zeroToOne = Math.random();   // Random integer number [0,1]

// Returns a random number between min (inclusive) and max (exclusive)
function getRandomArbitrary(min, max) {
  return Math.random() * (max - min) + min;
}
The example above was very simple and had only one instruction. However, we can have many instructions inside one function:

function gradeTheStudent () {
  const grades = ['Master', 'Good', 'Acceptable', 'Average', 'Poor', 'Fail'];

  let randomNumber = Math.random();            // Random decimal [0.0 - 1.0)
  randomNumber = randomNumber * grades.length; // Random decimal [0.0 - 6.0)
  randomNumber = Math.floor(randomNumber);     // Random integer [0   - 5]

  return grades[randomNumber];
}

const myGrade = gradeTheStudent();
console.log(myGrade);
We will be talking more about arrays very soon but we assume you remember basics from your prework. If you need a short reminder, you can sneak peak to the official MDN Array docs.

Anonymous functions
An anonymous function is a function that was declared without any named identifier to refer to it.

We actually already used an anonymous function in one of the snippets above with setTimeout():

setTimeout(function(){
    console.log("This is just an example of anonymous function since this function really doesn't have a name.")
}, 1000);
If we, for some reason, need to name this function, that could look like this:

function someFunctionName(){
    console.log("This is just an example of anonymous function since this function really doesn't have a name.")
}

setTimeout(someFunctionName, 1000);
But if we never again will use this function (someFunctionName()) there’s no need to name it really.

:thumbsup: An anonymous function is usually not accessible after its initial creation unless we assign it to a variable and keep a reference to it, like in this example:

const anon = function(){
  console.log("An0nym0us Funct10n");
}

anon();
// An0nym0us Funct10n
To summarize:

:bulb: Anonymous functions also help us avoid naming things that don’t necessarily need a name.

Anonymous functions can be used as a parameter passed to another function.


function doSomethingWithAFunction(name, functionToCall){
  functionToCall(name);
}
                                       // Anonymous Function
doSomethingWithAFunction("Ironhacker", function(someParameter){
  console.log(`Hello ${someParameter}.`);
});
// => Hello Ironhacker.
                                       // Anonymous Function
doSomethingWithAFunction("Ironhacker", function(someParameter){
  console.log(`Goodbye ${someParameter}.`);
});
// => Goodbye Ironhacker.

                            // Anonymous Function
doSomethingWithAFunction(2, function(someParameter){
  console.log(2 + someParameter);
});
// => 4
It’s important to become familiar with anonymous functions. We will use them during this course, but for now, it’s enough for you to know that they exist 😉

Practice Abstraction
Let´s imagine we are creating our own Math Quiz Game. For our game, we need to generate some quizzes, and it must be a way to do it randomly with JavaScript code.

All the quizzes are sums and should be adding 2 numbers between 0 and 100.

const newQuizz = Math.floor(Math.random()*101) + "+" + Math.floor(Math.random()*101);

console.log(newQuizz);

//We should get `a randomNumber`+ `a randomNumber`
Great, we have our quiz!

☝️ But we have a problem! This is a game, so we will need to make a lot more quizzes, right? And our code just runs it just once.

If we want to do it again, we need to type it out all over again. Instead, we can isolate the random number generator, and the quiz generator, into functions.

//with a function, we can event set different limit each time we call the function
function getRandomNumber(limit){
  return Math.floor(Math.random()*(limit+1));
}

function makeAQuizz(limit){
  const generateQuizz = getRandomNumber(limit) + "+" + getRandomNumber(limit);
  return generateQuizz;
}

newQuizz = makeAQuizz(100);
newQuizz = makeAQuizz(200);
newQuizz = makeAQuizz(300);

// Now we can create as many quizzes as we want, and change the limit as many times as we want!
Functions and variable declarations - matter of scope
Here we will touch a matter of scope in JavaScript.

A scope is a context in which a function or a variable is visible or can be referenced from different parts of code.

The matter of scope is pretty complex, and we have to be careful when introducing this concept so for now, let’s just talk about global and local/functional scope.

Local scope
A variable declared inside the function is scoped to that function, meaning it’s not possible to access it (use it) outside the function.

Let’s see the example:

function sayHello() {
  let firstName = "Ana"; // <== local variable
  console.log(`Hello ${firstName}!`); 
}

sayHello(); // <== Hello Ana!
console.log(firstName); // <== ReferenceError: firstName is not defined
Global Scope
If a variable is declared outside of the function, it is possible to use it in and outside of the function.

const firstName = "Ana"; // <== global variable
function sayHello() {
  console.log(`Hello ${firstName}!`); 
}

sayHello(); // <== Hello Ana!
console.log(firstName); // <== Ana
:warning: It is also possible to modify variables defined in the outter scope in the function.

let firstName = "Ana"; // <== global variable
function sayHello() {
  firstName = "Martina";
  console.log(`Hello ${firstName}!`); 
}

console.log(`Before the function executes the first name is ${firstName}.`); // <== Before the function executes the first name is Ana.
sayHello(); // <== Hello Martina!
console.log(`After the function executes the first name is ${firstName}.`); // <== After the function executes the first name is Martina.
However, since these are the two separate scopes, it is possible to declare the same named variables in both scopes. This is known as variable shaddowing. When it comes to variable shadowing, the function will use the variable declared locally (in the function):

let firstName = "Ana"; // <== global variable
function sayHello() {
  let firstName = "Martina"; // <== local variable with the same name as the global one
  console.log(`Hello ${firstName}!`); 
}

console.log(`Before the function executes the first name is ${firstName}.`); // <== Before the function executes the first name is Ana.
sayHello(); // <== Hello Martina!
console.log(`After the function executes the first name is ${firstName}.`); // <== After the function executes the first name is Ana.
To make a final conclusion:

Global variables are accessible from any function unless they are shaddowed by local variables (locally created variables with the same name).

Function Expression
So far we talked about function declaration which has this format:

                //     having parameters 
                //     is optional
                //         |
function someName(someParameters){
    // some code here
}
But we also saw in one of the previous examples something like this:

let someName = function(){
    // some code here
}
Now, we will explain the difference:

the first code snippet is function declaration
the second code snippet is function expression
What is the difference you might ask now?
Well besides the obvious difference in syntax, the more important difference is when the function is actually created by the JavaScript engine that executes the code.

Function Expression is created in a moment when the execution reaches to that point in the code, and it can be used from that point on
Function Declaration is created at the very beginning when the script starts the execution which means that this kind of functions can be used even before then they are created in the code
Let’s see the example and it should be easier to understand:

// Function Expression
greeting("Ana"); // TypeError: greeting is not a function

let greeting = function(name) {
  console.log(`Hello, ${name}`);
}
So using Function Expression we can’t call a function before it is initialized.

greeting("Ana"); // Hello Ana

function greeting(name) {
  console.log(`Hello, ${name}`);
}
So using Function Declaration we can call a function before it is initialized.

:warning: However, like for almost every rule, there’s an exception: if function declaration is inside some block scope (this is a new thing for you, but for now think of it like it is a local scope), it’s not reachable for the outside.

Let’s see:

let name = prompt("What is your name?");
if (name){
  function greeting(name) {
    console.log(`Hello, ${name}`);
  }
  greeting(name); // <== Hello nameYouEntered
}

greeting(name); // <== ReferenceError: greeting is not defined
In the previous example, greetings() lives inside the scope of the if statement, so it’s reachable only in there. Outside, it doesn’t exist.
Can we make it available outside? Yes. We could turn it into function expression and declare a variable in the outer scope, outside of the if statement.

let name = prompt("What is your name?");
let greeting;
if (name){
  greeting = function(name) {
    console.log(`Hello, ${name}`);
  }
  greeting(name); // <== Hello, nameYouEntered
}

greeting(name); // <== Hello, nameYouEntered
The error is gone 🏆

Next question you might have - when to use function declaration and when to go for function declaration?

:thumbsup: As a rule of thumb, when creating the function, the first choice should be function declaration since it gives more freedom and you can use it, if needed, even before it’s declared. But, if for some reason, using function declaration doesn’t serve you well, then go ahead and use function expression.

Arrow functions
One of the updates of ES6 was introducing a simpler syntax for creating the functions. This way reminds a lot of function expression and it’s called arrow functions. Let’s reuse one of the examples from before:

// function expression:
let greeting = function(name) {
  console.log(`Hello, ${name}`);
}

// arrow function:
let greeting = name => {
  return name;
}
As we can see, the keyword function is skipped, the parameter doesn’t have braces around (although this changes when we have more than one parameter) and there’s => arrow between the parameter and the body ({...}) of the function.
But this function can, even more, be shortened - since we return only one expression (there’s only one line of code in the body), we can omit the braces and skip the return since it’s implicit:

let greeting = name => name;

greeting("Ana"); // <== Ana
So much cleaner and shorter!
In case there are no parameters passed then empty parentheses are mandatory:

let greeting = () => console.log("Hello there!");
As a conclusion:

If the right side is only a one-line expression, we can omit the curly braces and return statement is omitted as well. However, if we need to write multiline statements in the function, then we can do it using the curly braces {...} and using mandatory return statement.

Writing Good Functions
Functions are one of the pillars of programming. Functions help us to keep our code clean and well organized, and as we write more and more code.

Reuse code: We can call a function as many times as we need it in our code, but we only need to define how it works once :)
Abstraction is a technique that allows us to think at higher, more abstract levels.
Ie. if we know what Math.floor() does, we can use it happily in our code… we don’t have to worry about how math.floor() performs it’s magic. It’s abstracted from us
Separation of Concerns: Functions allow us to separate a big problem into many smaller ones.
Single Responsibility Principle: A function has to do just one thing, and the name of the function has to be very clear so you can identify what is doing just reading the name.
Code reuse and division of responsibilities
From generalization, code reuse arises in a natural way: now we can perform the same operation on different places without repeating a single line of code. We are reusing the function.

Division of responsibilities refers to the level of isolation. One function should only do one thing. It sounds simple, but mastering the division of responsibilities is not that easy. Here are some tips:

Name your functions with verbs, but only one verb per function.
Making a decision is one thing to do
If your function is more than 20 lines of code, you’re probably doing it wrong.
If you’re grouping bunches of instructions, you’re probably doing more than one thing.
Refactoring
Code Refactoring is a technique in software development by which we change the way the code is structured, keeping the same functionality.

It is a good practice to refactor our code often, as it will help us to make it better, more modular, and easier to maintain.

Examples of refactoring techniques may include techniques such as:

Choosing better names for variables, functions, etc.
Taking pieces of functionality and abstracting them in separate functions
Let’s look at our avg() function:

function avg(array) {
  if (array.length === 0 ) { return; }

  for (let sum=0, i=0; i < array.length; i++) {
    sum += array[i];
  }
  return sum/array.length;
}
If we think about it, it actually does two separate things:

It calculates the sum of all the items in the array
It divides them by the length of the array
We can further improve this by isolating one of those calculations into a separate function. We need to break down the code so that it does the same thing, but it’s easier to understand.

Let’s call the first step sum() and make it into it’s a separate function. Then the avg() could be rewritten, now using our sum function:

function sum(array) {
  for (let sum=0, i=0; i < array.length; i++) {
    sum += array[i];
  }
  return sum;
}

function avg(array) {
  if (array.length === 0) { return; }
  return sum(array) / array.length;
}
As you can see, we are calling the functionsum() as part of the expression for the return statement of the avg() function. Cool, right?

Bonus: Recursion


Some function definitions are implemented in a way they use their own definition. It’s like function inception.

For instance, a factorial function is defined as factorial of n is n times the factorial of n - 1, except for factorial of 0, which is 1. Therefore, we can write this as:

function factorial(number) {
  if (number === 0) { return 1; }
  return number * factorial(number - 1);
}

factorial(4);
// 4 * factorial(3)
// 4 * 3 * factorial(2)
// 4 * 3 * 2 * factorial(1)
// 4 * 3 * 2 * 1 * factorial(0)
// factorial of 0 is 1 :)
// 4 * 3 * 2 * 1 * 1
// 4 * 3 * 2 * 1
// 4 * 3 * 2
// 4 * 6
// => 24
Functional Programming
Functional Programming (FP) is a programming paradigm based on the following principles:

using pure functions
avoiding data mutation and
avoiding side-effects.
Let’s now see what this means.
Pure function is a function which:

given the same inputs always returns the same outputs
has no side-effects.
If you want to read more, you can start here.

Immutability is one of the core concepts of functional programming. Basically means that once it’s created, value can’t be modified. Here please remember: immutable doesn’t mean creating a variable with const. const creates a variable that can’t be reassigned after it’s created. Creating a variable using const doesn’t make it immutable.

Side-effect that needs to be avoided is modifying any external variable, ex. a variable declared in the global scope. There are more side effects, and you can read more about it here.

FP has the following (non-exhaustive) features:

First-Class Functions: which means you can treat a function as any other piece of data: assign it to variable, pass it to the other functions, return them from functions, etc.
var add = function (a, b) {
  return a + b;
};

add(2, 3) // => 5
High-Order Functions: are any functions that can return functions or receive other functions as parameters.
var add = function (a) {
  return function (b) {
    return a + b;
  };
};

var add2 = add(2);
add2(3);
// => 5

add(4)(5);
// => 9
Functional programming is a declarative paradigm, meaning that the program logic is expressed without explicitly describing the flow control, but rather expressing what needs to be done.

Imperative programming is more descriptive - describes the steps that need to be taken to achieve results. This kind of programming is more focused on how to do things.

To summarize this short intro to functional programming:

FP prefers

pure functions over side-effects
immutability over mutating data
reusable code based on high-order functions
declarative over the imperative approach
