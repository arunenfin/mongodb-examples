## Find Operations
```javascript
db.collection.find()
db.collection.findOne()
```

```javascript
use exampledb

db.inventory.insertMany( [
   { item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "notebook", qty: 50, size: { h: 8.5, w: 11, uom: "in" }, status: "A" },
   { item: "paper", qty: 100, size: { h: 8.5, w: 11, uom: "in" }, status: "D" },
   { item: "planner", qty: 75, size: { h: 22.85, w: 30, uom: "cm" }, status: "D" },
   { item: "postcard", qty: 45, size: { h: 10, w: 15.25, uom: "cm" }, status: "A" }
]);
```

To select all documents in the collection
```javascript
db.inventory.find()
```
To select one document in the collection
```javascript
db.inventory.findOne()
```
The following example selects from the `inventory` collection all documents where the `status` equals "D":
```javascript
db.inventory.find( { status: "D" } )
```
The following example retrieves all documents from the `inventory` collection where `status` equals either "A" or "D"
```javascript
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
// SELECT * FROM inventory WHERE status in ("A", "D")
```
The following example retrieves all documents in the `inventory` collection where the `status` equals "A" and `qty` is less than (`$lt`) 30
```javascript
db.inventory.find( { status: "A", qty: { $lt: 30 } } )
// SELECT * FROM inventory WHERE status = "A" AND qty < 30
```
The following example retrieves all documents in the collection where 
the `status` equals "A" or `qty` is less than (`$lt`) 30
```javascript
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )
// SELECT * FROM inventory WHERE status = "A" OR qty < 30
```
Selects all documents in the collection where the `status` equals "A" and either `qty` is less than (`$lt`) 30 or `item` starts with the character p
```javascript
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )
// SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")
```
### Embedded or nested documents



The following query selects all documents where 
the field `size` equals the document `{ h: 14, w: 21, uom: "cm" }`
```javascript
db.inventory.find( { size: { h: 14, w: 21, uom: "cm" } } )
```
The following example selects all documents where the field `uom` nested in the `size` field equals "in"
```javascript
db.inventory.find( { "size.uom": "in" } )
```
The following query uses the less than operator (`$lt`) on the field `h` embedded in the `size` field
```javascript
db.inventory.find( { "size.h": { $lt: 15 } } )
```
The following query selects all documents where 
the nested field `h` is less than 15, the nested field `uom` equals "in", and the `status` field equals "D"
```javascript
db.inventory.find( { "size.h": { $lt: 15 }, "size.uom": "in", status: "D" } )
```
Count all Documents in a Collection
```javascript
db.orders.countDocuments({})
```
Count the number of the documents in the `orders` collection with the field `ord_dt` greater than `new Date('01/01/2012')`
```javascript
db.orders.countDocuments( { ord_dt: { $gt: new Date('01/01/2012') } }, { limit: 100 } )
```
### References
- https://docs.mongodb.com/manual/tutorial/query-documents/
- https://docs.mongodb.com/manual/tutorial/query-embedded-documents/
- https://docs.mongodb.com/manual/reference/method/db.collection.countDocuments/#db.collection.countDocuments
