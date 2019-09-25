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
### Ejemplo 1

<img src="https://docs.mongodb.com/manual/_images/map-reduce.bakedsvg.svg" width=75% height=75%>


---

### Ejemplo 2

Partimos de la siguiente colección:

```javascript
db.frases.drop()
db.frases.insert({_id:1,frase:"el que sabe no habla"})
db.frases.insert({_id:2,frase:"el que habla no sabe"})
db.frases.insert({_id:3,frase:"no me digas que no"})
```

Queremos contar el número de repeticiones de cada palabra.
???
```javascript
var mapFunctionFrase = function(){
   x = this.frase.split(" ");
   for (var i=0; i<x.length; i++)
        emit(x[i], 1);
};
var reduceFunctionFrase = function(palabra,cuantas){
     return Array.sum(cuantas);};
 
db.frases.mapReduce(mapFunctionFrase,
                       reduceFunctionFrase,
                       {out: "palabras"}
                      )
``` 
---
### Ejemplo 3

A partir de la siguiente colección: 

```javascript
use running
db.sesiones.insert({nombre:"Bertoldo", mes:"Marzo", distKm:6, tiempoMin:42})
db.sesiones.insert({nombre:"Herminia", mes:"Marzo", distKm:10, tiempoMin:60})
db.sesiones.insert({nombre:"Bertoldo", mes:"Marzo", distKm:2, tiempoMin:12})
db.sesiones.insert({nombre:"Herminia", mes:"Marzo", distKm:10, tiempoMin:61})
db.sesiones.insert({nombre:"Bertoldo", mes:"Abril", distKm:5, tiempoMin:33})
db.sesiones.insert({nombre:"Herminia", mes:"Abril", distKm:42, tiempoMin:285})
db.sesiones.insert({nombre:"Aniceto", mes:"Abril", distKm:5, tiempoMin:33})
```

Queremos saber cuántos kilómetros a recorrido cada persona al mes usando _MapReduce_:
???
```javascript
var mapKmPersonaMes = function(){
        emit({nombre:this.nombre, mes:this.mes}, this.distKm);
};
var reduceKmPersonaMes = function(dato,cuantos){
     return Array.sum(cuantos);
};
 
db.sesiones.mapReduce(mapKmPersonaMes,
                       reduceKmPersonaMes,
                       {out: "kmMes"}
                      )
```  
---
### Ejercicio
<hr>
1. Cargar el fichero people.json en una bd personas
2. Generar por map-reduce una colección de personas (campo name) y su puntuación (campo points)
3. Comprobar el resultado sobre la nueva colección
4. Generar el mismo resultado mediante una función aggregate
---

### Ejercicio
<hr>

Obtener por mapReduce una colección de directores y oscars de la colección movieDetails de la bd movies.

