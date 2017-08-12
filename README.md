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
  * [Use strict](#use-strict)
  * [Scope](#scope)
    * [Closures](#pros)
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

The browser has an event loop which checks the event queue and processes pending events. For example, if an event happens in the background (e.g., a script `onload` event) while the browser is busy (e.g., processing an `onclick`), the event gets appended to the queue. When the onclick handler is complete, the queue is checked and the event is then handled (e.g., the `onload` script is executed).

Similarly, `setTimeout()` also puts execution of its referenced function into the event queue if the browser is busy.

When a value of zero is passed as the second argument to `setTimeout()`, it attempts to execute the specified function “as soon as possible”. Specifically, execution of the function is placed on the event queue to occur on the next timer tick. Note, though, that this is not immediate; the function is not executed until the next tick. That’s why in the above example, the call to console.log(4) occurs before the call to `console.log(3)` (since the call to `console.log(3)` is invoked via setTimeout, so it is slightly delayed).



Use strict
============

Use strict content text





Scope
============

Scope content text



Closures
----

Closures content text





Reference
============

Reference content text



Oficial docs
----

Oficial content text



Essential JavaScript Interview Questions
----

Essential JavaScript Interview Questions content text
