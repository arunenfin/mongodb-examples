
### _id field
https://docs.mongodb.com/manual/reference/bson-types/#objectid
### Insert commands
```
db.collection.insertOne()
db.collection.insertMany()
db.collection.insert()
```
### insertOne
```
use exampledb
db.products.insertOne( { item: "box", qty: 20 } );
```
https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/
### insertMany
```
db.products.insertMany( [
  { item: "card", qty: 15 },
  { item: "envelope", qty: 20 },
  { item: "stamps" , qty: 30 }
] );
```
https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany
### insert
```
db.products.insert( { item: "card", qty: 15 } )
db.products.insert(
   [
     { _id: 11, item: "pencil", qty: 50, type: "no.2" },
     { item: "pen", qty: 20 },
     { item: "eraser", qty: 25 }
   ]
)
```
https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert
