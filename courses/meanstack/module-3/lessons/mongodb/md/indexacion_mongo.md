name: indexación
class: center, middle, inverse
## [Indexing](https://docs.mongodb.com/manual/indexes/)
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


---
name:Compuestos
### Índices compuestos

Mantienen bajo el número de índices de una colección. Se deben utilizar siempre que sean posible
Tipos de índices compuestos: 
índices multiclave: { titulo:”One Post”, autor:{nombre:”John”, email:”john@email.com”}}

        db.posts.createIndex(“autor”:1)

índices compuestos definidos por el usuario

        db.posts.createIndex(“nombre”:1,”email”:1)


En la ordenación no es bueno usar índices compuestos, salvo que la lista de términos y las direcciones de ordenación encajen exactamente con la estructura del índice. En estos casos, una elección mejor es usar índices simples individuales sobre cada campo.

---

### Índices de texto

Se pueden crear índices de texto para realizar búsquedas sobre campos de texto (string):
Búsquedas: db.collection.find({$text:{$search:”cadena o cadenas de texto a buscar”}})
Para crear el índice:

        db.reviews.createIndex( { comments: "text" } )

Si se incluyen varios campos de texto, se puede especificar la relevancia (peso) de la búsqueda de un campo respecto a los otros:

        db.blog.createIndex(
        { content: "text",  keywords: "text",   about: "text"  },
        { weights: { content: 10,   keywords: 5  },
            name: "TextIndex"   } )

---
### Otros índices

- Índices Hashed:

    Permiten reducir el tamaño de los índices almacenando sólo la clave hashed. Se utiliza en particiones-SHARDS

- Índice Geospatial:
  
    Permiten agilizar la búsqueda de geometrías en una superficie esférica (las búsquedas pueden ser de inclusión, intersección y proximidad)

- Índice TTL (Time-To-Live) 

    Índices de campo único que permiten eliminar documentos de una colección después de un intervalo de tiempo o de una hora especificada
    Útil para eliminar datos ligados a eventos, logs o información de session que necesitan que persistan en la bd durante un tiempo finito.

---
### Opciones de indexación

- Indexación en segundo plano: `{background: true}`
- Índices únicos: `{unique:true}`
    
---

### Estrategias de indexación

Para diseñar buenos índices para una aplicación es necesario tener en cuenta una serie de factores: los tipos de consultas, el ratio de lecturas y escrituras y la cantidad de memoria libre del sistema

- [Crea índices que optimicen tus consultas](https://docs.mongodb.com/manual/tutorial/create-indexes-to-support-queries/)

Un índice sirve para mejorar el rendimiento de una consulta cuando contiene todos los campos utilizados por la consulta

- [Usa los índices para ordenar los resultados de la consulta](https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/)

Cuando se especifica un orden secuencial y ordenado de los campos del índice

- [Aségurate que los índices completos cabe en la memoria RAM](https://docs.mongodb.com/manual/tutorial/ensure-indexes-fit-ram/)

Si los índices caben enteros en la RAM, el sistema evita leer del disco, procesándose mucho más rápido

- [Crear consultas que aseguren la selectividad](https://docs.mongodb.com/manual/tutorial/create-queries-that-ensure-selectivity/)

Capacidad de una consulta de afinar los resultados usando el índice. La selectividad permite a Mongodb usar el índice para realizar más cantidad de trabajo asociado a responder la consulta.

---

### Ejercicios
<hr>

Crear índices para optimizar las siguientes consultas. Comprobar la utilización del índice con `cursor.explain()`:

1. Buscar todos los documentos que contengan las etiquetas "ipsum" y "sint"
   ``` 
db.posts.find({tags:{$all:["ipsum","sint"]}},{tags:1,_id:0})
```

2. Buscar en los comentarios  por el nombre "Nielsen" y el email "nielsen@mail.com"

