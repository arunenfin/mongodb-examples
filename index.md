
### Installing MongoDB
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

To start mongod service

    sudo systemctl start mongod

To enable mongod service / start mongodb when system starts

    sudo systemctl enable mongod

#### Enable authentication on MongoDB
Please follow instructions at https://docs.mongodb.com/manual/tutorial/enable-authentication/

To enable authentication add the following in the security section of `/etc/mongod.conf`
```
security:
  authorization: enabled
```
and restart mongod service (`sudo systemctl restart mongod`)
### MongoDB Examples
https://github.com/arunenfin/mongodb-examples
#### Shell Reference
[https://docs.mongodb.com/manual/reference/mongo-shell/](https://docs.mongodb.com/manual/reference/mongo-shell/)
#### CRUD Operations
https://docs.mongodb.com/manual/crud/

https://docs.mongodb.com/manual/reference/method/db.collection.count/
https://docs.mongodb.com/manual/reference/method/db.collection.countDocuments/

#### Sort
https://docs.mongodb.com/manual/reference/method/cursor.sort/#examples

#### Limit
https://docs.mongodb.com/manual/reference/method/cursor.limit/

#### Skip
https://docs.mongodb.com/manual/reference/method/cursor.skip/

#### Aggregates
https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#examples

#### LookUp aggregation
https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#examples
#### Query Operators
https://docs.mongodb.com/manual/reference/operator/query/




### MongoDB data modelling
https://docs.mongodb.com/manual/applications/data-models/

### MongoDB Indexing
https://docs.mongodb.com/manual/applications/indexes/

### Example Node.js Application
https://github.com/arunenfin/reactjs/tree/master/sample-server
### Node.js MongoDB package
[mongoose](https://mongoosejs.com/)
### Exporting and importing - mongodump, mongorestore
- [mongodump](https://docs.mongodb.com/manual/reference/program/mongodump/#examples)
- [mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/#examples)
### Other Topics
- [MongoDB Compass](https://www.mongodb.com/download-center/compass)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- [Sharding](https://docs.mongodb.com/manual/sharding/)
- [Replication](https://docs.mongodb.com/manual/replication/)
