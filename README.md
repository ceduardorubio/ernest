# ernest
### Web framework, using expressjs and mongojs

Just create a public folder inside your project directory, put your files inside and do this:
```js
var Ernest = require('ernest');
new Ernest(null,__dirname + "/public").listen();    
```
And your server is running on PORT:80 (http), loading your "public" folder.
