### Update Operations
```javascript
db.collection.update(<filter>, <update>, <options>)
db.collection.updateOne(<filter>, <update>, <options>)
db.collection.updateMany(<filter>, <update>, <options>)
db.collection.replaceOne(<filter>, <update>, <options>)
```

```javascript
use exampledb

db.inventory.insertMany( [
   { item: "canvas", qty: 100, size: { h: 28, w: 35.5, uom: "cm" }, status: "A" },
   { item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "mat", qty: 85, size: { h: 27.9, w: 35.5, uom: "cm" }, status: "A" },
   { item: "mousepad", qty: 25, size: { h: 19, w: 22.85, uom: "cm" }, status: "P" },
   { item: "notebook", qty: 50, size: { h: 8.5, w: 11, uom: "in" }, status: "P" },
   { item: "paper", qty: 100, size: { h: 8.5, w: 11, uom: "in" }, status: "D" },
   { item: "planner", qty: 75, size: { h: 22.85, w: 30, uom: "cm" }, status: "D" },
   { item: "postcard", qty: 45, size: { h: 10, w: 15.25, uom: "cm" }, status: "A" },
   { item: "sketchbook", qty: 80, size: { h: 14, w: 21, uom: "cm" }, status: "A" },
   { item: "sketch pad", qty: 95, size: { h: 22.85, w: 30.5, uom: "cm" }, status: "A" }
] );
```

The following example uses the `db.collection.updateOne()` method on the `inventory` collection to update the first document where `item` equals "paper":
```javascript
db.inventory.updateOne(
   { item: "paper" },
   {
     $set: { "size.uom": "cm", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```

The following example uses the `db.collection.updateMany()` method on the `inventory` collection to update all documents where `qty` is less than 50:
```javascript
db.inventory.updateMany(
   { "qty": { $lt: 50 } },
   {
     $set: { "size.uom": "in", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```
The following example replaces the first document from the `inventory` collection where `item: "paper"`:
```javascript
db.inventory.replaceOne(
   { item: "paper" },
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 40 } ] }
)
```
### References
- https://docs.mongodb.com/manual/reference/update-methods/
- https://docs.mongodb.com/manual/tutorial/update-documents/

### Important update operators

- `$set` -> https://docs.mongodb.com/manual/reference/operator/update/set/
- `$unset` -> https://docs.mongodb.com/manual/reference/operator/update/unset/
- `$inc` -> https://docs.mongodb.com/manual/reference/operator/update/inc/

### Important Array update operators

- `$` -> https://docs.mongodb.com/manual/reference/operator/update/positional/
- `$[]` -> https://docs.mongodb.com/manual/reference/operator/update/positional-all/
- `$addToSet` -> https://docs.mongodb.com/manual/reference/operator/update/addToSet/
- `$push` -> https://docs.mongodb.com/manual/reference/operator/update/push/
- `$each` -> https://docs.mongodb.com/manual/reference/operator/update/each/



