<!-- 
Project name: Personal TypeScript revision notes

Author: Dut Kulang

Email: dutandrew78@gmail.com

GitHub: https://github.com/dutkulang

Resources used: [
      [Book] Learning TypeScript by Josh Goldberg 2022
      [Book] Effective TypeScript by Dan Vanderkam

      [YouTube video] TypeScript full course for beginners by Dave Gray teaches code
]
Copyrights: This material is under the copyleft GNU licence
 -->
## TypeScript
TypeScript is a superset of JavaScript that enforces the use of types at development time.

`Valid TypeScript is valid JavaScript`

_TypeScript_ is a strongly typed language. This means that you **MUST** specify the type of data that will be dealt with by the program.

It is also a statically typed language. This means that types are checked at _compile time_.

This means that the compiler will check the value to match if it corresponses with that specified.

```ts
// let variable_name: data_type = value;
// const variable_name: data_type = value;

let myName: string = "Dut Andrew Kulang";
const myAge: number = 23;
```

Other languages like Python, JavaScript, ruby are loosely or weakly typed langauges, they do not require data type specification and are also dynamically typed, a variable can be of type `int` and yet some where down the code change to store a `string` this sudden change can bring in bugs into software and that is what typescript tries to solve.

## Benefits of using TypeScript

- Code kind of self documents it'self.

- Bugs are quickly spotted during development.

- Good of teams to use

```ts
// TypeScript example code

let myName = "Dut"
// TypeScript will infer that myName is a string
// TypeScript on it's own concludes that myName is a string
// because myName's type was not specified

let otherName: string = "Dut Kulang"
// OtherName stores 'string type' values

otherName = 23
// will throw an error saying 23 is not of type string
```

### Define type with no value

```ts
// Defining variable types without values

// Using let
let bestLanguage: string;
bestLanguage = "Python"
bestLanguage = "TypeScript"

// Using const
const favoriteNumber: number;
favoriteNumber = 23

// Because we are using const re-assignment of
// favoriteNumber would cause compiler error
```

### TypeScript data types

 - number
 - string
 - boolean
 - any (when a variable can data of any type)
 - Union type ( | )

```ts
// data types in TypeScript

let aNumber: number = 78

let aString: string = "Hello, codes"

let aBooloean: boolean = true

let canBeAnyThing: any = 1234
canBeAnyThing = "hahahahahaha"
canBeAnyThing = false

let myUnion: string | number;
// myUnion can store values of either string or number type

myUnion = 23
myUnion = "Am TypeScript"

let isActive: booloean | number;
isActive = true
isActive = 1

let re: RegExp;
re = /\w+/g
```

### functions in TypeScript

You can specify when type parameters of fuction will be

Also the function's return type

```ts
const sum = (a: number, b: number) => {
      return a + b
}

let greet = (firstName: string, isPremium: boolean) => {
    if (isPremium){
       return `${firstName} is a Premium user.`
    } else {
      return `${firstName} is a regular user.`
}
```

### array

```ts
let stringArr: string[] = ["Python", "PHP", "JavaScript"]
let aPerson: (string | boolean | number)[];
aPerson = ["Dut", true, 23]
```

## Kinds of errors

- Syntax Errors

      This type of error blocks TypeScript code from 
      being converted to JavaScript.

      TypeScript detects incorrect syntax that it can 
      not understand as code hence blocking the proper 
      generation of JavaScript.

- Type errors

      Something mismatched has been detected by the type checker.

      They occur when your syntax is 
      valid but TypeScript type checker has detected an error 
      with the program's type, however, this type of error does
      not block TypeScript syntax from being converted to JavaScript.
      But it is an indication that something will crash or behave 
      unexpectedly if you code is allowed to run. 

## Assignability

TypeScript reads variables’ initial values to determine what type those variables are allowed to be.

If it later sees an assignment of a new value to that variable, it will
check if that new value’s type is the same as the variable’s.

TypeScript is fine with later assigning a different value of the same type to a variable. If a variable is, say, initially a string value, later assigning it another string would be fine.

```ts
let firstName = "Carole";
firstName = "Joan";
```

If TypeScript sees an assignment of a different type, it will give us a type error. We couldn’t, say, initially declare a variable with a string value and then later on put in a boolean.
```ts
let lastName = "King";
lastName = true;
// Error: Type 'boolean' is not assignable to type 'string'.
```

TypeScript’s checking of whether a value is allowed to be provided to a function call or variable is called `assignability` whether that value is `assignable` to the expected type it’s passed to.


### Installation

You will need to have node installed on your computer inorder to use node's package manager `npm` to install TypeScript

__NPM__ is NOT node package manager. It anything else but not node package manager
```sh
npm i -g typescript
```
Check what TypeScript version is available
```sh
tsc --version
```
make your working directory and initialize typescript in it
```sh
# 1. make directory and move into the directory
mkdir -pv ~/js/typescript && cd js/typescript
```
Create TypeScript config file `tsconfig.json` which will be used to configure TypeScript
```sh
# 2. initialize typescript
tsc --init
```
Compile a typeScript `.ts` file to JavaScript
```sh
tsc main.ts
```
you don't have to specify the output file because by default typeScript will create a JavaScript file with the same name as the typescript file but with a different file extension `.js`

Use the `-w` watch flag to watch for changes in our file and auto-compile to JavaScript

NB replace file_name.ts with your TypeScript file name

```bash
tsc file_name.ts -w
```
OR
watch all TypeScript files and compile them
```sh
tsc -w
```

#### set configurations

inside tsconfig.json 

`"rootDir":` ==> here you specify where your TS file will be in

`"outDir":` ==> specifies which folder  TypeScript will output compiled js files

`"target":` ==> this specifies what JavaScript standard TypeScript should use in compiling your code like es5,es2015,es2016

`"noEmitOnError": true` ==> This disables typeScript default behaviour of compiling even when there is an erro. This setting makes sure TypeScript compiles when your code is error free. 