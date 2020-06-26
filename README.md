# Javascript freecodecamp

This repo has been created to record what I'm learning from the Javascript section of freecodecamp.
I am creating this after having finished the first module and half of the second module. It mostly contains code snippets from freecodecamp that best helped me understand the concept and also some of their own explanations.

### ES6:Class syntax to define a constructor function

Class keyword declares a new function, to which a constructor is added. This constructor is invoked when new is called to create a new object. UpperCamelCase should be used by convention for ES6 class names

```
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
}
const zeus = new SpaceShuttle('Jupiter');
```

### ES6:Use getters and setters to Control Access to an Object

Getter FUNCTIONS are meant to simply return (get) the value of an object's private variable to the user without the user directly accessing the private variable.

Setter FUNCTIONS are meant to modify (set) the value of an object's private variable based on the value passed into the setter function. This change could involve calculations, or even overwriting the previous value completely.

```
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const lol = new Book('anonymous');
console.log(lol.writer);  // anonymous
lol.writer = 'wut';
console.log(lol.writer);  // wut
```

Note: It is convention to precede the name of a private variable with an underscore (\_). However, the practice itself does not make a variable private.

### ES6: Create a Module Script

```
<script type="module" src="filename.js"></script>
```

A script that uses this module type can now use the import and export features

### ES6: Use export to Share a Code Block

This is how we can export multiple functions from one js file to another

```
export { add, subtract };
```

### ES6: Reuse JavaScript Code Using import

./ is used to specify the relative file path. Through this, we can look for the file in the same folder

```
import { add, subtract } from './math_functions.js';
```

### ES6: Use \* to Import Everything from a File

```
import * as myMathModule from "./math_functions.js";
```

The above import statement will create an object called myMathModule. The object will contain all of the exports from math_functions.js in it, so you can access the functions like you would any other object property.

### ES6: Create an Export Fallback with export default

```
// named function
export default function add(x, y) {
  return x + y;
}

// anonymous function
export default function(x, y) {
  return x + y;
}
```

Since export default is used to declare a fallback value for a module or file, you can only have one value be a default export in each module or file. Additionally, you cannot use export default with var, let, or const

### ES6: Import a Default Export

The syntax differs in one key place. The imported value, is not surrounded by curly braces ({}). It is simply a variable name for whatever the default export of the js file is. We can use any name when importing a default.

```
import add from "./math_functions.js";
```

### ES6: Create a JavaScript Promise

When the task completes, you either fulfill your promise or fail to do so. Promise is a constructor function, so you need to use the new keyword to create one. It takes a function, as its argument, with two parameters - resolve and reject. These are methods used to determine the outcome of the promise.

```
const myPromise = new Promise((resolve, reject) => {

});
```

### ES6: Complete a Promise with resolve and reject

```
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```

### ES6: Handle a Fulfilled Promise with then

The then method is executed immediately after your promise is fulfilled with resolve.
The data from resolve gets passed as an argument to the then method.

```
myPromise.then(result => {
  // do something with the result.
});
```

### ES6: Handle a Rejected Promise with catch

catch is the method used when your promise has been rejected. It is executed immediately after a promise's reject method is called.

```
myPromise.catch(error => {
  // do something with the error.
});
```

Note: the then and catch methods can be chained to the promise declaration if you choose.
