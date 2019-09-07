### `$` Projection Operator


Both the `$` operator and the `$elemMatch` operator project the first matching element from an array based on a condition
```javascript
db.students.insertMany( [
  { "_id" : 1, "semester" : 1, "grades" : [ 70, 87, 90 ] },
  { "_id" : 2, "semester" : 1, "grades" : [ 90, 88, 92 ] },
  { "_id" : 3, "semester" : 1, "grades" : [ 85, 100, 90 ] },
  { "_id" : 4, "semester" : 2, "grades" : [ 79, 85, 80 ] },
  { "_id" : 5, "semester" : 2, "grades" : [ 88, 88, 92 ] },
  { "_id" : 6, "semester" : 2, "grades" : [ 95, 90, 96 ] }
]);
```
In the following query, the projection `{ "grades.$": 1 } ` returns only the first element greater than or equal to 85 for the `grades` field.
```javascript
db.students.find( { semester: 1, grades: { $gte: 85 } }, { "grades.$": 1 } )
```
**Output:**
```javascript
{ "_id" : 1, "grades" : [ 87 ] }
{ "_id" : 2, "grades" : [ 90 ] }
{ "_id" : 3, "grades" : [ 85 ] }
```
```javascript
db.students.insertMany( [
{ "_id" : 7, semester: 3, "grades" : [ { grade: 80, mean: 75, std: 8 },
                                       { grade: 85, mean: 90, std: 5 },
                                       { grade: 90, mean: 85, std: 3 } ] },
{ "_id" : 8, semester: 3, "grades" : [ { grade: 92, mean: 88, std: 8 },
                                       { grade: 78, mean: 90, std: 5 },
                                       { grade: 88, mean: 85, std: 3 } ] }
])
```
In the following query, the projection `{ "grades.$": 1 }` returns only 
the first element with the mean greater than 70 for the `grades` field:
```javascript
db.students.find(
   { "grades.mean": { $gt: 70 } },
   { "grades.$": 1 }
)
```
**Output:**
```javascript
{ "_id" : 7, "grades" : [  {  "grade" : 80,  "mean" : 75,  "std" : 8 } ] }
{ "_id" : 8, "grades" : [  {  "grade" : 92,  "mean" : 88,  "std" : 8 } ] }
```
The following query returns the first document inside a `grades` array 
that has a `mean` of greater than 70 and a `grade` of greater than 90.
```javascript
db.students.find( { grades: { $elemMatch: {
                                            mean: { $gt: 70 },
                                            grade: { $gt:90 }
                                          } } },
                  { "grades.$": 1 } )
```
**Output:**
```javascript
{ "_id" : 8, "grades" : [ { "grade" : 92, "mean" : 88, "std" : 8 } ] }
```

### `$elemMatch` Projection Operator

```javascript
db.schools.insertMany([
  {
  _id: 1,
  zipcode: "63109",
  students: [
                { name: "john", school: 102, age: 10 },
                { name: "jess", school: 102, age: 11 },
                { name: "jeff", school: 108, age: 15 }
            ]
  },
  {
  _id: 2,
  zipcode: "63110",
  students: [
                { name: "ajax", school: 100, age: 7 },
                { name: "achilles", school: 100, age: 8 },
            ]
  },
  {
  _id: 3,
  zipcode: "63109",
  students: [
                { name: "ajax", school: 100, age: 7 },
                { name: "achilles", school: 100, age: 8 },
            ]
  },
  {
  _id: 4,
  zipcode: "63109",
  students: [
                { name: "barney", school: 102, age: 7 },
                { name: "ruth", school: 102, age: 16 },
            ]
  }
])
```
The following `find()` operation queries for all documents where the value of the `zipcode` field is 63109. 
The `$elemMatch` projection returns only the first matching element of the students array where the `school` field has a value of 102:
```javascript
db.schools.find( { zipcode: "63109" },
                 { students: { $elemMatch: { school: 102 } } } )
```
**Output:**
```javascript
{ "_id" : 1, "students" : [ { "name" : "john", "school" : 102, "age" : 10 } ] }
{ "_id" : 3 }
{ "_id" : 4, "students" : [ { "name" : "barney", "school" : 102, "age" : 7 } ] }
```
The following `find()` operation queries for all documents where the value of the `zipcode` field is 63109. 
The projection includes the first matching element of the `students` array where the `school` field has a value of 102 and the `age` field is greater than 10:
```javascript
db.schools.find( { zipcode: "63109" },
                 { students: { $elemMatch: { school: 102, age: { $gt: 10} } } } )
```
**Output:**
```javascript
{ "_id" : 1, "students" : [ { "name" : "jess", "school" : 102, "age" : 11 } ] }
{ "_id" : 3 }
{ "_id" : 4, "students" : [ { "name" : "ruth", "school" : 102, "age" : 16 } ] }
```

### `$slice` projection operator


Here, `$slice` selects the first five items in an array in the comments field.
```javascript
db.posts.find( {}, { comments: { $slice: 5 } } )
```
The following operation returns the last five items in array.
```javascript
db.posts.find( {}, { comments: { $slice: -5 } } )
```

Here, the query will only return 10 items, after skipping the first 20 items of that array.
```javascript
db.posts.find( {}, { comments: { $slice: [ 20, 10 ] } } )
```
This operation returns 10 items as well, beginning with the item that is 20th from the last item of the array.
```javascript
db.posts.find( {}, { comments: { $slice: [ -20, 10 ] } } )
```
### References
- https://docs.mongodb.com/manual/reference/operator/projection/slice/
- https://docs.mongodb.com/manual/reference/operator/projection/elemMatch/
- https://docs.mongodb.com/manual/reference/operator/projection/positional/#proj._S_