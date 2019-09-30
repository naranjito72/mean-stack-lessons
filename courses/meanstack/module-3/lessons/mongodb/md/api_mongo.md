name: indexación
class: center, middle, inverse
## [API MongoDB for NodeJS](http://mongodb.github.io/node-mongodb-native/3.3/)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Instalación

Una vez creado el archivo `package.json`, con el comando `npm init`, el driver de MongoDB se instala con: 
.inverse[<pre class=codigo> npm install mongodb --save
</pre>


---
### Tipos de índices

- [Campo Único](#single-field) (https://docs.mongodb.com/manual/core/index-single/)
- [Compuestos](https://docs.mongodb.com/manual/core/index-compound/)
- [Multiclave](https://docs.mongodb.com/manual/core/index-multikey/)
- [Texto](https://docs.mongodb.com/manual/core/index-text/)
- [Comodín](https://docs.mongodb.com/manual/core/index-wildcard/)
- [2dspheres](https://docs.mongodb.com/manual/core/2dsphere/)
- [2d](https://docs.mongodb.com/manual/core/2d/)
- [geoHaystack](https://docs.mongodb.com/manual/core/geohaystack/)
- [Hashed](https://docs.mongodb.com/manual/core/index-hashed/)
  
---
name: single-field
task: [<< índice de contenidos >>](#contenido)

### Índice campo único

Función __`createIndex(clave:orden)`__:

  - clave: que se usará para crear el índice
  - orden: dirección de ordenación del índice: 1 ascendente y -1 descendente

Por defecto, MongoDB crea el índice sobre el campo _id.

El índice se creará para todos los valores de la clave indicada para todos los documentos de la colección:

    db.posts.createIndex(“Etiquetas”:1)

Para indexar un campo de un documento embebido:

    db.posts.createIndex(“comentarios.contador”:1)

Si se indexa un array, se incluyen todos los elementos del array en el índice, pero no se puede indicar el orden dentro del array.

Para consultar los índices:__` db.collection.getIndexes()`__

