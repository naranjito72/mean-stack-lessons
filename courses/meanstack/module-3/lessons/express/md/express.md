class: center, middle

<img src="https://imgur.com/Np6FvqO.png" width=50% height=50% alt="logo">


---

name: contenido
class: center, middle, inverse
## [Express.js](#Qué es Express.js?)
---
name: default
layout: true
task: &nbsp;

.task[{{task}}]

---
name:contenido

###Contenido

- [API REST](/courses/meanstack/module-3/lessons/nodejs/node.html#163)
- [MVC](#mvc)
- [Estructura de un proyecto con Express.js](#proyecto)
- [Routing](#rutas)
- [Motores de Plantillas](#engines)
- [mongoose](#mongoose)
- [Middlewares de autenticación](#authentication)
- [Pase a Producción](#produccion)

---
name:mvc
task: [<< índice de contenidos >>](#contenido)

### Arquitectura MVC

La arquitectura MVC separa los datos (__`modelo`__), las vistas (__`view`__) y la lógica de la aplicación (__`controlador`__). Esta separación entre componentes permite eliminar acoplamientos entre componentes, teóricamente hace el código más mantenible y reusable. Una ventaja más supone el hecho de que es posible diseñar prototipos rápidamente y concentrarse en cada uno de los aspectos del desarrollo en cada momento

<img src='https://imgur.com/IUnyivw.png' width=100% height=100%>

---
name:proyecto
task: [<< índice de contenidos >>](#contenido)

### ESTRUCTURA DE UN PROYECTO CON EXPRESS.JS

\- __`/models`__ contiene todos los modelos del ORM (Schemas en mongoose)

\- __`/views`__ contiene las vistas-templates (usando cualquier motor de plantillas de express

\- __`/public`__ contiene todo el contenido estático (imágenes, hojas de estilo, JavaScript del lado del cliente)
  -   __`/assets/images`__ archivos de imágenes
  -   __`/assets/pdf`__ archivos pdfs estáticos
  -   __`/css`__ hojas de estilos (o compilados por un motor de css)
  -   __`/js`__ JavaScript del lado cliente
  
\- __`/controllers`__ contiene las rutas de express, separadas por `modulo/area` de la aplicación (si se \- utiliza la funcionalidad de generación de estructuras de express, esta carpeta se llama __`/routes`__) 
---
name:proyecto
task: [<< índice de contenidos >>](#contenido)

### ESTRUCTURA DE UN PROYECTO CON EXPRESS.JS

- El código de la API debería permanecer separado del resto de la aplicación para evitar confusiones. 

- Debe ser la primera parte que se desarrolle de nuestra aplicación

- Lo primero es crear un área separada para la API, nombrando un directorio como __`app_api`__. Se situará al mismo nivel del directorio __`app_server`__, que contendrá el resto del código de la aplicación. 

- Dentro de `app_api` situaremos los directorios __`model`__, __`controllers`__ y __`routes`__.
  
---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Routing 

- Forma de responder una aplicación a una solicitud de un cliente en un _endpoint_ determinado, formado por un URI (o path) y un método de solicitud HTTP específico (GET, POST, etc.).
  
- Cada ruta puede tener una o varias funciones que gestionen la petición, siendo excluyentes entre si.


      app.METHOD(PATH, HANDLER) 

Donde:
- __app__ es una instancia de express.
- __METHOD__ es un método de solicitud HTTP.
- __PATH__ es una vía de acceso en el servidor.
- __HANDLER__ es la función que se ejecuta cuando se correlaciona la ruta.


---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Routing 

Ejemplo:

    // GET method route
    app.get('/', (req, res) => {
      res.send('GET request to the homepage');
    });

    // POST method route
    app.post('/', (req, res) => {
      res.send('POST request to the homepage');
    });

    //POST method route
    app.post('/user', (req, res) => {
      res.send('POST request to the homepage');
    });

---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Métodos de Routing 

- En Express se da soporte al direccionamiento de los siguientes métodos:

  - `get`, `post`, `put`, `head`, `delete`, `options`, `trace`, `copy`, `lock`, `mkcol`, `move`, `purge`, `propfind`, `proppatch`, `unlock`, `report`, `mkactivity`, `checkout`, `merge`, `m-search`, `notify`, `subscribe`, `unsubscribe`, `patch`, `search` y `connect`.
  
- Existe un direccionamiento especial: `app.all` para cargar funciones de middleware accesibles a todos los métodos de solicitud. Ej:


    app.all('/secret', (req, res, next) => {
      console.log('Accessing the secret section ...');
      next(); // pass control to the next handler
    });

---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Paths de Routing

- Los paths pueden ser strings, patrones de caracteres o expresiones regulares.
  
- Los caracteres:?, +, *, y () son parte de expresiones regulares. El guión o (-) y el punto (.) se interpretan literalmente.

- Ej.:


    app.get('/', (req, res)=> { res.send('root') }) 
    // This route path will match requests to /about.
    app.get('/about', (req, res)=> { res.send('about') }) 
    // This route path will match requests to /random.text.
    app.get('/random.text', (req, res)=> { res.send('random.text') }) 
    Here are some examples of route paths based on string patterns.
    // This route path will match acd and abcd.
    app.get('/ab?cd', (req, res)=> { res.send('ab?cd') }) 
    // This route path will match abcd, abbcd, abbbcd, and so on.
    app.get('/ab+cd', (req, res)=> { res.send('ab+cd') }) 
    // This route path will match abcd, abxcd, abRANDOMcd, ab123cd, and so on.
    app.get('/ab*cd', (req, res)=> { res.send('ab*cd') }) 
    // This route path will match /abe and /abcde.
    app.get('/ab(cd)?e', (req, res)=> { res.send('ab(cd)?e') }) 
    Examples of route paths based on regular expressions:
    // This route path will match anything with an “a” in it.
    app.get(/a/, (req, res)=> { res.send('/a/') }) 
    // This route path will match butterfly and dragonfly, but not butterflyman, dragonflyman, and so on.
    app.get(/.*fly$/, (req, res)=> { res.send('/.*fly$/') })

---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Parámetros de Routing

- Los parámetros de la dirección son segmentos de una URL utilizados para capturar valores en una posición de la URL. 
  
- A los valores capturados se accede mediante req.params object, con el nombre del parámetro especificado en la dirección
  
- Ej.:


      Route path: /users/:userId/books/:bookId
      Request URL: http://localhost:3000/users/34/books/8989
      req.params: { "userId": "34", "bookId": "8989" }

      app.get('/users/:userId/books/:bookId', 
              (req, res) => res.send(req.params));

---
### Ejercicio 19
<hr>

- Crear un _middleware_ con __Express__ que asocie un método `auth` a una URI `/admin` y a las subrutas. De manera que si no se obtiene un usuario y una password determinados en el request de la petición devolver: 
  
  `status_code = Not authorized`.
  
- Si se autoriza devolver en `/admin` mensaje `"Estás validado como admin"`

- Si entra a `/admin/user` devolver los datos de usuario y password
  
_TIP: El usr y pssw enviarlos como key|value desde POSTMAN._

---
name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Routing handlers

- Conjunto de _callbacks_ que se comportan como un único _middleware_ para manejar la respuesta a una petición. Requieren que cada una de las funciones _callback_ implemente el método `next()`.

- Ejemplo:


    app.get('/example/b', (req, res, next) => {
      console.log('the response will be sent by the next function ...')
      next()
    }, (req, res) => res.send('Hello from B!'))

---

name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: Routing   `app.route()`

- Permite encadenar _handlers_ de ruta. Facilita la lectura del código, reduce la redundancia y errores

- Ej.


    app.route('/book')
      .get  ((req, res)=> res.send('Get a random book'));
      .post ((req, res)=> res.send('Add a book'));
      .put  ((req, res)=> res.send('Update the book'));

---

name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express: `express.Router`

- Permite crear _handlers_ modulares. Una instancia de `Router` es un sistema _middleware_ y direccionamiento completo. Funciona como  una __miniaplicación__.
  
- Ej. para manejar la ruta `/birds` y las subrutas se crea un __módulo bird.js__. Después se carga en la aplicación:


    //módulo bird.mjs

    import Router from 'express';
    const router = Router();
    // middleware that is specific to this router 
    router.use((req, res, next) => {
        console.log('Time: ', Date.now());
        next();
    }); 
    // define the home page route 
    router.get('/', (req, res) => res.send('Birds home page'));
    // define the about route 
    router.get('/about', (req, res) => res.send('About birds'));
    export default router; 

      //app.mjs

      import birds from ('./birds.mjs'); 
      ... 
      app.use('/birds', birds); 

---

name:rutas
task: [<< índice de contenidos >>](#contenido)

### Express Routing: Métodos de respuesta
<br>

|Método|	Descripción|
|---|---
|res.download()|	Solicita un archivo para descargarlo.
|res.end()|	Finaliza el proceso de respuesta.
|res.json()|	Envía una respuesta JSON.
|res.jsonp()|	Envía una respuesta JSON con soporte JSONP.
|res.redirect()|	Redirecciona una solicitud.
|res.render()|	Representa una plantilla de vista.
|res.send()|	Envía una respuesta de varios tipos.
|res.sendFile|	Envía un archivo como una secuencia de octetos.
|res.sendStatus()|	Establece el código de estado de la respuesta y envía su representación de serie como el cuerpo de respuesta

---

### Ejercicio 20

Crear un controlador `admin.js` para el ejercicio anterior, añadiéndole un _middleware_ que imprima un timestamp en la respuesta.

---

### PROYECTO

- Crea las rutas, middlewares y controllers para la aplicación que presentarás como proyecto.

- Tienes que analizar que peticiones se harán desde el __frontend__ a las APIs teniendo en cuenta las funcionalidades discutidas en la estructuración de las aplicaciones.

- Comenzar a estructurar los proyectos:

    - __index.js__: conexión a la base de datos y configuración general de mongoose, 
    - __app.js__ servidor web con NodeJS y configuración de express, 
    - __middlewares__ (middleware de autenticación,...)
    - __models__: modelos y esquemas de mongoose, 
    - __controllers__: acciones y operaciones sobre la bd
    - __routes__: directorio de rutas, se definen las rutas a las que responderá la aplicación.



???
### Static Files

Static files are things like images, CSS, and client-side JavaScript that are sent directly from the server to the browser as is.

Express has built in support for serving these kinds of files.

Typically, these files are saved in a folder called `public`:

```
$ mkdir public
```

Let's create a folder for images, and download a cool cat picture to that folder:

```
$ cd public
$ mkdir images
$ cd images
$ curl -o cool-cat.jpg http://wallpapercave.com/wp/X7VjxFk.jpg
```

Inside of Express, we have to tell our server to serve static files from the `public` directory:

```javascript
// ...
const app = express();

app.use(express.static('public'));

app.get('/', (request, response, next) => {
// ...
```

Visit [localhost:3000/images/cool-cat.jpg](http://localhost:3000/images/cool-cat.jpg) and you will see your image!

We aren't going to have a web app full of static files, where people have to visit a million different pages to see different pictures.

One of the benefits of using static assets is that we can incorporate them into our HTML for the browser to read.

**Create a stylesheet:**

```
$ mkdir public/stylesheets
$ touch public/stylesheets/style.css
```
**Add the following styles:**

```css
body {
  color: blue;
  background-color: bisque;
}
```

**Create a new route:**
```javascript
// ...

app.get('/hello', (request, response, next) => {
  response.send(`
    <!doctype html>
    <html>
      <head>
        <link rel="stylesheet" href="stylesheets/style.css">
      </head>
      <body>
        This is my second route
      </body>
    </html>
  `);
});

// ...
```

Now visit [localhost:3000/hello](http://localhost:3000/hello)!

:::danger
:warning: Remember to restart your server in your terminal before checking the changes.
```
$ ctrl + c
$ node app.js
```
:::



### Statics Assets Request-Response Flow

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_e9728aae585f81940c61289c0125f9f2.png)

