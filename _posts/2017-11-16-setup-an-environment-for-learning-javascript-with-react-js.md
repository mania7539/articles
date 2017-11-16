---
published: true
tags:
  - javascript
  - react-js
---
* in Cmder (for Windows) or your bash console

```bat
$ create-react-app [any-name: learning-app]
$ cd learning-app
$ npm start
```

* Prepare your browser
* Open a IDE or a text editor
* In the path src/App.js

```javascript
class App extends Component {
	
	learn(field, event) {
		// if you don't pass value to field, it will be 'undefined',
		// but if you don't pass value to 'event', it will still be there
		// type your test code here:
		
	}

	render() {
		return (
		  <div className="fluid-container">
			<input onChange={this.learn.bind(this, "name")} className="form-control" type="text" placeholder="Name" /><br />
		  </div>
		);
	}
}
```


* **Add code snippet** to the **test code position** as above shown, **press *F5* each time you update your code**, then you can **validate your result with your browser**.

<br />
<br />
