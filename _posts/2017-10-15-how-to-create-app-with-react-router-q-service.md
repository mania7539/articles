---
published: false
---
$ create-react-app react-demo-2
$ npm install --save events lodash react@15 react-dom@15 react-router@2 history@2
$ npm install --save q
$ npm start

$ vi ./index.js

```js
// in /index.js
import React, { Component }  from 'react';
import ReactDOM from 'react-dom';
import './styles/app.css';
import Nav from './components/Nav';
import Screen1 from './screens/Screen1';
import Screen2 from './screens/Screen2';
import Screen3 from './screens/Screen3';
import registerServiceWorker from './registerServiceWorker';
import { EventEmitter } from 'events';

// $ npm install --save events lodash react@15 react-dom@15 react-router@2 history@2
import { Router, Route, IndexRoute, browserHistory, Link } from 'react-router'; 


class App extends Component {
	constructor(props) {
		super(props);
		this.state = {
			screenIndex: 1,
			
		}
	}

	componentWillMount() {
		this.eventEmitter = new EventEmitter();
		
		// pass a function
		this.eventEmitter.addListener("updateScreen", ({screenIndex}) => {
			this.updateScreen({newScreenIndex: screenIndex});
		});
		
	}
	
	updateScreen({newScreenIndex}) {
		this.setState({screenIndex: newScreenIndex})
	}

	
	render() {
		var ActiveScreen;
			
		if (this.state.screenIndex === 1) {
			ActiveScreen = <Screen1 />
		} else if (this.state.screenIndex === 2) {
			ActiveScreen = <Screen2 />
		} else if (this.state.screenIndex === 3) {
			ActiveScreen = <Screen3 />
		}
		
		return (
			<div className="app">
				<div className="app-header"></div>
				<div className="app-wrapper">
					<Nav 
						eventEmitter={this.eventEmitter}
						screenIndex={this.state.screenIndex}
					/>
					<div className="main-content">
						{/*ActiveScreen*/}
						{/*this.props.children*/ /*global props can't get the value*/}
						{
							// pass eventEmitter to every page
							React.cloneElement(this.props.children, {eventEmitter: this.eventEmitter})
						}
					</div>
				</div>
			</div>
		);
	}
}

//"Screen1" is the "this.props.children" of component "App"
ReactDOM.render(
	<Router history={browserHistory}>
		<Route path="/" component={App}>
			<IndexRoute component={Screen2} />
			<Route path="/screen1" component={Screen1} />
			<Route path="/screen2" component={Screen2} />
			<Route path="/screen3" component={Screen3} />
		</Route>
	</Router>, 
	document.getElementById('root'));

registerServiceWorker();

```


$ vi styles/app.sass

```css
/* in styles/app.sass */
body
  margin: 0
  padding: 10px
  font-family: sans-serif

.app-header 
  height: 60px
  background-color: black
  width: 100%
  
.app-wrapper 
  display: flex
  flex-direction: row
  justify-content: flex-start
  align-items: stretch
  min-height: 1000px
  height: 100%
  
  .app-nav 
    width: 100px
    background-color: blue
    display: flux
    flex-direction: column
    justify-content: flex-start
    align-items: stretch
    
    .nav-item
      height: 60px
      background-color: coral
      cursor: pointer
      display: flex
      flex-direction: column
      justify-content: center
      align-items: center
      
      &:hover
        background-color: yellow
      
      &.active-nav
        background-color: red
        
    
  .main-content
    flex: 1
    background-color: gray
  
```

$ node-sass ./styles/app.sass ./styles/app.css &


$ vi ./components/Nav.js

```js
// in components/Nav.js
import React, { Component } from 'react';
import { Link } from 'react-router';

class Nav extends Component {
    constructor(props) {
        super(props);
        // this.state = {
        //     screenIndex: 
        // };
    }
    
    
    render() {
        return (
            <div className="app-nav">
				<div className={this.props.screenIndex === 1 ? "nav-item screen1 active-nav" : "nav-item screen1"}
					onClick={(event) => { this.props.eventEmitter.emit("updateScreen", {screenIndex: 1})} }
					>
					<Link to="/screen1">Screen 1</Link>
				</div>
				<div className={this.props.screenIndex === 2 ? "nav-item screen2 active-nav" : "nav-item screen2"}
					onClick={(event) => { this.props.eventEmitter.emit("updateScreen", {screenIndex: 2})} }
					>
					<Link to="/screen2">Screen 2</Link>
				</div>
				<div className={this.props.screenIndex === 3 ? "nav-item screen3 active-nav" : "nav-item screen3"}
					onClick={(event) => { this.props.eventEmitter.emit("updateScreen", {screenIndex: 3})} }
					>
					<Link to="/screen3">Screen 3</Link>
				</div>
			</div>
            
        );        
    }
}


export default Nav
//module.exports = Nav

```

$ vi ./services/EtherService.js

```js
// in services/EtherService.js
import Q from 'q'

class EtherService {
    getEtherPrice() {
        var deferred = Q.defer();
        
        setTimeout(() => {
           deferred.resolve(44);
           
        }, 3000);
        
        return deferred.promise;
    }
    
    getEtherPrices() {
        var deferred = Q.defer();
        
        setTimeout(() => {
            deferred.resolve([
                 {day: "April 1", price: 40},   
                 {day: "April 2", price: 41},
                 {day: "April 3", price: 42}
            ]);
           
        }, 3000);
        
        return deferred.promise;
    }
}

export default new EtherService();
// module.exports = Screen2
```




```js
// in screens/Screen2.js

import React, { Component } from 'react';
import EtherService from '../services/EtherService';
import _ from 'lodash'

class Screen2 extends Component {
    constructor(props) {
        super(props);
        this.state = {
          etherPrice: undefined,
          etherPrices: []
        };
    }
    
    
    componentWillMount() {
        this.props.eventEmitter.emit("updateScreen", {screenIndex: 2});
                
        EtherService.getEtherPrice()
        .then((data) => {
            this.setState({etherPrice: data});
            // console.log("GOT DATA");
            // console.log(data);
        });
        
        EtherService.getEtherPrices()
        .then((data) => {
            this.setState({etherPrices: data});
            // console.log("GOT DATA");
            // console.log(data);
        });
    }
    
    render() {
        var TableRows = [];
        _.each(this.state.etherPrices, (etherPrice) => {
            TableRows.push(
                <tbody key={etherPrice.day}>
                    <tr>
                        <td>{etherPrice.day}</td>
                        <td>{etherPrice.price}</td>
                    </tr>
                </tbody>

            );
        });
        
        
        return (
            <div className="screen screen2">
                <h1>SCREEN 2 DATA</h1>
                <h4>{`The current price of Ether is: ${this.state.etherPrice}`}</h4>
                <table>
                    <thead>
                        <tr>
                            <th>Day</th>
                            <th>Price</th>
                        </tr>
                    </thead>
                    {TableRows}
                </table>
            </div>
            
        );        
    }
}

export default Screen2
// module.exports = Screen2

```





