name: indexación
class: center, middle, inverse
## [Relaciones por referencia](https://docs.mongodb.com/manual/reference/database-references/)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Relaciones

En determinadas ocasiones es necesario almacenar la información en documentos separados pero relacionados, normalmente en colecciones o bases de datos separadas.

MongoDB utiliza dos métodos para relacionar documentos separados:

- __Referencias manuales__: Se almacena un campo _id de un documento en otro documento como referencia. La aplicación es la responsable de lanzar una segunda consulta para recoger la información relacionada.

- __DBRefs__: Referencias de un documento a otro usando el _id del primer documento, nombre de colección y base de dato (opcional) Se utiliza sobre todo para localizar documentos en más de una coleccion desde una única colección (relaciones 1:n) La aplicación debe realizar queries adicionales para devolver el document referenciado.

    _Ejemplo de aplicación_: Visualizar autores de comentarios de una publicación en el caso de que los datos de usuario puedan cambiar y sea una consulta recurrente 

---
name: manuales
task: [<< índice de contenidos >>](/courses/meanstack/module-3/lessons/mongodb/mongo.html#contenido")

### Referencias manuales

Consiste en incluir el campo __`_id`__ de un documento en otro documento. La aplicación debe realizar una segunda consulta para resolver el campo referenciado.

ejemplo:

```javascript
original_id = ObjectId()

db.places.insert({
    "_id": original_id,
    "name": "Broadway Center",
    "url": "bc.example.net"
})

db.people.insert({
    "name": "Erin",
    "places_id": original_id,
    "url":  "bc.example.net/Erin"
})

```
Esta es la manera habitual de relacionar documentos. Aunque tiene la limitación de que no lleva ímplicito el nombre de la base de datos o de la colección.
---
name: dbrefs
task: [<< índice de contenidos >>](/courses/meanstack/module-3/lessons/mongodb/mongo.html#contenido")

### DBRefs

Es una convención para representar un documento. Incluye el nombre de la colección y, en algunos casos, el nombre de la bd, además del campo `_id`, .

```json
{ "$ref" : <value>, "$id" : <value>, "$db" : <value> }
```

<img src=https://imgur.com/ptZJOIR.png height=99% width=99%>

---

### Relaciones por Referencia: $lookup y $graphLookup

Etapas del pipe aggregate para obtener información de otros documentos relacionados por DBRefs:

```javascript
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```
Para realizar una búsqueda recursiva en una colección:
```javascript
{
   $graphLookup: {
      from: <collection>,
      startWith: <expression>,
      connectFromField: <string>,
      connectToField: <string>,
      as: <string>,
      maxDepth: <number>,
      depthField: <string>,
      restrictSearchWithMatch: <document>
   }
}
```
---
### Ejemplo

Utilizando las colecciones "sesiones" y "gustos" del documento de aggregation.md, queremos conocer, para la persona que mayor distancia total ha recorrido:

- Su nombre
- La distancia total recorrida
- Sus aficiones