# Javascript freecodecamp

This repo has been created to record what I'm learning from the Javascript section of freecodecamp.
I am creating this after having finished the first module and half of the second module. It mostly contains code snippets from freecodecamp that best helped me understand the concept and also some of their own explanations.

Table of contents:

1. [ES6](#es6)
2. [Regex](#regex)
3. [Debugging](#debugging)
4. [Basic data structures](#basic-data-structures)
5. [Basic algorithm scripting](#intro-to-basic-algorithm-scripting)
6. [Object oriented programming](#object-oriented-programming)

## ES6

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

## Regex

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

### Match Single Characters Not Specified

We can also a character set with characters that we do not want to match. These are called
**negated character sets**.
The caret( ^ ) character is used to create a negated character set. We place ^ before all the set of characters that we don't want to match.

Note : Characters like ., !, [, @, / and white space are also matched

```
//To create a negated character with all the vowels and digits, we do the following
let regex = /[^aeiou^0-9]/gi;
let string = "Manaswini 1832.";
let result = string.match(regex);  //Returns ["M", "n", "s", "w", "n", " ", "."]
```

### Match characters that occur one or more times

The + character is used here

This is better understood with the following examples.

```
let regex = /a+/gi;

//Case 1
let str1 = "abc";
let str2 = "aabc";
let str3 = "abab";

let result1 = str1.match(regex);  //Returns ["a"];
let result2 = str2.match(regex);  //Returns ["aa"];
let result3 = str3.match(regex);  //Returns ["a", "a"];
```

### Match characters that occur Zero or more times

The character used here is \*

```
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex); // Returns ["goooooooo"]
gPhrase.match(goRegex); // Returns ["g"]
oPhrase.match(goRegex); // Returns null
```

```
//To match A followed by any zero or more numbers of lowercase a, this would be the regex
let regex = /[Aa*]/
```

**_NOTE_** : Differrence between + and \* characters

- : To match one or more characters

* : To match zero or more characters

### Find Characters with Lazy Matching

Regular expressions are by default greedy i.e. they return the longest possible part of the
string that matches the given regex.

However, we can use the ? character to enable lazy matching.

```
let string = "Mississippi";

//Greedy match(default for regular expressions)
let greedyRegex = /m[a-z]*s/i;
let greedyResult = string.match(greedyRegex); //Returns ["Mississ"]

//Lazy matching using the ? character
let lazyRegex = /m[a-z]*?s/i;
let lazyResult = string.match(lazyRegex); //Returns ["Mis"]
```

### Match Beginning String Patterns only

Inside a character set, ^ can be used to match a set of characters present **anywhere**
in the string.
But when used outside a character set, ^can help match that string only if it is present
at the beginning of the string.

```
let string = "javascript";

//^ used inside a character set
let caretInRegex = /[^script]/;

//^ used outside a character set
let caretOutRegex = /^script/;

console.log(caretInRegex.test(string));  //Logs true
console.log(caretOutRegex.test(string)); //Logs false
```

### Match ending string patterns only

The dollar sign( \$ ) at the end of the regex can be used to do this

```
let str1 = "cupboard";
let str2 = "boardRoom";

let endRegex = /board$/;

console.log(endRegex.test(str1)); //Logs true
console.log(endRegex.test(str2));  //Logs false
```

## Shorthand character classes

### Match all letters and numbers (alphanumerics)

Here we look at the use of the **\w** character. It helps us write a **shorthand character class**

Using the \w is equivalent to initializing the regex as /[A-Za-z0-9_]/
Note: We have \_ included too

```
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
let numbers = "42";
let varNames = "important_var";
console.log(longHand.test(numbers)); // Returns true
console.log(shortHand.test(numbers)); // Returns true
console.log(longHand.test(varNames)); // Returns true
console.log(shortHand.test(varNames)); // Returns true
```

### Match all characters other than alphanumerics

We use the **\W** for this( note that this uses a capital letter(W) )

Using \W is equivalent to using the regex /[^a-za-z0-9_]/

```
let quoteSample = "The five boxing wizards jump quickly.";
let nonAlphabetRegex = /\W+/g;
/*used global flag to extract the white space character 5 times*/
let result = quoteSample.match(nonAlphabetRegex).length;

console.log(result); //Logs 6
```

### Match all numbers

**\d** is used as a shorthand for the character class [0-9]

### Match all the non-numbers

**\D** is equivalent to the character class [^0-9]

### Match whitespace

**\s** is equivalent to the character class [ \r\t\f\n\v] (i.e. whitespace, carriage return, tab, form feed, and new line)

### Match no white space

**\S** is equivalent to using the character class [^ \r\t\f\n\v]

### Specify Upper and Lower Number of Matches

**Quantity specifiers** are used for this. They can be declared using {}

```
//To search for a minimum of 3 As and a maximum of 5As, we can use a quantity specifier as shown below
let a4 = "AAAAh";
let a2 = "AAh";

let regex = /A{3,5}h/

let res1 = regex.test(a4); // Returns true
let res2 = regex.test(a2); // Returns false
```

### Specify Only the Lower Number of Matches

We can only specify the lower limit and followed by a comma inside the quantity specifier

```
//To match only the string "hah" with the letter a appearing at least 3 times, our regex would be /ha{3,}h/.
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/;
multipleA.test(A4); // Returns true
multipleA.test(A2); // Returns false
multipleA.test(A100); // Returns true
```

### Specify Exact Number of Matches

We specify only one number between the curly brackets of the quantity specifier

### Check for All or None

? can be used after such an optional character

```
let britSpell = "colour";
let amSpell = "color";

let regex = /colou?r/;

let res1 = regex.test(britSpell); //Returns true
let res2 = regex.test(amSpell); //Returns true
```

### Lookaheads ( Positive and negative )

Positive lookaheads ?= and negative lookaheads ?!=

```
//What we want: Look only for a number followed by $
let yesDollar = "Bought a choco for 2Rs";
let noDollar = "Bought a choco for 2";

let regex = /\d+(?=Rs)/
console.log(regex.test(yesDollar)); //Returns true
console.log(regex.test(noDollar)); //Returns false
```

### Check For Mixed Grouping of Characters

```
//To check for both Penguin or Pumpkin
let regex = /P(engu|umpk)in/;
```

### Reuse Patterns Using Capture Groups

**Capture groups** help us search for patterns that occur repeatedly
To specify where that repeat string will appear, you use a backslash (\) and then a number.
Example: \1 => This number starts at 1 and increases with each additional capture group you use.

```
let repeatStr = "regex regex";
let repeatRegex = /(\w+)\s\1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["regex regex", "regex"]
```

### Use Capture Groups to Search and Replace

We can search and replace a string using .replace()
The first argument that it takes is the string to be replaced.
The second argument is the string that it has to be replaced by.

```
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
// Returns "The sky is blue."
```

Capture groups in the second argument can also be accessed using the dollar sign.

```
"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1');
// Returns "Camp Code"
```

```
//Another example using the dollar sign syntax
let str = "one two three";
let fixRegex = /(one)\s(two)\s(three)/; // Change this line
let replaceText = "$3 $2 $1"; // Change this line
let result = str.replace(fixRegex, replaceText);
console.log(result) //Returns three two one
```

## Debugging

### Use typeof to Check the Type of a Variable

Immutable data types in JavaScript: Boolean, Null, Undefined, Number, String, Symbol
Mutable data type: Object ( Arrays are technically types of objects )

### Catch Misspelled Variable and Function Names

Variable and function names in JavaScript are case sensitive

### Catch Unclosed Parentheses, Brackets, Braces and Quotes

One way to avoid this mistake is as soon as the opening character is typed, immediately include the closing match, then move the cursor back between them and continue coding.

### Catch Mixed Usage of Single and Double Quotes

You can escape the quotes inside the string by using the backslash (\) escape character

### Catch Use of Assignment Operator Instead of Equality Operator

= ( Assignment operator ) helps us assign a value to a variable
== or === ( Equality operators ) help us check for equality

Almost every value on its own in JavaScript evaluates to true, except what are known as the **Falsy** values: **false, 0, "" (an empty string), NaN, undefined, and null**.

### Catch Missing Open and Closing Parenthesis After a Function Call

When a function is being called, it is important that we use the () brackets after the function name.

### Catch Off By One Errors When Using Indexing

**Off by one errors (sometimes called OBOE)** crop up when you're trying to target a specific index of a string or array (to slice or access a segment), or when looping over the indices of them. JavaScript indexing starts at zero, not one, which means the last index is always one less than the length of the item.

### Prevent Infinite Loops with a Valid Terminal Condition

Don't forget to mention the terminal condition while inside a loop.

## Basic data structures

### Use an Array to Store a Collection of Data

An array can take in a combination of JavaScript data types. Arrays have a length that can be accessed by the array.length property.

### Access an Array's Contents Using Bracket Notation

The fundamental feature of any data structure is, of course, the ability to not only store data, but to be able to retrieve that data on command. Each item in an array has an index. Arrays are zero-indexed i.e. their indices start from zero.

### Add Items to an Array with push() and unshift()

arr.push() ----> Add items to the end of an array
arr.unshift() -->Add items to the beginning of an array

### Remove Items from an Array with pop() and shift()

arr.pop() ------> Remove items from the end of an array
arr.shift() -----> Remove items from the beginning of an array

### Remove Items in an array Using splice()

First argument -----> The **index** where it should start removing elements from
Second argument ----> The **number** of elements it should remove from that index
Third argument -----> The **element(s)** that should be placed in that position

```
//Without third argument
const arr = [1, 2, 3, 4, 5, 6];
const splicedArr = arr.splice(1, 3);
console.log(splicedArr); //Logs [1, 5, 6]

//With the third argument
const numbers = [10, 11, 12, 12, 15];

numbers.splice(3, 1, 13, 14);
// the second entry of 12 is removed, and we add 13 and 14 at the same index
console.log(numbers);
// returns [ 10, 11, 12, 13, 14, 15 ]
```

### Copy Array Items Using slice()

First argument -----> Index at which the array should start forming
Second argument -----> Index upto which ( excluding it ) till where this array formation should happen

```
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];

let todaysWeather = weatherConditions.slice(1, 3);
// todaysWeather equals ['snow', 'sleet'];
// weatherConditions still equals ['rain', 'snow', 'sleet', 'hail', 'clear']
```

### Copy an Array with the Spread Operator

Provides a highly readable syntax to copy the contents of an array into another array.

```
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
// thatArray equals [true, true, undefined, false, null]
// thisArray remains unchanged, and is identical to thatArray
```

### Combine Arrays with the Spread Operator

```
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];

let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
// thatArray now equals ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']
```

### Check For The Presence of an Element With indexOf()

array. indexOf() takes an element as a parameter, and when called, it returns the position, or index, of that element, or -1 if the element does not exist on the array.

### Add Key-Value Pairs to JavaScript Objects

In an object, keys are mapped to properties called values.
Following are the two ways to add a key-value pair to an object.

```
//First way: When our value doesn't have a space
tekkenCharacter.origin = 'South Korea';

//Second way: When our key has a space
tekkenCharacter['hair color'] = 'dyed orange';
```

### Use the delete Keyword to Remove Object Properties

This is done using the **delete** keyword

```
delete foods.apples;
```

### Check if an Object has a Property

We can do so by using the **hasOwnProperty()** on the object or the **'in'** keyword.

```
users.hasOwnProperty('Alan');
'Alan' in users;
// both return true if 'Alan exists in the users object'
```

### Iterate Through the Keys of an Object with a for...in Statement

```
{
  Alan: {
    online: false
  },
  Jeff: {
    online: true
  },
  Sarah: {
    online: false
  }
}

for (let user in users) {
  console.log(user);
}

// logs:
Alan
Jeff
Sarah
```

### Generate an Array of All Object Keys with Object.keys()

Argument ------> Object whose keys have to be put in an array

```
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function getArrayOfUsers(obj) {
  // Only change code below this line
  let newArr = Object.keys(obj);
  return newArr;

  // Only change code above this line
}

console.log(getArrayOfUsers(users)); //Logs ["Alan", "Jeff", "Sarah", "Ryan"]
```

## Intro to basic algorithm scripting

This section contains info about all the new things that I learnt while playing around with the algorithms

### Reverse a String

1. .slice() method on a string

```
const str = "Hello";

console.log(str.slice(0, 1)); //Logs H
console.log(str.slice(3, 5)); //Logs 1o
console.log(str.slice(2)); //Logs llo
```

2. .reverse() on an array

```
const arr = [a, b, c];

console.log(arr.reverse()); //Logs [c, b, a]
```

3. .join() on an array

This method on a string helps join the items of an array using the symbol that we specify in the parentheses. If nothing is specified, the items are joined using a comma.

```
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```

### Find the longest word in a string

1. .split() on a string

This method helps split the string into an array as we wish

```
const str = "I am Human";

console.log(str.split());  //Logs [ 'I am Human' ]
console.log(str.split("")); //Logs [ 'I', ' ', 'a', 'm', ' ', 'H', 'u', 'm', 'a', 'n' ]
console.log(str.split(" ")); //Logs [ 'I', 'am', 'Human' ]
```

2. Math.max()

```
console.log(Math.max(1, 5, 15, 10)); //Logs 15

let arr = [3, 8, 9, 2];
console.log(Math.max(...arr)); //Logs 9
```

### Check if a string ends with a given string

1. The lastIndexOf() method returns the position of the last occurrence of a specified value in a string.

```
const str = "Manaswini";
console.log(str.lastIndexOf("wini"));  /Logs 5
```

2. We can declare a new Regex using the new keyword followed by RegExp

```
//Example
let re = new RegExp(target + "$", "i");
```

### Truncate a string

1. .substring() method on a string

```
const str = "A-tisket a-tasket A green and yellow basket";
console.log(str.substring(0, 8)); //Logs A-tisket
```

### Title Case a Sentence

1. .charAt() followed by toUpperCase()

```
const str = "manasWiNi";
console.log(str.charAt(0).toUpperCase() + str.slice(1).toLowerCase()); //Logs Manaswini
```

### Falsy bouncer

Falsy values in JavaScript are false, null, 0, "", undefined, and NaN

Checking for falsy values can be done using an if statement

## Object oriented programming

### Create a Method on an Object

```
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
// Returns "The name of this duck is Aflac."
```

### Make Code More Reusable with the this Keyword

If the variable name changes, any code referencing the original name would need to be updated as well. In a short object definition, it isn't a problem, but if an object has many references to its properties there is a greater chance for error.

```
let duck = {
 name: "Aflac",
 numLegs: 2,
 sayName: function() {return "The name of this duck is " + this.name + ".";}
};
//Here this refers to the object that the method is associated with.
```

### Define an object using a Constructor Function

Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object.

```
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```

This constructor defines a Bird object with properties name, color, and numLegs set to Albert, blue, and 2, respectively. Constructors follow a few conventions:

1. Constructors are defined with a capitalized name to distinguish them from other functions that are not constructors.
2. Constructors use the keyword this to set properties of the object they will create. Inside the constructor, this refers to the new object it will create.
3. Constructors define properties and behaviors instead of returning a value as other functions might.

### Use a Constructor to Create Objects

```
function Bird() {
  this.name = "Albert";
  this.color  = "blue";
  this.numLegs = 2;
  // "this" inside the constructor always refers to the object being created
}

let blueBird = new Bird();

blueBird.name; // => Albert
blueBird.color; // => blue
blueBird.numLegs; // => 2

// Its properties can be accessed and modified:
blueBird.name = 'Elvira';
blueBird.name; // => Elvira
```

### Extend Constructors to Receive Arguments

```
function Bird(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}
```

### Verify an Object's Constructor with instanceof

Anytime a constructor function creates a new object, that object is said to be an instance of its constructor. instanceof allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor.

```
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // => true
```

### Understand Own Properties

```
function Bird(name) {
  this.name  = name;
  this.numLegs = 2;
}

let duck = new Bird("Donald");

let ownProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}

console.log(ownProps); // prints [ "name", "numLegs" ]
```
