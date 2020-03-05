class: center, middle, inverse

###<img src="https://imgur.com/1IE1sHP.png" width=20% height=20% alt="logo">

---
name: default
layout: true
task: &nbsp;

.task[{{task}}]


---
name:contenido

### Contenido

- [Qué es CSS y como crear estilos inline y en documentos](#intro)
- [Cascada y Herencia](#cascada)
- [Selectores de elementos con element, class, id](#selectores)
- [Selección avanzada de elementos](#selectoresavanzados)
- [Unidades de Medidas, Colores y fuentes](#unidades)
- [Propiedades: margin, padding y border](#caja)
- [Posicionar elementos en la pantalla](#posicionamiento)
- [Flexbox](#flexbox)
- [Diseño Responsive](#responsive)
- [Efectos CSS: transform, transition, animate](#efectos)
- [CSS Grid](#grid)



---
name:intro
task: [<< índice de contenidos >>](#contenido)

## Introducción: Qué es CSS

- Reciben el nombre de __hojas de estilo en cascada__ o __CSS__ (siglas en inglés de cascading style sheets) es el lenguaje usado para definir la presentación de un documento HTML.
- Sin CSS, todas las páginas aparecerían como texto plano e imágenes. Tal y como pasaba con las [primeras páginas de Internet](http://info.cern.ch/hypertext/WWW/TheProject.html)
  
- Una indicación de estilo recibe el nombre de norma o regla de estilo:
    
      ```css
      p {color:red;}
      ```

- El "__destino__" (a quién se aplica una regla) se establece mediante un __selector__.
  

- El WorldWide Web Consortium(W3C) es el encargado de formular la especificación de las hojas de estilo que servirán de estándar para los agentes de usuario o navegadores:
  - http://www.w3.org/Style/CSS/current-work

---

### Norma o Regla de estilo

Una declaración está formada por una **propiedad** con su **valor** asociado.

    h1 {color: rgb(0,240,100); }

<table style="text-align:center";>
<th colspan=8 style="background-color: rgb(0,240,100)">Regla de estilo</th>
<tr style="border: rgb(0,240,100) 3px solid; font-weight:bold;"><td>h1</td><td>{</td><td>color</td><td>:</td><td>rgb(0,240,100)</td><td>;</td><td>...</td><td>}</td></tr>
<tr><td style="background-color: rgb(0,240,100)" rowspan=3>Selector</td><td rowspan=2></td><td style="background-color: rgb(0,240,100)">Propiedad</td><td></td><td style="background-color: rgb(0,240,100)">Valor</td><td></td><td colspan=2  >Propiedad: Valor...</td></tr>
<tr><td colspan=3>Declaración</td><td colspan=3>Declaración...</td></tr>
<tr><td colspan=7>Bloque de Declaración</td></tr>
</table>


---

## Aplicación de CSS

- Inline (dentro de las etiquetas HTML):
  
  ```html
    <p style="color:red">texto</p>
  ```

- Interno:

  ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>CSS Example</title>
    <style>
      p {color: red;}a {color: blue;}
    </style>
    ... 
  ```



Se recomienda no usar estas opciones, ya que acoplan el HTML con el estilo gráfico  

---

### Aplicar CSS Externo (preferido)

Se lleva el cssa un archivo externo. 

Este se referencia desde el HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>CSS Example</title>
    <link rel="stylesheet" href="style.css">
    ...
```

Fichero style.css:

```css
p {
  color: red;
  }
a {
  color: blue;
  }
```

---
name: cascada
task: [<< índice de contenidos >>](#contenido)

## Cascada de estilos

Las hojas de estilo se pueden combinar y las propiedades de todas ellas se van acumulando. Esto es muy útil cuando pensamos en sitios web grandes, donde podemos tener una hoja de estilos básica e ir incorporando otras hojas de estilo.

Puede darse el caso que haya propiedades que se contradigan. Si se da el caso, cómo se soluciona, qué propiedad tienen prioridad. Para ello se establece una jerarquía, en orden de prevalencia:

1. **Propiedades establecidas por el desarrollador**: Según donde se ubiquen pueden tener más o menos prioridad:
    
     `Inline style`> `Internal Style Sheet` > `External Style Sheet`.

2. **Propiedades establecidas por el usuario de la web**: Los navegadores permiten al usuario establecer diferentes propiedades de estilo: tamaño de letra, colores,...

3. **Propiedades establecidas por el navegador**: los navegadores tienen un estilo predeterminado para cada elemento. Si no se ha establecido ninguna propiedad para los ítems anteriores, las propiedades del navegador son las que prevalecen.

---
#### Ejemplo:

El fichero `index.html`:

```html
<!doctype html >
<html lang="es">
<head>
...
<link rel="stylesheet" href="estilos.css" />
<style>
   p {
      color: red;
   }
</style>
</head>
<body>
   <h1>Cabecera</h1>
   <p style="color: blue">Un párrafo</p>
   <p>Otro párrafo</p>
</body>
</html>
```

El fichero estilos.css:
```css
p {
  color: green;
}
h1 {
  color: violet;
}
```
---
### Casuística en la aplicación de Estilos

- En el caso de empate se aplica la última regla de la hoja de estilos.

- En el caso de prevalencia de propiedades del desarrollo y las fijadas por el usuario, se puede alterar el orden mediante la cadena **`!important`** después de la declaración.

```css
body{
   font-size: small !important;
}
```
  - Para que no se apliquen las propiedades del navegador, se pueden definir hojas de estilo que inicialicen todas las propiedades preestablecidas. Se denominan hojas de **reset css**, como las de  meyerweb.com.

```html
<!doctype html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Ejemplo de documento con reset CSS </title>
	<link rel="stylesheet" href="css/reset.css" />
	<link rel="stylesheet" href="css/estilos.css" />
	<!-- añadimos otras hojas de estilo si queremos -->
</head>

<body></body>
</html>
```
---
name: herencia
task: [<< índice de contenidos >>](#contenido)

### Herencia

Las propiedades CSS que aplicamos se transmiten de forma automática a todos los elementos descendientes

Por ejemplo, si aplicamos body {font-size:12px;}, se aplicaría este tamaño de letra a todos los elementos dentro de `<body>`.

Hemos de tener en cuenta que hay __excepciones__. Es decir, hay propiedades que no se propagan mediante la herencia. Las podemos ver en la especificación de cada propiedad en W3Schools según el valor de __`Inherit: Yes o No`__.

  - Por ejemplo, `font-size` sí lo es, `background-color` no.

#### Valores especiales

|Valor|Significado
|---|---
|__inherit__|	Hereda el valor de la propiedad del elemento padre.
|__initial__|Establece el valor que tenía la propiedad inicialmente.
|__unset__|Combinación de las dos anteriores: Hereda el valor de la propiedad del elemento padre, y en caso de no existir, su valor inicial.

---
name:selectores
task: [<< índice de contenidos >>](#contenido)

### Selectores, propiedades y valores

Los selectores son nombres asignados a los estilos en las hojas de estilo. De momento etiquetas HTML, por ejemplo:
     _p_, _div_, _header_...

Para cada selector hay "__propiedades__" entre llaves, que toman la forma de palabras como:
    _color_, _font-weight_ o _background-color_.

Se da un valor a cada propiedad después de dos puntos (__NO un signo "igual"__). 

Los punto y coma “;” se utilizan para separar las propiedades:

```css
  body {
    font-size: 14px;
    color: navy;
    }
```

---
### Selectores de clase

Sirven para seleccionar elementos según el valor del atributo __`class`__.

El atributo `class` requiere un nombre. Utilizaremos, por convenio, nombres en minúsculas. Si necesitamos varios nombres para identificar una clase los separaremos por un guión.

Ejemplo de html:
```html

<div class="red-box">
 ... // you can style this box with the .red-box selector
</div>
```

Ejemplo de css:
```css
.red-box {
   declaracions
}
```

Podemos marcar un elemento con más de un nombre de clase, para ello las escribimos separadas por un espacio:

    <div class="red-box dimensions"></div>
---
### Ejercicio
<hr>

Crea un documento HTML (en codepen o en local)

- Asigna el color #00D1AE como _background_ de la etiqueta `<body>`.

- Crea un `<div>` y asigna lo siguiente:

    Width = 400px

    Height = 200px

    `#00D1AE` como _background color_

- Crea otro `<div>` y asigna lo siguiente:

    Width = 100px

    Height = 200px

    Red como _background color_

- Crea un tercer `<div>` y haz que se parezca al primero.

- Añade un último `<div>` y haz que se parezca al segundo.

---

### Selectores de Identificador (id)

Un selector id identifica un elemento de HTML único e irrepetible.

Se declara en el atributo id y se declara en css mediante el símbolo __#__:

```css
#nomidentificador {
   declaracions
}
```

Si, por ejemplo queremos identificar el párrafo principal: `<p id=“principal”>` y que el texto esté centrado, escribiríamos:

```css
p#principal {
   text-align: center;
}
```

Si no importa la etiqueta, es decir, si queremos que cualquier elemento que se identifique como principal, esté centrado:

```css
#principal {
   text-align: center;
}
```

---
### Selectores de atributo

Sirven para aplicar las propiedades de la regla a los elementos que tienen un atributo concreto. El selector siguiente:

```css
tag[atribut] {
   declaracions
}
```

afecta a todos los elementos con la siguiente sintaxis:

`<etiqueta atribut="valor">...</etiqueta>`

Por ejemplo: margen de 2em en todos los elementos `<img>` que tengan establecido el atributo _title_:

```css
img[title] {
   margin-right: 2em;
}
```
Los elementos afectados serían similares al siguiente:

    <img src="imatges/river.png" alt="River" title="riv" />
Y no afectaría a:

    <img src="imatges/river.png" alt="River" />

---
### Variantes selección atributos


- `img[title="river"]`: Aplica estilos a elementos 
con un valor de atributo determinado.

- `img[title][class="preferent"]`: Filtra por más de 
un atributo

- `img[alt~="Río"]`: selecciona los elementos que 
contienen exactamente el valor (palabras separadas 
por espacio). Ejemplo Río Nilo.

- `p[lang|=en]`: selecciona los elementos que tienen 
como atributo la cadena o comienzan por el valor 
seguido de un guión. Ejemplo en, en-US, en-cockney,...

- `[id^=“text”]`: selecciona elementos con id que 
comienza por 'text'

- `[id$=“text”]`: selecciona elementos con id que 
acaba con 'text'.

- `[id*=“text”]`: selecciona elementos con id que contiene 'text'.

---
name: selectoresavanzados
task: [<< índice de contenidos >>](#contenido)

### Selectores de descendientes

Un elemento es __descendiente__ de otro cuando este elemento está contenido en el otro, sin importar el nivel. La sintaxis es:

```css
etiqueta etiqueta_descendiente { 
   declaraciones
}
```

Se pueden incluir tantos niveles como se quiera:

```css
div p .destaca {
   color: red;
}
```
```html
<div>
   <p> Esta <span class="destaca">palabra</span> la hemos destacado.</p>
</div>
```
---

### Selectores de hijos

Un elemento es hijo de otro si es un descendiente de primer nivel.

Se utiliza el símbolo __">"__

```css
etiqueta > etiqueta_hija {
   declaraciones
}
```


En un ejemplo quedaria:

<iframe height="265" style="width: 100%;" scrolling="no" title="selectors-css-fills" src="https://codepen.io/rglepe/embed/PLGXMY?height=265&theme-id=default&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/PLGXMY'>selectors-css-fills</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

### Selectores de hermanos adyacentes

Selecciona el hermano inmediatamente posterior. Se usa el símbolo __"+"__:

```css
etiqueta + etiqueta_adyacente {
   declaraciones
}
```

```css
h1 + h2 { 
   margin-top: -5mm;
}
```

### Selector general de hermanos

Con el símbolo __"~"__, selecciona todos los hermanos, adyacentes o no.

```css
h1 ~ p {
   color: gray;
}
```

### Agrupamiento de selectores

Se agrupan separados por comas:

```css
selector1, selector2, selector3 {
   declaracions
}
```
---

### Pseudoclases

Palabra clave que se añade a los selectores y que especifica un estado especial del elemento seleccionado

A continuació enumerem les **pseudoclasses** existents amb la seva descripció i alguns exemples:

* `:first-child`: representa el primer elemento entre un grupo de elementos hermanos.

* `:link`: representa un elemento que aún no se ha visitado. Coincide con cada elemento no visitado `<a>`, `<area>`, o `<link>` que tiene un atributo `href`.
  
* `:visited`: enlaces que el usuario ya ha visitado.
  
  Estas características permiten modificar los estilos por defecto que aplica el navegador a los enlaces.

* `:active`: elemento (como un botón) que el usuario está activando. Cuando se usa un mouse, la "activación" generalmente comienza cuando el usuario presiona el botón primario del mouse y termina cuando se suelta. 
  
* `:hover`: se activa cuando el usuario se desplaza sobre un elemento con el cursor (puntero del mouse).
    
* `:focus`: elemento (como una entrada de formulario) que ha recibido el foco. Generalmente se activa cuando el usuario hace clic, toca un elemento o lo selecciona con la tecla "Tab" del teclado.

Consultar [aquí](https://developer.mozilla.org/es/docs/Web/CSS/Pseudo-classes) la lista completa

---

### Pseudoelementos

Permiten añadir estilos a una parte concreta del documento. Por ejemplo, el pseudoelemento `::first-line` selecciona solo la primera línea del elemento especificado por el selector.

A continuació s'enumeren els pseudoelements disponibles:

* `::first-line`: Selecciona la primera línea del elemento.

* `::first-letter`: Selecciona la primera letra del elemento.

* `::after`: Permite introducir contenido al final del elemento. Requiere la propiedad content con el valor deseado.

* `::before`: Permite introducir contenido al inicio del elemento. Requiere la propiedad content con el valor deseado..

Otros pseudoelementos se pueden consultar [aquí](https://developer.mozilla.org/es/docs/Web/CSS/Pseudoelementos)

---
name: unidades
task: [<< índice de contenidos >>](#contenido)

### [Tamaños y porcentajes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)

Algunas propiedades que podemos establecer en las hojas de estilo tienen como valor una unidad de medida (tamaño de letra, dimensiones, márgenes,...)

Estas pueden ser relativas o absolutas:


- __px__ ( como en font-size: 12px) es la unidad de píxeles.

- __em__ ( como en font-size: 2em) es la unidad para el tamaño calculado en función del tamaño base de fuente. Así por ejemplo "2em“, indica dos veces el tamaño de fuente actual (por defecto 16 px).

- __pt__ ( como font-size: 12pt) es la unidad para puntos, para medidas típicamente en medios impresos.

- __%__  ( Como en width: 80%) es la unidad de porcentajes relativos al ancho o alto de la página o del elemento padre.

---
name:colores
task: [<< índice de contenidos >>](#contenido)

### Colores

CSS nos ofrece 16.777.216 colores. 

- Pueden tomar la forma de un nombre, un valor RGB (rojo / verde / azul) o un código hexadecimal.

- Por ejemplo, para indicar rojo, se puede usar:
    - `red`
    - `rgb(255,0,0)`
    - `rgb(100%,0%,0%)`
    - `rgba(255,0,0,0)`
    - `#ff0000`
    - `#f00`

- Los colores se pueden aplicar dentro de las propiedades __`color`__ y __`background-color`__:
  
  ```css
  .h1 {
            color: #ffc;
            background-color: #009;
         }
  ```

---
name:texto
task: [<< índice de contenidos >>](#contenido)

### Texto

Se puede cambiar el tamaño y la forma del texto en una página web con un rango de propiedades:


- __font-family__: familia de fuentes como Times New Roman, Arial, or Verdana. →font-family: "Times New Roman"

- __font-size__: Tamaño de fuente

- __font-weight__: El grado de negrita de una fuente → font-weight: bold

  - Valores: bold,normal, bolder, lighter, 100, 200, 300, 400 (same as normal), 500, 600, 700 (same as bold), 800 or 900.

- __font-style__: itálica o no →font-style: italic; font-style: normal.

- __text-decoration__: subrayado debajo, encima o atravesado →text-decoration: underline

- __text-transform__: Cambia el tamaño (mayúsculas o minúsculas) del texto →text-transform: capitalize

---
Ejemplo:

```css

body{font-family: arial, helvetica, sans-serif;font-size: 14px;}h1 {font-size: 2em;}h2 {font-size: 1.5em;}a {text-decoration: none;}strong{font-style: italic;text-transform: uppercase;}

```
---

### Espaciado de texto


- __letter-spacing__: espaciado entre letras
- __word-spacing__: espaciado entre palabras
- __line-height__: Alto de línea
- __text-align__: Alineado a izquierda, derecha, centro
- __text-indent__: Indentado de la primera línea de un párrafo

---
name:caja
task: [<< índice de contenidos >>](#contenido)

### El model de caja

Cada elemento del documento se ha de concebir como si fuera una caja. De cada caja se pueden distinguir los siguientes componentes:

* El contenido (**content**) del elemento: texto u otros elementos.
* El relleno (**padding**): espacio entre el contenido y el borde de la caja.
* Borde (**border**): delimita la caja.
* Margen (**margin**): espacio entre el borde y el resot de elementos.

  ![model-box](https://www.w3.org/TR/CSS2/images/boxdim.png)

Cada uno de los componentes de la caja se pueden configurar con las propiedades de CSS.

---

### Diferentes modelos de Caja

Además de este modelo de caja, estandarizado en la mayoría de servidores, Internet Explorer dispone del suyo propio, en el que el ancho (_width_) no coincide con el contenido sino que es la suma de `content + padding + border`.


**Model W3C**

<code>
ancho total = margin-left + border-left + padding-left + width + padding-right + border-right + margin-right
</code>

CSS3 permite modificar el comportamiento habitual del  modelo de caja mediante la propiedad `box-sizing`. Admite los valores: 
   - `content-box`: el ancho afecta únicamente al contenido 
   - `padding-box`: contenido + padding 
   - `border-box`: los tres valores. Valor más habitual.

Ejemplo:

<iframe height="265" style="width: 100%;" scrolling="no" title="model-box" src="http://codepen.io/rglepe/embed/YgNeom/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/YgNeom/'>model-box</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
---

name: posicionamiento
task: [<< índice de contenidos >>](#contenido)
### Posicionamiento

Propiedades que ayudan a definir el comportamiento de unas cajas respecto a otras:

* `display`: define el tipo de caja de un elemento:
  * `block`: El elemento será un elemento de bloque y generará un salto de línia, ocupando todo el ancho del viewport.
  * `inline`: El elemento se comportará como un elemento de línia, ocupando sólo el tamaño del contenido.
  * `list-item`: Comportamiento como elemento de lista.Tendrá por defecto el icono de lista.
  * `none`: El elemento no genera caja, ni es visible ni ocupa espacio en el documento. Son elementos como: `<script>`, `<input type=“hidden”>`, etc.
  * `run-in`: caja de bloque o línia según el contexto.
  * `table`, `inline-table`, `table-row-group`, `table-column`, `table-column-group`, `table-header-group`, `table-footer-group`, `table-row`, `table-cell` i `table-caption`: Elemento de una tabla.
  
Para invisibilizar imágenes:

```css
img { 
   display: none; 
}
```

---

### Ejemplo de formato en tres columnas:

 
 <iframe height="265" style="width: 100%;" scrolling="no" title="display-css" src="http://codepen.io/rglepe/embed/ZPeLVq/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/ZPeLVq/'>display-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


---

### position

propiedad que define la posición de una caja respecto al resto de cajas del documento, o respecto al mismo documento o ventana. Valores:

  * `static`: posicionamiento en el orden que toca. Valor por defecto.

  * `relative`: posición relativa a la posición que le tocaría. El espació que debería ocupar no se colapsa.

  * `absolute`: posición relativa a la caja contenedora. El espacio que tendría que ocupar se colapsa.

  * `fixed`: posición relativa a la caja contenedora, pero se queda fijada y no se desplaza por el documento.

Esta propiedad, para que tenga sentido se debe combinar con:

  * `top`, `right`, `bottom` i `left`: con estas propiedades podemos posicionar la caja desplazándola hacia arriba, derecha, abajo e izquierda, respectivamente
  * `width` y `height`: indican las medidas de ancho y alto de las cajas, respectivamente.
  

---

### Ejemplo de positioning


<iframe height="355" style="width: 100%;" scrolling="no" title="position-css" src="http://codepen.io/rglepe/embed/eXvvZa/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/eXvvZa/'>position-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



* `min-width`, `min-height`, `max-width` i `max-height`: sirven para determinar las dimensiones mínimas y máximas que pueden tomar las cajas. Sea cual sea la medida del viewport.
  
---

### float

Propiedad que hace que la caja quede flotando a la izquierda (si le damos el valor `left`) o a la derecha (si esta­blecemos `right`). Para una imagen que quede flotante daríamos:

   ```css  
   img { 
      float: right; 
   }
   ```

Otro ejemplo más completo:

<iframe height="265" style="width: 100%;" scrolling="no" title="float-css" src="http://codepen.io/rglepe/embed/aMJJQm/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/aMJJQm/'>float-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

### clear

Desactiva los elementos flotantes alrededor del elemento que tenga esta propiedad. Mediante el valor `left`, los da la parte izquierda, con `right` los de la derecha o a ambos lados con el valor `both`. Para anular la propiedad usaremos `none`.

Ejemplo:

<iframe height="265" style="width: 100%;" scrolling="no" title="clear-css" src="http://codepen.io/rglepe/embed/pYeVmM/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/pYeVmM/'>clear-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

### z-index

Esta­blece la profundidad de una caja en el eje Z. El valor es un número relativo que define esta profundidad, cuánto más bajo más al fondo estará el elemento.

<iframe height="265" style="width: 100%;" scrolling="no" title="z-index-css" src="http://codepen.io/rglepe/embed/moWvQo/?height=265&theme-id=0&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/moWvQo/'>z-index-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---


### overflow

Indica que hacer cuando el contenido mide más que la caja:

  * `visible`: el con­tenido se ve sobrepasando la caja
  
  * `hidden`: el con­tenido sobrante no se ve
  
  * `scroll`: apa­rece una barra de desplezamiento

  * `auto`: la barra de desplazamiento aparece sólo si es necesaria
  
Ejemplo:

<iframe height="265" style="width: 100%;" scrolling="no" title="overflow-css" src="http://codepen.io/rglepe/embed/EMWrMo/?height=265&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/EMWrMo/'>overflow-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

name:flexbox
task: [<< índice de contenidos >>](#contenido)
### [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)


__`Properties for the Parent (flex container)`__

```css

.container {

  display: flex; /* or inline-flex */
  
  flex-direction: row | row-reverse | column | column-reverse;
  
  flex-wrap: nowrap | wrap | wrap-reverse;
  
  flex-flow: <‘flex-direction’> || <‘flex-wrap’>;
  
  justify-content: flex-start | flex-end | center | space-between | space-around 
  | space-evenly | start | end | left | right ... + safe | unsafe;
  
  align-items: stretch | flex-start | flex-end | center | baseline | first baseline 
  | last baseline | start | end | self-start | self-end + ... safe | unsafe;
  
  align-content: flex-start | flex-end | center | space-between | space-around 
  | space-evenly | stretch | start | end | baseline | first baseline 
  | last baseline + ... safe | unsafe;

}
```

__`Properties for the Children (flex items)`__
```css
.container {
   order: <integer>; /* default is 0 */
   flex-grow: <number>; /* default 0 */
   flex-shrink: <number>; /* default 1 */
   flex-basis: <length> | auto; /* default auto */
   flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
   align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
---
name:responsive
task: [<< índice de contenidos >>](#contenido)

### Diseño Web _Responsive_

RWD (Responsive Web Design) consiste en construir sitios web que trabajen correctamente en cualquier dispositivo y en cualquier tamaño de pantalla. Se centra en ofrecer una __experiencia de usuario__ intuitiva y gratificante para cualquier usuario.


Para hacer un buen diseño _responsive_ es necesario centrarse en el tamaño del [_viewport_](https://en.wikipedia.org/wiki/Viewport).


__No tenemos que crear un diseño específico__ para el último iPhone o Samsung, Tenemos que crear un diseño para un _viewport_ de ancho 680px, tener el sitio web perfecto para cada uno de los dispositivos del mercado llevaría muchísimo tiempo y sería muy complejo. Lo que hacemos es __agrupar los dispositivos de tamaño de pantalla similar__.

---

## Mobile First

Creamos el diseño de las pantallas de móviles y después añadimos elementos incrementalmente para resoluciones mayores.


- En el móvil sólo se muestra la información necesaria. Esta técnica asegura una buena experiencia UI/UX. Nos enfocamos en lo realmente importante.


- Evitamos cargar recursos innecesarios. 

---
## [Media queries](https://developer.mozilla.org/es/docs/CSS/Media_queries)

Funciones CSS que delimitan las propiedades que se aplican en función del tipo de dispositivo (opcional) y distintas características del mismo: width, height, etc.

Para crear un _media query_:

Dentro de una hoja CSS:

```css
@media [(media-features)] {
  // Styles
}
```
Dentro del documento HTML:

`<link rel="stylesheet" media="(media-features)" href="styles.css" />`

Las [`media-features`] son opcionales, y expecifican dónde aplicar los estilos de la página.

Cuando las _media query_ se cumplen, se aplica la hoja de estilos o las reglas css, siguiendo las reglas en cascada de forma normal. Las hojas de estilo con media queries asociadas por etiquetas `<link>` se descargarán en el navegador aunque las media queries no se cumplan.

---

### Ejemplo de media queries
<br><br><br>
<iframe height="265" style="width: 100%;" scrolling="no" title="media-queries" src="https://codepen.io/rglepe/embed/mdJwqmv?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/mdJwqmv'>media-queries</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---

## Viewport meta tag

Es una ventana gráfica que fue creada por la compañía Apple para sus productos tales como: iPhone, iPod Touch o iPad, con la finalidad de solucionar el problema sobre el tamaño de la pantalla a la hora de visualizar y navegar en un sitio web.


La etiqueta `<meta name="viewport>` nos permite controlar el tamaño y la escala del dispositivo. Esta etiqueta permitirá cargar los estilos correctamente en distintos dispositivos. 

Añadimos en la sección `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

---

## Fuentes responsive con CSS

<br>
### Font-Size

La mayor parte de los sitios web usan un tamaño de fuente entre __14 y 18 píxeles para el texto__. Los expertos recomiendan al menos 16px.

También se suele recomendar el número de palabras por línea. Lo normal suele ser 18 palabras. Como regla general, usa el tamaño de fuente mayor que no aparezca desproporcionada y resulte en unas __20 palabras o menos por línea__.
<br><br>

### Line-Height

Altura de línea de texto recomendada entre __1.2 to 1.45em__ por estética y buena lectura.
<br><br>

### Tamaño de fuente responsive

- unidades viewport
- media queries +px +em. (recomendado)
<br>
---
name:efectos
### Efectes CSS: Transform, Transition y Animation

Las animaciones y transformaciones son herramientas muy potentes para llamar la atención de los usuarios.

- __Transformaciones 2D__: Modifican el espacio de coordenadas del modelo de formato visual CSS. Los elementos pueden ser trasladados, rotados, escalados o sesgados según los valores que se establecen.



- __Transiciones__: Efectos que hacen que un elemento pase de tener un esto a otro. Una transición se ejecuta cuando una propiedad cambia. Una manera de provocar este cambio es mediante la pseudoclase `:hover`. 

- __Animaciones__: Los elementos cambian las propiedades en un espacio de tiempo.

  Primero se tiene que declara la regla `@keyframes`, para definir los valores inicial, final e intermedios.

  ```css
      @ke0yframes canvicolorfons{
      0% {background-color: red;}
      25% {background-color: yellow;}
      50% {background-color: blue;}
      100% {background-color: green;}
    }
```

---

### Ejemplo de transformaciones
<br>

<iframe height="265" style="width: 100%;" scrolling="no" title="transformacions-css" src="https://codepen.io/rglepe/embed/KEmbZx?height=365&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/KEmbZx'>transformacions-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
---
### Ejemplo de transiciones
<br>

<iframe height="265" style="width: 100%;" scrolling="no" title="transition" src="https://codepen.io/rglepe/embed/xNZgKG?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/xNZgKG'>transition</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

---
### Ejemplo de animaciones
<br>

<iframe height="265" style="width: 100%;" scrolling="no" title="animations-css" src="https://codepen.io/rglepe/embed/moByGe?height=265&theme-id=light&default-tab=css,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rglepe/pen/moByGe'>animations-css</a> by Raul Garcia
  (<a href='https://codepen.io/rglepe'>@rglepe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>
---

### Transitions vs. Animations!
<br><br><br>

||Transiciones|	Animaciones|
|---|---|---|
|Inicio|	Requiere un evento que inicie la transición, CSS o JavaScript.|	No necesita evento externo. Corre automáticamente cuando se carga la página.
|Definición de puntos intermedios|	Sólo inicio y fin|  Puede incluir tantos puntos intermedios como se quieran (_keyframes_).
|CSS Interacción|	No cambia las propiedades CSS.|	Puede cambiar los valores dentro de su _keyframe_.|
|Looping	|No està diseñado para looping|	No hay problemas de looping.

---
CSS Grid

