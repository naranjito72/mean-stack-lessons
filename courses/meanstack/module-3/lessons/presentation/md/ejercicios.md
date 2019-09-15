#### 1. Colecciones y Documentos

Crea una colección de documentos (facturas) en formato JSON con al menos los siguientes campos:
- Código_Factura
- Cliente
- Importe
- Estado (Pagado, Pendiente, Vencido, …)

#### 2. Queries MongoDB -I

1. Crear una bd “libreria” y cargar los scripts de github: https://github.com/rglepe/MeanStack/tree/master/Ejercicio2

2. Obtener todos los autores
3. Obtener los autores cuyo apellido sea DATE
4. Obtener los libros editados en 1998 o en 2005
5. Obtener el número de libros de la editorial Addison‐Wesley
6. Obtener el libro que ocupa la tercera posición
7. Obtener la lista de autores de cada libro junto con el título
8. Obtener los títulos de libro publicados con posterioridad a 2004
9. Obtener los libros editados en 1998 o en 2005
10. Obtener los libros editados desde 2001 y precio mayor que 50
11. Obtener los libros publicados por la editorial Addison‐Wesley después de 2005
12. Obtener el título de libro y editorial para aquellos libros que tengan un precio superior a 50€
13. Obtener los libros publicados en 1998 o a partir de 2005

#### 3. Queries MongoDB - II


1. Obtener la población total de las ciudades cuyo nombre empieza por A o B

2. Obtener la media de población de entre todas las ciudades de Nueva York y California cuya población supera los 25000 ciudadanos

3. Obtener los usuarios que han hecho más comentarios y los que han hecho menos de entre todos los posts de un blog. (tip: usar la cláusula unwind para crear un documento por cada comentario de cada post (que inicialmente estarían en un array dentro de el post correspondiente)



#### 4. Operaciones CRUDs

1. Insertar los documentos de la colección media.json en una base de datos llamada «media» en una única operación.

2. Actualizar el documento que hace referencia a la película «Matrix», de manera que se cambia su estructura a:
        {“tipo”: “DVD”,
        “Titulo”: “Matrix”,
        “estreno”: 1999,
        “genero”:”accion”
        }

3. Considerar un nuevo documento para la colección media:

        {“tipo”: “Libro”,
        “Titulo”: “Constantinopla”,
        “capitulos”:12,
        “leidos”:3
        }

    Añadir el documento a la colección media y a continuación incrementar en 5 unidades el valor de la clave «leídos».

4. Actualizar el documento referido a la película «Matrix» cambiando el valor de la clave «género» a «ciencia ficción».
5. Actualizar el documento referido al libro «Java para todos» de manera que se elimine la clave «editorial».
6. Actualizar el documento referido al libro «Java para todos» añadiendo el autor «María Sancho» al array de autores.
7. Actualizar el documento referido a la película «Matrix» añadiendo al array «actores» los valores de «Antonio Banderas» y «Brad Pitt» en una única operación.
8. Actualizar el documento referido a la película «Matrix» añadiendo al array «actores» los valores «Joe Pantoliano», «Brad Pitt» y «Natalie Portman» en caso de que no se encuentren, y si se encuentran no se hace nada.
9. Actualizar el documento referido a la película «Matrix» eliminando del array el primer y último actor.
10. Actualizar el documento referido a la película «Matrix» añadiendo al array actores los valores «Joe Pantoliano» y «Antonio Banderas».
11. Actualizar el documento referido a la película «Matrix» eliminado todas las apariciones en el array «actores» de los valores «Joe Pantoliano» y «Antonio Banderas».
12. Actualizar el documento referido al disco «Recuerdos» y añadir una nueva canción al array «canciones»:

        {“cancion”:5,
        “titulo”: “El atardecer”,
        “longitud”: “6:50”
        }

13. Actualizar el documento referido al disco «Recuerdos» de manera que la canción «El atardecer» tenga asignado el número 3 en vez de 5.
14. Actualizar el documento referido al disco «Recuerdos» de manera que en una sola operación se cambia el nombre del artista a «Los piratillas» y se muestre el documento resultante.
15. Renombrar el nombre de la colección «media» a «multimedia».

#### 5. Índices

#### 6. Map-Reduce

1. Cargar el fichero people.json en una bd personas
2. Generar por map-reduce una colección de personas (campo name) y su puntuación (campo points)
3. Comprobar el resultado sobre la nueva colección
4. Generar el mismo resultado mediante una función `aggregate`

#### 7. Map-Reduce II

Obtener por map-reduce una colección de directores y oscars de la colección movieDetails de la bd movies.

#### 8. Sharding y Clusters
Monta un cluster de sharding con un router, un servidor de configuración y dos shards. Servidores de configuración y shards formarán parte de grupos de réplica.

	Seguir el fichero: github

#### 9. Optimización

1. Ordenar por millis todos los documents para obtener las 10 queries más lentes
2. Obtener todas las queries que tardan más de 30 millisegundos en ejecutarse
3. Obtener las 10 queries de agregación/commandos más lentas
4. Obtener todas las operaciones  que implicaron movimiento de documentos
5. Obtener las queries que realizan operaciónes de scanning demasiado largas (Más de 10000 documentos)
6. Tiempo máximo y medio de las operaciones de agregación
7. Tº máx y medio de operaciones de agregación por bd.


