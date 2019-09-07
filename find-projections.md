
### Project Fields to Return from Query

```javascript
db.inventory.insertMany( [
  { item: "journal", status: "A", size: { h: 14, w: 21, uom: "cm" }, instock: [ { warehouse: "A", qty: 5 } ] },
  { item: "notebook", status: "A",  size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "C", qty: 5 } ] },
  { item: "paper", status: "D", size: { h: 8.5, w: 11, uom: "in" }, instock: [ { warehouse: "A", qty: 60 } ] },
  { item: "planner", status: "D", size: { h: 22.85, w: 30, uom: "cm" }, instock: [ { warehouse: "A", qty: 40 } ] },
  { item: "postcard", status: "A", size: { h: 10, w: 15.25, uom: "cm" }, instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }
]);
```
Return only the `item`, `status` and, by default, the `_id` fields return in the matching documents.
```javascript
db.inventory.find( { status: "A" }, { item: 1, status: 1 } )
// SELECT _id, item, status from inventory WHERE status = "A"
```
Suppress `_id` Field
```javascript
db.inventory.find( { status: "A" }, { item: 1, status: 1, _id: 0 } )
// SELECT item, status from inventory WHERE status = "A"
```
The following example which returns all fields except for the 
`status` and the `instock` fields in the matching documents:
```javascript
db.inventory.find( { status: "A" }, { status: 0, instock: 0 } )
```

The following example returns:
The `_id` field (returned by default), The `item` field, The `status` field, The `uom` field in the size document
```javascript
db.inventory.find(
   { status: "A" },
   { item: 1, status: 1, "size.uom": 1 }
)
```
**Output:**
```json
{ "_id" : ObjectId("5d6e8e430c67e26428cb4323"), "item" : "journal", "status" : "A", "size" : { "uom" : "cm" } }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4324"), "item" : "notebook", "status" : "A", "size" : { "uom" : "in" } }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4327"), "item" : "postcard", "status" : "A", "size" : { "uom" : "cm" } }
```
The following example specifies a projection to exclude the `uom` field inside the `size` document. 
All other fields are returned in the matching documents:
```javascript
db.inventory.find(
   { status: "A" },
   { "size.uom": 0 }
)
```
**Output:**
```json
{ "_id" : ObjectId("5d6e8e430c67e26428cb4323"), "item" : "journal", "status" : "A", "size" : { "h" : 14, "w" : 21 }, "instock" : [ { "warehouse" : "A", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4324"), "item" : "notebook", "status" : "A", "size" : { "h" : 8.5, "w" : 11 }, "instock" : [ { "warehouse" : "C", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4327"), "item" : "postcard", "status" : "A", "size" : { "h" : 10, "w" : 15.25 }, "instock" : [ { "warehouse" : "B", "qty" : 15 }, { "warehouse" : "C", "qty" : 35 } ] }
```

The following example specifies a projection to return:

The `_id` field (returned by default), The `item` field, The `status` field, 
The `qty` field in the documents embedded in the `instock` array.
```javascript
db.inventory.find( { status: "A" }, { item: 1, status: 1, "instock.qty": 1 } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8e430c67e26428cb4323"), "item" : "journal", "status" : "A", "instock" : [ { "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4324"), "item" : "notebook", "status" : "A", "instock" : [ { "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4327"), "item" : "postcard", "status" : "A", "instock" : [ { "qty" : 15 }, { "qty" : 35 } ] }
```
For fields that contain arrays, MongoDB provides the following 
projection operators for manipulating arrays: `$elemMatch`, `$slice`, and `$`.

The following example uses the `$slice` projection operator to return the last element in the `instock` array:
```javascript
db.inventory.find( { status: "A" }, { item: 1, status: 1, instock: { $slice: -1 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e8e430c67e26428cb4323"), "item" : "journal", "status" : "A", "instock" : [ { "warehouse" : "A", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4324"), "item" : "notebook", "status" : "A", "instock" : [ { "warehouse" : "C", "qty" : 5 } ] }
{ "_id" : ObjectId("5d6e8e430c67e26428cb4327"), "item" : "postcard", "status" : "A", "instock" : [ { "warehouse" : "C", "qty" : 35 } ] }
```
### References
- https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/