---
layout: post
title: Export a Class from a Module in Nodejs 6
description: This article aims to be a very short and simple introduction to exporting classes from modules when using the new ECMAScript-6 standard in Node.js version 6.
             To keep it simple, we have organized it into 2 sections. In the first section we create a class with some functions and we add the statement to export the class.
             In the second section, we simply write the code to use that class.
category: blog
---

#Introduction

ECMAScript-6 introduces a new way of defining classes in javascript or nodejs which closely resembles
the way classes are defined in other class based OOP languages like JAVA, Python, C++ etc.
However it's just a syntactical sugar and behind the scenes javascript still has no concept of classes the way they are in class based languages.
This article aims to be a very short and simple introduction to exporting classes from modules when using the new ECMAScript-6 standard in Node.js version 6.
To keep it simple, we have organized it into 2 sections. In the first section we create a class with some functions and we add the statement to export the class.
In the second section, we simply write the code to use that class.
ECMAScript-6 

Let's Get Started with Code.

#Step-1 Create a Class File & Export it
Create a file with the name Ganit.js and add the following code to it.

```javascript
// index.js
"use strict"

class Ganit{
	constructor(x,y) {
		this.x = x;
		this.y = y;
	}
	add(){
		return this.x + this.y;
	}
	subtract(){
		return this.x - this.y;
	}
	multiply(){
		return this.x * this.y;
	}
	divide(){
		return this.x / this.y
	}
	remainder(){
		return this.x % this.y
	}
}
module.exports = Ganit
```

Note the ECMAScript6 features being utilized while writing the above code. It's tested to work fine in Node v6.4.0

#Step-2 Import the file and use it!
Create another file Test.js	in the same directory as above and add following code to it.

```javascript
// Test.js
"use strict";
var Ganit = require('./Ganit.js');

var calc = new Ganit(3,4);

console.log("addition of operands is: " + calc.add());
console.log("subtraction of operands is: " + calc.subtract());
console.log("multiplication of operands is: " + calc.multiply());
console.log("quotient on dividing operands is: " + calc.divide());
console.log("remainder on dividing operands is: " + calc.remainder());
```

On executing the file Test.js . We get the following output.

$node Test.js

* addition of operands is: 7
* subtraction of operands is: -1
* multiplication of operands is: 12
* quotient on dividing operands is: 0.75
* remainder on dividing operands is: 3

