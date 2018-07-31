---
title: JS Notes Built-Ins
---

# ***Built-Ins***

# **Symbols**
A symbol is a unique and immutable data type that is often used to identify object properties.

To create a symbol, you write Symbol() with an optional string as its description.

```js
const sym1 = Symbol('apple');
console.log(sym1);
Symbol(apple)
```
This will create a unique symbol and store it in sym1. The description "apple" is just a way to describe the symbol, but it can’t be used to access the symbol itself.

If you compare two symbols with the same description…
```js
const sym2 = Symbol('banana');
const sym3 = Symbol('banana');
console.log(sym2 === sym3);
false
```
…then the result is false because the description is only used to describe the symbol. It’s not used as part of the symbol itself—each time a new symbol is created, regardless of the description.

Here’s the code to represent a bowl:
```js
const bowl = {
  'apple': { color: 'red', weight: 136.078 },
  'banana': { color: 'yellow', weight: 183.15 },
  'orange': { color: 'orange', weight: 170.097 }
};
```
The bowl contains fruit which are objects that are properties of the bowl. But, we run into a problem when the second banana gets added.
```js
const bowl = {
  'apple': { color: 'red', weight: 136.078 },
  'banana': { color: 'yellow', weight: 183.151 },
  'orange': { color: 'orange', weight: 170.097 },
  'banana': { color: 'yellow', weight: 176.845 }
};
console.log(bowl);
```
`Object {apple: Object, banana: Object, orange: Object}`

***previous banana is overwritten by the new banana*** being added to the bowl. 

To fix this problem, we can use symbols:
```js
const bowl = {
  [Symbol('apple')]: { color: 'red', weight: 136.078 },
  [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
  [Symbol('orange')]: { color: 'orange', weight: 170.097 },
  [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
};
console.log(bowl);
```
`Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}`

By changing the bowl’s properties to use symbols, each property is a unique Symbol and the first banana doesn’t get overwritten by the second banana.

</br>

# **Iteration & Iterable Protocols**

The iterable protocol is used for defining and customizing the iteration behavior of objects.
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for (const digit of digits) {
  console.log(digit);
}
```
`0` </br> 
`1` </br> 
`2` </br> 
`3` </br> 
`4` </br> 
`5` </br> 
`6` </br> 
`7` </br> 
`8` </br> 
`9`

The **iterator protocol** is used to define a standard way that an object produces a sequence of values.An object becomes an iterator when it implements the .next() method. The .next() method is a zero arguments function that returns an object with two properties:
1. value : the data representing the next value in the sequence of values within the object 

2. done : a boolean representing if the iterator is done going through the sequence of values 
    - If done is true, then the iterator has reached the end of its sequence of values. 
    - If done is false, then the iterator is able to produce another value in its sequence of values. 
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const arrayIterator = digits[Symbol.iterator]();

console.log(arrayIterator.next());
console.log(arrayIterator.next());
console.log(arrayIterator.next());
```
`Prints`</br>
`Object {value: 0, done: false}`</br>
`Object {value: 1, done: false}`</br>
`Object {value: 2, done: false}`</br>

</br>

## for of:
```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; 

for (const digit of digits) { 
  console.log(digit); 
} 
```
`Prints`</br>
`0 1 2 3 4 5 6 7 8 9`

</br>




# **Sets**
Sets are collections of unique values

The biggest differences between a set and an array are: 
- Sets are not indexed-based - you do not refer to items in a set based on their position in the set 
- Items in a Set can’t be accessed individually 

Basically, a Set is an object that lets you store unique items. You can add items to a Set, remove items from a Set, and loop over a Set. These items can be either primitive values or objects. 

## **How to Create a Set**
```js
const games = new Set(); 
console.log(games); 
```
`Set {}`

This creates an empty Set games with no items. 

</br>

Create a Set from a list of values, you use an array: 
```js
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']); 
console.log(games); 
```
`Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}`

Notice the example above automatically removes the duplicate entry "Super Mario Bros." when the Set is created. Pretty neat! 

</br>

## **Modify Sets**

_.clear() .delete() . Add()_

```js
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']); 

games.add('Banjo-Tooie'); 
games.add('Age of Empires'); 
games.delete('Super Mario Bros.'); 

console.log(games); 
```
`Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}`

</br>

On the other hand, if you want to delete all the items from a Set, you can use the .clear() method. 
```js
games.clear() 
console.log(games); 
```
`Set {}`

</br>

## **Working With Sets**

**Checking Length**

_.size_

```js
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']); 
console.log(months.size); 
```
`12`

 Sets can’t be accessed by their index like an array, so you use the .size property instead of .length property to get the size of the Set.

</br>

**Checking If An Item Exists**

_.has()_

Use the .has() method to check if an item exists in a Set.
```js
console.log(months.has('September')); 
```
`true`

</br>

**Retrieving All Values**

_.values()_

return the values in a Set.  

```js
console.log(months.values()); 
```
`SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}`

</br>

**Using the SetIterator**

Because the .values() method returns a new iterator object (called SetIterator), you can store that iterator object in a variable and loop through each item in the Set using .next().
```js
const iterator = months.values();
iterator.next();
```
`Object {value: 'January', done: false}`

And if you run .next() again?
```js
iterator.next();
```
`Object {value: 'February', done: false}`

And so on until done equals true which marks the end of the Set.

</br>

**Using a for...of Loop**

An easier method to loop through the items in a Set is the for...of loop.
```js
const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
for (const color of colors) {
  console.log(color);
}
```
`Prints:` </br>
`red ` </br>
`orange ` </br>
`yellow ` </br>
`green ` </br>
`blue ` </br>
`violet ` </br>
`brown ` </br>
`black`

</br>


# **WeakSet**

A WeakSet is just like a normal Set with a few key differences:
- a WeakSet can only contain objects 

- a WeakSet is not iterable which means it can’t be looped over 

- a WeakSet does not have a .clear() method 

```js
const student1 = { name: 'James', age: 26, gender: 'male' }; 
const student2 = { name: 'Julia', age: 27, gender: 'female' }; 
const student3 = { name: 'Richard', age: 31, gender: 'male' }; 

const roster = new WeakSet([student1, student2, student3]); 
console.log(roster);
```
`WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}`

…but if you try to add something other than an object, you’ll get an error! 
```js
roster.add('Amanda'); 
```
`Uncaught TypeError: Invalid value used in weak set(…)`

This is expected behavior because WeakSets can only contain objects. But why should it only contain objects? Why would you even use a WeakSet if normal Sets can contain objects and other types of data? Well, the answer to that question has more to do with why WeakSets do not have a .clear() method...

</br>

## **Garbage Collection**

Freeing up memory after it is no longer needed is what is known as garbage collection. WeakSets take advantage of this by exclusively working with objects. If you set an object to null, then you’re essentially deleting the object. And when JavaScript’s garbage collector runs, the memory that object previously occupied will be freed up to be used later in your program. 
```js
student3 = null; 
console.log(roster); 
```
`WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}`


</br>









# **Maps**

Maps are collections of key-value pairs

## **create a Map**
```js
const employees = new Map(); 
console.log(employees); 
```
`Map {}`

</br>

## **Modifying Maps**

Add key-values by using the Map’s .set() method 
```js
const employees = new Map(); 

employees.set('james.parkes@udacity.com', {  
    firstName: 'James', 
    lastName: 'Parkes', 
    role: 'Content Developer'  
}); 
employees.set('julia@udacity.com', { 
    firstName: 'Julia', 
    lastName: 'Van Cleve', 
    role: 'Content Developer' 
}); 
employees.set('richard@udacity.com', { 
    firstName: 'Richard', 
    lastName: 'Kalehoff', 
    role: 'Content Developer' 
}); 

console.log(employees); 
```
`Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}`

The .set() method takes two arguments. The first argument is the key, which is used to reference the second argument, the value. 

</br>

**.delete() method.**
```js
employees.delete('julia@udacity.com'); 
employees.delete('richard@udacity.com'); 
console.log(employees); 
```
`Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}`

</br>

Again, similar to Sets, you can use the .clear() method to remove all key-value pairs from the Map. 
```js
employees.clear() 
console.log(employees); 
```
`Map {}`

</br>

**.has() method**
```js
const members = new Map(); 

members.set('Evelyn', 75.68); 
members.set('Liam', 20.16); 
members.set('Sophia', 0); 
members.set('Marcus', 10.25); 

console.log(members.has('Xavier')); 
console.log(members.has('Marcus')); 
```
`false` </br>
`true`

</br>

**.get() method**
```js
console.log(members.get('Evelyn')); 
```
`75.68`

 </br>


# **Looping Through Maps**

You’ve created a Map, added some key-value pairs, and now you want to loop through your Map. Thankfully, you’ve got three different options to choose from: 

1. Step through each key or value using the Map’s default iterator 
2. Loop through each key-value pair using the new for...of loop 
3. Loop through each key-value pair using the Map’s .forEach() method 

</br>

## *1. Using the MapIterator*

Using both the .keys() and .values() methods on a Map will return a new iterator object called MapIterator. You can store that iterator object in a new variable and use .next() to loop through each key or value. Depending on which method you use, will determine if your iterator has access to the Map’s keys or the Map’s values. 
```js
let iteratorObjForKeys = members.keys(); 
iteratorObjForKeys.next(); 
```
`Object {value: 'Evelyn', done: false}`

</br>

Use .next() to the get the next key value. 
```js
iteratorObjForKeys.next(); 
```
`Object {value: 'Liam', done: false}`

</br>

And so on. 
```js
iteratorObjForKeys.next(); 
```
`Object {value: 'Sophia', done: false}`

</br>

On the flipside, use the .values() method to access the Map’s values, and then repeat the same process. 
```js
let iteratorObjForValues = members.values(); 
iteratorObjForValues.next(); 
```
`Object {value: 75.68, done: false}`

</br>


## *2. Using a for...of Loop*

Your second option for looping through a Map is with a for...of loop. 
```js
for (const member of members) { 
  console.log(member); 
} 
```
`['Evelyn', 75.68]` </br>
`['Liam', 20.16]` </br>
`['Sophia', 0]` </br>
`['Marcus', 10.25]`

</br>

However, when you use a for...of loop with a Map, you don’t exactly get back a key or a value. Instead, the key-value pair is split up into an array where the first element is the key and the second element is the value. If only there were a way to fix this? 

```js
const members = new Map(); 
 
members.set('Evelyn', 75.68); 
members.set('Liam', 20.16); 
members.set('Sophia', 0); 
members.set('Marcus', 10.25); 

for (const [key,value] of members) { 
    console.log(key,value); 
} 
```
`prints`</br>
`Evelyn 75.68`</br>
`Liam 20.16`</br>
`Sophia 0`</br>
`Marcus 10.25`</br>

</br>

## *3. Using a forEach Loop*

Your last option for looping through a Map is with the .forEach() method. 

```js
members.forEach((key, value) => console.log(key, value)); 
```
`'Evelyn' 75.68` </br>
`'Liam' 20.16` </br>
`'Sophia' 0` </br>
`'Marcus' 10.25`

Notice how with the help of an arrow function, the forEach loop reads fairly straightforward. For each value and key in members, log the value and key to the console.


</br>











# **WeakMap**

A WeakMap is just like a normal Map with a few key differences:

- a WeakMap can only contain objects as keys, 
- a WeakMap is not iterable which means it can’t be looped and 
- a WeakMap does not have a .clear() method. 

You can create a WeakMap just like you would a normal Map, except that you use the WeakMap constructor:

```js
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' }; 
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' }; 
const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' }; 

const library = new WeakMap(); 
library.set(book1, true); 
library.set(book2, false); 
library.set(book3, true); 

console.log(library); 
```
`WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}`

</br>

…but if you try to add something other than an object as a key, you’ll get an error! 
```js
library.set('The Grapes of Wrath', false); 
```
`Uncaught TypeError: Invalid value used as weak map key(…)`

</br> 

## **Garbage Collection**

In JavaScript, memory is allocated when new values are created and is "automatically" freed up when those values are no longer needed. 
```js
book1 = null; 
console.log(library); 
```
`WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}`

</br>

</br>











# **Promises**

A promise will let you start some work that will be done asynchronously and let you get back to your regular work.  

```js
new Promise(function () { 
    window.setTimeout(function createSundae(flavor = 'chocolate') { 
        const sundae = {}; 
        // request ice cream 
        // get cone 
        // warm up ice cream scoop 
        // scoop generous portion into cone! 
    }, Math.random() * 2000); 
}); 
```

This code creates a promise that will start in a few seconds after I make the request. Then there are a number of steps that need to be made in the createSundae function. 

</br>

## **Indicated a Successful Request or a Failed Request**

But once that's all done, how does JavaScript notify us that it's finished and ready for us to pick back up? It does that by passing two functions into our initial function. Typically we call these `resolve` and `reject`. 

</br>

_Resolve_
 
`resolve` is used to indicate that this function should be called when the request completes successfully. 
```js
new Promise(function (resolve, reject) { 
    window.setTimeout(function createSundae(flavor = 'chocolate') { 
        const sundae = {}; 
        // request ice cream 
        // get cone 
        // warm up ice cream scoop 
        // scoop generous portion into cone! 
        resolve(sundae); 
    }, Math.random() * 2000); 
}); 
```
Now when the sundae has been successfully created, it calls the resolve method and passes it the data we want to return - in this case the data that's being returned is the completed sundae. So the resolve method is used to indicate that the request is complete and that it completed successfully. 

</br>

_ReJect_

 `reject` to indicate that this function should be used if the request fails for some reason. Check out the reject on the first line: 

```js
new Promise(function (resolve, reject) { 
    window.setTimeout(function createSundae(flavor = 'chocolate') { 
        const sundae = {}; 
        // request ice cream 
        // get cone 
        // warm up ice cream scoop 
        // scoop generous portion into cone! 
        if ( /* iceCreamConeIsEmpty(flavor) */ ) { 
            reject(`Sorry, we're out of that flavor :-(`); 
        } 
        resolve(sundae); 
    }, Math.random() * 2000); 
}); 
```
So the reject method is used when the request could not be completed. Notice that even though the request fails, we can still return data - in this case we're just returning text that says we don't have the desired ice cream flavor.  

A Promise constructor takes a function that will run and then, after some amount of time, will either complete successfully (using the resolve method) or unsuccessfully (using the reject method). When the outcome has been finalized (the request has either completed successfully or unsuccessfully), the promise is now fulfilled and will notify us so we can decide what to do with the response. 

</br>

## **Promises Return Immediately**

The first thing to understand is that a Promise will immediately return an object. 
```js
const myPromiseObj = new Promise(function (resolve, reject) { 
    // sundae creation code 
}); 
```

That object has a .then() method on it that we can use to have it notify us if the request we made in the promise was either successful or failed. The .then() method takes two functions: 

1. the function to run if the request completed successfully 
2. the function to run if the request failed to complete 

```js
mySundae.then(function(sundae) { 
    console.log(`Time to eat my delicious ${sundae}`); 
}, function(msg) { 
    console.log(msg); 
    self.goCry(); // not a real method 
});
```

As you can see, the first function that's passed to .then() will be called and passed the data that the Promise's resolve function used. In this case, the function would receive the sundae object. The second function will be called and passed the data that the Promise's reject function was called with. In this case, the function receives the error message "Sorry, we're out of that flavor :-(" that the reject function was called with in the Promise code above. 

</br>

</br>











# **Proxy**

To create a proxy object, we use the Proxy constructor - `new Proxy();`. The proxy constructor takes two items: 
- the object that it will be the proxy for 

- an object containing the list of methods it will handle for the proxied object 

The second object is called the `handler` 

</br>

## **A Pass Through Proxy**

The simplest way to create a proxy is to provide an object and then an empty handler object. 
```js
var richard = {status: 'looking for work'}; 
var agent = new Proxy(richard, {}); 

agent.status; // returns 'looking for work' 
```
The above doesn't actually do anything special with the proxy - it just passes the request directly to the source object! If we want the proxy object to actually intercept the request, that's what the handler object is for! 

The key to making Proxies useful is the handler object that's passed as the second object to the Proxy constructor. The handler object is made up of a methods that will be used for property access. Let's look at the get:  

</br>

## **Get Trap**

The get trap is used to "intercept" calls to properties: 
```js
const richard = {status: 'looking for work'}; 
const handler = { 
    get(target, propName) { 
        console.log(target); // the `richard` object, not `handler` and not `agent` 
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking 
    } 
}; 
const agent = new Proxy(richard, handler); 
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`) 
```
In the code above, the handler object has a get method (called a "trap" since it's being used in a Proxy).  

</br>

## **Accessing the Target object from inside the proxy**

If we wanted to actually provide the real result, we would need to return the property on the target object: 
```js
const richard = {status: 'looking for work'}; 
const handler = { 
    get(target, propName) { 
        console.log(target); 
        console.log(propName); 
        return target[propName]; 
    } 
}; 
const agent = new Proxy(richard, handler); 
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status 
```

We added the return target[propName]; as the last line of the get trap. Accessing the property on the target object and will return it. 

</br>
 
Having the proxy return info, directly 

Alternatively, we could use the proxy to provide direct feedback: 
```js
const richard = {status: 'looking for work'}; 
const handler = { 
    get(target, propName) { 
        return `He's following many leads, so you should offer a contract as soon as possible!`; 
    } 
}; 
const agent = new Proxy(richard, handler); 
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!` 
```
With this code, the Proxy doesn't even check the target object, it just directly responds to the calling code. 

</br>

So the get trap will take over whenever any property on the proxy is accessed. If we want to intercept calls to changeproperties, then the set trap needs to be used! 

The set trap is used for intercepting code that will change a property. The set trap receives: the object it proxies the property that is being set the new value for the proxy 
```js
const richard = {status: 'looking for work'}; 
const handler = { 
    set(target, propName, value) { 
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission 
            value = value * 0.85; 
        } 
        target[propName] = value; 
    } 
}; 
const agent = new Proxy(richard, handler); 
agent.payRate = 1000; // set the actor's pay to $1,000 
agent.payRate; // $850 the actor's actual pay 
```
In the code above, notice that the set trap checks to see if the payRate property is being set. If it is, then the proxy (the agent) takes 15 percent off the top for her own commission! Then, when the actor's pay is set to one thousand dollars, since the payRate property was used, the code took 15% off the top and set the actual payRate property to 850; 

</br>

## **Other Traps**

A total of 13 different traps that can be used in a handler! 

1. the get trap - lets the proxy handle calls to property access
2. the set trap - lets the proxy handle setting the property to a new value 
3. the apply trap - lets the proxy handle being invoked (the object being proxied is a function) 
4. the has trap - lets the proxy handle the using in operator 
5. the deleteProperty trap - lets the proxy handle if a property is deleted 
6. the ownKeys trap - lets the proxy handle when all keys are requested 
7. the construct trap - lets the proxy handle when the proxy is used with the new keyword as a constructor 
8. the defineProperty trap - lets the proxy handle when defineProperty is used to create a new property on the object 
9. the getOwnPropertyDescriptor trap - lets the proxy handle getting the property's descriptors 
10. the preventExtenions trap - lets the proxy handle calls to Object.preventExtensions() on the proxy object 
11. the isExtensible trap - lets the proxy handle calls to Object.isExtensible on the proxy object 
12. the getPrototypeOf trap - lets the proxy handle calls to Object.getPrototypeOf on the proxy object 
13. the setPrototypeOf trap - lets the proxy handle calls to Object.setPrototypeOf on the proxy object 

As you can see, there are a lot of traps that let the proxy manage how it handles calls back and forth to the proxied object. 

</br>

## **Proxy  Recap**

A proxy object sits between a real object and the calling code. The calling code interacts with the proxy instead of the real object. To create a proxy: 

- use the new Proxy() constructor 
    - pass the object being proxied as the first item 
    - the second object is a handler object 
- the handler object is made up of 1 of 13 different "traps" 
- a trap is a function that will intercept calls to properties let you run code 
- if a trap is not defined, the default behavior is sent to the target object 

Proxies are a powerful new way to create and manage the interactions between objects. 


</br>










# **Generators**

Whenever a function is invoked, the JavaScript engine starts at the top of the function and runs every line of code until it gets to the bottom. There's no way to stop the execution of the function in the middle and pick up again at some later point. This "run-to-completion" is the way it's always been:
```js
function getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
    }

    console.log('the function has ended');
}

getEmployee();
```

`the function has started` </br>
`Amanda` </br>
`Diego` </br>
`Farrin` </br>
`James` </br>
`Kagure` </br>
`Kavita` </br>
`Orit` </br>
`Richard` </br>
`the function has ended` 

But what if you want to print out the first 3 employee names then stop for a bit, then, at some later point, you want to continue where you left off and print out more employee names. With a regular function, you can't do this since there's no way to "pause" a function in the middle of its execution.

</br>

## **Pausable Functions**
If we do want to be able to pause a function mid-execution, then we'll need a new type of function available to us in ES6 - generator functions! Let's look at one:
```js
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log( name );
    }

    console.log('the function has ended');
}
```
Notice the asterisk (i.e. *) right after the function keyword? That asterisk indicates that this function is actually a generator!

Now check out what happens when we try running this function:
```js
getEmployee();
```
`getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}`

</br>

## **Generators & Iterators**

When a generator is invoked, it doesn't actually run any of the code inside the function. Instead, it creates and returns an iterator. This iterator can then be used to execute the actual generator's inner code.
```js
const generatorIterator = getEmployee();
generatorIterator.next();
```
`the function has started` </br>
`Amanda` </br>
`Diego` </br>
`Farrin` </br>
`James` </br>
`Kagure` </br>
`Kavita` </br>
`Orit` </br>
`Richard` </br>
`the function has ended` 

</br>
Now if you tried the code out for yourself, the first time the iterator's .next() method was called it ran all of the code inside the generator. Did you notice anything? The code never paused! So how do we get this magical, pausing functionality?

</br>

## **The Yield Keyword**
The yield keyword is new and was introduced with ES6. It can only be used inside generator functions. yield is what causes the generator to pause. Let's add yield to our generator and give it a try:
```js
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
        yield;
    }

    console.log('the function has ended');
}
```
Notice that there's now a yield inside the for...of loop. If we invoke the generator (which produces an iterator) and then call .next(), we'll get the following output:
```js
const generatorIterator = getEmployee();
generatorIterator.next();
```
`the function has started`</br>
`Amanda`

It's paused! But to really be sure, let's check out the next iteration:
```js
generatorIterator.next();
```
`Diego`

So it remembered exactly where we left off! It took the next item in the array (Diego), logged it, and then hit the yield again, so it paused again.

</br>

Now pausing is all well and good, but what if we could send data from the generator back to the "outside" world? We can do this with yield.

## **Yielding Data to the "Outside" World**
Instead of logging the names to the console and then pausing, let's have the code "return" the name and then pause.
```js
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        yield name;
    }

    console.log('the function has ended');
}
```
Notice that now instead of `console.log(name);` that it's been switched to `yield name;`. With this change, when the generator is run, it will "yield" the name back out to the function and then pause its execution. Let's see this in action:
```js
const generatorIterator = getEmployee();
let result = generatorIterator.next();
result.value // is "Amanda"

generatorIterator.next().value // is "Diego"
generatorIterator.next().value // is "Farrin"
```

</br>

## **Sending Data into/out of a Generator** 
So we can get data out of a generator by using the yield keyword. We can also send data back into the generator, too. We do this using the .next() method:
```js
function* displayResponse() {
    const response = yield;
    console.log(`Your response is "${response}"!`);
}

const iterator = displayResponse();

iterator.next(); // starts running the generator function
iterator.next('Hello Udacity Student'); // send data into the generator
// the line above logs to the console: Your response is "Hello Udacity Student"!
```
Calling .next() with data (i.e. .next('Richard')) will send data into the generator function where it last left off. It will "replace" the yield keyword with the data that you provided.

So the yield keyword is used to pause a generator and used to send data outside of the generator, and then the .next() method is used to pass data into the generator. Here's an example that makes use of both of these to cycle through a list of names one at a time:
```js
function* getEmployee() {
    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
    const facts = [];

    for (const name of names) {
        // yield *out* each name AND store the returned data into the facts array
        facts.push(yield name); 
    }

    return facts;
}

const generatorIterator = getEmployee();

// get the first name out of the generator
let name = generatorIterator.next().value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is cool!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is awesome!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is stupendous!`).value; 

// you get the idea
name = generatorIterator.next(`${name} is rad!`).value; 
name = generatorIterator.next(`${name} is impressive!`).value;
name = generatorIterator.next(`${name} is stunning!`).value;
name = generatorIterator.next(`${name} is awe-inspiring!`).value;

// pass the last data in, generator ends and returns the array
const positions = generatorIterator.next(`${name} is magnificent!`).value; 

// displays each name with description on its own line
positions.join('\n');
```
`Amanda is cool!` </br>
`Diego is awesome!` </br>
`Farrin is stupendous!` </br>
`James is rad!` </br>
`Kagure is impressive!` </br>
`Kavita is stunning!` </br>
`Orit is awe-inspiring!` </br>
`Richard is magnificent!` 
