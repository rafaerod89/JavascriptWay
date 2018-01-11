# JavaScript Way

So, we have the web, browsers, HTML, CSS... and the world start spinning. But we needed a cute, little, light, easy and fast language to give life to our new web page. And so, JavaScript was born.

But hey, JavaScript is A LOT more than just that, and for that reason and after having a huge grow in the tech community, JavaScript is everywhere. We have JavaScript on frontend frameworks (if this is a surprise for you then this project isn't for you, start somewhere else and then come back :)! ), backend frameworks, databases, teas, soups, etc, etc.

For this reason companies are starting to need JavaScript Experts, and a lot of Senior Developers whose experience is more pointed to this new JavaScript stack of technologies.

This project aint for beginners, instead is for:

  * **You Senior Developer who wants to:**
    * Clarify some aspects of this language that are making you crazy.
    * Stop making the fool out of yourself with every PR you make with this new millennials developers you're working with.

  * **Companies who wants to:**
    * Know how to recruit this new JavaScript Experts or JavaScript Senior Developers, I mean, what should this guys know right?

So, if this project is for you then welcome to

### Basic Javascript for Senior JavaScript programmers.

Table of Contents
-----------------

  * [Intro](#intro)
    * [Pros](#pros)
    * [Cons](#cons)
  * [Events and timing](#events-and-timing)
  * [Scope](#scope)
    * [Hoisting](#hoisting)
    * [Closures](#closures)
  * [Anon Functions](#anon-functions)


  * [Call by Sharing](#call-by-sharing)


  * [Prototypal Inheritance (Coming soon)](#prototypal-inheritance)
  * [Operators](#operators)
    * [Comparison](#comparison)
    * [Comma](#comma)
  * [Immutable](#immutable)
  * [Semicolons](#semicolons)
  * [Use strict](#use-strict)
  * [Optimizing JavaScript code](#optimizing-javascript-code)
    * [Defining class methods](#defining-class-methods)
    * [Initializing instance variables](#initializing-instance-variables)
    * [Avoiding pitfalls with closures](#avoiding-pitfalls-with-closures)
    * [Avoiding with](#avoiding-with)
  * [Reference](#reference)
    * [Oficial docs](#oficial-docs)
    * [Essential JavaScript Interview Questions](#essential-javascript-interview-questions)





Work In Progress..
------





Intro
============

What is JavaScript? We're answering this question with the help of the [Stanford University](http://web.stanford.edu/class/cs98si/slides/overview.html)

JavaScript is primarily a client-side language. JavaScript started at Netscape, a web browser developed in the 1990s. A webpage can contain embedded JavaScript, which executes when a user visits the page. The language was created to allow web developers to embed executable code on their webpages, so that they could make their webpages interactive, or perform simple tasks. Today, browser scripting remains the main use-case of JavaScript.

JavaScript’s syntax is heavily inspired by C++ and Java. If you have experience in C++ or Java, JavaScript’s syntax will seem familiar to you. However, the inner workings of JavaScript is closer to a dynamically-typed, interpreted language such as Python or Ruby.

JavaScript is an interpreted language, not a compiled language. In contrast to C++ or Java, JavaScript has no compilation step. Instead, an interpreter in the browser reads over the JavaScript code, interprets each line, and runs it. More modern browsers use a technology known as Just-In-Time (JIT) compilation, which compiles JavaScript to executable bytecode just as it is about to run.

JavaScript is a very useful language. JavaScript runs in every web browser, out of the box. A JavaScript application runs on every device, whereas a desktop or mobile application runs only on the application it is targeted to (Windows, Mac OSX, Linux, iPhone, Android). This allows you to write cross-platform apps in a really easy way. JavaScript’s role has also expanded significantly. Platforms such as Node.js allow developers to run JavaScript server-side. It is now possible to create entire web applications in which both client-side and server-side logic is written in JavaScript.



Pros
----

  * Performance
    * Really fast language
    * Reduces the load on the server making operations on the frontend
  * Language
    * Interpreted language
    * Loosely typed
    * No need of function overloading
  * Object instead of Classes
    * Can add a property on a object at any time at it will affect every implementation
    * Everything is a object, functions included
  * Semicolons are handled automatically
  * Async
  * Simple
  * Event-Prograding
  * Platform independent: Run in every web browser out of the box and Platforms such as Node.js allow developers to run JavaScript server-side and so they can go full stack with the language.
  * Helps creating rich UI and great UX



Cons
----

  * JavaScript Fatigue
  * Is really easy to get started, but if the user has no solid knowledge of the language the resulting product can be harmful
    * Bad use of the Scope
    * Bad use of variables
    * Bad use of mutable objects
  * Single inheritance only
  * Some of the Pros can become Cons depending on the project and/or developers.





Events and timing
============

So, we're not new to JavaScript and that means we know that it's an async language. Having that in mind, in what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

```
(function() {
    console.log(1);
    setTimeout(function(){console.log(2)}, 1000);
    setTimeout(function(){console.log(3)}, 0);
    console.log(4);
})();
```
The values will be logged in the following order:
```
1
4
3
2
```

Let’s first explain the parts of this that are presumably more obvious:

  * `1` and `4` are displayed first since they are logged by simple calls to `console.log()` without any delay
  * `2` is displayed after `3` because `2` is being logged after a delay of 1000 msecs (i.e., 1 second) whereas `3` is being logged after a delay of 0 msecs.

OK, fine. But if `3` is being logged after a delay of 0 msecs, doesn’t that mean that it is being logged right away? And, if so, shouldn’t it be logged *before* `4`, since `4` is being logged by a later line of code?

The answer has to do with properly understanding JavaScript events and timing.

The browser has an event loop which checks the event queue and processes pending events. For example, if an event happens in the background (e.g., a script `onload` event) while the browser is busy (e.g., processing an `onclick`), the event gets appended to the queue. When the `onclick` handler is complete, the queue is checked and the event is then handled (e.g., the `onload` script is executed).

Similarly, `setTimeout()` also puts execution of its referenced function into the event queue if the browser is busy.

When a value of zero is passed as the second argument to `setTimeout()`, it attempts to execute the specified function “as soon as possible”. Specifically, execution of the function is placed on the event queue to occur on the next timer tick. Note, though, that this is not immediate; the function is not executed until the next tick. That’s why in the above example, the call to console.log(4) occurs before the call to `console.log(3)` (since the call to `console.log(3)` is invoked via setTimeout, so it is slightly delayed).





Scope
============

We must understand how variable scope, closures, variable hoisting and `this` value work in JavaScript, if want to understand JavaScript well. These concepts may seem straightforward; they are not. Some important subtleties exist that we must understand, if we want to thrive and excel as JavaScript developers.

First we need to remember that **in JavaScript, objects and functions are also variables**. And so, scope is the set of variables, objects, and functions you have access to.

Unlike most programming languages, JavaScript normally does not have block-level scope (variables scoped to surrounding curly brackets); instead, JavaScript normally has function-level scope: **The scope changes inside functions**.


### Variable Scope
A variable’s scope is the context in which the variable exists. The scope specifies from where you can access a variable and whether you have access to the variable in that context. Variables have either a local scope or a global scope.

#### Local Variables (Function-level scope)
  * Variables declared within a function are local variables and are only accessible within that function or by functions inside that function.
  * The lifetime of a JavaScript variable starts when it is declared and in the case of local variables they are deleted when the function is completed.

#### Global Variables
  * Global Variables are bad, never use them. No matter what your trying to accomplish, there are better ways of doing it.
  * If you declare a global variable and a local variable with the same name, the local variable will have priority when you attempt to use the variable inside a function (local scope)
  * In a web browser, global variables are deleted when you close the browser window (or tab), but remains available to new pages loaded into the same window.
  * If is not a local Variable, then it's a Global Variable. That simple.


So, **Declaring a variable outside a function scope should automatically add it to the global scope?**

Well.. Yes and no.

In fact both this sceneries declare a variable in the global scope:

  * Declaring a variable outside a function scope in a script
```
<script>
    var x = 123;

    // The current scope is global
    console.log('x' in window); // true
</script>
```

  * Assigning a value to a undeclared variable
```
<script>
    function aux() {
         x = 123
    }

    // The current scope is global
    console.log('x' in window); // true
</script>
```

But with ES6 we now have modules (import and export) and, as you can see in here -> http://exploringjs.com/es6/ch_modules.html . Every module has it's own scope so, not even something like this will be added to the global scope:

```
<script type="module">
    import $ from 'lib/jquery';
    var x = 123;

    // The current scope is not global
    console.log('$' in window); // false
    console.log('x' in window); // false
</script>
```

And just so you remember.. IT'S BAD TO SET VARIABLES IN THE GLOBAL SCOPE.


### Let & Const in ES6
Starting this section we said that *JavaScript **normally** has function-level scope*, and the exception to this is the `let` and `const` declarations in ES6.

Both of this declarations have **block-level scope** meaning:

```
var fs = []

for (var i = 0; i < 3; i++) {
  fs.push(function () {
    console.log(i)
    })
}

fs.forEach(function (f) {
	f()
})

/* Prints out
  3
  3
  3
*/
```

But:
```
var fs = []

for (let i = 0; i < 3; i++) {
  fs.push(function () {
    console.log(i)
    })
}

fs.forEach(function (f) {
	f()
})

/* Prints out
  0
  1
  2
*/
```


### Arrow Function in ES6

As introduced in ES6, an arrow function expression has a shorter syntax than a function expression and does not bind its own `this`, `arguments`, `super`, or `new.target`. These function expressions are best suited for non-method functions, and they cannot be used as constructors.

Our main concern here is `this`. Until arrow functions, every new function defined its own this value. This proved to be annoying with an object-oriented style of programming.

For example:
```
var deliveryBoy = {
	name: 'John',
  handleMessage: function (message, handler) {
  	handler(message)
  },
  receive: function () {
  	var that = this
    this.handleMessage('Hello ', function (message) {
      console.log(message + that.name)
    })
  }
}

deliveryBoy.receive()
```

Now we can use:
```
var deliveryBoy = {
	name: 'John',
  handleMessage: function (message, handler) {
  	handler(message)
  },
  receive: function () {
    this.handleMessage('Hello ', (message) => {
      console.log(message + this.name)
    })
  }
}

deliveryBoy.receive()
```



Hoisting
----

Hoisting was thought up as a general way of thinking about how execution context (specifically the creation and execution phases) work in JavaScript. But, hoisting can lead to misunderstandings. For example, hoisting teaches that variable and function declarations are physically moved to the top of your coding, but this is not what happens at all. What does happen is that variable and function declarations are put into memory during the compile phase, but stays exactly where you typed it in your coding.

One of the advantages of JavaScript putting function declarations into the memory before it executes any code segment is that it allows you to use a function before you declare it in your code. For example:
```
function catName(name) {
  console.log("My cat's name is " + name);
}

catName("Tigger");
```

And:
```
catName("Chloe");

function catName(name) {
  console.log("My cat's name is " + name);
}
```
Both results in: *"My cat's name is Tigger"*

Hoisting works well with other data types and variables as well. The variables can be initialized and used before declared. But they cannot be used without initialization.

```
num = 6;
num + 7;
var num;
/* gives no errors as long as num is declared*/
```

JavaScript only hoists declarations, not initializations. If you are using a variable that is declared and initialized after using it, the value will be undefined. The below two examples demonstrate the same behavior.

```
var x = 1; // Initialize x
console.log(x + " " + y); // '1 undefined'
var y = 2;


// The following code will behave the same as the previous code:
var x = 1; // Initialize x
var y; // Declare y
console.log(x + " " + y); // '1 undefined'
y = 2; // Initialize y
```



Closures
----

A closure is an inner function that has access to the outer (enclosing) function’s variables—scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function’s variables, and it has access to the global variables.

You create a closure by adding a function inside another function.

### A Basic Example of Closures in JavaScript:
#### Emulating private methods with closures

Languages such as Java provide the ability to declare methods private, meaning that they can only be called by other methods in the same class.

JavaScript does not provide a native way of doing this, but it is possible to emulate private methods using closures. Private methods aren't just useful for restricting access to code: they also provide a powerful way of managing your global namespace, keeping non-essential methods from cluttering up the public interface to your code

```
var counter = (function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  };   
})();

console.log(counter.value()); // logs 0
counter.increment();
counter.increment();
console.log(counter.value()); // logs 2
counter.decrement();
console.log(counter.value()); // logs 1
```

### Closures’ Rules and Side Effects

#### Closures have access to the outer function’s variable even after the outer function return
```
function celebrityName (firstName) {
    var nameIntro = "This celebrity is ";
    // this inner function has access to the outer function's variables, including the parameter​
   function lastName (theLastName) {
        return nameIntro + firstName + " " + theLastName;
    }
    return lastName;
}
​
​var mjName = celebrityName ("Michael"); // At this juncture, the celebrityName outer function has returned.​
​
​// The closure (lastName) is called here after the outer function has returned above​
​// Yet, the closure still has access to the outer function's variables and parameter​
mjName ("Jackson"); // This celebrity is Michael Jackson 
```

#### Closures store references to the outer function’s variables; they do not store the actual value.
```
function celebrityID () {
    var celebrityID = 999;
    // We are returning an object with some inner functions​
    // All the inner functions have access to the outer function's variables​
    return {
        getID: function ()  {
            // This inner function will return the UPDATED celebrityID variable​
            // It will return the current value of celebrityID, even after the changeTheID function changes it​
          return celebrityID;
        },
        setID: function (theNewID)  {
            // This inner function will change the outer function's variable anytime​
            celebrityID = theNewID;
        }
    }
​
}
​
​var mjID = celebrityID (); // At this juncture, the celebrityID outer function has returned.​
mjID.getID(); // 999​
mjID.setID(567); // Changes the outer function's variable​
mjID.getID(); // 567: It returns the updated celebrityId variable 
```

#### Closures Gone Awry
 Because closures have access to the updated values of the outer function’s variables, they can also lead to bugs when the outer function’s variable changes with a for loop

```
// This example is explained in detail below (just after this code box).​
​function celebrityIDCreator (theCelebrities) {
    var i;
    var uniqueID = 100;
    for (i = 0; i < theCelebrities.length; i++) {
      theCelebrities[i]["id"] = function ()  {
        return uniqueID + i;
      }
    }

    return theCelebrities;
}
​
​var actionCelebs = [{name:"Stallone", id:0}, {name:"Cruise", id:0}, {name:"Willis", id:0}];
​
​var createIdForActionCelebs = celebrityIDCreator (actionCelebs);
​
​var stalloneID = createIdForActionCelebs [0];  console.log(stalloneID.id()); // 103
```

We can solve this be using more closures: in particular, to use an anonymous closure:

```
function celebrityIDCreator (theCelebrities) {
    var i
    var uniqueID = 100
    for (i = 0; i < theCelebrities.length; i++) {
        theCelebrities[i]["id"] = function ()  {
            return function () {
                return uniqueID + i // each iteration of the for loop passes the current value of i into this closure and it saves the correct value to the array
            } () // BY adding () at the end of this function, we are executing it immediately and returning just the value of uniqueID + i, instead of returning a function.
        } () // immediately invoke the function passing the i variable as a parameter
    }
    return theCelebrities;
}

var actionCelebs = [{name:"Stallone", id:0}, {name:"Cruise", id:0}, {name:"Willis", id:0}];
var createIdForActionCelebs = celebrityIDCreator (actionCelebs);
var stalloneID = createIdForActionCelebs [0];
console.log(stalloneID.id); // 100
var cruiseID = createIdForActionCelebs [1];
console.log(cruiseID.id); // 101
```

#### Performance considerations
It is unwise to unnecessarily create functions within other functions if closures are not needed for a particular task, as it will negatively affect script performance both in terms of processing speed and memory consumption.

To read more about this read the `Optimizing JavaScript code` section.





Anon Functions
============

Anon Functions or Anonymous Functions in JavaScript, just as they their name hints at, have no identity. They are functions that are created, used and discarded just as quickly.

We use anonymous functions all the time is JavaScript, and there are multiple daily uses for them (we can see one in the anonymous closure example on the previous section), mostly as callback functions to execute some quick functionality. For example the arrow functions inside the `then` and `catch` on the next example:

```
function printPhone (model, brand, callback) {
    // REQUEST THE ACTUAL PHONE TO AN EXTERNAL ENDPOINT
    dataProvider(model, brand)
    .then(() => {
    	console.log('we got the phone!')
    })
    .catch(() => {
    	console.log('there's no phone.....')
    })
}
```

As you probably noticed so far, there are two important thing in here: is probable that you were using Anon Functions even if you were not familiar with the concept and.. Anon Functions are AWESOME. With that said, they are not perfect and they could bring some misunderstanding a buggy behaviour to our developments as you can see in here -> http://johnnyji.me/react/2016/06/27/why-arrow-functions-murder-react-performance.html





Call by Sharing
============

In JavaScript, all variables refers to values. So, when we pass a variable to a function, the argument is a value which is itself a reference. This is called call-by-sharing.

When we pass a variable to a function, a new variable is created in function scope which refers to the passed value. In JavaScript, objects are mutable. While, strings and numbers are immutable. So, changes to the object’s properties (mutations) in function scope are visible to the caller’s scope because of shared reference, but assignment of the new value do not influence external object.




















Prototypal Inheritance
============

Prototypal Inheritance content text




















Operators
============

JavaScript, as any other major language, has all kind of operators, but we're only going to focus on two of them that often get confused.



Comparison
----

JavaScript provides three different value-comparison operations:
  * **strict equality** (or "triple equals" or "identity") using ===,
  * **loose equality** ("double equals") using ==,
  * **Object.is** (new in ECMAScript 2015).

But excluding some border cases, normally you would be using the first two so we're digging a little deeper on those.

**NOTE:** `Object.is` will behave the same way as triple equals, but with special handling for NaN and -0 and +0 so that the last two are not said to be the same, while Object.is(NaN, NaN) will be true. (Comparing NaN with NaN ordinarily—i.e., using either double equals or triple equals—evaluates to false, because IEEE 754 says so.)


#### Strict equality using ===

Strict equality compares two values for equality. Neither value is implicitly converted to some other value before being compared. If the values have different types, the values are considered unequal. Otherwise, if the values have the same type and are not numbers, they're considered equal if they have the same value. Finally, if both values are numbers, they're considered equal if they're both not NaN and are the same value, or if one is +0 and one is -0.


#### Loose equality using ==

Loose equality compares two values for equality, after converting both values to a common type.  After conversions (one or both sides may undergo conversions), the final equality comparison is performed exactly as === performs it.  Loose equality is symmetric: A == B always has identical semantics to B == A for any values of A and B (except for the order of applied conversions).

If you want to know more about how the equality comparison is performed you can check it out here -> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness



Comma
----

The comma operator evaluates each of its operands (from left to right) and returns the value of the last operand.

You can use the comma operator when you want to include multiple expressions in a location that requires a single expression. The most common usage of this operator is to supply multiple parameters in a for loop.

**Example:**

If a is a 2-dimensional array with 10 elements on each side, the following code uses the comma operator to increment two variables at once.

The following code prints the values of the diagonal elements in the array:

```
for (var i = 0, j = 9; i <= 9; i++, j--)
  console.log('a[' + i + '][' + j + '] = ' + a[i][j]);
```





Immutable
============

**What's immutability?**

The text-book definition of mutability is liable or subject to change or alteration. In programming, we use the word to mean objects whose state is allowed to change over time. An immutable value is the exact opposite – after it has been created, it can never change.

**Then, why is immutability important?**

Well, mutating data can produce code that’s hard to read and error prone. For primitive values (like numbers and strings), it is pretty easy to write ‘immutable’ code, because primitive values cannot be mutated themselves. Variables containing primitive types always point to the actual value. If you pass it to another variable, the other variable get’s a fresh copy of that value.

Now, Objects (Remember that an Array is also an Object) are a different story, if you would pass an object to another variable, they will both refer to the same object. If you would then mutate the object from either variable, they will both reflect the changes.

**The problem**
```
const person = {
  name: 'John',
  age: 28
}
const newPerson = person
newPerson.age = 30
console.log(newPerson === person) // true
console.log(person) // { name: 'John', age: 30 }
```

When we change `newObj`, we also automatically change the old `obj` variable. This is because they refer to the same object. In most cases this is unwanted behaviour and bad practice, but remember that every project is different and so are they answers, meaning, mutating data might not be a problem to your particular project, instead, it might be a plus. So before you start preaching about immutability know that JavaScript is not like other languages and neither do the problems you might be facing, so know your problem and know your options before you start.

If you want/need to work with immutable objects know that it's AWESOME and a lot of great libraries use them, for example, Redux. With this said, there are a lot of different ways you can achieve this, you might go with an [external library](http://facebook.github.io/immutable-js/) or you may try to implement them using native ES6 (have [this](https://wecodetheweb.com/2016/02/12/immutable-javascript-using-es6-and-beyond/) as an example).

External libraries usually have some performance enhancements that makes them production/battle ready, but keep in mind that Immutable libraries usually have the tradeback that you just don't use them in one file.. instead, they tend to extend to your WHOLE app, meaning that getting rid of them along the way might be difficult. But on a lot of cases they're worth it, just have it in mind.





Semicolons
============

I can write A LOT about this, but honestly, I happen to ran into this [Post](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding "Awesome semicolons post") that sums pretty much everything I had on my mind. Hope you enjoy it :).





Use strict
============

Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode isn't just a subset: it intentionally has different semantics from normal code. Browsers not supporting strict mode will run strict mode code with different behavior from browsers that do, so don't rely on strict mode without feature-testing for support for the relevant aspects of strict mode. Strict mode code and non-strict mode code can coexist, so scripts can opt into strict mode incrementally.

Strict mode makes several changes to normal JavaScript semantics. First, strict mode eliminates some JavaScript silent errors by changing them to throw errors. Second, strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. Third, strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.

Having strict mode enabled or not, you should keep in mind that your code should work in strict mode.





Optimizing JavaScript code
============

Defining class methods
----

The following is inefficient, as each time a instance of baz.Bar is constructed, a new function and closure is created for foo:
```
baz.Bar = function() {
  // constructor body
  this.foo = function() {
    // method body
  };
}
```

The preferred approach is:
```
baz.Bar = function() {
  // constructor body
};

baz.Bar.prototype.foo = function() {
  // method body
};
```

With this approach, no matter how many instances of `baz.Bar` are constructed, only a single function is ever created for `foo`, and no closures are created.



Initializing instance variables
----

Place instance variable declaration/initialization on the prototype for instance variables with value type (rather than reference type) initialization values (i.e. values of type number, Boolean, null, undefined, or string). This avoids unnecessarily running the initialization code each time the constructor is called. (This can't be done for instance variables whose initial value is dependent on arguments to the constructor, or some other state at time of construction.)

For example, instead of:
```
foo.Bar = function() {
  this.prop1_ = 4;
  this.prop2_ = true;
  this.prop3_ = [];
  this.prop4_ = 'blah';
};
```

Use:
```
foo.Bar = function() {
  this.prop3_ = [];
};

foo.Bar.prototype.prop1_ = 4;

foo.Bar.prototype.prop2_ = true;

foo.Bar.prototype.prop4_ = 'blah';
```



Avoiding pitfalls with closures
----

Closures are a powerful and useful feature of JavaScript; however, they have several drawbacks, including:
  * They are the most common source of memory leaks.
  * Creating a closure is significantly slower than creating an inner function without a closure, and much slower than reusing a static function. For example:
```
function setupAlertTimeout() {
  var msg = 'Message to alert';
  window.setTimeout(function() { alert(msg); }, 100);
}
```

is slower than:
```
function setupAlertTimeout() {
  window.setTimeout(function() {
    var msg = 'Message to alert';
    alert(msg);
  }, 100);
}
```

which is slower than:
```
function alertMsg() {
  var msg = 'Message to alert';
  alert(msg);
}

function setupAlertTimeout() {
  window.setTimeout(alertMsg, 100);
}
```

  * They add a level to the scope chain. When the browser resolves properties, each level of the scope chain must be checked. In the following example:
```
var a = 'a';

function createFunctionWithClosure() {
  var b = 'b';
  return function () {
    var c = 'c';
    a;
    b;
    c;
  };
}

var f = createFunctionWithClosure();
f();
```
when f is invoked, referencing `a` is slower than referencing `b`, which is slower than referencing `c`.



Avoiding with
----

Avoid using `with` in your code. It has a negative impact on performance, as it modifies the scope chain, making it more expensive to look up variables in other scopes.





Reference
============

Oficial docs
----

  * https://developer.mozilla.org/en-US/docs/Web/JavaScript
  * https://babeljs.io/learn-es2015/
  * https://www.ecma-international.org/publications/standards/Ecma-262.htm
  * http://dmitrysoshnikov.com/
  * http://exploringjs.com/es6/
  * http://2ality.com/2015/02/es6-classes-final.html



Essential JavaScript Interview Questions
----

Don't matter if you're a Developer or a Recruiter, you should take a look into this:

  * https://www.toptal.com/javascript/interview-questions#note-1
  * https://www.upwork.com/i/interview-questions/javascript/
  * https://www.codementor.io/nihantanu/21-essential-javascript-tech-interview-practice-questions-answers-du107p62z
