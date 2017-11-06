---
published: true
tags:
  - react-js
  - react-native
  - web
  - js
---

* Describe in the sequence of bash command

```sh
$ cd [app-project-directory]
$ npm install --save express
$ vi procfile
```

* Edit procfile

```
// in procfile
web: node index.js
```

```sh
$ vi index.js 
```

* Edit index.js

```javascript
// in index.js
var express = require('express')
var app = express()

// set your server port number to 3000 as below
app.set('port', (process.env.PORT || 3000))

// this make /build as the default source directory
app.use(express.static(__dirname + '/build'))

// this make /build/index.html as the default portal
app.get('*', function(request, response) {
	response.sendFile(__dirname + '/build/index.html')	
})

app.listen(app.get('port'), function() {
	console.log("Express server started on port", app.get('port'))
})
```

```bash
$ node index.js
```

**Note: c9.io doesn't support http (only https), so can't use "$ npm run build" for production build**


## What's Next?
**[Read the article: "Create Git Repository With Heroku Cloud Service" to backup your work online](https://mania7539.github.io/articles/create-git-repository-with-heroku-cloud-service.html)**
