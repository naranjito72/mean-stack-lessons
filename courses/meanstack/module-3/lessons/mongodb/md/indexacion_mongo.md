
class: center, middle, inverse

###<img src="https://imgur.com/StvjTKm.png" width=50% height=50% alt="logo">  
---

name: base de datos
class: center, middle, inverse
## [Data Modelling](#bbdd)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Modelado de datos en MongoDB

Una de las ventajas de MongoDB es su __esquema flexible__. Esto nos permite crear documentos con diferente estructura, incluso tener documentos con campos completamente diferentes dentro de la misma colección. No obstante, el escenario más común es agrupar documentos con una estructura similar dentro de la misma colección

Cuando se diseña un modelo de datos de una base de datos, se debe tener en cuenta los tipos de datos que se utilizarán en la aplicación. La clave es entender cual es la estructura de documentos más idónea y cual es la relación entre esos documentos que mejor responda a las necesidades de la aplicación.

La relación entre documentos se puede representar de dos maneras:

- Documentos embebidos
- Relación por referencia

---

name: 1fn
task: [<< índice de contenidos >>](#contenido)

### La Primera Forma Normal (1FN)
Partimos de la estructura de datos clásica de un [modelo relacional](https://es.wikipedia.org/wiki/Modelo_relacional)
<br>
<br>

| id| name | Phone |
|--------------------|------|-----------|
| 3212  | John  | 555-111-1234 | 
| 4324  | Willy | 555-222-2345 |
| 6542  | James | 555-222-6789  |

<br>
Si queremos almacenar más de un teléfono ya no podemos disponer de la primera forma normal:

| id| name | Phone |
|--------------------|------|-----------|
| 3212  | John  | 555-111-1234 | 
| 4324  | Willy | 555-222-2345;555-212-2322 |
| 6542  | James | 555-222-6789;555-334-3411  |


---
### Documentos embebidos

Un documento incorpora dentro de su estructura el documento con el que se relaciona:

![](https://i.imgur.com/yrliwPP.png)
---
### Documentos embebidos

El caso del ejemplo con documentos embebidos quedaría:

```javascript
{
"_id": 3,
"name": "Jenny",
"zip_code": "01209",
"numbers": [ "555-333-3456", "555-334-3411" ]
}
```
---

### Relaciones

Relacionar significa realizar asociaciones entre documentos de diferentes colecciones mediante su  `_id`.

Si tenemos documentos `contact` y `access`. Si queremos relacionar un  `contacto` y un `acceso` a un usuario en particular (`user`), necesitaríamos añadir una propiedad que los relacionara mediante el `user_id`:

![](https://i.imgur.com/GmBjx9W.png)

---

### Relaciones
El caso del ejemplo con documentos referenciados quedaría de la siguiente manera:

    // Contact document:
    {
    "_id": 3,
    "name": "Jenny",
    "zip_code": "01209"
    }
    // Number documents:
    { "contact_id": 3, "number": "555-333-3456" }
    { "contact_id": 3, "number": "555-334-3411" }

Para obtener la información de un usuario tenemos que conseguir su `id` y después realizar una segunda consulta para obtener la información de contacto en base a ese `id`
???

---
task: [<< índice de contenidos >>](#contenido)

## Cómo definir el mejor esquema

Se debe comenzar el diseño del esquema considerando los requisitos de consultas de la aplicación.

El modelo debería aprovechar la ventaja de contar con un modelo flexible.

En este caso debemos tener en cuenta:
- que datos queremos,
- la frecuencia de consulta de los datos,
- el tamaño de los documentos,
- etc.
---
### Tiempo de acceso:

En el caso que el tiempo de acceso sea prioritario utilizaremos documentos embebidos para aprovechar el sistema de almacenamiento de documentos en discos duros rotatorios (spinning disks)
    + MongoDB almacena todos los documentos de forma contigua en el disco
    + MongoDB funcionaría aún peor en búsquedas por referencia:

```javascript
    contact_info = db.contacts.find_one({'_id': 3})
    number_info = list(db.numbers.find({'contact_id': 3})
```
---
### Control de Transacciones
Si queremos asegurar la integridad de una transacción, aseguraremos la
__atomicidad__ y el __aislamiento__ (A+I de ACID) ya que los documentos embebidos no necesitan control de las transacciones:

```sql

    BEGIN TRANSACTION;
    DELETE FROM contacts WHERE contact_id=3;
    DELETE FROM numbers WHERE contact_id=3;
    COMMIT;
```

      db.contacts.remove({'_id': 3})
      db.numbers.remove({'contact_id': 3})
---

### Información dependiente de contexto

Si un subdocumento sólo tiene sentido en el contexto del padre. Caso de las [relaciones 1 a 1](https://docs.mongodb.com/manual/tutorial/model-embedded-one-to-one-relationships-between-documents/)

Ejemplo:

```javascript
{
   _id: 57,
   name: "Joe Bookreader",
   address: {
              street: "123 Fake Street",
              city: "Faketon",
              state: "MA",
              zip: "12345"
            }
}
```
En este caso no tiene sentido la dirección por si misma. En nuestra aplicación está asociada a un usuario, por tanto usaríamos documentos embebidos aquí.
---

### Sub-documentos Múltiples

Distintos documentos que necesitan el contexto del padre o cuando una aplicación necesita muchas peticiones para resolver una relación.

```javascript
{
   _id: 57,
   name: "Joe Bookreader",
   addresses: [
      {
        street: "123 Fake Street",
        city: "Faketon",
        state: "MA",
        zip: "12345"
      },
      {
        street: "1 Some Other Street",
        city: "Boston",
        state: "MA",
        zip: "12345"
      }
    ]
 }
```

Hay que vigilar cuantos subdocumentos se embeben en un único documento. **Tener en cuenta que el tamaño de un documento en MongoDB no puede exceder los 16Mb de tamaño.**
---
### Separación en colecciones

Usaremos relaciones cuando el mismo subdocumento aparezca en muchos sitios y dentro de muchos documentos. En el siguiente ejemplo la estructura no sería correcta:

```javascript
{
   title: "MongoDB: The Definitive Guide",
   author: [ "Kristina Chodorow", "Mike Dirolf" ],
   published_date: ISODate("2010-09-24"),
   pages: 216,
   language: "English",
   publisher: {
              name: "O'Reilly Media",
              founded: 1980,
              location: "CA"
            }
},
{
   title: "50 Tips and Tricks for MongoDB Developer",
   author: "Kristina Chodorow",
   published_date: ISODate("2011-05-06"),
   pages: 68,
   language: "English",
   publisher: {
              name: "O'Reilly Media",
              founded: 1980,
              location: "CA"
            }
}
```
---
En este caso se repite la información del `publisher`. Podríamos evitar repeticiones de esta manera:


**Publisher** collection
```javascript
{
   _id: 123,
   name: "O'Reilly Media",
   founded: 1980,
   location: "CA",
   books: [454, 581]
}
```
**Book** collection
```javascript
{
   _id: 454,
   title: "MongoDB: The Definitive Guide",
   author: [ "Kristina Chodorow", "Mike Dirolf" ],
   published_date: ISODate("2010-09-24"),
   pages: 216,
   language: "English",
   publisher_id: 123
},
{
   _id: 581,
   title: "50 Tips and Tricks for MongoDB Developer",
   author: "Kristina Chodorow",
   published_date: ISODate("2011-05-06"),
   pages: 68,
   language: "English",
   publisher_id: 123
}
```
---
### Referencias para:

- __Flexibilidad__

Ejemplo: A una búsqueda por autor de comentarios se ajusta mejor un esquema parcialmente normalizado

    { "_id": "First Post",
    "comments": [
    { "author": "Stuart", "text": "Nice post!" },
    { "author": "Mark", "text": "Dislike!" } ] },
    { "_id": "Second Post",
    "comments": [
    { "author": "Danielle", "text": "I am intrigued" },
    { "author": "Stuart", "text": "I would like to subscribe" } ] }
    ----------------
    // db.posts schema                    // db.comments schema
    {                                     {
    "_id": "First Post",                  "_id": ObjectId(...),
    "author": "Rick",                     "post_id": "First Post",
    "text": "This is my first post"       "author": "Stuart",
    }                                     "text": "Nice post!"
                                          }

---
task: [<< índice de contenidos >>](#contenido)

### Referencias para:

- En __relaciones de alto grado (aridad)__ es conveniente __normalizar__
	Ej.: blog con muchos comentarios (⁓100-1000)

- Cuanto más grande es un documento más RAM es necesaria para cargar la información.
- Los documentos muy grandes se desplazan a otros espacios de disco. El límite de un documento es de 16 MB

- En las __relaciones M:N__ se ha de llegar a un compromiso entre normalizar o no.

```json
   // db.product schema            // db.product schema
   { "_id": "My Product", ... }    { "_id": "My Product",
                                   "category_ids": [ "My Category",...] }
   // db.category schema           // db.category schema
   { "_id": "My Category", ... }   { "_id": "My Category" }
 
   // db.product_category schema
   { "_id": ObjectId(...),
   "product_id": "My Product",
   "category_id": "My Category" }
```

---
### Esquemas polimórficos

- Los esquemas polimórficos (POO) se refieren a colecciones de documentos que son similares pero que no están idénticamente estructurados
- __Inconveniente__: Almacenamiento ineficiente de BSON => Cabeceras repetidas por documento

Ej.: Wiki comentarios y fotos

      // "Page" document (stored in "nodes" collection")
      {
      _id: 1,
      title: "Welcome",
      url: "/",
      type: "page",
      text: "Welcome to my wonderful wiki."
      }
      ...
      // "Photo" document (also in "nodes" collection)
      {
      _id: 3,
      title: "Cool Photo",
      url: "/photo.jpg",
      type: "photo",
      content: Binary(...)
      }
---
### Soporte a Esquemas semi-estructurados 

Productos con atributos pero no todos los productos tienen los mismos atributos 
Ej. Discos duros con distintas características 
```json
{                                  {                               
  _id: ObjectId(...),               _id: ObjectId(...),
  price: 499.99,                    price: 499.99,                  
  title: 'Big and Fast Disk Drive', title: 'Big and Fast Disk Drive',
  gb_capacity: 1000,                gb_capacity: 1000,              
  properties: {                     properties: [                   
  'Seek Time': '5ms',                    ['Seek Time', '5ms' ],          
  'Rotational Speed': '15k RPM',         ['Rotational Speed', '15k RPM'],
  'Transfer Rate': '...'                 ['Transfer Rate', '...'],  
    ... }                                ... ]                           
}                                  }                               
```
En el último caso podemos crear un índice, con la siguiente instrucción:
```json
    db.products.ensure_index('properties')
```
Una vez creado el índice, la query necesaria para buscar por una propiedad quedaría:

    db.products.find({'properties': [ 'Seek Time': '5ms' ]})
---
name:diseño

### Data Modelling

MongoDB presenta un esquema flexible de documentos en la misma colección:

- Pueden tener distinto grupo de campos
- Un mismo campo puede tener distinto tipo de dato

A la hora de diseñar:

- Diseña según los requerimientos de usuario
- Combina objetos en un mismo documento si se van a utilizar juntos. Si no, sepáralos pero asegúrate de que no necesitarás JOINS
- Duplica datos. Disco + barato que Memoria
- Realiza las JOINS al escribir y no al leer
- Optimiza el esquema para los casos de uso más frecuentes
- Realiza agregaciones complejas en el esquema
---

task: [<< índice de contenidos >>](#contenido)
#### Ejercicio entregable
<hr>

- Crear una bd para un ecommerce que contenga las siguientes colecciones:
  - USER
  - PRODUCT
  - CATEGORY
  - CART

- Generar consultas sobre las colecciones anteriores para llevar a cabo las siguientes operaciones:
  
  -  Generar al menos consultas sobre productos que puedan ser requeridas por los usuarios (Buscar por tipo de producto, talla, tamaño, precios, recomendados, ofertas, últimas adquisiciones, etc…)
  -  Realizar un mantenimiento de la jerarquía de categorías añadiendo una nueva categoría y modificando una categoría. Realizar también las consultas para obtener el hilo de Ariadna de un producto determinado
  -  Gestionar el carrito: Añadir un producto al carrito, eliminar un producto del carrito, abandono del carrito sin comprar, pagar.

---

## Recursos extra

Algunos artículos y libros interesantes para modelar datos en MongoDB:

- [6 Rules of Thumb for MongoDB Schema Design: Part 1](http://blog.mongodb.org/post/87200945828/6-rules-of-thumb-for-mongodb-schema-design-part-1)
- [6 Rules of Thumb for MongoDB Schema Design: Part 2](http://blog.mongodb.org/post/87892923503/6-rules-of-thumb-for-mongodb-schema-design-part-2)
- [Thinking in Documents: Part 1](https://www.mongodb.com/blog/post/thinking-documents-part-1?jmp=docs)
- [Thinking in Documents: Part 2](https://www.mongodb.com/blog/post/thinking-documents-part-2)
- [Data Modeling Article](https://www.infoq.com/articles/data-model-mongodb)
- [MongoDB Applied Design Patterns](https://www.amazon.com/MongoDb-Applied-Design-Patterns-Copeland/dp/1449340040)
---

[_Volver al Menú Principal_](/courses/meanstack/content.html)