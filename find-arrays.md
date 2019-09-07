### Querying Arrays

```javascript
use exampledb
db.inventory.insertMany([
   { item: "journal", qty: 25, tags: ["blank", "red"], dim_cm: [ 14, 21 ] },
   { item: "notebook", qty: 50, tags: ["red", "blank"], dim_cm: [ 14, 21 ] },
   { item: "paper", qty: 100, tags: ["red", "blank", "plain"], dim_cm: [ 14, 21 ] },
   { item: "planner", qty: 75, tags: ["blank", "red"], dim_cm: [ 22.85, 30 ] },
   { item: "postcard", qty: 45, tags: ["blue"], dim_cm: [ 10, 15.25 ] }
]);
```

The following example queries for all documents where the field tags value is an array with exactly two elements, `"red"` and `"blank"`, in the specified order:
```javascript
db.inventory.find( { tags: ["red", "blank"] } )
```
To find an array that contains both the elements `"red"` and `"blank"`, without 
regard to order or other elements in the array, use the `$all` operator:
```javascript
db.inventory.find( { tags: { $all: ["red", "blank"] } } )
```
The following example queries for all documents where tags is an array that 
contains the string `"red"` as one of its elements:
```javascript
db.inventory.find( { tags: "red" } )
```
The following operation queries for all documents where 
the array `dim_cm` contains at least one element whose value is greater than 25.
```javascript
db.inventory.find( { dim_cm: { $gt: 25 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b5"), "item" : "planner", "qty" : 75, "tags" : [ "blank", "red" ], "dim_cm" : [ 22.85, 30 ] }
```
The following example queries for documents where the `dim_cm` array 
contains elements that in some combination satisfy the query conditions; 
e.g., one element can satisfy the greater than 15 condition and 
another element can satisfy the less than 20 condition, or a single element can satisfy both:
```javascript
db.inventory.find( { dim_cm: { $gt: 15, $lt: 20 } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b2"), "item" : "journal", "qty" : 25, "tags" : [ "blank", "red" ], "dim_cm" : [ 14, 21 ] }
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b3"), "item" : "notebook", "qty" : 50, "tags" : [ "red", "blank" ], "dim_cm" : [ 14, 21 ] }
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b4"), "item" : "paper", "qty" : 100, "tags" : [ "red", "blank", "plain" ], "dim_cm" : [ 14, 21 ] }
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b6"), "item" : "postcard", "qty" : 45, "tags" : [ "blue" ], "dim_cm" : [ 10, 15.25 ] }
```
The following example queries for documents where the `dim_cm` array contains at least 
one element that is both greater than (`$gt`) 22 and less than (`$lt`) 30:
```javascript
db.inventory.find( { dim_cm: { $elemMatch: { $gt: 22, $lt: 30 } } } )
```
**Output:**
```javascript
{ "_id" : ObjectId("5d6e825fad9e2cf2984e37b5"), "item" : "planner", "qty" : 75, "tags" : [ "blank", "red" ], "dim_cm" : [ 22.85, 30 ] }
```
The following example queries for all documents where the second element in the array `dim_cm` is greater than 25:
```javascript
db.inventory.find( { "dim_cm.1": { $gt: 25 } } )
```
Use the `$size` operator to query for arrays by number of elements. 
For example, the following selects documents where the array tags has 3 elements.
```javascript
db.inventory.find( { "tags": { $size: 3 } } )
```
### References
- https://docs.mongodb.com/manual/tutorial/query-arrays/
