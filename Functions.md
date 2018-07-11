---
title: JS Notes Functions
---

# ***Functions***

# **Arrow functions**

ES6 introduces a new kind of function called the arrow function. Arrow functions are very similar to regular functions in behavior, but are quite different syntactically. The following code takes a list of names and converts each one to uppercase using a regular function: 

```js
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) {   
    return name.toUpperCase();
});
```
</br>

The code below does the same thing except instead of passing a regular function to the map() method, it passes an arrow function. Notice the arrow in the arrow function ( => ) in the code below: 

```js
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(  
    name => name.toUpperCase()
); 
```
</br>

## **Arrow function stored in a variable**

```js
const greet = name => `Hello ${name}!`; 
```

In the code above, the arrow function is stored in the greet variable and you'd call it like this: 

```js
greet('Asser'); 
```
`Returns: Hello Asser!`

</br>

```js
// empty parameter list requires parentheses
const sayHi = () => console.log('Hello Udacity Student!');sayHi(); 
```
`Prints: Hello Udacity Student!`

</br>

```js
// multiple parameters requires parentheses
const orderIceCream = (flavor, cone) => 
    console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
orderIceCream('chocolate', 'waffle'); 
```
`Prints: Here's your chocolate ice cream in a waffle cone.`

</br>

## **block body syntax**
If you need more than just a single line of code in your arrow function's body, then you can use the "block body syntax". 

```js
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {  
    name = name.toUpperCase();  
    return `${name} has ${name.length} characters in their name`;
}); 
```

Important things to keep in mind with the block syntax: 

- It uses curly braces to wrap the function body 

- A return statement needs to be used to actually return something from the function. 

</br>

Take a look at this code: 

```js
function greet(name, greeting) {  
    name = (typeof name !== 'undefined') ?  name : 'Student';  
    greeting = (typeof greeting !== 'undefined') ?  greeting : 'Welcome';  
    return `${greeting} ${name}!`;}greet(); // Welcome Student!
    greet('James'); // Welcome James!
    greet('Richard', 'Howdy'); // Howdy Richard! 
``` 
`Returns:` </br>
`Welcome Student!` </br>
`Welcome James!` </br>
`Howdy Richard!` 


What is all that horrible mess in the first two lines of the greet() function? All of that is there to provide default values for the function if the required arguments aren't provided. It's pretty ugly, though... 

</br>

# **Default function parameters**

Default function parameters are quite easy to read since they're placed in the function's parameter list: 

```js
function greet(name = 'Student', greeting = 'Welcome') {  
    return `${greeting} ${name}!`;
    }
    greet(); // Welcome Student!
    greet('James'); // Welcome James!
    greet('Richard', 'Howdy'); // Howdy Richard! 
```
`Returns:` </br>
`Welcome Student!` </br>
`Welcome James!` </br>
`Howdy Richard!`

</br>

Defaults and destructuring arrays 

You can combine default function parameters with destructuring to create some pretty powerful functions! 

```js
function createGrid([width = 5, height = 5]) {  
    return `Generates a ${width} x ${height} grid`;
    }
    createGrid([]); // Generates a 5 x 5 grid
    createGrid([2]); // Generates a 2 x 5 grid
    createGrid([2, 3]); // Generates a 2 x 3 grid
    createGrid([undefined, 3]); // Generates a 5 x 3 grid 
```
`Returns:` </br>
`Generates a 5 x 5 grid` </br>
`Generates a 2 x 5 grid` </br>
`Generates a 2 x 3 grid` </br>
`Generates a 5 x 3 grid`

The createGrid() function expects an array to be passed to it. It uses destructuring to set the first item in the array to the width and the second item to be the height. If the array is empty or if it has only one item in it, then the default parameters kick in and give the missing parameters a default value of 5. 

There is a problem with this though, the following code will not work: 
```js
createGrid(); // throws an error 
```
Uncaught TypeError: Cannot read property 'Symbol(Symbol.iterator)' of undefined 

This throws an error because createGrid() expects an array to be passed in that it will then destructure. Since the function was called without passing an array, it breaks. But, we can use default function parameters for this! 

```js
function createGrid([width = 5, height = 5] = []) {  
    return `Generates a ${width} x ${height} grid`;
} 
```

See that new = [] in the function's parameter? If createGrid() is called without any argument then it will use this default empty array. And since the array is empty, there's nothing to destructure into widthand height, so their default values will apply! So by adding = [] to give the entire parameter a default, the following code will now work: 

```js
createGrid(); // Generates a 5 x 5 grid 
```
`Returns: Generates a 5 x 5 grid`

</br>
 
# **Defaults and destructuring objects**

Just like array destructuring with array defaults, a function can have an object be a default parameter and use object destructuring: 

```js
function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {   
    const scoopText = scoops === 1 ? 'scoop' : 'scoops';   
    return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`; 
} 
createSundae({}); // Your sundae has 1 scoop with Hot Fudge toppings.
createSundae({scoops: 2}); // Your sundae has 2 scoops with Hot Fudge toppings.
createSundae({scoops: 2, toppings: ['Sprinkles']}); // Your sundae has 2 scoops with Sprinkles toppings.
createSundae({toppings: ['Cookie Dough']}); // Your sundae has 1 scoop with Cookie Dough toppings. 
```
`Returns:` </br>
`Your sundae has 1 scoop with Hot Fudge toppings.` </br>
`Your sundae has 2 scoops with Hot Fudge toppings.` </br>
`Your sundae has 2 scoops with Sprinkles toppings.` </br>
`Your sundae has 1 scoop with Cookie Dough toppings.`

Just like the array example before, if you try calling the function without any arguments it won't work: 

```js
createSundae(); // throws an error 
```

Uncaught TypeError: Cannot match against 'undefined' or 'null'. 

We can prevent this issue by providing a default object to the function: 

```js
function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {  
    const scoopText = scoops === 1 ? 'scoop' : 'scoops';  
    return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
} 
```

By adding an empty object as the default parameter in case no arguments are provided, calling the function without any arguments now works. 

```js
createSundae(); // Your sundae has 1 scoop with Hot Fudge toppings. 
```
`Returns: Your sundae has 1 scoop with Hot Fudge toppings.`

 
# **Classes**

"Class" with ES5 code: 

```js
function Plane(numEngines) { 
    this.numEngines = numEngines; 
    this.enginesActive = false; 
} 

// methods "inherited" by all instances
Plane.prototype.startEngines = function () { 
    console.log('starting engines...'); 
    this.enginesActive = true; 
}; 

const richardsPlane = new Plane(1); 
richardsPlane.startEngines();

const jamesPlane = new Plane(4); 
jamesPlane.startEngines();
```
 

## **ES6 Classes**

Here's what that same Plane class would look like if it were written using the new class syntax: 

```js
class Plane { 
    constructor(numEngines) { 
     this.numEngines = numEngines; 
     this.enginesActive = false; 
    } 

    startEngines() { 
     console.log('starting engines…'); 
     this.enginesActive = true; 
    } 
} 
```

 

 
 

 

 

 

 

 

 

 