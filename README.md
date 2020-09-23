# Redux Tutorial
1. [Functional Programming](#functional-programming)
## Functional Programming
### Higher-order function
A higher-order function is a function that takes a function as an argument or returns a function or both.

###### Example:
```javaScript
function greeting(fun) {
 console.log(fun());
}
 
function sayHello() {
 return function() {
   return "Hello world";
 }
}
 
setTimeOut(() => console.log("Hello world"), 1000);
```

### Function Composition
Divide a program into small-small functions is called function composition.

###### Example:
Programm to wrap the input inside the div tag.
```javaScript
const input = " JavaScript ";
 
const trim = str => str.trim();
const wrapInDiv = str => `<div>${str}</div>`;
const toLowerCase = str => str.toLowerCase();
 
const output = wrapInDiv(toLowerCase(trim(input)));
 
console.log(output);
```

### Composition and Piping
In the function composition section, we write a program to wrap the input inside the div tag but there is a problem in reading code. We are calling a function inside another function and because of that, we need to read the code from right to left.

```javaScript 
const output = wrapInDiv(toLowerCase(trim(input)));
```

We can simplify the code by using [lodash](https://lodash.com/) compose function.

###### Example:
```javaScript
const { compose } = require("lodash/fp");
 
const input = " JavaScript ";
 
const trim = str => str.trim();
const wrapInDiv = str => `<div>${str}</div>`;
const toLowerCase = str => str.toLowerCase();
 
const transform = compose(wrapInDiv, toLowerCase, trim);
const output = transform(input);
 
console.log(output);
```

You can notice in compose function I just pass the reference of the functions not calling the functions because compose function is a higher-order function it takes the reference of the function as an argument and returns another function which responsible to compose the functions.

```javaScript 
const transform = compose(wrapInDiv, toLowerCase, trim);
```

Now we simplify the function calls but still, we need to read the code from right to left. To simplify the code little bit more we can use the lodash pipe function.

```javaScript 
const transform = pipe(wrapInDiv, toLowerCase, trim);
```

###### Example:
```javaScript
const { pipe } = require("lodash/fp");
 
const input = " JavaScript ";
 
const trim = str => str.trim();
const wrapInDiv = str => `<div>${str}</div>`;
const toLowerCase = str => str.toLowerCase();
 
const transform = pipe(wrapInDiv, toLowerCase, trim);
const output = transform(input);
 
console.log(output);
```
