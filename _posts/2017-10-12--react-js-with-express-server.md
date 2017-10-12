---
published: true
---

$ cd [app-project-directory]

$ npm install --save express

$ vi procfile

```	javascript
web: node index.js
```

$ vi index.js 

```javascript
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))

app.use(express.static(__dirname + '/build'))

app.get('*', function(request, response) {
	response.sendFile(__dirname + '/build/index.html')	
})

app.listen(app.get('port'), function() {
	console.log("Express server started on port", app.get('port'))
})

```

$ node index.js

**Note: c9.io doesn't support http (only https), so can't use "$ npm run build" for production build** 
