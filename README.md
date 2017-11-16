# ernest
### Web framework for HTTP and HTTPS, using ExpressJS, Session, Mongo, Socket IO, Redis 

Just create a public folder inside your project directory, put your files inside and do this:
```js
var Ernest = require('ernest');
new Ernest(null,__dirname + "/public").listen();    
```
And your server is running on PORT:80 (http), loading your "public" folder.

If you are trying something bigger:
```js
var Ernest = require('ernest');
var srv = new Ernest(db_name,ipublic,iport,jsonlimt_mb,session_name,session_secret).listen(otherorigins,key,cert,socketio_redis_port, isocketio_redis_server).ServerData();

var app = srv.app;
var dbc = srv.dbc;
var msg = srv.messenger_io;

app.get("/hiernest",function(req,res,next)
{
	res.send("Ernest is Online");
});

app.get("/allcollectionelements",function(req,res,next)
{
	if(dbc != null)
	{
		dbc.FindInCollection({},"mongo_db_collection",function(docs)
		{
			res.json(docs);
		});
	}
	else
	{
		res.send("No DB connection");
	}
});

svr.console(function(command,att,content)
{	
	callback(command,att,content);
});
```

### Ernest
Creates a new instance of Ernest

#### db_name
Your mongo DB name(using mongojs name sintax).
By default no database.

#### ipublic
Your public folder. 
By default the public folder inside ernest node_module
On "/" request = index.html

#### iport
The TCP Port you want the server to run(HTTP)
By default 80.

#### jsonlimt_mb
The max size of json body-parser urlencode
By default 90Mb

#### session_name
This is the name parameter for session (string)
By default the current date (string)

#### session_secret
this is the secret parameter for session (string)
By default the current date (string) 

### listen
this function starts the service


#### allowothersite
If is set(as true) will allow cross site request
by default disabled

#### key

The path to the file ".pem" (key.pem) of ssl certificate. If is set, enables https.
By default is undefined and disable https.

#### cert
The path to the file ".crt" (server.crt) of ssl certificate. If kep aparameter is set, ermest looks for it and enables https.
By default is undefined and disable https.

#### socketio_redis_port
If is set, enables socket_io with redis for asincronic real time communication.
this parameter is the port where redis server is running.
Dont forget, for using this option you have to start your Redis Server and put these scripts on your header html files:
```js
<script src="/socket.io/socket.io.js"></script>
<script > var socket = io(); socket.on('disconnect', function () { alert('Server unreachable');});
```
By default is undefined and disable the socket_io system.

#### isocketio_redis_server
If socketio_redis_port is set, this parameter is the redis server ip. By default, is set as "localhost"

### ServerData
Return and object with two properties:

#### app
The express instance in which is running the server. You can use all the express methods (post,get, use, etc)

### messenger_io
Contains the function for emit messages through socket.io.
For emiting a new message you can use:
```js
var msg = srv.messenger_io;

//async
	...
	...
	msg.call(this,type_msg,content);
```
this: "this" golbal object current scope. (this serves as an identity function, providing our neighborhoods a way of referring to themselves.).
type_msg: String. Word the socket.io on client side will be waiting for emition
content: String.String that receives socket.io on client site when type_msg is emitted 

### console
This is an interface for implementing a user command prompt system. 
After the ernest service is running, it reads everything that is written on node prompt, and if it begins with "e.", is considered a command:
By example, if you write in the node prompt this line:
```js
e.msg admin hello world!
```
and having these function on your main script
```js
srv.console(function(cmd, att, content)
{
	if( cmd == "msg")
	{
		var type_msg = att;
		msg.call(this,type_msg,content);
	}
	else
	{
		console.log("Invalid Ernest command");
	}
});
```
Ernest will red "msg" as command, "admin" as attribute and "hello world!" as content
and will emit a message through socket.io using msg.call(this,type,message);



#### dbc 
The mongo database controller ErnestDB which hace the following methods:

```js

dbc.InsertInCollection (data,collec,function()
{
	res.json({});
})

//inserted by user;
dbc.InsertInCollectionBy (data,collec,insertedBy,function()
{
	res.json({});
});

//find one element by crit in collec
dbc.FindOneInCollection (crit,collec,function(data)
{
	res.json(data);
});	

//find all elements by crit in collec
dbc.FindInCollection (crit,collec,function(data_array)
{
	res.json(data_array);
});				

//find all and return one particular array element in selected documents.
dbc.FindProyectInCollection	(crit,proj,collec,function(data_array)
{
	res.json(data_array);
});						

//find one and return only the selected properties
dbc.FindOneInCollMostrar 	(crit,mostrar,collec,function(data)
{
	res.json(data);
});						

//find all and return only the selected properties
dbc.FindInCollecMostrar	(crit,mostrar,collec,function(data_array)
{
	res.json(data_array);
});						

//update one document that matches crit in the collection collec
dbc.UpdateOneinCollec (crit,set,collec,function()
{
	res.json({});
});				 			

//update one document that matches crit in the collection collec. Save the user in changedBy	
dbc.UpdateOneinCollecBy (crit,set,collec,changedBy,function()
{
	res.json({});
});				

//update many documents that match crit in the collection collec. 
dbc.UpdateManyinCollec (crit,set,collec,function()
{
	res.json({});
});				 			

//delete the documents that match the crit in the collection collec	
dbc.DeleteFromCollection (crit,collec,function()
{
	res.json({});
});				 			

//Find all documents that match the criteria crit, sorts the array of documents and limits the array
dbc.FindSortLimInCollect (crit,order,lim,collec,function(data_array)
{
	res.json(data_array);
});				 	

//Find all documents that match the criteria crit, sorts the array of documents and limits the array
	
dbc.FindSortInCollection (crit,order,collec,function(data_array)
{
	res.json(data_array);
});				 		

//Executes an aggregation on collect
dbc.AggregatetoArray (agg_arry,collec,function(data_array)
{
	res.json(data_arry);
});				 			

//Return all documents distincs on query that match the crit
dbc.GetDistincts (crit,query,collec,function(data_array)
{
	res.json(data_array);
});				 				

//Return all collection names
dbc.getCollectionNames (function(data_array)
{
	res.json(data_array);
});											

//Return the collection mongojs obj
dbc.GetCollection (collec)								

//Renames the collection
dbc.RenameCollection (oldcollec,newcollec,function()
{
	res.json({});
});						

//Creates the collection collec
dbc.CreateCollection (collec,function()
{
	res.json({});
});									

//Drops the collections collec
dbc.DropCollection (collec,function()
{
	res.json({});
});									
	
//Empty the collection collec
dbc.EmptyCollection	(collec,function()
{
	res.json({});
});									

//Erase the collections in Erase Arry
dbc.EraseCollections (erase,function()
{
	res.json({});
});				 					

//Creates a clone of the collection src, with the name dst
dbc.CloneCollection	(src,dst,function()
{
	res.json({});
});									
```

## README in edition
