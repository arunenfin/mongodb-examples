
### Mongodb shell commands
| Command | Description |
|--|--|
| `mongo` | Open the mongodb shell. |
| `show dbs` | Print a list of all databases on the server. |
| `use <db>` | Switch current database to <db> or create a new database. The mongo shell variable db is set to the current database.  |
| `show collections` | Print a list of all collections for current database |
| `load("scripts.js")` | Run commands in scripts.js |
               
To connect to a remote server
`mongo --host mongodb0.example.com --port 27017 -u <username> -p`

### Delete a database
To delete database called sampledb
```
use sampledb
db.dropDatabse() 
```
### Dump and Restore

To dump or restore a database exit the mongo shell interface and run the following from the terminal.

To dump a db called test in the current directory

`mongodump --db test`

To restore a db called test from the folder dump/ in the current directory

`mongorestore --db test dump/`


### References:

 - https://docs.mongodb.com/manual/reference/mongo-shell/
 - https://docs.mongodb.com/manual/tutorial/write-scripts-for-the-mongo-shell/
 - https://docs.mongodb.com/manual/reference/program/mongodump/#examples