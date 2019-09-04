### Posts Collection
```javascript
db.posts.insertMany([
  {
    "_id": 1,
    "user_id": 313,
    "title": "Ad voluptas perferendis officia ad quas. Consequatur aut molestiae dolor.",
    "body": "Non quidem aut quo et sed omnis. Odio ea illum quam ad officiis et. Velit sit et non tempora quod rerum quis.\n\nDucimus facilis minus assumenda adipisci occaecati ratione. Voluptatum dolores est autem itaque. Qui velit quia aut deserunt et nostrum.\n\nIpsam nostrum dolorem expedita labore quibusdam corrupti repudiandae. Veniam asperiores adipisci expedita est. Ad qui rem ipsam.",
  },
  {
    "_id": 2,
    "user_id": 1637,
    "title": "Labore aut consequatur praesentium iste ex quo. Rerum totam officia aut odio.",
    "body": "Dolore porro nihil voluptas ullam. Dolorem maxime quasi quis quo tempora alias facere. Ab et cumque delectus. Iste inventore sapiente quod culpa. Illo corrupti distinctio officia recusandae est assumenda ut.\n\nEveniet corporis unde est praesentium. Porro velit magni distinctio sunt at eum et. Fuga est debitis repudiandae pariatur soluta quam voluptates. Numquam eum quia id velit ipsum aut ut.",
  },
  {
    "_id": 3,
    "user_id": 1068,
    "title": "Sapiente ut illo consequatur vero sed officia officia velit. Odio ipsam est aliquam autem fugiat.",
    "body": "Assumenda consectetur molestiae ut nam. Voluptas quis qui similique voluptatem quis occaecati. Quisquam recusandae sunt est.\n\nQuia commodi ad laudantium cupiditate aut quasi nobis et. Enim dignissimos cum eum quis iusto rerum. Mollitia temporibus non natus et a eos. Nulla cumque velit sunt assumenda.",
  }
])
```
### Users collection
```javascript
db.users.insertMany([
  {
    "_id": 313,
    "first_name": "Verdie",
    "last_name": "Feeney",
    "gender": "female",
    "dob": "1921-12-12",
    "email": "georgianna98@example.net",
    "phone": "(916) 558-9424",
    "website": "http://batz.com/dolor-unde-perferendis-amet-repellat.html",
    "address": "2326 Kihn Street\nEast Ulises, TX 45030",
    "status": "active"
  },
  {
    "_id": 1068,
    "first_name": "Darrin",
    "last_name": "Yundt",
    "gender": "male",
    "dob": "2002-03-17",
    "email": "casper.karlee@example.net",
    "phone": "+1-413-218-0816",
    "website": "http://www.pfeffer.com/aperiam-odio-non-ut-soluta-libero-possimus",
    "address": "630 Oswaldo Crossing\nEast Sydneytown, CO 94925-4912",
    "status": "active",
  },
  {
    "_id": 56,
    "first_name": "Betty",
    "last_name": "Schimmel",
    "gender": "female",
    "dob": "2001-09-25",
    "email": "leuschke.zola@example.com",
    "phone": "+1-594-390-6682",
    "website": "https://franecki.com/et-impedit-atque-corporis-aspernatur-ab-veritatis-perspiciatis-eum.html",
    "address": "133 VonRueden Curve\nSouth Filomenashire, ME 38453-9113",
    "status": "inactive",
  }
])
```
### Comments Collection
```javascript
db.comments.insertMany([
  {
    "_id": 930,
    "post_id": 3,
    "name": "Imani Kling",
    "email": "rhoda10@corkery.com",
    "body": "Repellendus voluptate numquam aspernatur reprehenderit et incidunt quod. Omnis et saepe commodi sint. Aspernatur neque et esse.\n\nVoluptates earum earum rerum vel est quod. Eveniet iusto iste ut voluptatem et debitis. Enim quam nihil nulla cum iure culpa neque.",
  },
  {
    "_id": 1,
    "post_id": 3,
    "name": "Eduardo Greenholt MD",
    "email": "shyanne.ebert@ziemann.com",
    "body": "Sed eaque animi error temporibus corrupti sed. Illo et ullam ut praesentium ut qui. Labore enim quo voluptates illum omnis quis. Voluptatem quas nam quis ab.\n\nQuia maiores recusandae reiciendis sunt sit. Ea placeat consequatur quasi quia. Voluptate enim fugit vitae similique corrupti similique ut.\n\nDignissimos esse molestiae sit perferendis. Hic doloribus facilis asperiores dolores. Vel ab at consequatur tempora voluptas. Molestiae ducimus et rerum velit nulla dolor.",
  },
  {
    "_id": 2,
    "post_id": 2473,
    "name": "Dr. Jamison Rolfson DDS",
    "email": "zdickinson@doyle.com",
    "body": "Tempora ut debitis provident nesciunt laboriosam nobis itaque omnis. Delectus reiciendis veritatis aperiam quasi aliquid voluptas fugiat. Ad modi iusto velit molestiae molestias est labore. Laboriosam corrupti aspernatur quis eos.\n\nItaque et esse illum itaque reiciendis itaque magnam aut. Ducimus ad delectus doloremque distinctio adipisci ullam quo velit. Quam facilis doloremque facere. Quod delectus dolor vero.",
  }
])
```
### Query 1 - Join posts and users collections.
```javascript
db.posts.aggregate([
  {
    $lookup: {
      from: "users",       
      localField: "user_id",
      foreignField: "_id",
      as: "author"
    }
  },
  { $match:{ _id :  3 } }
])
```
**Output**
```json
{
  "_id": 3,
  "user_id": 1068,
  "title": "Sapiente ut illo consequatur vero sed officia officia velit. Odio ipsam est aliquam autem fugiat.",
  "body": "Assumenda consectetur molestiae ut nam. Voluptas quis qui similique voluptatem quis occaecati. Quisquam recusandae sunt est.\n\nQuia commodi ad laudantium cupiditate aut quasi nobis et. Enim dignissimos cum eum quis iusto rerum. Mollitia temporibus non natus et a eos. Nulla cumque velit sunt assumenda.",
  "author": [
    {
      "_id": 1068,
      "first_name": "Darrin",
      "last_name": "Yundt",
      "gender": "male",
      "dob": "2002-03-17",
      "email": "casper.karlee@example.net",
      "phone": "+1-413-218-0816",
      "website": "http://www.pfeffer.com/aperiam-odio-non-ut-soluta-libero-possimus",
      "address": "630 Oswaldo Crossing\nEast Sydneytown, CO 94925-4912",
      "status": "active"
    }
  ]
}
```
### Query 2 - unwind author
```javascript
db.posts.aggregate([
  {
    $lookup: {
      from: "users",       
      localField: "user_id",
      foreignField: "_id",
      as: "author"
    }
  },
  { $unwind:"$author" },
  { $match:{ _id :  3 } }
])
```
**output**
```json
{
  "_id": 3,
  "user_id": 1068,
  "title": "Sapiente ut illo consequatur vero sed officia officia velit. Odio ipsam est aliquam autem fugiat.",
  "body": "Assumenda consectetur molestiae ut nam. Voluptas quis qui similique voluptatem quis occaecati. Quisquam recusandae sunt est.\n\nQuia commodi ad laudantium cupiditate aut quasi nobis et. Enim dignissimos cum eum quis iusto rerum. Mollitia temporibus non natus et a eos. Nulla cumque velit sunt assumenda.",
  "author": {
    "_id": 1068,
    "first_name": "Darrin",
    "last_name": "Yundt",
    "gender": "male",
    "dob": "2002-03-17",
    "email": "casper.karlee@example.net",
    "phone": "+1-413-218-0816",
    "website": "http://www.pfeffer.com/aperiam-odio-non-ut-soluta-libero-possimus",
    "address": "630 Oswaldo Crossing\nEast Sydneytown, CO 94925-4912",
    "status": "active"
  }
}
```
### Query 3 - Join posts and comments collections.
```javascript
db.posts.aggregate([
  {
    $lookup: {
      from: "users",       
      localField: "user_id",
      foreignField: "_id",
      as: "author"
    }
  },
  { $unwind:"$author" },
  {
    $lookup: {
      from: "comments",       
      localField: "_id",
      foreignField: "post_id",
      as: "comments"
    }
  },
  { $match:{ _id : 3 } }
])
```
**output**
```json
{
  "_id": 3,
  "user_id": 1068,
  "title": "Sapiente ut illo consequatur vero sed officia officia velit. Odio ipsam est aliquam autem fugiat.",
  "body": "Assumenda consectetur molestiae ut nam. Voluptas quis qui similique voluptatem quis occaecati. Quisquam recusandae sunt est.\n\nQuia commodi ad laudantium cupiditate aut quasi nobis et. Enim dignissimos cum eum quis iusto rerum. Mollitia temporibus non natus et a eos. Nulla cumque velit sunt assumenda.",
  "author": {
    "_id": 1068,
    "first_name": "Darrin",
    "last_name": "Yundt",
    "gender": "male",
    "dob": "2002-03-17",
    "email": "casper.karlee@example.net",
    "phone": "+1-413-218-0816",
    "website": "http://www.pfeffer.com/aperiam-odio-non-ut-soluta-libero-possimus",
    "address": "630 Oswaldo Crossing\nEast Sydneytown, CO 94925-4912",
    "status": "active"
  },
  "comments": [
    {
      "_id": 930,
      "post_id": 3,
      "name": "Imani Kling",
      "email": "rhoda10@corkery.com",
      "body": "Repellendus voluptate numquam aspernatur reprehenderit et incidunt quod. Omnis et saepe commodi sint. Aspernatur neque et esse.\n\nVoluptates earum earum rerum vel est quod. Eveniet iusto iste ut voluptatem et debitis. Enim quam nihil nulla cum iure culpa neque."
    },
    {
      "_id": 1,
      "post_id": 3,
      "name": "Eduardo Greenholt MD",
      "email": "shyanne.ebert@ziemann.com",
      "body": "Sed eaque animi error temporibus corrupti sed. Illo et ullam ut praesentium ut qui. Labore enim quo voluptates illum omnis quis. Voluptatem quas nam quis ab.\n\nQuia maiores recusandae reiciendis sunt sit. Ea placeat consequatur quasi quia. Voluptate enim fugit vitae similique corrupti similique ut.\n\nDignissimos esse molestiae sit perferendis. Hic doloribus facilis asperiores dolores. Vel ab at consequatur tempora voluptas. Molestiae ducimus et rerum velit nulla dolor."
    }
  ]
}
```
### Query 4 - Project fields from users collection
```javascript
db.posts.aggregate([
  {
    $lookup: {
      from: "users",  
      let: { post_user_id: "$user_id" },
      pipeline: [ 
        { $match: 
          { $expr: 
            { $eq: ["$_id", "$$post_user_id"] } 
          } 
        },
        { $project: { first_name: 1, last_name: 1, email: 1, status: 1 } } 
      ],
      as: "author"
    }
  },
  { $unwind:"$author" },
  {
    $lookup: {
      from: "comments",       
      localField: "_id",
      foreignField: "post_id",
      as: "comments"
    }
  },
  { $match:{ _id : 3 } }
])
```
**output**
```json
{
  "_id": 3,
  "user_id": 1068,
  "title": "Sapiente ut illo consequatur vero sed officia officia velit. Odio ipsam est aliquam autem fugiat.",
  "body": "Assumenda consectetur molestiae ut nam. Voluptas quis qui similique voluptatem quis occaecati. Quisquam recusandae sunt est.\n\nQuia commodi ad laudantium cupiditate aut quasi nobis et. Enim dignissimos cum eum quis iusto rerum. Mollitia temporibus non natus et a eos. Nulla cumque velit sunt assumenda.",
  "author": {
    "_id": 1068,
    "first_name": "Darrin",
    "last_name": "Yundt",
    "email": "casper.karlee@example.net",
    "status": "active"
  },
  "comments": [
    {
      "_id": 930,
      "post_id": 3,
      "name": "Imani Kling",
      "email": "rhoda10@corkery.com",
      "body": "Repellendus voluptate numquam aspernatur reprehenderit et incidunt quod. Omnis et saepe commodi sint. Aspernatur neque et esse.\n\nVoluptates earum earum rerum vel est quod. Eveniet iusto iste ut voluptatem et debitis. Enim quam nihil nulla cum iure culpa neque."
    },
    {
      "_id": 1,
      "post_id": 3,
      "name": "Eduardo Greenholt MD",
      "email": "shyanne.ebert@ziemann.com",
      "body": "Sed eaque animi error temporibus corrupti sed. Illo et ullam ut praesentium ut qui. Labore enim quo voluptates illum omnis quis. Voluptatem quas nam quis ab.\n\nQuia maiores recusandae reiciendis sunt sit. Ea placeat consequatur quasi quia. Voluptate enim fugit vitae similique corrupti similique ut.\n\nDignissimos esse molestiae sit perferendis. Hic doloribus facilis asperiores dolores. Vel ab at consequatur tempora voluptas. Molestiae ducimus et rerum velit nulla dolor."
    }
  ]
}
```
### References

 - [https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/)
 - [https://docs.mongodb.com/manual/reference/operator/aggregation/match/](https://docs.mongodb.com/manual/reference/operator/aggregation/match/)
 - [https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/](https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/)
