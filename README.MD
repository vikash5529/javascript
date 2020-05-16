### What are the javascript data types?

    Below are the list of javascript data types available
    1. Number
    2. String
    3. Boolean
    4. Object
    5. Undefined
    6. Symbol

### What is the difference between == and === operators?

JavaScript provides both strict(===, !==) and type-converting(==, !=) equality comparison. The strict operators takes type of variable in consideration, while non-strict operators make type correction/conversion based upon values of variables. The strict operators follow the below conditions for different types,

1. Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal. i.e, Having the same number value.
   There are two special cases in this,
   1. NaN is not equal to anything, including NaN.
   2. Positive and negative zeros are equal to one another.
3. Two Boolean operands are strictly equal if both are true or both are false.
4. Two objects are strictly equal if they refer to the same Object.
5. Null and Undefined types are not equal with ===, but equal with ==. i.e,
   null===undefined --> false but null==undefined --> true

Some of the example which covers the above cases

```javascript
0 == false   // true
0 === false  // false
1 == "1"     // true
1 === "1"    // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```

### What is the purpose of let keyword?

The let statement declares a **block scope local variable**. Hence the variables defined with let keyword are limited in scope to the block, statement, or expression on which it is used. Whereas variables declared with the var keyword used to define a variable globally, or locally to an entire function regardless of block scope. Let's take an example to demonstrate the usage,

```javascript
let counter = 30;
if (counter === 30) {
  let counter = 31;
  console.log(counter); // 31
}
console.log(counter); // 30 (because if block variable won't exist here)
```

### What is the difference between let and var?

You can list out the differences in a tabular format

| var                                                   | let                         |
| ----------------------------------------------------- | --------------------------- |
| It is been available from the beginning of JavaScript | Introduced as part of ES6   |
| It has function scope                                 | It has block scope          |
| Variables will be hoisted                             | Hoisted but not initialized |

Let's take an example to see the difference,

```javascript
function userDetails(username) {
  if (username) {
    console.log(salary); // undefined(due to hoisting)
    console.log(age); // error: age is not defined
    let age = 30;
    var salary = 10000;
  }
  console.log(salary); //10000 (accessible to due function scope)
  console.log(age); //error: age is not defined(due to block scope)
}
```

### const variable makes the value immutable?

No, the const variable doesn't make the value immutable. But it disallows subsequent assignments(i.e, You can declare with assignment but can't assign another value later).

```javascript
const userList = [];
userList.push('John'); // Can mutate even though it can't re-assign
console.log(userList); // ['John']
```

### What is a freeze method?

The freeze() method is used to freeze an object. Freezing an object does'nt allow adding new properties to an object,prevents from removing and prevents changing the enumerability, configurability, or writability of existing properties. i.e, It returns the passed object and does not create a frozen copy.

     const obj = {
       prop: 100
     };

     Object.freeze(obj);
     obj.prop = 200; // Throws an error in strict mode

     console.log(obj.prop); //100
**Note:** It causes a TypeError if the argument passed is not an object.

### What is Hoisting?

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. Remember that JavaScript only hoists declarations, not initialisation.
Let's take a simple example of variable hoisting,

````javascript
console.log(message); //output : undefined
var message = 'The variable Has been hoisted';
```
  The above code looks like as below to the interpreter,
  ```;
javascript;
var message;
console.log(message);
message = 'The variable Has been hoisted';
````

### What is ES6?

ES6 is the sixth edition of the javascript language and it was released on June 2015. It was initially known as ECMAScript 6 (ES6) and later renamed to ECMAScript 2015. Almost all the modern browsers support ES6 but for the old browsers there are many transpilers, like Babel.js etc.

### What is scope in javascript?

Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.
JavaScript has 4 diffrent scopes: 1) Global Scope 2) Function Scope 3) Class Scope 4) Block Scope

### What are the possible ways to create objects in JavaScript?

There are many ways to create objects in javascript as below,

1. **Object constructor:**

The simplest way to create an empty object is using Object constructor. Currently this approach is not recommended.

      var object = new Object();

2.  **Object's create method:**

The create method of Object creates a new object by passing the prototype object as a parameter

      var object = Object.create(null);

3.**Object literal syntax:**
    The object literal syntax is equivalent to create method when it passes null as parameter

      var object = {};

4.  **Function constructor:**
    Create any function and apply the new operator to create object instances,

```javascript
function Person(name) {
  var object = {};
  object.name = name;
  object.age = 21;
  return object;
}
var object = new Person('test user');
```

5.  **Function constructor with prototype:**
    This is similar to function constructor but it uses prototype for their properties and methods,

```javascript
function Person() {}
Person.prototype.name = 'test user';
var object = new Person();
```

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

```javascript
function func {};

new func(x, y, z);

**(OR)**

// Create a new instance using function prototype.
var newInstance = Object.create(func.prototype)

// Call the function
var result = func.call(newInstance, x, y, z),

// If the result is a non-null object then use it otherwise just use the new instance.
console.log(result && typeof result === 'object' ? result : newInstance);
```

6. **ES6 Class syntax:**
   ES6 introduces class feature to create the objects

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

var object = new Person('test user');
```

7. **Singleton pattern:**
   A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

```javascript
var object = new (function () {
  this.name = 'test user';
})();
```

### What is an arguments object?

The arguments object is an Array-like object accessible inside functions that contains the values of the arguments passed to that function. For example, let's see how to use arguments object inside sum function,

```javascript
   function sum() {
       var total = 0;
       for (var i = 0, len = arguments.length; i < len; ++i) {
           total += arguments[i];
       }
       return total;
   }

   sum(1, 2, 3) // returns 6
  ```  

### What are closures?

A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains
1. Own scope where variables defined between its curly brackets
2. Outer function’s variables
3. Global variables
Let's take an example of closure concept,

    ```javascript
      function Welcome(name){
        var greetingInfo = function(message){
        console.log(message+' '+name);
        }
      return greetingInfo;
      }
      var myFunction = Welcome('John');
      myFunction('Welcome '); //Output: Welcome John
      myFunction('Hello Mr.'); //output: Hello Mr.John
    
  As per the above code, the inner function(greetingInfo) has access to the variables in the outer function scope(Welcome) even after outer function has returned
  
 ### What is prototype chain?

  **Prototype chaining** is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language. The prototype on object instance is available through Object.getPrototypeOf(object) or **proto** property whereas prototype on constructors function is available through object.prototype.

### What is the difference between Call, Apply and Bind?

The difference between Call, Apply and Bind can be explained with below examples,
**Call:** The call() method invokes a function with a given `this` value and arguments provided one by one

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
console.log(
  greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
);
}

invite.call(employee1, 'Hello', 'How are you?'); // Hello John Rodson, How are you?
invite.call(employee2, 'Hello', 'How are you?'); // Hello Jimmy Baily, How are you?
````

**Apply:** Invokes the function and allows you to pass in arguments as an array

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
  );
}

invite.apply(employee1, ['Hello', 'How are you?']); // Hello John Rodson, How are you?
invite.apply(employee2, ['Hello', 'How are you?']); // Hello Jimmy Baily, How are you?
```

**bind:** returns a new function, allowing you to pass in an array and any number of arguments

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
  );
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1('Hello', 'How are you?'); // Hello John Rodson, How are you?
inviteEmployee2('Hello', 'How are you?'); // Hello Jimmy Baily, How are you?
```

Call and apply are pretty interchangeable. Both execute the current function immediately. You need to decide whether it’s easier to send in an array or a comma separated list of arguments. You can remember by treating Call is for comma (separated list) and Apply is for Array. Whereas Bind creates a new function that will have `this` set to the first parameter passed to bind().

### What are lambda or arrow functions?

An arrow function is a shorter syntax for a function expression and does not have its own **this, arguments, super, or new.target**. These function are best suited for non-method functions, and they cannot be used as constructors.

### What is a first class function?

In Javascript, functions are first class objects. First-class functions means when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable. For example, in the below example, handler functions assigned to a listener

```javascript
const handler = () => console.log('This is a click handler function');
document.addEventListener('click', handler);
```

### What is currying function?

Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. Currying is named after a mathematician Haskell Curry. By applying currying, a n-ary function turns it into a unary function. Let's take an example of n-ary function and how it turns into a currying function

```javascript
const multiArgFunction = (a, b, c) => a + b + c;
const curryUnaryFunction = (a) => (b) => (c) => a + b + c;
curryUnaryFunction(1); // returns a function: b => c =>  1 + b + c
curryUnaryFunction(1)(2); // returns a function: c => 3 + c
curryUnaryFunction(1)(2)(3); // returns the number 6
```

Curried functions are great to improve code re-usability and functional composition.

### What is a pure function?

A **Pure function** is a function where the return value is only determined by its arguments without any side effects. i.e, If you call a function with the same arguments 'n' number of times and 'n' number of places in the application then it will always return the same value. Let's take an example to see the difference between pure and impure functions,

```javascript
//Impure
let numberArray = [];
const impureAddNumber = (number) => numberArray.push(number);
//Pure
const pureAddNumber = (number) => (argNumberArray) =>
  argNumberArray.concat([number]);

//Display the results
console.log(impureAddNumber(6)); // returns 6
console.log(numberArray); // returns [6]
console.log(pureAddNumber(7)(numberArray)); // returns [6, 7]
console.log(numberArray); // returns [6]
```

As per above code snippets, Push function is impure itself by altering the array and returning an push number index which is independent of parameter value. Whereas Concat on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects. Also, the return value is a concatenation of previous array.
Remember that Pure functions are important as they simplify unit testing without any side effects and no need for dependency injection. They also avoid tight coupling and makes harder to break your application by not having any side effects. These principles are coming together with **Immutability** concept of ES6 by giving preference to **const** over **let** usage.

### What is IIFE(Immediately Invoked Function Expression)?

IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined. The signature of it would be as below,


      (function ()
          {
            // logic here
          }
      )
        ();
  
  The primary reason to use an IIFE is to obtain data privacy because any variables declared within the IIFE cannot be accessed by the outside world. i.e, If you try to access variables with IIFE then it throws an error as below,

  ```
  (function ()
          {
            var message = "IIFE";
            console.log(message);
          }
   )
  ();
  console.log(message); //Error: message is not defined
  ```

### What are classes in ES6?

  In ES6, Javascript classes are primarily syntactical sugar over JavaScript’s existing prototype-based inheritance.
  For example, the prototype based inheritance written in function expression as below,
  ```javascript
  function Bike(model,color) {
      this.model = model;
      this.color = color;
  }

  Bike.prototype.getDetails = function() {
      return this.model + ' bike has' + this.color + ' color';
  };
  ```
Whereas ES6 classes can be defined as an alternative
```javascript
  class Bike{
    constructor(color, model) {
      this.color= color;
      this.model= model;
    }

    getDetails() {
      return this.model + ' bike has' + this.color + ' color';
    }
  }
  ```

### What is a callback function?

  A callback function is a function passed into another function as an argument. This function is invoked inside the outer function to complete an action.
  Let's take a simple example of how to use callback function
  ```javascript
  function callbackFunction(name) {
    console.log('Hello ' + name);
  }

  function outerFunction(callback) {
    let name = prompt('Please enter your name.');
    callback(name);
  }

  outerFunction(callbackFunction);
  ```


###Why do we need callbacks?

  The callbacks are needed because javascript is a event driven language. That means instead of waiting for a response javascript will keep executing while listening for other events.
  Let's take an example with first function invoking an API call(simulated by setTimeout) and next function which logs the message.
  ```javascript
  function firstFunction(){
    // Simulate a code delay
    setTimeout( function(){
      console.log('First function called');
    }, 1000 );
  }
  function secondFunction(){
    console.log('Second function called');
  }
  firstFunction();
  secondFunction();

  Output
  // Second function called
  // First function called
  ```
  As observed from the output, javascript didn't wait for the response of first function and remaining code block get executed. So callbacks used in a way to make sure that certain code doesn’t execute until other code finished execution.



### What is a callback hell?

  Callback Hell is an anti-pattern with multiple nested callbacks which makes code hard to read and debug when dealing with asynchronous logic. The callback hell looks like below,
  ```javascript
  async1(function(){
      async2(function(){
          async3(function(){
              async4(function(){
                  ....
              });
          });
      });
  });
  ```
   ### What is callback in callback?
  You can nest one callback inside in another callback to execute the actions sequentially one by one. This is known as callbacks in callbacks.
  ```javascript
  loadScript('/script1.js', function(script) {
     console.log('first script is loaded');

    loadScript('/script2.js', function(script) {

      console.log('second script is loaded');

      loadScript('/script3.js', function(script) {

          console.log('third script is loaded');
        // after all scripts are loaded
      });

    })

  });
  ```

### What is a promise?

  A promise is an object that may produce a single value some time in the future with either a resolved value or a reason that it’s not resolved(for example, network error). It will be in one of the 3 possible states: fulfilled, rejected, or pending.
  The syntax of promise would be as below
  ```javascript
  const promise = new Promise(function(resolve, reject) {
    // promise description
  })
  ```



### Why do you need a promise?

  Promises are used to handle asynchronous operations. They provide an alternative approach for callbacks by reducing the callback hell and writing the cleaner code.



### What are the three states of promise?

  Promises have three states:
  1. **Pending:** This is an initial state of the Promise before an operation begins
  2. **Fulfilled:** This state indicates that specified operation was completed.
  3. **Rejected:** This state indicates that the operation did not complete. In this case an error value will be thrown.

### What is promise.all?

  Promise.all is a promise that takes an array of promises as an input (an iterable), and it gets resolved when all the promises get resolved or any one of them gets rejected. For example, the syntax of promise.all method is below,
  ```javascript
  Promise.all([Promise1, Promise2, Promise3]) .then(result) => {   console.log(result) }) .catch(error => console.log(`Error in promises ${error}`))
  ```
  **Note:** Remember that the order of the promises(output the result) is maintained as per input order.



### What is the purpose of race method in promise?

  Promise.race() method will return the promise instance which is firstly resolved or rejected. Let's take an example of race() method where promise2 is resolved first
  ```javascript
  var promise1 = new Promise(function(resolve, reject) {
      setTimeout(resolve, 500, 'one');
  });
  var promise2 = new Promise(function(resolve, reject) {
      setTimeout(resolve, 100, 'two');
  });

  Promise.race([promise1, promise2]).then(function(value) {
    console.log(value); // "two" // Both promises will resolve, but promise2 is faster
  });
  ```



### What are the differences between promises and observables?

   Some of the major difference in a tabular form

   | Promises | Observables |
   |---- | ---------
   | Emits only a single value at a time  | Emits multiple values over a period of time(stream of values ranging from 0 to multiple) |
   | Eager in nature; they are going to be called immediately  | Lazy in nature; they require subscription to be invoked |
   | Promise is always asynchronous even though it resolved immediately | Observable can be either synchronous or asynchronous|
   | Doesn't provide any operators | Provides operators such as map, forEach, filter, reduce, retry, and retryWhen etc |
   | Cannot be canceled | Canceled by using unsubscribe() method |

### What is a strict mode in javascript?

  Strict Mode is a new feature in ECMAScript 5 that allows you to place a program, or a function, in a “strict” operating context. This way it prevents certain actions from being taken and throws more exceptions. The literal expression `"use strict";` instructs the browser to use the javascript code in the Strict mode.


### Why do you need strict mode?

  Strict mode is useful to write "secure" JavaScript by notifying "bad syntax" into real errors. For example, it eliminates accidentally creating a global variable by throwing an error and also throws an error for assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object.


### How do you declare strict mode?

  The strict mode is declared by adding "use strict"; to the beginning of a script or a function.
  If declare at the beginning of a script, it has global scope.
  ```javascript
  "use strict";
  x = 3.14; // This will cause an error because x is not declared
  ```
  and if you declare inside a function, it has local scope
  ```javascript
  x = 3.14;       // This will not cause an error.
  myFunction();

  function myFunction() {
    "use strict";
    y = 3.14;   // This will cause an error
  }
  ```

70. ### What is the purpose of delete operator?
  The delete keyword is used to delete the property as well as its value.


  ```javascript
  var user= {name: "John", age:20};
  delete user.age;

  console.log(user); // {name: "John"}
  ```


### What is typeof operator?

  You can use the JavaScript typeof operator to find the type of a JavaScript variable. It returns the type of a variable or an expression.
  ```javascript
  typeof "John Abraham"     // Returns "string"
  typeof (1 + 2)        // Returns "number"
  ```



### What is undefined property?

  The undefined property indicates that a variable has not been assigned a value, or not declared at all. The type of undefined value is undefined too.
  ```javascript
  var user;    // Value is undefined, type is undefined
  console.log(typeof(user)) //undefined
  ```
  Any variable can be emptied by setting the value to undefined.
  ```javascript
  user = undefined
  ```


### What is null value?

  The value null represents the intentional absence of any object value. It is one of JavaScript's primitive values. The type of null value is object.
  You can empty the variable by setting the value to null.
  ```javascript
  var user = null;
  console.log(typeof(user)) //object
  ```



### What is the difference between null and undefined?

  Below are the main differences between null and undefined,

  | Null | Undefined |
  |---- | -----------|
  | It is an assignment value which indicates that variable points to no object.  | It is not an assignment value where a variable has been declared but has not yet been assigned a value. |
  | Type of null is object | Type of undefined is undefined  |
  | The null value is a primitive value that represents the null, empty, or non-existent reference. | The undefined value is a primitive value used when a variable has not been assigned a value.|
  | Indicates the absence of a value for a variable | Indicates absence of variable itself |
  | Converted to zero (0) while performing primitive operations | Converted to NaN while performing primitive operations |

### What is the difference between Shallow and Deep copy?

  There are two ways to copy an object,

  ### Shallow Copy
  Shallow copy is a bit-wise copy of an object. A new object is created that has an exact copy of the values in the original object. If any of the fields of the object are references to other objects, just the reference addresses are copied i.e., only the memory address is copied.

  ### Example
    var empDetails = {
      name: "John", age: 25, expertise: "Software Developer"
    }
to create a duplicate
    
    var empDetailsShallowCopy = empDetails    //Shallow copying!
    empDetailsShallowCopy.name = "Johnson"

  The above statement will also change the name of `empDetails`, since we have a shallow copy. That means we're loosing the original data as well.

  ### Deep copy
  A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.
    ### Example
    var empDetails = {
      name: "John", age: 25, expertise: "Software Developer"
    }
    Create a deep copy by using the properties from the original object into new variable

    var empDetailsDeepCopy = {
      name: empDetails.name,
      age: empDetails.age,
      expertise: empDetails.expertise
    }
Now if you change 
    `empDetailsDeepCopy.name`, it will only affect `empDetailsDeepCopy` & not `empDetails`

### What are the differences between javascript and typescript?

   Below are the list of differences between javascript and typescript,

   | feature | typescript | javascript |
   |---- | --------- | ----
   | Language paradigm  | Object oriented programming language  | Scripting language |
   | Typing support | Supports static typing  | It has dynamic typing |
   | Modules | Supported | Not supported |
   | Interface | It has interfaces concept | Doesn't support interfaces |
   | Optional parameters | Functions support optional parameters | No support of optional parameters for functions |

### How do you encode an URL?

   The encodeURI() function is used to encode complete URI which has special characters except (, / ? : @ & = + $ #) characters.
   ```javascript
   var uri = 'https://mozilla.org/?x=шеллы';
   var encoded = encodeURI(uri);
   console.log(encoded); // https://mozilla.org/?x=%D1%88%D0%B5%D0%BB%D0%BB%D1%8B
   ```

211. ### How do you decode an URL?
   The decodeURI() function is used to decode a Uniform Resource Identifier (URI) previously created by encodeURI().
   ```javascript
   var uri = 'https://mozilla.org/?x=шеллы';
   var encoded = encodeURI(uri);
   console.log(encoded); // https://mozilla.org/?x=%D1%88%D0%B5%D0%BB%D0%BB%D1%8B
   try {
     console.log(decodeURI(encoded)); // "https://mozilla.org/?x=шеллы"
   } catch (e) {
     // catches a malformed URI
     console.error(e);
   }
   ```

### What is tree shaking?

   Tree shaking is a form of dead code elimination. It means that unused modules will not be included in the bundle during the build process and for that it relies on the static structure of ES2015 module syntax,( i.e. import and export). Initially this has been popularized by the ES2015 module bundler `rollup`.

### What is the need of tree shaking?

   Tree Shaking can significantly reduce the code size in any application. i.e, The less code we send over the wire the more performant the application will be. For example, if we just want to create a “Hello World” Application using SPA frameworks then it will take around  few MBs, but by tree shaking it can bring down the size to just few hundred KBs. Tree shaking is been implemented in Rollup and Webpack bundlers.

### What is BOM?

   The Browser Object Model (BOM) allows JavaScript to "talk to" the browser. It consists of the objects navigator, history, screen, location and document which are children of window. The Browser Object Model is not standardized and can change based on different browsers.
   ### What is IndexedDB?
  IndexedDB is a low-level API for client-side storage of larger amounts of structured data, including files/blobs. This API uses indexes to enable high-performance searches of this data.

### What is DOM?

  The Document Object Model (DOM) is a programming interface for HTML and XML(Extensible markup language) documents. It defines the logical structure of documents and the way a document is accessed and manipulated.

Note: It is called as a Logical structure because DOM doesn’t specify any relationship between objects.

DOM is a way to represent the webpage in the structured hierarchical way so that it will become easier for programmers and users to glide through the document. With DOM, we can easily access and manipulate tags, IDs, classes, Attributes or Elements using commands or methods provided by Document object.

### What is web storage?

  Web storage is an API that provides a mechanism by which browsers can store key/value pairs locally within the user's browser, in a much more intuitive fashion than using cookies. The web storage provides two mechanisms for storing data on the client.
  1. **Local storage:** It stores data for current origin with no expiration date.
  2. **Session storage:** It stores data for one session and the data is lost when the browser tab is closed.

### What is a Cookie?

  A cookie is a piece of data that is stored on your computer to be accessed by your browser. Cookies are saved as key/value pairs.
  For example, you can create a cookie named username as below,
  ```javascript
  document.cookie = "username=John";
  ```

### Why do you need a Cookie?

  Cookies are used to remember information about the user profile(such as username). It basically involves two steps,
  1. When a user visits a web page, user profile can be stored in a cookie.
  2. Next time the user visits the page, the cookie remembers user profile.

### What are the options in a cookie?

  There are few below options available for a cookie,
  1. By default, the cookie is deleted when the browser is closed but you can change this behavior by setting expiry date (in UTC time).
  ```javascript
  document.cookie = "username=John expires=Sat, 8 Jun 2019 12:00:00 UTC";
  ```
  2. By default, the cookie belongs to a current page. But you can tell the browser what path the cookie belongs to using a path parameter.
  ```javascript
  document.cookie = "username=John path=/services";
  ```

### How do you delete a cookie?

  You can delete a cookie by setting the expiry date as a passed date. You don't need to specify a cookie value in this case.
  For example, you can delete a username cookie in the current page as below.
  ```javascript
  document.cookie = "username=; expires=Fri, 07 Jun 2019 00:00:00 UTC; path=/;";
  ```
  **Note:** You should define the cookie path option to ensure that you delete the right cookie. Some browsers doesn't allow to delete a cookie unless you specify a path parameter.

### What are the differences between cookie, local storage and session storage?

  Below are some of the differences between cookie, local storage and session storage,

  | Feature | Cookie | Local storage | Session storage |
  |---- | --------- | ----- | ----- |
  | Accessed on client or server side | Both server-side & client-side | client-side only | client-side only |
  | Lifetime | As configured using Expires option  | until deleted | until tab is closed |
  | SSL support | Supported | Not supported | Not supported |
  | Maximum data size | 4KB | 5 MB | 5MB |



### What is the main difference between localStorage and sessionStorage?

  LocalStorage is same as SessionStorage but it persists the data even when the browser is closed and reopened(i.e it has no expiration time) whereas in sessionStorage data gets cleared when the page session ends.

### How do you access web storage?

  The Window object implements the `WindowLocalStorage` and `WindowSessionStorage` objects which has `localStorage`(window.localStorage) and `sessionStorage`(window.sessionStorage) properties respectively. These properties create an instance of the Storage object, through which data items can be set, retrieved and removed for a specific domain and storage type (session or local).
  For example, you can read and write on local storage objects as below
  ```javascript
  localStorage.setItem('logo', document.getElementById('logo').value);
  localStorage.getItem('logo');
  ```
