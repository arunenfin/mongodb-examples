### Querying Object Arrays

```javascript
use exampledb

db.inventory.insertMany( [
   { item: "journal", instock: [ { warehouse: "A", qty: 5 }, { warehouse: "C", qty: 15 } ] },
   { item: "notebook", instock: [ { warehouse: "C", qty: 5 } ] },
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 15 } ] },
   { item: "planner", instock: [ { warehouse: "A", qty: 40 }, { warehouse: "B", qty: 5 } ] },
   { item: "postcard", instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }
]);
```

The following example selects all documents where an element in the `instock` array matches the specified document:
```javascript
db.inventory.find( { "instock": { warehouse: "A", qty: 5 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
```
The following example selects all documents where the `instock` array has at least one embedded document that contains the field `qty` whose value is less than or equal to 20:
```javascript
db.inventory.find( { 'instock.qty': { $lte: 20 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16a"), "item" : "notebook", "instock" : [ { "warehouse" : "C", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16b"), "item" : "paper", "instock" : [ { "warehouse" : "A", "qty" : 60 }, { "warehouse" : "B", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16c"), "item" : "planner", "instock" : [ { "warehouse" : "A", "qty" : 40 }, { "warehouse" : "B", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16d"), "item" : "postcard", "instock" : [ { "warehouse" : "B", "qty" : 15 }, { "warehouse" : "C", "qty" : 35 } ] }
```
The following example selects all documents where the `instock` array has as its first element a document that contains the field `qty` whose value is less than or equal to 20:
```javascript
db.inventory.find( { 'instock.0.qty': { $lte: 20 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16a"), "item" : "notebook", "instock" : [ { "warehouse" : "C", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16d"), "item" : "postcard", "instock" : [ { "warehouse" : "B", "qty" : 15 }, { "warehouse" : "C", "qty" : 35 } ] }
```
The following example queries for documents where the `instock` array has at least one embedded document that contains both the field `qty` equal to 5 and the field `warehouse` equal to A:
```javascript
db.inventory.find( { "instock": { $elemMatch: { qty: 5, warehouse: "A" } } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
```
The following example queries for documents where the `instock` array has at least one embedded document that contains the field `qty` that is greater than 10 and less than or equal to 20:
```javascript
db.inventory.find( { "instock": { $elemMatch: { qty: { $gt: 10, $lte: 20 } } } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16b"), "item" : "paper", "instock" : [ { "warehouse" : "A", "qty" : 60 }, { "warehouse" : "B", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16d"), "item" : "postcard", "instock" : [ { "warehouse" : "B", "qty" : 15 }, { "warehouse" : "C", "qty" : 35 } ] }
```
The following query matches documents where any document nested in the `instock` array has the `qty` field greater than 10 and any document (but not necessarily the same embedded document) in the array has the `qty` field less than or equal to 20:
```javascript
db.inventory.find( { "instock.qty": { $gt: 10,  $lte: 20 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16b"), "item" : "paper", "instock" : [ { "warehouse" : "A", "qty" : 60 }, { "warehouse" : "B", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16c"), "item" : "planner", "instock" : [ { "warehouse" : "A", "qty" : 40 }, { "warehouse" : "B", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16d"), "item" : "postcard", "instock" : [ { "warehouse" : "B", "qty" : 15 }, { "warehouse" : "C", "qty" : 35 } ] }
```
The following example queries for documents where the `instock` array has at least one embedded document that contains the field `qty` equal to 5 and at least one embedded document (but not necessarily the same embedded document) that contains the field warehouse equal to A:
```javascript
db.inventory.find( { "instock.qty": 5, "instock.warehouse": "A" } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f169"), "item" : "journal", "instock" : [ { "warehouse" : "A", "qty" : 5 }, { "warehouse" : "C", "qty" : 15 } ] }
{ "_id" : ObjectId("5d6e8c2b3ef553d9bd79f16c"), "item" : "planner", "instock" : [ { "warehouse" : "A", "qty" : 40 }, { "warehouse" : "B", "qty" : 5 } ] }
```
### References
- https://docs.mongodb.com/manual/tutorial/query-array-of-documents/