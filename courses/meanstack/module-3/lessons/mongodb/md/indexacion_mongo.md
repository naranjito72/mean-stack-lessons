name: indexación
class: center, middle, inverse
## [Data Modelling](#bbdd)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Indexación

Estructura de datos que mantiene información acerca de los valores de campos específicos en los documentos de una colección

- Se utiliza para ordenar y clasificar rápidamente los documentos de una colección

- Se asegura una búsqueda y recuperación rápida de datos de los documentos

- Cuando se crea un índice, aumenta la velocidad de las consultas, pero se reduce la velocidad de las inserciones y las eliminaciones

- Deben mantenerse (borrarse o reconstruirse) por:
    + Limpiar algunas irregularidades que aparecen en los índices.
    + Aumento del tamaño de la base de datos.
    + Espacio excesivo ocupado por los índices. Solo se pueden definir como máximo cuarenta índices por colección.

---
### Tipos de índices

- [Campo Único](https://docs.mongodb.com/manual/core/index-single/)
- [Compuestos](https://docs.mongodb.com/manual/core/index-compound/)
- [Multiclave](https://docs.mongodb.com/manual/core/index-multikey/)
- [Texto](https://docs.mongodb.com/manual/core/index-text/)
- [Comodín](https://docs.mongodb.com/manual/core/index-wildcard/)
- [2dspheres](https://docs.mongodb.com/manual/core/2dsphere/)
- [2d](https://docs.mongodb.com/manual/core/2d/)
- [geoHaystack](https://docs.mongodb.com/manual/core/geohaystack/)
- [Hashed](https://docs.mongodb.com/manual/core/index-hashed/)
  
---
name: 1fn
task: [<< índice de contenidos >>](#contenido)

### Índice campo único

Función __`createIndex(clave:orden)`__:

  - clave: que se usará para crear el índice
  - orden: dirección de ordenación del índice: 1 ascendente y -1 descendente

El índice se creará para todos los valores de la clave indicada para todos los documentos de la colección:

db.posts.createIndex(“Etiquetas”:1)


Para indexar un documento embebido:

db.posts.createIndex(“comentarios.contador”:1)


Si se indexa un array, se incluyen todos los elementos del array en el índice, pero no se puede indicar el orden dentro del array.

Para consultar los índices:__` db.collection.getIndexes()`__


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