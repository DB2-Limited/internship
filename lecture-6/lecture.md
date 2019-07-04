# Lecture 6

### Functions

Functions are objects that:
- Can be created dynamically at runtime
- Can be assigned to variables
- Can be passes as arguments and be returned by other functions
- Can have their own properties and methods

###### Syntax

```js
function sayHello() {
  console.log('Hello world!');
}

sayHello();
```

```js
// never declare a function like this
var add = new Function('a, b', 'return a + b');

add(2, 3);
```

###### Variables

You can declare as many **local** variables as you want in your function body. They will be accessible only inside function scope.

```js
function sayHello() {
  var name = 'John';
  console.log('Hello, ' + name);
}

sayHello();

console.log(name);
```

You can also read & write global variables which declared outside of function body.

```js
var name = 'John';

function sayHello() {
  console.log('Hello, ' + name);
  name = 'Vasya';
}

sayHello();
console.log(name);
```

###### Arguments

You can define which arguments you function will accept. This arguments will be copiend into function scope local variables. Also you can use arguments with the default values.
```js
function sayHello(name='John') {
  console.log('Hello, ' + name);
}

sayHello();
sayHello('Vasya');
```


###### Hoisting

**Hoisting** - mechanism where variables and functions declarations are moved to the top of their scrope before exectuion.

![Lifecycle](./lifecycle.jpg ':size=300x500')

```js
function hoist() {
  a = 20;
  var b = 100;
}

hoist();

console.log(a); 
console.log(b); 
```

###### Function expression

```js
var f = function() {
  // body
}
```

###### Function expression vs Function declaration

|                             | Function expression              | Function declaration |
|-----------------------------|----------------------------------|----------------------|
| Creation time               | When runtime reach this function | Before runtime       |
| Callable before declaration | No                               | Yes                  |


###### Anonymous functions

**Anonymous function** - function expression which is not stored in variable.

```js
function() {
  // body
}
```


###### Callback pattern

Function are objects, so we can passed them as arguments to other functions.

```js
function sayHello(callback) {
  console.log('Hello!');
  callback();
}

function reply() {
  console.log('Hey!');
}

sayHello(reply);
```

###### Working with DOM

- Document object model
- Browser object model
- Javascript

![Window](./window.png)

###### DOM navigation

**Structure:**
- document.head - `<head>`
- document.body - `<body>`
- document.documentElement - `<html>`

**Childs and parent:**
- parentNode
- childNodes
- firstChild
- lastChild

**Neighborhoods:**
- previousSibling
- nextSibling