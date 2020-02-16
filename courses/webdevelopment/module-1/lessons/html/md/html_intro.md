class: center, middle, inverse

###<img src="https://imgur.com/WKQ9juz.png" width=20% height=20% alt="logo">

---
name: default
layout: true
task: &nbsp;

.task[{{task}}]


---
name:contenido

### Contenido

[Introducción](#intro)

[Elementos de Bloque vs En línea](#bloquelinea)

[Etiquetas estructurales y semánticas](#semanticas)

[Pasos para generar una página HTML](#generacionpagina)

---
name:intro
task: [<< índice de contenidos >>](#contenido)

## Introducción: El desarrollador web

- Mindset programador => patrones
- Conocer la tecnología
- Trabajo en equipo
- Saber buscar / preguntar => Aprender a aprender
- Aprendizaje continuo
- Divertirse

---
class: center, middle, inverse
<img src="https://imgur.com/CjNBExj.png" width=90%>

---

## Introducción: Aplicaciones web

- Son __aplicaciones__ que los usuarios pueden utilizar accediendo a un __servidor web__ a través de Internet o de una intranet mediante un __navegador__.

- Es una aplicación de software compuesta por páginas web que se codifican en un lenguaje soportado por los navegadores web, a los cuales se confía su ejecución.

Existen aplicaciones como los webmails, wikis, weblogs, tiendas online… son ejemplos bien conocidos de aplicaciones web.

Otras aplicaciones son más del ámbito empresarial como ERPs, CMSs, CRMs, aplicaciones de gestión

Una página Web puede contener elementos que permiten una comunicación activa entre el usuario y la información. 

  - Por ejemplo rellenar y enviar formularios, participar en juegos diversos y acceder a gestores de base de datos de todo tipo.

---

### Tipos de aplicación web

__Orientada a la presentación__

Genera paginas web  interactivas que contienen varios tipos de lenguaje de marca (HTML, XML, etc.) y contenido dinámico en respuesta a peticiones.

__Orientada al servicio__

Estas paginas implementan el punto final del servicio web. Son los servicios Web


Las aplicaciones orientadas a la presentación frecuentemente son clientes de las aplicaciones web orientadas al servicio.

---
### Interacción entre un cliente y una aplicación Web

- El cliente envía una petición HTTP al servidor  web 
- Las tecnologías del servidor convierten la petición en un objeto  que representa la petición
- Esta petición es entregada a un componente Web, el cual puede interactuar con otros componentes para - generar un contenido dinámico
- El componente web puede generar un objeto que representa la respuesta
- El servidor web convierte este objeto en una respuesta HTTP y es enviada a su cliente.

---
### Ejercicio 1
<hr>

Examina la aplicación https://freedcamp.com/
- Date de alta
- Crea proyectos
- Observa sus funcionalidades
- Qué valor que aporta?

---
## Introducción: HTML

HyperText Markup Language (HTML) es un lenguaje para crear páginas y aplicaciones web. Las instrucciones de HTML definen la estructura de las páginas web.

Una página web es una colección de muchos tipos de contenido. Puede haber texto, gráficos, formularios, audio, vídeo, etc. Estos elementos se definen dentro de las etiquetas de HTML. Los navegadores usan estas etiquetas para decidir cual es el orden y el estilo del contenido que se muestra en la pagina.

Los ficheros HTML son sólo ficheros de texto. El formato de texto es la manera universal de representar los datos en los ordenadores; cualquier fichero HTML creado en un PC Windows puede funcionar en un Mac, Linux/Unix, o cualquier sistema operativo.

---

## Puesta en práctica

Mira la imagen:

<img src="https://imgur.com/DhgcTot.png" width=50% style="float:left; margin-right: 1em;">

<span> Muestra una página web sencilla con un título, un menú, una foto y algo de información escrita.

Los navegadores Web leen y muestran el resultado de las etiquetas HTML. Estas etiquetas, con algo de ayuda de CSS, que veremos más adelante, indican al navegador la manera de realizar estos procesos.
</span>
---

En el fichero HTML anterior encontrarías los siguientes componentes.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>The HTML5 Breakfast Site</title>
    <meta charset="UTF-8" />
  </head>
  <body>
    <div id="container">
      <div id="topnav">
        <a href="index.html">HOME</a> | <a href="about.html">ABOUT US</a> |
        <a href="menu.html">MENU</a> |
        <a href="contact.html">CONTACT US</a>
      </div>
      <div id="content">
        <h1>The good breakfast</h1>
        <!-- Insert your preformated text here -->
        <p>Here you will find all sorts of delicious treats</p>
        <figure>
          <img
            src="https://i.postimg.cc/htxcJGB6/ZKkCecn.jpg"
            width="400"
            alt="breakfast"
          />
          <figcaption>powered by biscuit.</figcaption>
        </figure>
      </div>
      <!-- Insert paragraph here -->
      <!-- Insert your menu here -->
      <!-- Insert your reservations form here -->
      <div class= footer>
        <p class="love">From the oven with love</p>
      </div>
    </div>
  </body>
</html>
```
---

### Ejercicio 2
<hr>

Intenta localizar los siguientes componentes en el código anterior:

__Title__: The HTML5 Breakfast Site

__Navigation Bar__: (HOME | ABOUT US | MENU | CONTACT US)

__The breakfast Image__

__The signature of the webpage creators__

---

### Estructura HTML básica

```html
<!DOCTYPE html> 
<html>
  <head>
	<title>My first document</title>
	<meta charset="UTF-8">
  </head>
  <body>
	...
  </body>
</html>
```

__`<!DOCTYPE html>`__: <span style="font-size:14px"> Indica que el lenguaje de marcas de la página es HTML5.</span>

__`<html>`__:<span style="font-size:14px"> Es la raíz del documento HTML. El resto de elementos de la página deben ser descendientes de este elemento.

__`<head>`__:<span style="font-size:14px"> Define un elemento que proporciona información general (metadatos) sobre el documento, como por ejemplo el título o los _links_ a ficheros de script u hojas de estilo:

__`<title>`__:<span style="font-size:14px"> Título del documento. Se muestra en la pestaña del navegador.

__`<meta>`__:<span style="font-size:14px"> Incluye información sobre estilos, scripts y datos que ayudan al navegador a renderizar la página. Uno de los más comunes es el `<meta charset="UTF-8">` en nuestro ejemplo. Indica el tipo de codificación del documento como UTF-8.

__`<body>`__:<span style="font-size:14px"> engloba el contenido del documento. Cada componente HTML se debe escribir con etiquetas de apertura y cierre. Sólo puede haber un elemento `<body>`.

---
### Sintaxis HTML5 - Etiquetas

La sintaxis de HTML se basa en etiquetas:
https://developer.mozilla.org/es/docs/HTML/HTML5/HTML5_lista_elementos:

<img src="https://imgur.com/Y63lvbc.png" width=90%>

---
name: bloquelinea
task: [<< índice de contenidos >>](#contenido)

## “Block” Vs “Inline”

<p style="background-color:palegoldenrod">Este es uno de los conceptos que deben quedar muy claros para interpretar correctamente la disposición de los elementos HTML y la aplicación de estilos CSS.</p>

Dentro del elemento `<body>` escribiremos los elementos que queremos mostrar en la página. Estos elementos serán de tipo __bloque__ o __en línea__.


Miremos el ejemplo en CodePen:

<iframe height="265" style="width: 100%;" scrolling="no" title="JavaScript - Block vs Inline" src="https://codepen.io/rglepe/embed/KKpKRxj?height=265&theme-id=default&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/KKpKRxj'>JavaScript - Block vs Inline</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

## Elementos de Bloque

Son aquellos que hacen comenzar una nueva línea en la pagina. Si no se proporciona un ancho, se extiende todo el ancho disponible de su elemento padre.

Ejemplos de bloque son los párrafos o las divisiones de páginas. 

Haz click en __`Edit on CodePen`__ para poder modificar el código

<iframe height="265" style="width: 100%;" scrolling="no" title="HTML Body block Elements" src="https://codepen.io/rglepe/embed/dLZXOQ?height=265&theme-id=default&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/dLZXOQ'>HTML Body block Elements</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

### Ejercicio 3: CodePen
<hr>

En la sección HTML del CodePen anterior, encontrarás el código en el _body_ del archivo HTML. CodePen permite simplificar el código, añadiendo por nosotros el resto de metadata, doctype y otra información de las cabeceras.

Si echas un vistazo, verás que también hay una pestaña para CSS y otra para JavaScript. Las tres en conjunto dan lugar a la página final.

Vamos a añadir a la pestaña de HTML un nuevo párrafo que explique algo de nuestro lugar favorito para desayunar. Para ello usaremos la etiqueta `<p>` para el párrafo, sustituyendo el comentario:

`<!-- Insert paragraph here -->`

Haz copy paste de este código:

```html
<p>Our commitment is to use impeccable sourcing and quality ingredients to help 
  you code.An ongoing collaboration between the classroom staff and the development
   team allow us to iterate our content and give our students the coding 'fruits and
    vegetables' -mainly made of JavaScript- that they need to grow as a healthy 
    developer.</p>
```
---

### Párrafos

Etiqueta `<p>`. Los parrafos son bloques de texto separados de bloques contiguos por un espacio vertical y/o una indentación en la primera línea.

### Texto preformateado

Etiqueta `<pre>`. El texto entre estas etiquetas se muestra en fuente no proporcional (“monospace”), igual que si estuviera en el fichero, básicamente es la fuente en que se muestra el código.

<pre>This is a preformatted text</pre>

### Cabeceras

Seis niveles de cabeceras: `<h1>` es la más importante y `<h6>` la que menos. Describe brevemente el tema de la sección.

```html
<h1>Heading level 1</h1>
<h2>Heading level 2</h2>
<h3>Heading level 3</h3>
<h4>Heading level 4</h4>
<h5>Heading level 5</h5>
<h6>Heading level 6</h6>
```

Cópialos al  CodePen para ver cómo se muestran!

---
### Listas

__Ordenadas__: `<ol>` Cada miembro de la lista se numera.

__Desordenadas__: `<ul>` Aparecen con un indicador.

Para averiguar cuándo usar una u otra: prueba a cambiar el orden de los elementos; si cambia el significado entones debes usar `<ol>` si no, utiliza `<ul>`.

No hay límite en la profundidad y solapado de listas de elementos `<ol>` y `<ul>`.

### Elementos de lista

Se declaran como `<li>`. Necesitan siempre un elemento contenedor (`<ol>` ó `<ul>`).

Ej:

```html
<ol>
  <li>first item</li>
  <li>second item</li>
  <li>third item</li>
</ol>
```

---

### Tablas

table, tr, td, tfoot, thead

La etiqueta `<table>` se utiliza para expresar información en dos dimensiones. Requiere otros elementos en el interior para que tenga sentido.

El elemento de fila `<tr>` define una fila de celdas en una tabla. Si es la fila de cabeceras hay que usar `<th>` (table header), si no usaremos `<td>` (table data).

Ejemplo:

<table style="float:left; font-size:0.75em">
  <tr>
    <th>Nombre</th>
    <th>Curso</th>
    <th>Ciudad</th>
  </tr>
  <tr>
    <td>José Todo</td>
    <td>FullStack WebDev</td>
    <td>Madrid</td>
  </tr>
  <tr>
    <td>Karen Latada</td>
    <td>FrontEnd WebDev</td>
    <td>Barcelona</td>
  </tr>
  <tr>
    <td>Jim Nasium</td>
    <td>MasterChef WebDev</td>
    <td>Toronto</td>
  </tr>
</table>

```html
<table>
  <tr>
    <th>Name</th>
    <th>Bootcamp</th>
    <th>City</th>
  </tr>
  <tr>
    <td>José Todo</td>
    <td>FullStack WebDev</td>
    <td>Madrid</td>
  </tr>
  <tr>
    <td>Karen Latada</td>
    <td>FrontEnd WebDev</td>
    <td>Barcelona</td>
  </tr>
  <tr>
    <td>Jim Nasium</td>
    <td>MasterChef WebDev</td>
    <td>Toronto</td>
  </tr>
</table>
```



---

### Formularios

El elemento `<form>` indica una sección del documento que el usuario puede utilizar para introducir información en la página. Incluyen elementos __inputs__, __radio buttons__, __select boxes__, etc. Normalmente la información se envía al servidor web, pero también podemos manipularla con JavaScript.

Requiere dos atributos para funcionar correctamente: __action__ y __method__.


#### Action
Proporciona la URI al programa que procesa la información del formulario.Es decir, dónde hay que enviar la información

#### Method
Indica  el método HTTP que debe utilizar el navegador para enviar el formulario.

El método HTTP POST envía todo el formulario con los datos, al servidor.


Ejemplo:

```html
    <form action="" method="post">
        <label for="name">Name:</label>
        <input id="name" type="text">
        <button type="submit">Save</button>
    </form>
```

---
#### Fieldset

El elemento `<fieldset>` se utiliza para agrupar controles con una única etiqueta dentro del formulario (`<label>`) 

Se utilizan para aplicar estilos conjuntos, organizar o proporcionar características de accesibilidad.

Ejemplo de campo agrupador con un elemento clicable.

```html
<form action="/users" method="post">
  <fieldset>
    <input type="radio" id="radio"> <label for="radio">Click me</label>
  </fieldset>
</form>
```
---


### Ejercicio 4
<hr>


1. Usa `<pre>` para añadir un mensaje divertido: "Buen código y buen café, cada día"

2. Crea un menú para indicar el café que servimos.
  - Introduce una cabecera que indique el menú.
  - Una lista de Cafés: Café latte, Americano, Machiatto, Capuccino
  - Una lista de tés: Earl Grey, Té verde, Rooibos

  Insértalo en CodePen reemplazando el comentario:

  `<!-- Insert your menu here -->`

3. Crea un formulario de reservas, con el título "Reservas Aquí". De momento queda vacío.

    `<!-- Insert your reservations form here -->`

4. ➕ Bonus: Transforma el menú en una tabla. 

---

### Elementos en línea

Los elementos __en línea__ fluyen con el texto. No comienzan en una nueva línea y aparecen justo al lado derecho del elemento previo

Algunos ejemplos

#### Énfasis del texto

Vamos a enfatizar las palabras “impeccable” y “quality” rodeándolas de etiquetas _em_:

    ... commitment is to use `<em>`impeccable`</em>` sourcing
    and `<em>`quality`</em>` ingredients...

Modifica codepen para ver el resultado

---
_Cuándo usamos `<i>` y cuándo `<em>`?_

Aunque el resultado visible es cursiva (_italic_) la diferencia se encuentra en el significado de la enfatización. 

 `<em>`, en el caso: “Just _do_ it already!”, o: “We _had_ to do something about it”. Una persona o software leería el texto enfatizando las palabras marcadas.

`<i>` en: “The _Queen Mary_ sailed last night”. Aquí se resalta la palabra “Queen Mary” para indicar que es un término en otro idioma o para diferenciarlo de "queen" Mary. Otro ejemplo de `<i>` sería: “The word _the_ is an article”.

---

#### Strong

Damos importancia a un texto mostrándolo en negrita (_bold_).

#### Fechas y horas

`<time>` lo utilizaremos para presentar horas interpretables por la máquina. Podríamos acompañarlo del atributo `<datetime>`, y en este caso el texto podría ser en forma to humano.

#### Links (Ánclas)

`<a>` Definen hipervínculos a lugares de la misma página o a otras páginas web. Llevan el atributo ‘href’.`<a href = "http://www.example.com">`

#### Break
`<br>` provocan un salto de línea (retorno de carro) y no llevan etiqueta de cierre.

#### Ímagenes
`<img>` define una imagen. Va seguido del atributo ‘src’ y es obligatorio añadir la URL de la imagen.

    <img src = "http://www.example.com">

---

#### Scripts

`<script>` se utiliza para incluir código o referencias a archivos ejecutables dentro de un fichero HTML.

#### Spans

`<span>` contenedor en línea genérico, normalmente se utiliza para agrupar elementos con propósitos estilísticos. No es muy recomendable.

#### Botones

`<button>` se transforma en un botón <button>clicable</button>.

#### Inputs

Se utiliza para crear controles interactivos en formularios web que acepeten datos del usuario. Su funcionamiento depende de los atributos.

---

#### Etiquetas

Etiquetas de elementos en la pantalla. Pueden asociarse a otros controles si éstos los incluímos entre las etiquetas de `<label></label>`, o si usamos el atributo _for_. Un elemento _input_ puede asociarse a muchos _label_

#### Selects

El elemento `<select>` representa un control de menú de opciones. Cada opción se representa con elementos `<option>`, que se pueden agrupar con elementos `<optgroup>`.

#### Áreas de texto

`<textarea>` es un elemento de control de texto multilínea. Se puede indicar su tamaño en columnas y filas.

---
### Ejercicio 5
<hr>

1. Usa `<strong>` para resaltar las palabras ‘impeccable’ and ‘quality’:


2. Añade un link __‘Contact Us’__ en la sección del pie de página. Debería abrir la aplicación de correo del usuario y enviar un mail al equipo:

3. Muestra el horario de apertura del restaurante dentro del pie de página:

4. Crea dentro del formulario anterior, la información que queremos recoger para hacer una reserva:

  - Elemento input con etiqueta para recoger el nombre.
  - Elemento select de opciones para elegir entre Desayuno o Merienda
  - Elemento select para elegir cuántas personas serán (de 1 a 4).
  - Botón de tipo submit para enviar la información

5. Ahora juega un poco con el resto de elementos. Inserta un elemento span, cambia o personaliza el texto. Inserta nuevas imágenes, áreas de texto para clientes con alergias,...

---

### Elementos ocultos

Un tercer tipo de elementos en HTML: Los que no se muestran nunca. Llevan información relevante para el navegador (como por ejemplo todos los elementos de la sección `<head>`).


---
name:semanticas
task: [<< índice de contenidos >>](#contenido)

### Etiquetas estructurales y semánticas

★ Crean el armazón de la página Web

★ Ayudan a los buscadores en su labor de indexación “inteligente” de las páginas.

★ Aportan información acerca de la relación semántica entre los elementos

★ Recogen la información específica, que tiene en si un significado común (fechas, comentarios, entradas, calendarios, etc.)

---
class:inverse

### Estructura en HTML5: El santo Grial
<br>
<br>
<br>
<br>
![](https://imgur.com/EtTZEk7.png width=50%)

---

### Divitis

Enfermedad que sufren muchos desarrolladores web:  Abuso en la utilización de las etiquetas __`<div>`__ y __`<span>`__ como elementos contenedores genéricos y sin significado semántico para reemplazar elementos estructurales de HTML. 

![](https://imgur.com/GXXwsf9.png)

---
### Validación de HTML

https://validator.w3.org/

---
### Ejercicio 6
<hr>

Utiliza cualquier referencia de elementos semánticos y rehaz el ejemplo de CodePen con elementos semánticos de manera que no se altere la presentación.

---
name:generacionpagina
task: [<< índice de contenidos >>](#contenido)

### Pasos para generar una página HTML

1. Generar el sketch
   
2. Identificar los bloques y codificarlos
   
  - Primero horizontales y luego verticales
  
3. Identificar los sub-bloques dentro de los bloques en 2 y codificarlos
   
4. Repetir 3 hasta que se completen los detalles

---
### 1. Generar el sketch

![](https://imgur.com/AS3Dua4.png)

---
### 2. Identificar los bloques y codificarlos

<img src="https://imgur.com/WG9nwFB.png" width=75%>

---

<img src="https://imgur.com/a2942Up.png" width=75%>
![](https://imgur.com/3Pb9wvJ.png)

---

### 3. Identificar los subloques dentro de los bloques y codificarlos

<img src="https://imgur.com/SMgrbAl.png" width=75%>

---

<img src="https://imgur.com/ipSlLxL.png" width=50% style="float:left">

![](https://imgur.com/EImEqob.png)

---
### 3. Repetir hasta que se completen los detalles

<img src="https://imgur.com/wUex5gh.png" width=75%>

---
### Ejercicio 7. Crea una pagina HTML5 básica

★ Crea una Github Page

★ Crea un nueva carpeta y clona el repositorio

★ En VSCode abre el directorio y crea un fichero index.html (Puedes usar emmet: http://docs.emmet.io/cheat-sheet/)

★ Crea una página básica (puedes usar: html:5 ->)

★ Guarda los cambios y haz un push a tu repositorio de GitHub.

---
### Extra Resources

[Guía Rápida de elementos](./pdf/HTML5-Etiquetas.pdf)

[MDN HTML5 Documentation](https://developer.mozilla.org/es/docs/Web/HTML) - Documentación completa desarrollo web.

[html5doctor](http://html5doctor.com/) - Implementar HTML5

[Elementos en línea](https://developer.mozilla.org/es/docs/Web/HTML/Elementos_en_l%C3%ADnea)

[Elementos de bloque](https://developer.mozilla.org/es/docs/Web/HTML/Block-level_elements)

[Elementos semánticos](https://www.w3schools.com/html/html5_semantic_elements.asp)

[Elementos estructurales](https://www.mclibre.org/consultar/amaya/html/html-secciones.html)
