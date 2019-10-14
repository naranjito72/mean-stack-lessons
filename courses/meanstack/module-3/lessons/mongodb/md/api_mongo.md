name: indexación
class: center, middle, inverse
## [API MongoDB for NodeJS](http://mongodb.github.io/node-mongodb-native/3.3/)
---

name: default
layout: true
task: &nbsp;

.task[{{task}}]

---

### Instalación y Conexión

Una vez creado el archivo `package.json`, con el comando `npm init`, el driver de MongoDB se instala con: 
.inverse[<pre class=codigo> npm install mongodb --save
</pre>
]

Para trabajar con MongoDB desde Node.js se tiene que importar la clase MongoClient del package:

```javascript
  import {MongoClient} from 'mongodb';
```

Una vez importado se invoca el método `connect()` de una instancia de la clase MongoClient, pasándole la url de la bd como argumento:

```javascript
  const url = 'mongodb://localhost:27017';
  const db = 'myproject';

  const client = new MongoClient(url);
//pasamos un callback para gestionar la conexión
  client.connect(err=>{
    console.log("Connected successfully to server");

    const db = client.db(dbName);

    client.close();
  })
```

---

### Conexión con ES7

Si al método de conexión no se le pasa un _callback_, éste devuelve una promesa:

```javascript
import {MongoClient}  from 'mongodb';

async () => {
  // Connection URL
  const url = 'mongodb://localhost:27017/myproject';
  // Database Name
  const dbName = 'myproject';
  const client = new MongoClient(url, { useNewUrlParser: true });

  try {
    // Use connect method to connect to the Server
    await client.connect();

    const db = client.db(dbName);
  } catch (err) {
    console.log(err.stack);
  }

  client.close();
})();

```
---

### Operaciones CRUD: Insert

Usamos los métodos `insertOne()` o `insertMany()`:

```javascript
    ...
    // Insert a single document
    let r = await db.collection('inserts').insertOne({a:1});
    assert.equal(1, r.insertedCount);

    // Insert multiple documents
    r = await db.collection('inserts').insertMany([{a:2}, {a:3}]);
    assert.equal(2, r.insertedCount);
  } catch (err) {
    console.log(err.stack);
  }
  ...
```
---

### Operaciones CRUD: Update

Usamos los métodos `updateOne()` o `updateMany()`:

```javascript
    ...
    const col = db.collection('updates');
    let r;

    // Insert multiple documents
    r = await col.insertMany([{a:1}, {a:2}, {a:2}]);
    // Update a single document
    r = await col.updateOne({a:1}, {$set: {b: 1}});
    // Update multiple documents
    r = await col.updateMany({a:2}, {$set: {b: 1}});
    // Upsert a single document
    r = await col.updateOne({a:3}, {$set: {b: 1}}, {upsert: true});

} catch (err) {
    console.log(err.stack);
  }
  ...
```
---

### Operaciones CRUD: Delete

Usamos los métodos `deleteOne()` o `deleteMany()`:

```javascript
    ...
    let r;

    // Insert multiple documents
    r = await col.insertMany([{a:1}, {a:2}, {a:2}]);
    // Remove a single document
    r = await col.deleteOne({a:1});
    assert.equal(1, r.deletedCount);

    // Remove multiple documents
    r = await col.deleteMany({a:2});

  } catch (err) {
    console.log(err.stack);
  }

  ...
```
---
### Operaciones CRUD: Métodos especiales

`findOneAndUpdate`, `findOneAndDelete` and `findOneAndReplace` permiten modificar o reemplazar un documento y devolverlo. Requiere el bloqueo del documento hasta que se devuelve.

```javascript
    ...
    // Get the findAndModify collection
    const col = db.collection('findAndModify');
    let r;

    // Insert multiple documents
    r = await col.insert([{a:1}, {a:2}, {a:2}]);
    
    // Modify and return the modified document
    r = await col.findOneAndUpdate({a:1}, {$set: {b: 1}}, {
      returnOriginal: false,
      sort: [['a',1]],
      upsert: true
    });

  } catch (err) {
    console.log(err.stack);
  }
    ...
```
---
### Operaciones CRUD: Read

Los principales métodos son `find()` y `aggregate()` que devuelven un cursor.

Ejemplo devuelve los dos primeros documentos de una colección en un Array();

```javascript
    ...
    // Get the collection
    const col = db.collection('find');

    // Insert multiple documents
    const r = await col.insertMany([{a:1}, {a:1}, {a:1}]);
    
    // Get first two documents that match the query
    const docs = await col.find({a:1}).limit(2).toArray();
  } catch (err) {
    console.log(err.stack);
  }

  ...
```
También podemos iterar sobre el cursor con el método next(), de manera más limpia:

```javascript
...
    // Get the cursor
    const cursor = col.find({a:1}).limit(2);

    // Iterate over the cursor
    while(await cursor.hasNext()) {
      const doc = await cursor.next();
      console.dir(doc);
    }
...
```
### Más información

[Referencias ECMAScript Next](https://mongodb.github.io/node-mongodb-native/3.3/reference/main/)

---
### Ejercicio: Crunchbase

Realizar un menú desde el terminal para obtener información de la bd _crunchbase_.
