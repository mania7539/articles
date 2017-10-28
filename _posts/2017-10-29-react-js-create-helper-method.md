---
published: true
---
## Manually Create Your Own Helper Method


```javascript
import {combineReducers} from "redux";

export const makeRootReducer = () => {
    return combineReducers({});
}

// create helper method
export default makeRootReducer;

```
