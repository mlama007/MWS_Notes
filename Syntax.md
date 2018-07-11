---
title: JS Notes Syntax
---

# ***Syntax***

# **Const and Let**

If a variable is declared using let or const inside a block of code (denoted by curly braces { }), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared. 

- use let when you plan to reassign new values to a variable, and 

- use const when you don’t plan on reassigning new values to a variable 

**Suggested Use**

- don’t use var anymore 

- always declare variables with const (update it from const to let if needed) 





# **Template Literals**

Denoted with backticks ( `` ) and can contain placeholders which are represented using ${expression} 

```js
const student = { 
  name: 'Richard Kalehoff', 
  guardian: 'Mr. Kalehoff' 
}; 

const teacher = { 
  name: 'Mrs. Wilson', 
  room: 'N231' 
} 

let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`; 
```
`Returns: Richard Kalehoff please see Mrs. Wilson in N231 to pick up your report card.`

The quotes and string concatenation operator have been dropped, as well as the newline characters ( \n ). 

</br>

***String Concantenation***

```js
let note = teacher.name + ',\n\n' + 
  'Please excuse ' + student.name + '.\n' + 
  'He is recovering from the flu.\n\n' + 
  'Thank you,\n' + 
  student.guardian;  
```
  
</br>

***Template Literals***
```js
let note = `${teacher.name},   

Please excuse ${student.name}. 

He is recovering from the flu. 



Thank you, 

${student.guardian};`
```

`Returns:`
`Mrs. Wilson, `

`Please excuse Richard Kalehoff.`

`He is recovering from the flu.`

</br>

`Thank you,`

`Mr. Kalehoff`
 
</br>





# **Destructuring**

**Destructuring values from an arrray**

Allows you to specify the elements you want to extract from an array or object on the left side of an assignment. 

```js
const point = [10, 25, -34]; 

const [x, y, z] = point; 

console.log(x, y, z); 
``` 
`prints: 10 25 -34 `

</br> 
Instead of:

```js
const point = [10, 25, -34];

const x = point[0]; 
const y = point[1]; 
const z = point[2]; 

console.log(x, y, z); 
``` 

`prints: 10 25 -34 `

</br>

You can also ignore values when destructuring arrays.  

For example: `const [x, , z] = point;` ignores the y coordinate and discards it.  

</br> 

**Destructuring values from an object**

The curly braces { } represent the object being destructured and type, color, and karat represent the variables where you want to store the properties from the object. You don’t have to specify the property from where to extract the values.  


```js
const gemstone = { 
  type: 'quartz', 
  color: 'rose', 
  karat: 21.29 
}; 

const {type, color, karat} = gemstone; 

console.log(type, color, karat); 
```
`prints: quartz rose 21.29`

</br> 
Instead of: 

```js
const gemstone = {
  type: 'quartz', 
  color: 'rose', 
  karat: 21.29 
}; 

const type = gemstone.type; 
const color = gemstone.color; 
const karat = gemstone.karat; 

console.log(type, color, karat); 
```
`prints: quartz rose 21.29`

</br>





# **Object literal shorthand**

You can remove those duplicate variables names from object properties if the properties have the same name as the variables being assigned to them. 
 
```js
let type = 'quartz'; 
let color = 'rose'; 
let carat = 21.29; 

const gemstone = { 
  type, 
  color, 
  carat, 

  calculateWorth() { ... } 

}; 

console.log(gemstone); 
```
`prints: Object {type: "quartz", color: "rose", carat: 21.29} `

Instead of: 
```js
let type = 'quartz'; 

let color = 'rose'; 
let carat = 21.29; 

 

const gemstone = { 
  type: type, 
  color: color, 
  carat: carat 

  calculateWorth: function() {...} 

}; 

console.log(gemstone); 
```
`prints: Object {type: "quartz", color: "rose", carat: 21.29}`

</br>






# **Iteration**

# *for… loop*


***Advantage:*** looping through arrays  (Most common) 

***Downside:*** having to keep track of the counter and exit condition. 
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (let i = 0; i < digits.length; i++) { 
  console.log(digits[i]); 
} 
```
`returns: 0 1 2 3 4 5 6 7 8 9 `

</br>

# *for… in loop*

***Advantage***: eliminates the counting logic and exit condition but uses an index to access values of the array  

***Downside***: discouraged when looping over arrays. 

```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const index in digits) { 
  console.log(digits[index]); 
} 
```
`prints: 0 1 2 3 4 5 6 7 8 9`

for...in loops loop over all enumerable properties. Added properties of array's prototype will appear in loop 

```js
Array.prototype.decimalfy = function() { 
  for (let i = 0; i < this.length; i++) { 
    this[i] = this[i].toFixed(2); 
  } 
}; 

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const index in digits) { 
  console.log(digits[index]); 
} 
```
`prints:` </br>
`0 1 2 3 4 5 6 7 8 9`</br>
`function() {`</br>
`    for (let i = 0; i < this.length; i++) {`</br>
`        this[i] = this[i].toFixed(2);`</br>
`    }`</br>
`}`

</br>

# *for… of loop*

**Advantage**: used to loop over any type of data that is iterable (String, Array, Map, and Set—Objects are not iterable, by default) 

**Downside**:  none
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const digit of digits) { 
  console.log(digit); 
} 
```
`prints: 0 1 2 3 4 5 6 7 8 9 `

</br>

```js
const days = ['sunday', 'monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday']; 

for (const day of days) { 

    console.log(day[0].toUpperCase() + day.substr(1)); 

} 
```
`prints: Sunday Monday Tuesday Wednesday Thursday Friday Saturday `

</br>

You can stop or break a for...of loop at any time:
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const digit of digits) { 
  if (digit % 2 === 0) { 
    continue; 
  } 
  console.log(digit); 
} 
```
`prints: 1 3 5 7 9`

</br>

The for...of loop will only loop over the values in the object. 
```js
Array.prototype.decimalfy = function() { 
  for (i = 0; i < this.length; i++) { 
    this[i] = this[i].toFixed(2); 
  } 
}; 

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const digit of digits) { 
  console.log(digit); 
} 
```
`prints: 0 1 2 3 4 5 6 7 8 9`
 

*TIP:*

It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection. For example, for (const button of buttons) {...} 

</br> 

# *forEach loop*

forEach loop is another type of for loop in JavaScript. However, forEach() is actually an array method, so it can only be used exclusively with arrays. There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop. 

</br>

# **Spread Operator**

Gives you the ability to expand, or spread, iterable objects into multiple elements 
```js
const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"]; 
console.log(...books); 
```
`Prints: Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities`

</br>

```js
const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]); 
console.log(...primes);  
```
`Prints: 2 3 5 7 11 13 17 19 23 29`

</br>

**Combining arrays with concat()**
```js
const fruits = ["apples", "bananas", "pears"]; 

const vegetables = ["corn", "potatoes", "carrots"]; 

const produce = fruits.concat(vegetables); 

console.log(produce); 
```
`Prints: ["apples", "bananas", "pears", "corn", "potatoes", "carrots"]`

</br>

**Spread Operator**
```js
const fruits = ["apples", "bananas", "pears"]; 

const vegetables = ["corn", "potatoes", "carrots"]; 

const produce = [...fruits, ...vegetables]; 

console.log(produce); 
```
`Prints:[ 'apples', 'bananas', 'pears', 'corn', 'potatoes', 'carrots' ]`

</br>

# **Rest Parameter**

Bundle multiple elements back into an array. Allows you to represent an indefinite number of elements as an array. 

Assigning the values of an array to variables: 
```js
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"]; 

const [total, subtotal, tax, ...items] = order; 

console.log(total, subtotal, tax, items); 
```
`Prints: 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]` 

Variadic Functions are functions that take an indefinite number of arguments. 

- It doesn’t have any parameters (even though sum() function can handle an indefinite amount of arguments) 

- It can be hard to understand if you’ve never used the arguments object before 

**Variadic Function**
```js
function sum() { 

  let total = 0;   

  for(const argument of arguments) { 

    total += argument; 

  } 

  return total; 

} 
```

**Rest Parameter**
```js
function sum(...nums) { 

  let total = 0;   

  for(const num of nums) { 

    total += num; 

  } 

  return total; 

}
```

Example:
```js
function average(...nums) { 

    let sum = 0; 

    let len = nums.length; 

    if (len === 0){ 

        return 0     

    } 

    for (const num of nums){ 

        sum += num; 

        resutls = sum/len;     

    } 

    return resutls; 

} 

console.log(average(2, 6)); 

console.log(average(2, 3, 3, 5, 7, 10)); 

console.log(average()); 
```
`prints: 4 5 0`

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 