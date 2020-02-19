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

- [Qué es CSS y como crear estilos inline y en documentos](#)
- [Colores, fuentes y fondos en HTML](#)
- [Selectores de elementos con element, class, id](#)
- [Propiedades: margin, padding y border properties](#)
- [Posicionar elementos en la pantalla](#)
- [Selección avanzada de elementos](#)
- [Flexbox](#)
- [CSS Grid](#)
- [Transiciones](#)
- [Animaciones](#)


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

Ej:
```html
<div class="red-box">
 ... // you can style this box with the .red-box selector
</div>

<div class="blue-box">
 ... // you can style this box with the .blue-box selector
</div>

<div class="red-box">
 ... // you can style this box with the .red-box selector
</div>
```

Las clases no hacen nada por si mismas, son sólo marcadores que se utilizan para categorizar.

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



---
### Tamaños y porcentajes

Hay unidades generales para los valores usados en CSS para expresar dimensiones como tamaño, ancho, alto.


- __px__ ( como en font-size: 12px) es la unidad de píxeles.

- __em__ ( como en font-size: 2em) es la unidad para el tamaño calculado en función del tamaño base de fuente. Así por ejemplo "2em“, indica dos veces el tamaño de fuente actual (por defecto 16 px).

- __pt__ ( como font-size: 12pt) es la unidad para puntos, para medidas típicamente en medios impresos.

- __%__  ( Como en width: 80%) es la unidad de porcentajes relativos al ancho o alto de la página o del elemento padre.

---

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


- letter-spacing: espaciado entre letras
- word-spacing: espaciado entre palabras
- line-height: Alto de línea
- text-align: Alineado a izquierda, derecha, centro
- text-indent: Indentadode la primera línea de un párrafo
