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

## Regular expressions(Regex)

### Using the Test Method

Regular expressions are used to match parts of strings. The .test() method takes the regex, applies it to a string (which is placed inside the parentheses), and returns **_true_** or **_false_** if your pattern finds something or not.

```
let testStr = "freeCodeCamp";
let testRegex = /Code/;
testRegex.test(testStr);
// Returns true

```

Note: The regex /Kevin/ will not match "kevin" or "KEVIN".

### Searching for more than two regexes

OR operator '|' is used for this.

### Using the case insensitive flag (i) to take care of case differences(uppercase and lowercase)

```
let testRegex = /javascript/i;
//This will search for javascript, Javascript, javaScript...
```

### Using the .match method to extract matches

Returns the **_matching string_**. If there is no such string, it returns **_null_**.

```
"Hello, World!".match(/Hello/);
// Returns ["Hello"]
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex);
// Returns ["expressions"]

```

**DIFFERENCE BETWEEN .test() AND .match()**:
.test method is applied to REGEX and the argument passed into it is the string that we are testing for, so that we get to know if there is a match..
.match method is applied to a string with the argument being the regex so that the matching string is returned.

### Usage of the global flag (g)

To extract a pattern more than once, the g flag is used.

```
//Without the g flag
let testStr = "Repeat, Repeat, Repeat";
let ourRegex = /Repeat/;
testStr.match(ourRegex);
// Returns ["Repeat"]

//With the g flag
let repeatRegex = /Repeat/g;
testStr.match(repeatRegex);
// Returns ["Repeat", "Repeat", "Repeat"]
```

Note: We can use multiple flags

```
let regex = /search/gi
```

### Wildcard or dot or period character(.)

The following example best illustrates the use of this character

```
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr); // Returns true
huRegex.test(hugStr); // Returns true
```

### Character classes

Character classes allow us to define a group of characters we wish to match by placing them inside square ([ and ]) brackets.

```
let bigStr = "big";
let bagStr = "bag";
let bugStr = "bug";
let bogStr = "bog";
let bgRegex = /b[aiu]g/;
//Note that there are no commas separating the characters inside the character class
bigStr.match(bgRegex); // Returns ["big"]
bagStr.match(bgRegex); // Returns ["bag"]
bugStr.match(bgRegex); // Returns ["bug"]
bogStr.match(bgRegex); // Returns null
```

### Using the hyphen(-) character

For a range of characters: Inside a character set, you can define a range of characters to match using a hyphen character.
For example, to match lowercase letters a through e you would use [a-e].

```
let regex = /[a-e]/
//Note that the square brackets are important since it is a character class
```

For a range of numbers: Using the hyphen (-) to match a range of characters is not limited to letters. It also works to match a range of numbers.

```
let regex = /[1-5]/
```

For a combination of a range of characters and numbers:

```
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
// matches all letters and numbers in jennyStr
jennyStr.match(myRegex);
```
