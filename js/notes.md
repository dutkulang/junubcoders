# Introduction JavaScript

# _JavaScript programming language_
<!-- 
JavaScript from beginner to professional

 -->
JavaScript is a single threaded, synchronous programming language.<br>Developed by Brandon Eich at NetScape (now mozilla) in 1995 in just 10 days.

`single-threaded:` meaning that it can only perform a single operation at a single time/sequence/thread from top to bottom.

This model is used to avoid complexities and conflicts that can araise from multithreading, such as a race conditions.

`synchronous:` meaning it can process instruction one at a time, waiting for each operation to complete before moving on to the next.

This ensures that the code executes in a predictable and ordered manner.

__Indepth__

When a javascript code is executed, a global execution context is created, it consists of 
	
1. __The memory component (variable environment)__<br>
	- Variables and functions are allocated memory and stored as key-value pairs.
	- is a skim through process

2. __The code component (thread of execution)__<br>
	- code is executed one line at a time

### Excution also happens in two phases.
	
1. __memory allocation phase__
	* This happens inside the memory component of execution.

	* In this phase the js engine skims through the file
	and allocates memory to all variables and functions.

	* Data (variables & functions) is stored as _key-value_.

	* All variables get __`undefined`__ as a default value
	while functions get their body code block as their value.
	This phase is what causes *hoisting*.
	
2. __excution phase__
	* This happens inside the code component of execution.
	* In this phase variables are now allocated the defined values.
	* And executions starts from top to bottom.
	* If a function call is encountered, the the program pauses
	and creates another execution context to handle the function.<br>
	During which phase 1 & 2 of the execution context are repeated.

## Hoisting

This is a process unquie to the javaScript language.<br>
It allows variables and functions to be used at the top of a js file even when declarion is at the bottom of the file.

Hoisting is possible due to the 1st phase of the execution in which functions and variables are allocated memory.

```js
// hoisting

greet() // Am a greet function
console.log(my_name); // undefined but no error

function greet(){
	console.log("Am a greet function");
}
var my_name = "Dut Kulang"
```

__<u>REMEMBER</u>__<br>
* Hoisting is possible ONLY on pure functions. Functions declared using the function keyword.

```js
// pure function are hoisted

square();
greet();
allStudents();

function square(num1, num2){
	return num1 + num2;
}

function greet(name){
	return `Hey ${name}!!`
}

function allStudents(...names){
...
}
```

* arrow functions & nameless functions are _NEVER_ hoisted, they are treated as normal variables therefore during phase 1 will be undefined 

```js
// will be treated as normal fvariables

greet() // undefined
square() // undefined

let greet = () => {
	...
}
const square = function (num1, num2){
	...
}
```
### Closures


### Variables

variables in JS have a <u>__lexical__</u> scope (static scope) meaning that variables are binded to specific locations in the source code.<br>

Variables are scoped to the function they are declared within. 

This means that a variable's scope is determined by the location of its declaration in code, not by where it is used or invoked. 

Variables are a way to represent value in code.

```js
let name = "Dut Kulang";
console.log(`My name is ${name}, I love JavaScript`);
```

### **let, var & const**

`let` - variables declared using let are accessible only the code block in which they are defined in. An code block starts from `{` and ends at `}`.

```js
function greet(name){
	console.log(`Greetings ${name} from greet function`)
	function bye(){
		//message is only accessible inside the bye '{ block }'
		let message = "Bye";
		console.log(message);
	}
	bye();
	console.log(message); // throws an error
}
greet
```

`var` - var defined variables are accessile globally in the script file, hence saying that var gives variables a global scope.

<!-- var only respects the function block scope but not a loop block scope -->

```js
var topic = "JavaScript";
if (topic) {
	// over-writes the global value of topic
	var topic = "React";
	console.log("block", topic); // block React
}
console.log("global", topic); // global Reac
```

`const` - when a avariable is defined by the const keyword, it missing that that the value assigned to the variable will `NOT` change.

Use const when you have no future intensions of changing the changing the variable value.

```js
const favorite_language = "JavaScript";
favorite_language = "Python"; // will throw an error
```



### Rest function in JS

A rest function is a function that takes in an limited
number of arguments.

```js
#!/usr/bin/node

function sum(x, ...y){
    console.log(x);
    console.log(y);
}

```

---
rest array is denoted by 3 dots `...` before the argument name, it MUST be the last argument passed to a function 

# map, filter & reduce

`[].map(function)` works by passing every element in the <br>array through function parameter as arguments one  <br> by one and returns a new arraywith the transformed values.

`example 1`
```js
// file name: double_array.js

// double every element in the array
const my_array = [2,3,4,5,6,7];

function double(num){
    return num * 2;
} 

const output = my_array.map(double);
console.log(output);
```
```sh
node double_array.js

[4, 6, 8, 10, 12, 14];
```
<hr>

`example 2`

```js
// file name: square_numbers.js

const numbers = [2, 3, 4, 5, 6, 7, 10, 12];
const output = numbers.map(num => num * num);
console.log(output);
```

```sh
node square_numbers.js
[
   4,  9,  16,  25,
  36, 49, 100, 144
]
```

`example 3`

```js
// file name: to_binary.js
// convert all array elements to binary

const numbers = [2, 3, 4, 5, 6, 7, 10, 12];
const output = numbers.map(num => num.toString(2));
console.log(output);
```
```sh
node to_binary.js
[
  '10',   '11',
  '100',  '101',
  '110',  '111',
  '1010', '1100'
]
```
`example 4`

```js
// file name: times_ten.js
// multiple every element by 10

const numbers = [1, 2, 3, 4, 5, 6, 7];
const output = numbers.map(num => num * 10);
console.log(output)
```
```sh
node times_ten.js

[
  10, 20, 30, 40,
  50, 60, 70
]

```

```js
// file name: greetings.js
// greet every student in the array
const students = ['Dut', 'Denaya', 'Vuga', 'Timm'];
console.log(students.map(student => `Hey ${student}`));
```
```sh
node greetings.js

[ 'Hey Dut', 'Hey Denaya', 'Hey Vuga', 'Hey Timm' ]
```
## filter
`[].filter(function)` this is a function that filters out the elements from the array by passing them through a function and returns only elements that passed the filter check (elements that returned true value).

`example 1`

```js
// file name: isOdd.js
// array of only odd numbers, filter out even numbers

const my_numbers =  [13, 11, 10, 12, 111, 37,32, 61, 98];

const output = my_numbers.filter(num => num % 2 === 1 );
console.log(output)
```

```sh
node is
[ 13, 11, 111, 37, 61 ]
```
<hr>

`example 2`




# Document Object Model (DOM) Manipulation
 
The Document Object Model is an API (Application Programming Interface) for manipulating
HTML documents.

The DOM provides functions that allow you to add, remove, and modify parts of the document
effectively.

It represents an HTML document as a tree of nodes.

`nodes`: refers to elements or text with in an HTML document.

#### Example of nodes / elements:
- Element type nodes

    `<html> </html>`, `<!DOCTYPE html>`, `<body></body>`, `<p></p>`, `<img>`, `<a></a>`
    
- Text nodes
    
    text enclosed in an element is also a node.

- comment nodes

    `<!-- some html comment -->`

## Node relationships

Any node has relationships to other nodes in the DOM tree, and it is same as described in the traditional family tree

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <!-- Some comment -->
        <p>Am a inside a paragraph element </p>
    </body>
</html>
```

- `<html>` node is the parent node of `<head>`,`<body>` nodes.

- `<head>` & `<body>` nodes are sibling nodes to each other the share the same parent `<html>` element.

- `<body>` is the parent node of `<!-- some comment -->` and `<p>` make these two elements siblings to one another.


```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <p>Am the first child paragraph</p>
            <p>Am the second child paragraph</p>
            <p>Am the third child paragraph</p>
            <p>Am the forth child paragraph</p>
            <p>Am the fifth and last child paragraph</p>
        </div>
    </body>
</html>
```

`<p>` nodes are children nodes of the `<div>` node.

## Selecting elements

The DOM provides several methods for selecting elements from an HTML document.

1. getElementById()

```js
getElementById('element Id')
```
returns an element object that represents an HTML element with the specified Id and `null` if no element in the HTML document has the Id. If multiple elements have the same id, then the method returns only the first element with the specified Id.

This method is only available on the document object.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <p id="creationDay">Did know that JavaScript was intially created in 10 days</p>
        </div>
        
        <script>
            let message = document.getElementById('creationDay');
            console.log(message);
        </script>
    </body>
</html>
```

2. getElementsByName()

Elements on an HTML document can have the same `name` value, the DOM provides a way to select these elements with the same name values.

It returns a list of nodes.

```js
getElementsByName("Element Name")
```

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <input type="radio" name="language", value="JS">
            <input type="radio" name="language", value="python">
            <input type="radio" name="language", value="C">
            <input type="radio" name="language", value="C++">
        </div>
        
        <script>
            let btns = document.getElementsByName('language');
            console.log(btns);
        </script>
    </body>
</html>
```

3. getElementsByTagName()

This method accepts a tag name and returns a live HTML Collection of elements.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <h1>first heading</h1>
            <h1>Second heading</h1>
            <h1>third heading</h1>
            <h1>Fourth heading</h1>
        </div>
        
        <script>
            let heading = document.getElementsByTagName('h1');
            console.log(heading);
        </script>
    </body>
</html>
```

4. getElementsByClassName()

This method returns an array-like of the objects of the child elements with a specified class name.

This method is avialable on the document element or any other element also.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <h1 class="message">first heading</h1>
            <h1 class="message">Second heading</h1>
            <div id="container">
                <h1 class="message">third heading</h1>
                <h1 class="message">Fourth heading</h1>
            </div>
        </div>
        
        <script>
            // using the document object
            let msg = document.getElementsByClassName('message');
            console.log(msg);

            // using normal element
            // first find the parent container then get all
            // elements with the container that match the
            // specified class name

            let container = document.getElementById('container');
            let container_msg = container.getElementsByClassName('message');
            console.log(container_msg);
        </script>
    </body>
</html>
```

5. querySelector()

`querySelector('CSS query selector')`

`querySelector('h1')`, `querySelector('.message')`
this method allows selection of the first element that matches one or more CSS selectors.

It is also accessable on other element.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <h1 class="message">first heading</h1>
            <h1 class="message">Second heading</h1>
            <div id="container">
                <h1 class="message">third heading</h1>
                <h1 class="message">Fourth heading</h1>
            </div>
        </div>
        
        <script>
            // only return the first element with the CSS
            let msg = document.querySelector('.message');            
            console.log(msg);
        </script>
    </body>
</html>
```

6. querySelectorAll()

Similar to `querySelector()` but this method allows selection of the all elements that matches one or more CSS selectors.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Junub coders</title>
    </head>
    <body>
        <div>
            <h1 class="message">first heading</h1>
            <h1 class="message">Second heading</h1>
            <h1 class="message">third heading</h1>
            <h1 class="message">Fourth heading</h1>
        </div>
        
        <script>
            // only return the first element with the CSS
            let msgs = document.querySelectorAll('.message');            
            console.log(msgs); // all elements with .message class name
        </script>
    </body>
</html>
```
## Traversing elements

1. selecting parent element
2. selecting child element
3. Selecting Sibling elements

## Manipulating HTML elements

1. createElement()
2. appendChild()
3. textContent()
4. innerHTML
5. after()
6. append()
7. preprend()
8. insertAdjacentHTML()
9. replaceChild()
10. cloneNode()
11. removeChild()
12. insertBefore()

## Attribute methods
 
1. getAttribute()
2. setAttribute()
3. hasAttribute()
4. removeAttribute()

## Manipulating Element's style

1. style property
2. cssText
3. getComputedStyle()
4. ClassName property
5. ClassList property

## JavaScript Events

1. What is an event
2. Event bubbling & Event Capture
3. Event handler in HTML Attributes
4. DOM level 0 event handlers
5. addEventListener()
6. removeEventListener()
7. Event Objects
8. Different Types of Events





