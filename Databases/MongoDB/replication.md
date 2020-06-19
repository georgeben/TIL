### Creating a MongoDB replica set locally
A MongoDB replica set is a bunch of MongoDB servers that store the same data. Instead of having just one MongoDB server that stores all your application's data, a replica set it involves setting up additional MongoDB servers, so 
that the data from one database server (referred to as the primary server) is copied to the other database servers (referred to as secondary servers). 

The major benefit of creating replica sets in MongoDB is to increase data availability. What this means is, if one of your MongoDB servers goes down, your application can still continue functioning correctly by using the data stored in the other MongoDB servers.  

To set up a mongodb replica set **locally (do not use this instructions in production)**, follow the following steps.
- Create directories where the data from the MongoDB servers in the replica set will be stored. For this example, our replica set will contain three(3) MongoDB servers You can run
```bat
mkdir -p my-replica-set/server1 my-replica-set/server2 my-replica-set/server3
```
This created three folders `server1, server2 and server2` to store data from the three MongoDB servers.

- Set up the MongoDB servers for your replica set.  
Run the commands:
```bat
mongod --replSet rs0 --port 27017 --dbpath my-replica-set/server1 --oplogSize 128
```
This command starts a mongod process (a database server). The `--replSet` specifies that this server belongs to a replicaset called rs0.  
`--dbpath` sets the path where the database server will store its data (we already created this directory in the previous step).  
`--port` sets the port the database server will listen on.  
`--oplogSize` specifies the maximum size for the oplog file. The oplog file stores an ordered history of logical writes to a MongoDB database. The oplog file is what makes replication possible.  

Run these commands to set up the remaining database servers.
```bat
mongod --replSet rs0 --port 27018 --dbpath my-replica-set/server2 --oplogSize 128 
mongod --replSet rs0 --port 27019 --dbpath my-replica-set/server3 --oplogSize 128
```
Make sure you specify the different ports and dbPath

- Initiate the replica set
Now you should have three database servers running. You can connect to anyone of these servers by executing the `mongo` command and specifying the connection port, Example
```bat
mongo --port 27017
```
to connect to the database server running on port 27017.
Before you can initiate a replica set, you must create a configuration for that replica set. Copy this sample replica set configuration and paste it in your mongo shell.
```js
rsconf = {
  _id: "rs0",
  protocolVersion: 1,
  members: [
    {
     _id: 0,
     host: "localhost:27017"
    },
    {
     _id: 1,
     host: "localhost:27018"
    },
    {
     _id: 2,
     host: "localhost:27019"
    }
   ]
}
```
This creates a variable `rsconf` to store the replica set configuration. Initiate the replica set by entering:
```bat
rs.initiate(rsconf)
```
The rs.initiate() function takes a configuration as an argument.

- Check the status of your replica set
To check the status of your replica set, Run
```bat
rs.status()
```

- Connect to your replica set from your app.  
To connect to your replica set from your application. Use the following format for your connection string:
`mongodb://localhost:27017,localhost:27018,localhost:27019/?replicaSet=rs0`

Type `rs.help()` for more useful commands. 

Now you have a MongoDB replica set, if one database server fails or is unavailable, your application would still function as it use the data stored in the other db servers in your replica set.


Useful links
- https://docs.mongodb.com/manual/replication/
- https://www.npmjs.com/package/run-rs

