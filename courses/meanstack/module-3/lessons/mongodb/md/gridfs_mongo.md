name: gridfs
class: center, middle, inverse
## [gridFS](https://docs.mongodb.com/manual/core/gridfs/)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

name: intro
task: [<< índice de contenidos >>](/courses/meanstack/module-3/lessons/mongodb/mongo.html#contenido")

### gridFS

Es un protocolo para almacenar y recuperar archivos que exceden el tamaño máximo de documentos de 16 MB. 

En vez de almacenar un archivo en un único documento, se divide el archivo en partes (chunks) y se almacena cada parte en documentos separados. Por defecto, cada trozo está limitado a 255 k.

Se usan dos colecciones para almacenar los archivos, una para almacenar los archivos de trozos y otro para almacenar archivos de metadatos asociados:
- `fs.files`
- `fs.chunks`

Cuanto se realiza una consulta a un almacén GridFS por un archivo, se reensamblan los trozos necesarios.

Se pueden realitzar consultas sobre secciones arbitrarias de los archivos

No hace falta cargar todo el archivo en memoria para acceder a él.

---
name: instrucciones
task: [<< índice de contenidos >>](/courses/meanstack/module-3/lessons/mongodb/mongo.html#contenido")

### trabajar con gridFS

Para trabajar con GridFS desde MongoDB se utiliza el comando mongofiles

Ejemplo: guardar un fichero c:\video.mp4

.inverse[<pre class=codigo> mongofiles -d media put c:\mongodb\video.mp4</pre>
]
Desde la db: show collections:
.inverse[<pre class=codigo> show collections
        fs.chunks
        fs.files
        multimedia</pre>

Para mostrar el contenido del documento:
    
    db.fs.files.find();

Para recuperar un fichero y guardarlo en un directorio determinado:
.inverse[<pre class=codigo> mongofiles -d media get c:\video.mp4</pre>
]
--- 
