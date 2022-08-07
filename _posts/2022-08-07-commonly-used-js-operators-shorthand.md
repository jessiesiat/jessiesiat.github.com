---
layout: post
title: Commonly used Javascript operators or shorthand
categories: js
comments: true
---

There was a significant advancement in the javascript language for the past years and it was because of
[ES2015](https://262.ecma-international.org/6.0/) or ES6. It brings in new features and sugaring patterns that
requires significant biolerplate in ES5. It includes arrow functions, classes, modules and many more.

In this post, we will just highlight the features that javascript developers should know and use to make
our code more succinct.

### Nullish Coalescing Operator `(??)`
Is a logical operator that returns its right-hand side operand when its left-hand side operand is `null` or `undefined`, and otherwise returns its left-hand side operand.

    const foo = null ?? 'default foo value';
    console.log(foo);
    // expected output: "default foo value"

    const bar = undefined ?? 'default bar value';
    console.log(bar);
    // expected output: "default bar value"

### Optional chaining `(?.)`
This operator is like the `.` chaining operator, except that instead of causing an error if a reference is nullish (`null` or `undefined`), the expression short-circuits with a return value of undefined.
When used with function calls, it returns undefined if the given function does not exist.

    const adventurer = {
      name: 'Alice',
      cat: {
        name: 'Dinah'
      }
    };

    const dogName = adventurer.dog?.name;
    console.log(dogName);
    // expected output: undefined

    console.log(adventurer.someNonExistentMethod?.());
    // expected output: undefined

### Arrow functions
An arrow function expression is a compact alternative to a traditional function expression, but is limited and can't be used in all situations.
Arrow functions don't have their own bindings to this or arguments.

    const names = [
      'jose',
      'juan',
      'maria',
    ];

    console.log(names.map(name => name.charAt(0).toUpperCase() + name.slice(1)));
    // expected output: Array ["Jose", "Juan", "Maria"]

### Array and object destructuring
The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

Array Destructuring

    let animals = ["Carabao", "Dog", "Cat", "Eagle"];
    let [animalA, animalB] = animals;

    console.log(animalA); // "Carabao"
    console.log(animalB); // "Dog"

    // you can also skip items in the array
    let [,,animalC, animalD] = animals;

    console.log(animalC); // "Cat"
    console.log(animalD); // "Eagle"

    // assigning the rest of an array
    let [animalA,...restOfAminals] = animals;
    console.log(animalA); // "Carabao"
    console.log(restOfAminals); // ["Dog", "Cat", "Eagle"]

Object Destructuring

    let person = {name: "Juan", country: "PH", job: "Developer"};
    let {name, job: work, test = 'default'} = person;

    console.log(name); // "Juan"
    console.log(work); // Developer"
    console.log(test); // default"

### Template literals
Template literals are literals delimited with backtick characters, allowing for multi-line strings,
for string interpolation with embedded [expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators),
and for special constructs called tagged templates.

    let expression = 1 + 1;
    console.log(`string text ${expression} another text`);
    // expected "string text 2 another text"

### Function default parameter
Default function parameters allow named parameters to be initialized with default values if no value or undefined is passed.

    function getValue(object, defaultVal = 'test') {
      return object?.value ?? defaultVal;
    }

    console.log(getValue(null));
    // expected "test"


### Rest parameter and spread operator

Rest parameter

    function sumAll(...args) {
      let sum = 0;
      for (let arg of args) sum += arg;
      return sum;
    }

    console.log( sumAll(1) ); // 1
    console.log( sumAll(1, 2) ); // 3
    console.log( sumAll(1, 2, 3) ); // 6

Spread operator

    let person = {name: "Mario", country: "PH", job: "Developer" friends: ["Jojo", "Anjo"]};

    let {name, friends, ...others} = person;

    console.log(name); // "Mario"
    console.log(friends); // ["Jojo", "Anjo"]
    console.log(others); // {country: "PH", job: "Developer"}






