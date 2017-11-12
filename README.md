# ernest
### Web framework, using expressjs and mongojs

Just create a public folder inside your project directory, put your files inside and do this:
```js
var Ernest = require('ernest');
new Ernest(null,__dirname + "/public").listen();    
```
And your server is running on PORT:80 (http), loading your "public" folder.

If you are trying something bigger:
```js
var Ernest = require('ernest');
var srv = new Ernest(db_name,ipublic,iport,jsonlimt_mb,session_name,session_secret).listen(allowothersite).ServerData();
var app = srv.app;
var dbc = srv.dbc;

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

### ServerData
Return and object with two properties:

#### app
The express instance in which is running the server. You can use all the express methods (post,get, use, etc)

#### dbc 
The mongo database controller ErnestDB which hace the following methods:
```js
InsertInCollection (data,collec,callback) 				

InsertInCollectionBy (data,collec,insertedBy,callback) 	

FindOneInCollection	(data,collec,callback)				

FindInCollection (data,collec,callback)					
	
FindProyectInCollection	(data,proy,collec,callback)		

FindOneInCollMostrar (data,mostrar,collec,callback)		

FindInCollecMostrar	(data,mostrar,collec,callback)		

UpdateOneinCollec (crit,set,collec,callback) 			
	
UpdateOneinCollecBy (crit,set,collec,changedBy,callback)
	
UpdateManyinCollec (crit,set,collec,callback) 			
	
DeleteFromCollection (crit,collec,callback) 			

FindSortLimInCollect (crit,order,lim,collec,callback) 	
	
FindSortInCollection (crit,order,collec,callback) 		

AggregatetoArray (agg_arry,collec,callback) 			

GetDistincts (crit,query,collec,callback) 				

getCollectionNames (callback)							

GetCollection (collec)								

RenameCollection (oldcollec,newcollec,callback)		

CreateCollection (collec,callback)					

DropCollection (collec,callback)					
	
EmptyCollection	(collec,callback)					

EraseCollections (erase,callback) 					

CloneCollection	(src,dst,callback)					
```













