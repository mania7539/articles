---
published: true
tags:
  - javascript
  - react-js
---
* in **Cmder (for Windows)** or your **Bash (for Linux)** console

```bat
$ create-react-app [any-name: learning-app]
$ cd learning-app
$ npm start
```

* Prepare your browser *(Chrome, Firefox, Internet Explorer, and etc..)*
* Open an *IDE* or a *text editor*
* In the path *learning-app/src/App.js*

```javascript
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  
  // add a custom function: 'learn' or you can use any other name you want, 
  // just remember to update the function name used in onChange property of 
  // <input> tag in the render function below.
  learn(field, event) {
    // if you don't pass value to field, it will be 'undefined',
    // but if you don't pass value to 'event', it will still be there
    // type your test code below



    // type your test code above
  }

  render() {
    return (
      <div className="fluid-container">
      	<input onChange={this.learn.bind(this, "name")} className="form-control" type="text" placeholder="Name" /><br />
      </div>
    );
  }
}

export default App;

```


* **Add your code snippet** to the **test code position** as above shown
* **Press *F5* on your keyboard** each time you update and save your code
* Then you can **validate your result with your browser** by opening *Console* interface of them *(Chrome: Mouse Action: __Right Click > Inspect__ or Keyboard Action: __Ctrl+Shift+I__)*.

<br />
<br />
