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

task: [<< índice de contenidos >>](#contenido)

### Express: Routing handlers

- Conjunto de _callbacks_ que se comportan como un único _middleware_ para manejar la respuesta a una petición. Requieren que cada una de las funciones _callback_ implemente el método `next()`.

- Ejemplo:


    app.get('/example/b', (req, res, next) => {
      console.log('the response will be sent by the next function ...')
      next()
    }, (req, res) => res.send('Hello from B!'))

---


task: [<< índice de contenidos >>](#contenido)

### Express: Routing   `app.route()`

- Permite encadenar _handlers_ de ruta. Facilita la lectura del código, reduce la redundancia y errores

- Ej.


    app.route('/book')
      .get  ((req, res)=> res.send('Get a random book'));
      .post ((req, res)=> res.send('Add a book'));
      .put  ((req, res)=> res.send('Update the book'));

---


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

name:rutasproyecto
task: [<< índice de contenidos >>](#contenido)

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
---

name:estaticos
task: [<< índice de contenidos >>](#contenido)

### Ficheros estáticos: Imágenes

Las imágenes, CSS o JavaScript del lado de cliente se envían directamente desde el servidor al navegador

Express soporta de forma navitva el envío de estos ficheros.

Normalmente se almacenan en una carpeta `public`:

Creamos un directorio para imágenes y descargamos la imagen de gato a este directorio

.inverse[<code class="codigo">public/images/ curl -o cool-cat.jpg http://wallpapercave.com/wp/X7VjxFk.jpg</code>
]

Desde Express, se indica al servidor el directorio de ficheros estáticos `public`:

```javascript
// ...
const app = express();
app.use(express.static('public'));
app.get('/', (request, response, next) => {
// ...
```

Desde [localhost:3000/images/cool-cat.jpg](http://localhost:3000/images/cool-cat.jpg)  se puede ver la imagen

El contenido estático se puede incorporar dentro de plantillas HTML.
---
task: [<< índice de contenidos >>](#contenido)

### Ficheros estáticos: Estilos

.inverse[<code class="codigo">public/styles/touch style.css</code>
]

```css
body {
  color: blue;
  background-color: bisque;
}
```

Creamos una nueva ruta: 

```javascript

app.get('/hello', (request, response, next) => {
  response.send(`
    <!doctype html>
    <html>  <head> 
    <link rel="stylesheet" href="styles/style.css">  </head>
    <body> This is my second route </body> </html>`);});

```
Visitamos [localhost:3000/hello](http://localhost:3000/hello)!

---
class: center, middle

<img src="https://imgur.com/MA6cGfk.png" width=50% height=50% alt="logo">

---

name: mongoose
class: center, middle, inverse
## [Mongoose](https://mongoosejs.com/)
---

name:mongooseintro
task: [<< índice de contenidos >>](#contenido)

### OBJECT DATA MAPPING

__Data Mapper__ es un patrón de diseño utilizado para separar la capa de acceso a la base de datos de la capa de dominio que contiene una representación de los datos

La capa de separación puede estar compuestas de uno más mappers (o __Data Access Objects__), que llevan a cabo la transferencia de los datos

La implementación del patrón en aplicaciones con bases de datos SQL se denomina __ORM__.

Con bases de datos NoSQL se conoce como __ODM__.

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE

- Es un framework javascript que permite el acceso a una base de datos MongoDB usando un __modelo de objetos__
  
- Una __db__ contiene muchas __colecciones__ y una colección muchos __documentos__. No existe ningun requerimiento que obligue a que dos documentos de una misma colección tengan la misma estructura. Aunque normalmente se establece que dos documentos almacenados en la misma colección tendrán una estructura parecida
  
- En Mongoose se definen los __esquemas de documentos__; Cada esquema puede contener una lista de campos y sus restricciones:

      - Tipo de dato y restricciones específicas tales como: valor mínimo, valor requerido, único,... 

- Un __modelo__ representa una conexión a una colección de la bd que usa el esquema anterior. 

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: Instalación y conexión a BD

para instalar Mongoose usamos: .inverse[<code style="codigo">npm i mongoose</code>
]

para conectar a MongoDB desde Mongoose se usa el método __`createConnection()`__ con argumentos: URL de la bd y los parámetros de conexión: username, password, server host, and database name:

    import mongoose from 'mongoose';

    const url ='mongodb+srv://admin:1234@mean-stack-3-7ufox.mongodb.net/test'
    const connection = mongoose.createConnection(url,
        {
        useNewUrlParser: true, 
        useUnifiedTopology: true
        });

Una vez que se ha establecido la conexión, el objeto __`connection`__ emite el evento __`open`__. La conexión puede terminar con el método __`close()`__:

    connection.on("open", _ => {
      }).then(connection => console.log("Connection established") )
        .catch(error => console.error.bind(console, 'ha habido un error'));

    connection.close(error => console.log('bye'));   

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: SCHEMAS

- Los esquemas se utilizan para definir la estructura y los atributos de un documento. Cada esquema mapea a una colección de la bd y define la "forma" del documento dentro de la colección.
  
- Para crear un esquema determinado se genera una instancia del objeto Schema
 
Ej: Esquema de dos colecciones: estudiantes y proyectos

    //db/schema.js
    const Schema = mongoose.Schema
    const StudentSchema = new Schema({
      name: String,
      age: Number
    });
    const ProjectSchema = new Schema({
      title: String,
      unit: String
    });


---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: SUBDOCUMENTOS

En el caso de querer almacenar información referente a una relación entre objetos (subdocumentos), se almacenaría como un objeto embebido:
Ej:

    import mongoose from "mongoose";
    const Schema = mongoose.Schema;

    const StudentSchema = new Schema({
      name: String,
      age: Number,
      projects:  [projectSchema]
    });

Existen dos tipos diferentes de subdocumentos: 
- arrays de subdocumentos
- subdocumento anidado simple (a partir de mongoose  4.2.0)

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: MODELS

- Para usar el objeto __Schema__ creado es necesario asociarlo a la conexión a la __bd__. Esta asociación se denomina __model__. 
  
- Para crear un modelo se utiliza el método __`model()`__ del objeto `connection`. Este método tiene dos argumentos: string del __nombre de la colección__ y un __objeto Schema__ y devuelve un objeto Model.


        //StudentModel.js


    export default connection => 
      connection.model("Student", StudentSchema);


_El primer argumento es el nombre en singular de la colección. Mongoose automáticamente busca el nombre en plural. _


---

task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: MODELS

- Para trabajar con el modelo creado importamos el fichero en otro documento:


      import mongoose from 'mongoose';
      import Student from './StudentModel.mjs';

      (async _ => {
      
          try {
              await  mongoose.connect('mongodb://localhost:27017/test',
          { useNewUrlParser: true, useUnifiedTopology: true });

              (await Student(mongoose.connection)
                              .find({}))
                              .forEach(student => console.log(student.name))

              mongoose.disconnect();

          } catch (error) {
              throw error;
          }
      })();

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: INSERT DATA

- Insertar datos en MongoDB es un proceso de dos pasos que utiliza los modelos Mongoose:
  
1. Instanciar un objeto usando el constructor de un __modelo__. En el ejemplo anterior el constructor es `Student()`. Una vez creado se puede manipular como cualquier objeto JavaScript. 
2. Insertar los datos utilizando el método `save( )` del modelo, que recibe una función callback con el parámetro para tratar el error.


    //db/schema.mjs

    ...
    let ana = new Student({
      name: 'ana'
    })
    let project1 = new Project({
      title: 'Mongoose'
    })
    ana.projects.push(project1);
    ana.save((err,student)=>{
    if(err) { console.log(err)}
    else {console.log(student+' se guardó en la bd!!!')}
    })

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: PROMESAS

Todos los métodos de Mongoose están preparados para trabajar con callbacks o con promesas. Ej:

    //db/schema.js

    ...
    let ana = new Student({
      name: 'ana'
    })
    let project1 = new Project({
      title: 'Mongoose'
    })
    ana.projects.push(project1);
    anna.save().then(student => {  console.log(student)})
      .catch(err => {console.log(err)});
---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: QUERY DATA

Mongoose provee de una serie de consultas predefinidas:

    Model.deleteMany()
    Model.deleteOne()
    Model.find()
    Model.findById()
    Model.findByIdAndDelete()
    Model.findByIdAndRemove()
    Model.findByIdAndUpdate()
    Model.findOne()
    Model.findOneAndDelete()
    Model.findOneAndRemove()
    Model.findOneAndUpdate()
    Model.replaceOne()
    Model.updateMany()
    Model.updateOne()

- Todos los métodos pueden usarse pasando un __callbacks__ con los parámetros de error y resultado o como promesa resolviendo el cumplimiento de la __promesa__ a través del método __.then()__ o con __async/await__

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: QUERY DATA

- Mongoose provee de una serie de consultas predefinidas:
  

      Model.find({}, callback) 
      //Busca todas las ocurrencias
      Model.findById(someId, callback) 
      //Busca un único modelo por id
      Model.findOne({someKey: someValue}, callback) 
      //Busca un único modelo por clave:valor
      Model.remove({someKey: someValue}, callback) 
      //Elimina todos los  modelos que cumplen la condición

Ej.: Implementando los métodos dentro de un controlador: `controllers/studentsController.js`

    import Schema from "../db/schema.js";
    const Student = Schema.Student;
    const Project = Schema.Project;
    let studentsController = {
      index(){
        Student.find({}, (err, students) => {
          console.log(students);
        });
      }
    };
    studentsController.index();

---

### Ejercicio 22
<hr>

- Implementa el resto de métodos descritos, sobre el ejemplo: show, update y delete.
- Implementa un método que devuelva el número de estudiantes o proyectos
- Implementa un método para borrar todos los proyectos de un estudiante

---

### Ejercicio 23
<hr>
Crea la capa de persistencia del ejemplo de movies

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: VALIDATORS

- Mongoose ofrece validadores a nivel de campo de un documento, que se ejecutan en el momento de guardar el documento.

- Si ocurre un error de validación, la operación de guardado se interrumpe y el error pasa al _callback_.

- Existen __validadores predefinidos__ y opciones para crear __validaciones personalizadas__:

- Validadores predefinidos: 
  
    - Todos los tipos de datos: `Required`
    - Numbers: `min` y `max`
    - Strings: `enum`, `match`, `minlength` y `maxlength`


      const UserSchema = new Schema({
        username: {
          type: String,
          *unique: true,
          required: true
        }
      });

_*unique no es un validador como tal. Es un helper para la construcción de índices; obliga a construir un índice sobre el campo_ 

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: VALIDATORS

- __`required`__: valida la existencia del campo. Evita que se guarde un documento sin este campo.
- __`unique`__: Valida que el valor a guardar sea único en la colección.
- __`match`__: Valida que el valor a  guardar tenga un determinado patrón
- __`enum`__: Obliga a que el valor sea uno de los definidos en una colección de strings.

Ej.:

    const  UserSchema = new Schema({
      username: {   
        type: String,
        unique: true,
        required: [true, 'nombre obligatorio']
      },
      email: {
        type: String,
        match: /.+\@.+\..+/
      },
      role: {
        type: String,
        enum: ['Admin', 'Owner', 'User']
      },
    });

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: VALIDATORS

Podemos definir validaciones personalizadas mediante la propiedad __`validate`__. A la propiedad se le pasa un array con una función validadora:

    const UserSchema = new Schema({
      ...
      password: {
        type: String,
        validate: {
          function(password) {
            return password.length >= 6;
          },
          'Password should be longer'
        }
      },
    });

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: MIDDLEWARE

También conocidos como __hooks__, son funciones que toman el control durante la ejecución de funciones asíncronas.

Existen dos tipos: __pre__ y __post__.

Se define a nivel de esquema y puede modificar la consulta o el documento mismo al ser ejecutado. 

Mongoose presenta 4 tipos de middleware:

- __Documento__. 

  Incorpora un middleware en las siguientes funciones: `validate`, `save`, `remove`, `init` (síncrono)

- __Query__

  Midleware para `count`, `find`(`findOne`, `findOneAndRemove`,`findOneAndUpdate`), `remove` y `update` (`updateOne`,`updateMany`)

- __Aggregate__

- __Model__
  
  `insertMany`

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: PRE middleware

- El middleware __`pre`__ se ejecuta antes de que suceda la operación

- Ejemplo, un middleware pre-save sera ejecutado antes de guardar el documento. Útil para:
    -  validaciones más complejas,
    -  asignación de valores por defecto o 
    -  para eliminar documentos dependientes (eliminando un usuario eliminamos sus posts)
  
Las funciones __Pre__ se ejecutan de forma consecutiva cuando cada función invoca el método `next()`.

    const schema = new Schema(..); 
    schema.pre('save', next => {
    // do stuff 
    next(); 
    }); 

Con promesas...

    schema.pre('save', async function() { 
      await doStuff(); 
      await doMoreStuff(); 
    }); 

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: POST middleware

El middleware __`post`__ se ejecuta después de la operación
Ejemplo `post-save` se ejecutará después de grabar en la bd.
Las funciones post si llevan dos parámetros el segundo será el método `next` que llamará al siguiente post middleware
Ej:

    schema.post('save', function(doc) {
    console.log('%s has been saved', doc._id); }); 

---
### Ejercicio 24
<hr>

Sobre el ejercicio 22 (students y projects) crear un middleware __`pre`__ que convierta el campo `name` a mayúsculas antes de guardarlo en la bd

Generar una función de log con un middleware post que recoja los registros borrados de la aplicación

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: DBRef

- En MongoDB podemos definir referencias a otras colecciones incluyendo el __`_id`__ de la colección referenciada y la propiedad __`DBRef`__.
- En los schemas de Mongoose la relación se establece de manera análoga utilizando una propiedad que contenga un array de propiedades: 


       {type: Schema.ObjectId, ref:'Nombre_colección' }

Ej:

    import mongoose from 'mongoose';

      const Schema = mongoose.Schema;

      const PersonSchema = new Schema({
        name : String,
        age : Number,
        stories : [{ type: Schema.ObjectId, ref: 'Story' }]
        });

      const StorySchema = new Schema({
        _creator : { type: Schema.ObjectId, ref: 'Person' },
        title : String,
        fans : [{ type: Schema.ObjectId, ref: 'Person' }]
      });

      const Story = mongoose.model('Story', StorySchema);
      const Person = mongoose.model('Person', PersonSchema);

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: DBRef

Guardando documentos en la bd:


    try{

      const aaron = new Person({ name: 'Aaron', age: 100 });
      
      await aaron.save();
      
      const story1 = new Story({
          title: "A man who cooked Nintendo",
          _creator: aaron._id
        });

      await story1.save();

    } catch (error){
      console.log(error);
    }

---
task: [<< índice de contenidos >>](#contenido)

### MONGOOSE: Populate

- Para recuperar documentos referenciados utilizamos el método __`populate`__ para incorporar el contenido del documento hijo al documento padre.

 - En este caso se utiliza la función de callback __`.exec()`__ para ejecutar la función.


      const story = await Story
        .findOne({ title: /Nintendo/i })
        .populate('_creator') // <--
        .exec();

      console.log('The creator is %s', story._creator.name);
        // prints "The creator is Aaron"
      
- Para recuperar sólo ciertos campos utilizar un array de propiedades a mostrar dentro de la función populate:


    .populate('_creator', ['name']) // <-- only return the Persons name

---
### Ejercicio 25
<hr>

Rehacer la función __create__ del ejercicio 22 para incorporar la creación de __proyectos__ dentro de la colección __proyectos__ y después incorporarlos por referencia a la colección __students__. Para ello tienes que seguir los siguientes pasos:

  - Rehacer el `studentSchema` incorporando el `_id` del `projectSchema` por referencia en una propiedad projects.
  - Convertir la función `create` en `async` y rehacer la lógica de la función para guardar proyectos en la colección `projects` y `students` que referencien los projects.
  - Devolver el documento students con el contenido del documento projects.

