# React JS
<!-- Resources

- Namaste react (video)
- The Road to react (PDF book)

 -->
React is a JavaScript UI library. It uses a component based structure i.e parts of the UI are broken down as components.

React is very good at DOM manipulation that's why it is the best UI library.
It uses a reconciliation algorithm (react fibre)
[read more](https://github.com/acdlite/react-fiber-architecture)

### setup

1. Download nodejs

2. Use vite bundler to create react project

```sh
npm create vite@latest

# project_name
# choose React
# choose vanilla JavaScript
```
3.change into your project directory 
```sh
cd project_name
```
4. Install dependencies. This process takes sometime (minutes) to complete

```sh
npm install
```
OR
```sh
npm i
```
**NPM** does <u>NOT</u> stand for Node Package Manager. It is any word but not node package manager

4. run development server
```sh
npm run dev
```
### File structure
```sh
#file structure

project_name/
        index.html
        node_modules
        package.json
        package-lock.json
        src/
        |---- App.jsx
        |---- assets/
                |---- logos.png
        |---- main.jsx
        |---- style.css
        |---- public/
                |---- vite.svg
        |---- README.md  
```
- `index.html`: This is the entry point of our ptoject. This is the single HTML of a project

- `node_modules:` contains all the package dependencies and also other dependencies that our dependencies rely on. eg react, react-dom, vite, chalk

- `package.json:` is a json file that contains the project configuration settings, dependence versions, deveplopment & deployment scripts. 
All the necessary requirements to build the project at deployment.

- `package-lock.json`: This json file contains all the dependence versions of all our project's dependencies and also their dependencies. This is very important because it can be used to build the project deployment using the accurate package version. 

- `src / source folder`: This folder conatins the source code of custom components. It is in the folder that you will spend most pf your development time. 

- `src/Main.jsx`, `src/App.jsx`, 

## Components
A component is an independent module/part of a UI. It can also contain another Component. Think of components as breaking down your UI into small parts, with each part being independent from the other.

```jsx
Header.jsx
Sidebar.jsx
App.jsx
Main.jsx
Footer.jsx
Card.jsx
CheckOut.jsx
Cart.jsx
```
For order seek components can be grouped into a foler named components or any other name you or your team choses.
When using vite bundler component names must start with an uppercase letter (capital letter).

`jsx` stands for _<u>JavaScript XML</u>_. It allows HTML & CSS like sytnaxes to be written within a JavaScript file.

```jsx
// Main.jsx
/**
 * Main component can contain other components as well
*/

import Header from './components/Header'
import Sidebar from './components/Sidebar'
import Footer from './components/Footer'

function Main(){
    return (
        <>
        <Header />
        <Sidebar />
        <Footer />
        </>
    )
}
```
### **props (properties)**
props are a way to dynamically pass data to a component.

__REMEMBER__ <br>That components are just functions and being functions can take in as many arguments as wished.

`props` are therefore just arguments that we pass to functions.

```js
// one argument
function greet(name){
        console.log(`Hey ${name}, how are you doing.`);
}
```

```js
// take in as many arguments as the user can provide
function greet(...names) {
        names.map((name, index) =>  
        console.log(`${index + 1}: Hey ${name}, nice to meet ya..`));
}

greet('Dut', 'Kulang', 'Machour', 'Jeff', 'Atem', 'Garang');
// result
// 1: Hey Dut, nice to meet ya..
// 2: Hey Kulang, nice to meet ya..
// 3: Hey Machour, nice to meet ya..
// 4: Hey Jeff, nice to meet ya..
// 5: Hey Atem, nice to meet ya..
// 6: Hey Garang, nice to meet ya..
```
Or using the `**kwargs` in python3

```py
def greet(**kwargs):
        for key, value in kwargs:
                print(f"Hey {value}, nice to meet ya..")
```

My point is that props are just like arguments to a function, react converts them into a javascript object and then passed to a component.

```jsx
//components/ProfileCard.jsx

/*
UserProfile takes props are an argument it MUST recieve.
*/
const UserProfile = (props) =>{
        return (
                <div>
                        <img src={ props.user_photo_link }>
                        <p>{ props.username }</p>
                        <span>{ props.user_rating }</span>
                </div>
        )
}

export default UserProfile;
```

```jsx
// App.jsx
/*
Here we specify the user_photo_link,
username & user_rating parameter values.

Using just one component UserProfile we were able to have several unique profiles thanks to props
*/
import UserProfile from "./components/ProfileCard.jsx"

function App(){
        return (
                <>
                <UserProfile
                user_photo_link='https://some_link.jpg'
                username = "John Deo"
                user_rating = '4.4'
                />
                <UserProfile
                user_photo_link='https://some_link.png'
                username = "Achilla Deo"
                user_rating = '1.4'
                />
                <UserProfile
                user_photo_link='https://some_link.jpeg'
                username = "Boaz Moses"
                user_rating = '3.0'
                />
        )
}
export default App;
```
**props destructuring**

React converts props into a javaScript object before being passed to a component.
JavaScript objects can be destructured.

```js
const StudentInfor = {
        name: 'Dut Andrew Kulang',
        index_number: '003267/081',
        marks: {
                maths: 92,
                english: 85,
                science: 90,
                sst: 65
        },
        aggregates: 9,
        division: 1
}

// without destructuring
console.log(`Name: ${StudentInfor.name}`);
console.log(`Index number: {StudentInfor.index_number}`);
console.log(`Marks ${StudentInfor.marks}`);
console.log(`Aggregates: ${StudentInfor.aggregates}`);
console.log(`Division: ${StudentInfor.division}`);

// with destructuring
const {name, index_number, marks, aggregates, division} = StudentInfor

// marks destructing
const {maths, english, science, sst} = marks
console.log(`
Name: ${name}
index number : ${index_number}

maths: ${maths}
English: ${english}
Science: ${science}
SST: ${sst}

Aggregates: ${aggregates}
Division: ${division}
`);
```

Destructuring being a javaScript operation can be performed also in react.

```jsx
//components/ProfileCard.jsx

/*
Object destructuring v1
*/
const UserProfile = (props) =>{
        const {user_photo_link, username, user_rating } = props;
        return (
                <div>
                        <img src={ user_photo_link }>
                        <p>{ username }</p>
                        <span>{ user_rating }</span>
                </div>
        )
}

export default UserProfile;
```

```jsx
//components/ProfileCard.jsx

/*
Object destructuring v2
*/
const UserProfile = (
        {
        user_photo_link,
        username,
        user_rating 
        }) => {
        return (
                <div>
                        <img src={ user_photo_link }>
                        <p>{ username }</p>
                        <span>{ user_rating }</span>
                </div>
        )
}

export default UserProfile;
```


### **_States (a.k.a Hooks_)**
States allow react to track an alternation of the current state on a page and then only re-render the page to the new state.

React does this by having it own virtual DOM (Document Object Mapper) that it compares with the broswer's DOM and only re-renders new changes on the document. It does so because writing to the broswer DOM every time a change occurs is a expensive very resource process.

The `useState()` method from `'react'`

`useState(Initial_state)` takes an initial value as the default state value and returns an array of 2 elements.

   - 0th element as the variable whose state is being tracked (_state variable_)
   - 1st element as the method that will write the 0th element

__Important to note that__
`Whenever a state variable changes/updates, react re-renders the component`<br>

_In object oriented terms, think of the zeroth (0th) element as a private instance attribute, that is hidden from the outside world and the first (1st) element as an instance set method that alters the private instance attribute._

```jsx
import { useState } from 'react'

let [] = useState(0)
```
if you were creating timer, the zeroth (0) element can be called `counter` and the first (1st) element as `setCounter`.

or if it was a background changing functionality that you were implementing, then the zeroth (0th) element would be `color` and the first (1st) as `setColor`

```jsx
// timer example
import { useState } from 'react'

const [counter, setCounter] = useState(0);
```

```jsx
//background changing example
import { useState } from 'react'

const [color, setColor] = useState['white'];
```

_REMEMBER_ <br>
You can set the names to whatever you wish or want but that is the convention.

## key