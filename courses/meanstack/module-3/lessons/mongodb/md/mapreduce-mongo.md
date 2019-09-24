name: indexación
class: center, middle, inverse
## [MapReduce](https://docs.mongodb.com/manual/core/map-reduce/)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Map-Reduce

Map-reduce es un _framework_ creado por Google, y pensado
para realizar operaciones de forma paralela sobre grandes colecciones
de datos.
Las operaciones map-reduce constan de tres partes:

1. Una etapa de __map__, en la que se procesa cada documento y se emite uno o varios objetos por cada documento procesado. Se implementa mediante una función que mapea los datos de origen, de manera que, para cada dato de origen, se genera una tupla clave-valor, que son unidas en una lista que se pasa a la etapa _reduce_.
   
2. Una etapa __reduce__ en la que se combinan las salidas de la etapa anterior. Se implementa mediante una función `reduce`, que trata cada elemento de la lista de pares y realiza operaciones sobre ella para devolver un dato concreto.
   
3. Una tercera etapa opcional, __finalize__, en la que se permite realizar algunas modificaciones adicionales a las salidas de la etapa reduce.
   
---
name: command
### mapReduce command

    db.runCommand(
                {
                    mapReduce: <collection>,
                    map: <function>,
                    reduce: <function>,
                    finalize: <function>,
                    out: <output>,
                    query: <document>,
                    sort: <document>,
                    limit: <number>,
                    scope: <document>,
                    jsMode: <boolean>,
                    verbose: <boolean>,
                    bypassDocumentValidation: <boolean>,
                    collation: <document>,
                    writeConcern: <document>
                }
                )  
---
name: helper
task: [<< índice de contenidos >>](#contenido)

### mapReduce helper

        db.coleccion.mapReduce (
            mapFunction,
            reduceFunction,
            {
                out: <salida>,
                query: <documento>,
                sort: <documento>,
                limit: <número>,
                finalize: <función>,
                scope: <documento>,
                jsMode: <booleano>,
                verbose: <booleano>
            }
        )

---
name:ejemplo
### Ejemplo

![](https://docs.mongodb.com/manual/_images/map-reduce.bakedsvg.svg)
---
