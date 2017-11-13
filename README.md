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
