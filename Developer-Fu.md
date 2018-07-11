---
title: JS Notes Developer-Fu
---

# ***Developer-Fus***

# **How Can You Know What Features Browsers Support? **

Platform feature updates: 
- Google Chrome - https://www.chromestatus.com/features#ES6 
- Microsoft Edge - https://developer.microsoft.com/en-us/microsoft-edge/platform/status/?q=ES6 
- Mozilla Firefox - https://platform-status.mozilla.org/ 
- Safari is powered by the open source browser engine, Webkit. Webkit features status - here. 
- The status of all ES6 features supported by your current browser - http://kangax.github.io/compat-table/es6/ 

</br>





# **Polyfill**

A polyfill, or polyfiller, is a piece of code (or plugin) that provides the technology that you, the developer, expect the browser to provide natively.

https://en.wikipedia.org/wiki/Polyfill

An example polyfill
The code below is a polyfill for the new ES6 String method, startsWith():
```js
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (searchString, position) {
    position = position || 0;
    return this.substr(position, searchString.length) === searchString;
  };
}

'Udacity'.startsWith('Udac'); //returns 'true'
'Udacity'.startsWith('Udac', 2); //returns 'false'
'Udacity'.startsWith('ES6'); //returns 'false'
```
As you can see, a polyfill is just regular JavaScript.

This code is a simple polyfill (check it out on MDN), but there's also a significantly more robust one, [here](https://github.com/mathiasbynens/String.prototype.startsWith/blob/master/startswith.js)

</br>

## **Polyfills aren't only for patching missing JavaScript features**
JavaScript is the language used to create a polyfill, but a polyfill doesn't just patch up missing JavaScript features! There are polyfills for all sorts of browser features:

- SVG
- Canvas
- Web Storage (local storage / session storage)
- Video
- HTML5 elements
- Accessibility
- Web Sockets
- and many more!

For a more-complete list of polyfills, check out this [link](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)

</br>







# **Tranfiling**

- Compiler- takes source language turns it into lower level language 
- Transpiler- takes source  code turns it into target code(human readable - human readable) 

</br>

## **Babel**

The most popular JavaScript transpiler is called Babel. 
Babel converts ES6 to ES5, JSX to JavaScript, and Flow to JavaScript. 
Check out [Babel's REPL](http://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015) and paste the following code into the section on the left: 

```js
class Student {
  constructor (name, major) {
    this.name = name;
    this.major = major;
  }

  displayInfo() {
    console.log(`${this.name} is a ${this.major} student.`);
  }
}

const richard = new Student('Richard', 'Music');
const james = new Student('James', 'Electrical Engineering');
```
</br>

![This is babel's JS output from ES6 to ES5](https://d17h27t6h515a5.cloudfront.net/topher/2017/January/5888fc24_babel-es6-to-es5/babel-es6-to-es5.png)

</br>

## **Transpiling project in repo**

If you check in the repo for this project, inside the Lesson 4 directory is a little project that's all set up for transpiling ES6 code to ES5 code.  


 

The way Babel transforms code from one language to another is through plugins. (the ES2015 arrow function plugin)(the ES2015 template literals transform). For a full list, check out all of Babel's plugins. 

Babel has presets which are groups of plugins bundled together- ES2015 preset  

 

You can see that the project has a .babelrc file. This is where you'd put all of the plugins and/or presets that the project will use. Since we want to convert all ES6 code, we've set it up so that it has the ES2015 preset. 


Code editor with .babelrc file that has ES2015 preset listed. 

 

Transpiling Walkthrough 

From <https://classroom.udacity.com/nanodegrees/nd001/parts/9e34624d-cdc8-4cd7-9d7e-78943413e645/modules/2fc0e696-4879-47f6-afeb-48730cd8fb1e/lessons/2baa2512-b298-4796-aa5a-9135d82ff298/concepts/b91e41ba-c30a-4772-868a-e57dd96e0684>  

 

 