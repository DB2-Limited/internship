# Lecture 8

### Introduction

Object Oriented Programming (OOP) and Functionnal Programming (FP) are programming paradigms. Roughly speaking, following a programming paradigm is writing code compliant with a specific set of rules. For example, organizing the code into units would be called OOP, avoiding side effects would be called FP.

**OOP Pros:**

- Objects and methods are very readable and understandable.

- OOP utilizes an imperative style, in which code reads like a straight-forward set of instructions as a computer would read it.

**OOP Cons:**

- OOP commonly depends upon shareable state. The unfortunate result of so many objects and methods existing within the same state and being accessed in an entirely undetermined order can lead the pre-discussed concept of “race conditions”.

**FP Pros:**

- Utilizing pure functions, leads to reliable functions with no side effects that accomplish and return exactly what you expect them to.

- FP utilizes a more declarative style, which focuses more on what to do and less about how it’s being done. This places the emphasis on performance and optimization, leaving the door to refactor without completely reworking your code.

**FP Cons:**

- Functional programming is a newer paradigm. It’s much easier to find documentation and information on the OOP approach.

- Similar to one of OOP’s strengths, functional programming can lack readability at times. Sometimes functions can become very verbose and become difficult to follow comparatively to the object-oriented style.

You saw a simple example of this in the Person object and createPerson function we discussed earlier.

### Functional OOP

```js
function Machine() {
  var enabled = false;

  this.enable = function() {
    enabled = true;
  };

  this.disable = function() {
    enabled = false;
  };
}
```

```js
function CoffeeMachine(power) {
  Machine.call(this); // отнаследовать

  var waterAmount = 0;

  this.setWaterAmount = function(amount) {
    waterAmount = amount;
  };

}

var coffeeMachine = new CoffeeMachine(10000);

coffeeMachine.enable();
coffeeMachine.setWaterAmount(100);
coffeeMachine.disable();
```


```js
showFullName.call(user, 'firstName', 'surname'); // arguments listed
showFullName.apply(user, ['firstName', 'surname']); // arguments as array
```

access to parents properties
```js
function Machine() {
  var enabled = false;

  this.enable = function() {
    enabled = true;
  };

  this.disable = function() {
    enabled = false;
  };
}

function CoffeeMachine(power) {
  Machine.call(this);

  this.enable();

  alert( enabled ); // ERROR!
}

var coffeeMachine = new CoffeeMachine(10000);
```


```js
function Machine() {
  this._enabled = false; // -> var enabled

  this.enable = function() {
    this._enabled = true;
  };

  this.disable = function() {
    this._enabled = false;
  };
}

function CoffeeMachine(power) {
  Machine.call(this);

  this.enable();

  alert( this._enabled ); // -> true
}

var coffeeMachine = new CoffeeMachine(10000);
```

if we want to extend some inherited property

```js
function CoffeeMachine(params) {
  Machine.apply(this, arguments);

  var parentProtected = this._protectedProperty;
  this._protectedProperty = function(args) {
    parentProtected.apply(this, args); // (*)
    // ...
  };
}
```

### Prototype OOP

###### Property proto
*except IE10 -* 
```js
var animal = {
  eats: true
};
var rabbit = {
  jumps: true
};

rabbit.__proto__ = animal;

alert( rabbit.jumps ); // true
alert( rabbit.eats ); // true
```

###### Method hasOwnProperty
```js
var animal = {
  eats: true
};

var rabbit = {
  jumps: true,
  __proto__: animal
};

for (var key in rabbit) {
  alert( key + " = " + rabbit[key] ); // `eats` and `jumps`
}
```
with `hasOwnProperty` check
```js
alert( rabbit.hasOwnProperty('jumps') ); // true
alert( rabbit.hasOwnProperty('eats') ); // false
```
check only own object 
```js
var animal = {
  eats: true
};

var rabbit = {
  jumps: true,
  __proto__: animal
};

for (var key in rabbit) {
  if (!rabbit.hasOwnProperty(key)) continue; // пропустить "не свои" свойства
  alert( key + " = " + rabbit[key] ); // выводит только "jumps"
}
```

### Interfaces
- 

### Algorithms
- 

