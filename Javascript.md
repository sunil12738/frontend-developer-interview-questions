# Table of Contents

- [Hoisting](#hoisting)
- [Equality Testing](#equality-testing)
- [this](#this)
- [Event Loop](#event-loop)
- [Closure](#closure)
- [Scope](#scope)
- [Datatypes](#datatypes)
- [Implementation/Coding Questions](#implementation-or-coding-questions)
- [Design based open ended problems](#design-based-open-ended-problems)
- [Theoretical Questions](#theoretical-questions)

# Hoisting:

## Give the output/error in the following cases
- ```javascript
  function a(){
    console.log(b) // output: ƒ b(){ console.log("hi") }
    var b = 10;
    return
    function b(){ console.log("hi") }
  }
  a()
  ```

- ```javascript
  var a = 10;
  function b() {
    a = 1;
    return;
    function a(){};
  }
  b();
  console.log(a) // output: 10
  ```

- ```javascript
  function sayHi() {
      console.log(name); // output: undefined
      console.log(age); // reference error
      var name = 'sunil';
      let age = 21;
  }
  sayHi()
  ```

- ```javascript
  console.log(a) // output: undefined
  var a = "test"
  sayHello() // error
  a()
  var a = function sayHello(){ console.log("hi") }
  ```

- ```javascript
  var x = 10
  function y(){
    x = 100
    return 
  }
  y()
  console.log(x) // output: 100
  ```

- ```javascript
  var x = 10
  function y(){
    x = 100
    return 
    var x = function(){ console.log("hi") }
  }
  y()
  console.log(x) // output: 10
  ```

- ```javascript
  var x = 10
  function y(){
    x = 100
    return 
    x = function(){ console.log("hi") }
  }
  y()
  console.log(x) // output: 100
  ```

- ```javascript
  console.log(a())
  function a(){
    console.log("gg")
  }

  console.log(b())
  var b = function(){
    console.log("gg")
  }

  console.log(c(), d())
  var c = function d(){
    console.log("gg")
  }
  ```

# Equality Testing:

- ```javascript
  var a = {key: 1};
  var b = {key: 1};
  console.log(a == b); // false    
  console.log(a === b); // false   
  ```
- ```javascript
  console.log(null == null); // true 
  console.log(null === null); // true 
  console.log(undefined == undefined); // true 
  console.log(undefined === undefined); // true
  console.log(NaN == NaN); //false
  console.log(NaN === NaN); //false
  ```

# this

## Give the output/error in the following cases


- ```javascript
  const x = {
    firstName: '',
    lastName: '',
    setName: function(name) {
      console.log(this)
      let splitName = function(n) {
        console.log(this)
        const nameArr = name.split(' ');
        this.firstName = name[0];
        this.lastName = name[1];
      }
      splitName(name);
    }
  }
  var name = 'Jon doe';
  x.setName(name);
  console.log(x.firstName); // undefined
  console.log(x.lastName); // undefined
  ```

- ```javascript
  var Foo = function( a ) {
    function bar() {   
      return a; 
    }
    
    this.baz = function() {
      return a; 
    };
  };
  
  Foo.prototype = {
    biz: function() {    
      return a; 
    }
  };
  
  var f = new Foo( 7 );
  f.bar(); // error bar is not fn
  f.baz(); // 7
  f.biz(); // undefined

  // Modify the above declaration so that the output is 7 for each of the declared functions
  ```

- ```javascript
  function a(){
    console.log(this)
  }
  a() // window


  var a = function(){
    console.log(this)
  }
  a() // window


  var a = function sayHello(){
    console.log(this)
  }
  a() // window
  ```

- ```javascript
  obj = {
    name: "supername",
    getN: function(){
      console.log(this.name) // supername, this = obj
      function x(){
        console.log(this.name) // undefined, this = window
      }
      x()
    }
  }
  obj.getN()
  // How to fix above so that inside function x, this refers to obj
  // Hint: Fat arrow, Bind, Call
  ```


# Event Loop

## Give the output in the following cases
- ```javascript
  console.log("A")
  setTimeout(function(){ console.log("B") }, 1000)
  console.log("C")
  // output:
  // A
  // C
  // B (after atleast 1 sec)
  ```

- ```javascript
  console.log("A")
  setTimeout(function(){ console.log("B") }, 0)
  console.log( console.log("C") )
  // output:
  // A
  // C
  // B (immediately after C is printer)
  ```

- ```javascript
  setTimeout(function(){ console.log("2000") }, 2000)
  setTimeout(function(){ console.log("1000") }, 1000)
  setTimeout(function(){ console.log("4000") }, 4000)
  ```

# Closure

## Write function definition for the following cases

### Infinite Argument Problem
- Create a function sum which when called `sum(1,2,3....n)()` or `sum(1)(2)(3)...(n)()` should yield same result.

- For a given n number of arguments, create a function sum which when called
  - sum(1,2,3....n)
  - sum(1)(2)(3)...(n)
  - sum(1,2,3)(4,5,...n)
  - sum(1,2)(3,4)(5)(6,7)..(n)
  - sum(1,2,3...n-2)(n-1, n) 
  all should yield the same result.
- Create a function such that `sentence("I")("am")("going")("out.")` should output I am going out. The last parameter will always contain full stop. 
  - sentence("I")("am")("going")("out.")
  - sentence("I am")("going")("out.")
  - sentence("I am going")("out.")
  - sentence("I")("am going out.")
  all should yield same result `I am going out.`

# Scope

- ```javascript
  for(var i = 0 ; i < 10; i++) {
      setTimeout(function(){
          console.log(i)
      }, 1000)
  }
  ```
  What will be the output?
  What are the various ways so that proper value for `i` is printed? (Hint: let, iife)

- ```javascript
  function createButtons(){
    for (var i = 1; i <= 5; ++i) {
      var body = document.getElementsByTagName("body")
      var button = document.createElement("button")
      button.innerHTML = 'button' + i
      button.onclick = function(){
        console.log('this is button' + i)
      }
      body.appendChild(button)
    }
  }
  ```
  How can you fix the issue if any?

# Datatypes

## String

```javascript
s = "google"
s[2]= "d"
console.log(s) // google, strings are immutable
```

## Object

- Can object contain keys with numeric values. Is the following object possible?
  `var a = {1: 1, '1': 2};`

- Is numbered index possible in object?
  `a.1, a."1", a[1], a["1"]`
  What is the output in each of the following for object a
- Create a person object with firstname and lastname and printfullname. Print full name
  ```javascript
  const person = {
    firstName: "Sunil",
    lastName: "Chaudhary",
    printFullName: function() {
      console.log(`${this.firstName} ${this.lastName}` )
    }
  }
  ```
  Suppose there is a `person2 = { firstName: "Sunil", lastName: "Chaudhary" }`. How can you call printFullName method (without modifying definition)


# Implementation or Coding Questions

- Create a search autosuggest in vanilla javascript. It should have a input bar where user can type and it should show a dropdown list of the results fetched after API call. Implement other optimizations such as debounce, caching etc.

- Create a Timer displaying time of format `hh:mm:ss`. There should be a start, stop and reset button and user should be able to give time for the timer. (additional: How the same problem can be redesigned if milliseconds also are to be shown)

- Write native functionality for bind.

- Write a polyfill for [get function from lodash](https://lodash.com/docs/#get).
- Write a polyfill for sort
- Write a polyfill for promise
- Write a polyfill for map
- Write a polyfill for filter

- Write javascript code to rotate a div in circle. Additional: Improve the code in a way such that one rotation is completed in certain specified time. Also, how can you modify the code to run for screens with different fps.

- Write a function to do deep equality checks in objects

- Suppose you have input like:
  ```javascript
  var skillsArray = [
    { skill: 'css', user: 'Bill' },
    { skill: 'javascript', user: 'Chad' },
    { skill: 'javascript', user: 'Bill' },
    { skill: 'css', user: 'Sue' },
    { skill: 'javascript', user: 'Sue' },
    { skill: 'html', user: 'Sue' }
  ];
  ```
  Convert it into result of the following form:
  ```javascript
  [
    { skill: 'javascript', user: [ 'Chad', 'Bill', 'Sue' ], count: 3 },
    { skill: 'css', user: [ 'Sue', 'Bill' ], count: 2 },
    { skill: 'html', user: [ 'Sue' ], count: 1 } 
  ]
  ```
  ```javascript
  // Solution
  function groupBySkill(endorsements) {
    const obj = {}

    endorsements.forEach((endorsement) => {
      if(!obj[endorsement.skill]) {
        obj[endorsement.skill] = {
          skill: endorsement.skill,
          user: [],
          count: 0,
        }
      }
      obj[endorsement.skill] = {
        ...obj[endorsement.skill],
        user: [ ...obj[endorsement.skill].user, endorsement.user ],
        count: obj[endorsement.skill].count + 1,
      }
    })
    return Object.values(obj).sort((a,b) => { return a.count < b.count ? 1 : -1 })
  }
  ```

- Write a function to reverse a string
  ```javascript
    str.split("").reverse().join("")
  ```

- Given the following input and output arrays. Write function `zip` which will take the input arrays as arguments and give the output
  ```javascript 
  // input arrays - arr1, arr2
  const arr1 = [{a : 1}, {b : 2}]
  const arr2 = [{c : 1}, {d : 4}]
  // output
  const output = [{a : 1, c : 1}, {b : 2, d : 4}]

  zip(arr1, arr2) -> [{a : 1, c : 1}, {b : 2, d : 4}]
  ```

- Given array containing positive and negative numbers (both integers and decimals). Separate them in 4 groups: integers +ve, integers -ve, decimals +ve, decimals -ve and show their separate sums.
  ```javascript
  // e.g.
  arr = [1,5,7,8,0.8,0.7,0.6,0.5,-1,-2,-6,-8,-1.7,-2.5,-7.6];
  result = { 
    output = negDec: -11.8
    negNo: -17
    posDec: 2.6
    posNo: 21
  }
  ```
  [Solution in JSBin](https://jsbin.com/joyexazeki/1/edit?html,js,output)

- Suppose there is a tunnel through which train can pass. You are standing inside the tunnel. Train enters from left side and exits from right side. Trains have bogeys numbered from 0 to 10. You can see only the bogeys which are inside the tunnel. Write a program mimicing this behaviour. [Solution in JSBin](https://jsbin.com/goyuludayi/edit?css,js,output)

- Usually the output of 1 + function x() {alert(1);} is "1function x(){alert(1);}". Can you write a code such that the output should be "1start:function x() {alert(1);}:end". For that matter, it should work for any function by prepending 'start:' at the beginning of function and appending ':end' at the end of the function.

- How to block the main thread of javascript? [Hint](https://jsfiddle.net/sunil12738/sf6v5jxk/7/)

- Create a memoizer function. It should take some function to return a new memoized function. For a given input, it should store the value and if the same input is encountered again, it should give the stored value.    
  e.g.    
    fib(n): function to calculate nth fibonacci    
    memoize(fn): memoizer function    
    memoizeFib = memoize(fib) : memoizeFib is a new function which won't calculate the fib(n) again if already calculated

- Suppose there is a object `a = { b: {}, c: {} }`. How can you change reference of b without changing reference of c

- Let string = “+++++*(e)abcdefff” where + means any single character, * means any number of characters, *(e) any 3 same characters only. Given a string where first half consists of combination of +, *, *(e) and second half consists of alphabets only. Write a validator.

- Create a Person class/function in such a way that `new Person().setFirstName("Sunil").setLastName("Chaudhary").printFullName()` prints `Sunil Chaudhary` on screen
  ```javascript
  // Solution
  class Person {
    constructor(fName, lName){
        this.fName = fName
        this.lName = lName
      }
      setFirstName(fName){
        this.fName = fName
        return this
      }
      setLastName(lName){
        this.lName = lName
        return this
      }
      printFullName(){
        console.log(`${this.fName} ${this.lName}`)
      }
  }
  ```

# Design based open ended problems

- How to design google calendar month view? 
- How to design a crossword puzzle app? User should be able to view the crossword puzzle, fill in and check if he is correct or not
- How to design candy crush game?
- Design a priority queue in javascript where values with certain priorities can be pushed and popped. In case two values have the same priority, the one pushed earlier should be popped first. (Hint: Use 2D array)
- Usually the output of 1 + function x() {alert(1);} is "1function x(){alert(1);}". Can you write a code such that the output should be "1start:function x() {alert(1);}:end". For that matter, it should work for any function by prepending 'start:' at the beginning of function and appending ':end' at the end of the function.
- Given a array of paragraphs, how can you search if certain sentences are present inside those paragraphs. The array can be very big.
- A system consists of some subscribers, events, and actions. A subscriber can subscribe to a certain events in a way that when event is trigerred, relevant action is performed 
e.g.    

  - Subscriber can be S1, S2...Sn
  - Events can be E1, E2...En
  - Actions can be A1, A2..An
        
  | Subscriber | Event | Action |
  |------------|-------|--------|
  | S1         | E1    | A1     | 
  | S1         | E2    | A1     | 
  | S2         | E1    | A2     | 
  | S2         | E2    | A3     | 
  | S3         | E1    | A4     | 
  | S3         | E2    | A5     |

  Here, When E1 event happens, action A1 happens for S1, action A2 happens for S2 and action A4 happens for S3
  What will be the data-structure you will choose and the overall architecture.
- Suppose there is a company which does some analytics work and returns data. The company (let's say X) gets a stream of numbers and it calculates average at that instant for all numbers received and returns the average. There could be other companies (let's say Y) which can ask for the average.

  Data:   1  3  5  7  9    
  Avg:    1  2  3  4  5

  So, in the above example, the average are calculated by company X.

  After first no, average is 1,    
  After second no (i.e. 3), average is 2 ((3+1)/2) and so on    
  At any point in time, companies are only concerned about average at that time (basically, if average is asked after data value 5, you only need to return 3)
  [Solution](https://codereview.stackexchange.com/questions/238416/finding-average-of-stream-of-numbers)
- A page has some links. On clicking the link, you want some other page to load (can be in same website or other website) as well as make the API call. What are various ways to do it? 
- Suppose there is a bank which has some money. You can call a function `withdraw` to withdraw money updating and returning the total money. There should be no global variables and value shouldn't be modified except by the function call it.
  ```javascript
  // one solution is using closures
  function withDrawMoney(total){
    let initMoney = total
    return function(money){
      //other validations
      initMoney = initMoney - money
      return initMoney
    }
  }
  ```

# Theoretical Questions

- What is Server Side Rendering? Why do we need it?
- Why Google crawlers are unable to crawl Client Side Rendered applications?
- What is ES6 and give some new features?
- What are promises?
- What is async/await?
- How does browser renders HTML on screen?
- What are service workers and what are the advantages?
- How is caching implemented in browsers?
- What are side effects?
- How is the value of `this` decided?
- Explain the usage of bind, call, apply.
- Is javascript compiled or interpreted?
- Difference between http and https?
- What is TCP/UDP?
- What is event loop?
- What is telnet?
- Array a consists of 3 elements [1,2,3]. What is the array length if you do a[20]=1. What is the array length if you do a[3000000000000]=1
- What is cors?
- What are various types of storages?
- Can you access hard drive from browser?
- How does browser builds a page?
- What is the difference between XHR request and fetch?
- Various methods to do API calls
- What is JWT
- What is npm?
- What is SCSS and advantages
- What is Unit Testing
- What is the difference and possible use cases for:
  - localStorage
  - sessionstorage
  - cookie
  - indexdb
- What is the scope of hoisted variables?
- Difference between shallow copy and deep copy of a object.
- Give some examples of tree shaking algorithms and how they work.










