# Lecture 7

### Objects

###### Declaration

```js
let obj = new Object();
let obj2 = {};
```

###### Access object property
```js
let obj = {
  firstName: 'John',
  lastName: 'Smith'
}

console.log(obj.firstName);
console.log(obj['firstName']);
```

###### Check if object has a property

```js
let obj = {
  firstName: 'John',
  lastName: 'Smith'
}

// using 'in'
if ('firstName' in obj) {
  console.log('With first name');
} else {
  console.log('Without first name');
}

// equal to undefined
if (obj.firstName !== undefined) {
  console.log('With first name');
} else {
  console.log('Without first name');
}
```

###### Loop through object properties

```js
for (let key in obj) {
  let value = obj[key];
  console.log(key, value);
}
```

###### Loop ordering
```js
let obj = {
  '3': 'Third',
  '2': 'Second',
  '1': 'First'
}

for (let key in obj) {
  console.log(key, obj[key]);
}
```

###### Objects in memory

Browser engine will create a `structure` for each objects type and store only values.

```js
let people: [
  {
    firstName: 'John',
    lastName: 'Smith',
    age: 23
  },
  {
    firstName: 'Vasya',
    lastName: 'Pupkin',
    age: 25
  },
  {
    firstName: 'Ivan',
    lastName: 'Ivanov',
    age: 27
  }
]

/* Will produce the next structure in memory
 * <structure: <string> firstName, <string> lastName, <number> age>
 */
```

Storing the same object in different variables will fill only one memory cell.

```js
// variables flow
let a = 'Just a regular string'; // will be saved to a memory cell "A" 
let b = a; // will be saved to a memory cell "B"

// objects flow
let obj = {
  firstName: 'John',
  lastName: 'Smith'
}; // will be saved to a memory cell "A"

let obj2 = obj; // will use memory cell "A"
```

> If name not numeric string, than you can loop properties as you define them. If name is a number or numeric string then this properties will be sorted.

If you still need to store the same object, you need to create a copy of it. You can use the next ways to do that:
- `Object.assign()`
- spread operator
- `JSON.parse()` and `JSON.stringify()`
- `for ... in ...`

###### Transfrom objects

- `toString`
- `valueOf`

String transformation with `toString`:

```js
let obj = {
  firstName: 'John',
  lastName: 'Smith'
};

alert(obj); // [object Object]


let obj2 = {
  firstName: 'John',
  lastName: 'Smith',
  toString: function() {
    return this.firstName + ' ' + this.lastName;
  }
};

alert(obj2); // John Smith

```

Numeric transformation with `valueOf`:

```js
let obj = {
  number: 12,
  valueOf: function() {
    return this.number + 1;
  },
  toString: function() {
    return this.number;
  }
};

alert(+obj);
delete obj.valueOf;
alert(+obj);
```

###### Property descriptors

```js
Object.defineProperty(obj, property, descriptor);
```

**Descriptor** - object, which can configure property behavior.
- **value**, property value. (`undefined`)
- **writable**, define if property can be changed. (`false`)
- **configurable**, define, if property can be removed. (`false`)
- **enumerable**, define if property can be used in `for ... in ...` and in `Object.keys()` (`false`)
- **get**, return property value. (`undefined`)
- **set**, set property value. (`undefined`)

Conflicts:
- get/set & writable
- get/set & value

###### Getters & Setters

```js
let obj = {
  firstName: 'John',
  lastName: 'Smith'
};

Object.defineProperty(obj, 'fullName', {
  get: function() {
    return this.firstName + ' ' + this.lastName;
  },
  set: function(val) {
    let splittedVal = val.split();
    this.firstName = splittedVal[0];
    this.lastName = splittedVal[1];
  }
})

console.log(obj.fullName);
obj.fullName = 'Vasya Pupkin';
console.log(obj.fullName);
```

###### Object creation via constructor

```js
function Man(fullName) {
  let splittedFullName = fullName.split();
  this.firstName = splittedFullName[0];
  this.lastName = splittedFullName[1];

  this.sayHello = function() {
    console.log('Hello. I\'m ', this.firstName);
  }
}

let man = new Man('John Smith');
let man2 = new Man('Vasya Pupkin');
console.log(man);
console.log(man2);
man.sayHello();
```

### Working with DOM

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