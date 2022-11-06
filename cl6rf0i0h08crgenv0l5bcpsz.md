# Intro to Node.js - What is it?

#### Intro
This is an entry level intro to Node.js from one beginner developer to another. 

#### Lore
Once upon a time in the year of 2008, JavaScript developers lived a simple humble life only able to run JS in a browser. 

That naïve time however, was soon to end. The man responsible, Ryan Dahl? It was his mad-man frankensteining of googles v8 engine and a C++ program that resulted in the birth of Node.js. 

#### What is it Though?
Node is JavaScript runtime environment. Basically, JavaScript code can work here. 

What it isn't is as important as what it is. Keep in mind that node.js is not a programming language. It's a space in which the language of JavaScript is meaningful. 

Another thing node is not: a framework. Rails is a framework for the language Ruby for example. Node is not that, though it might seem comparable at first. Don't be fooled. Runtime Environment only. Remember it. 

#### What's the Difference between Node.js and the Browser?

In the browser we have certain objects that JavaScript work with. When you use something like this:
```
document.querySelector(".container")
```
You're working with the document object. 

Node doesn't have access to the document object however. You instead have access to things that wouldn't be possible inside your browser. Things like:

- The File System
```
fs.readFile();
```

- Listen for Requests on the Network
```
http.createServer();
```

#### Asynchronous, whaaaat?

Node is asynchronous. Everything runs whenever, chaos! But also less waiting!

When things are synchronous, one thing is ran, then another. If the thing currently executing happens to have some wait time, e.g. when receive data from a database. Nothing else is going to run while we're waiting. 

#### Event Queue
The way Node.js manages it's asynchronous chaos is with the Event Queue. Node monitors the event queue for things which are now ready to be executed. Like our data from the previous example being ready.

This makes Node a great choice for Input and Output (I/O) intensive applications: Real-Time and/or Data Intensive Apps. 

An app utilising WebSockets for example tend to send a lot of Data which pose unique issues for developers in managing the WebSocket `messages`. Node.js is probably a good addition to the tech stack of an App using WebSockets. 

#### Ok, I'm Sold. How Do I Use Node?
To use node you must first *have* node. In terminal run this command to see if you have node installed on your machine `node -v`. You should see something with the following shape `v16.16.0`. You're reading this in the future though, and so numbers may differ. To install node or to get the latest version head [here](https://nodejs.org/en/). It's my strong recommendation that you go for the latest *stable* version rather than the truly latest version. 

Once you've got node installed you can use it to run JavaScript files right from your terminal. 

To test this out, `touch node-test.js` in some file on your terminal. Take it to your editor and write the following. 
```
console.log("look at you go, using node. Wow!")
```
Then back in terminal run `node node-test.js`. "look at you go, using node. Wow!" should be printed out in your terminal if you've done everything correctly. 

#### The Module System

When running JavaScript in your browser (i.e. the client side), the JavaScript engine adds `window` to your `console.log` behind the scenes, unless you love typing so much that you put it in yourself like so:
```
window.console.log("something goes here");
```
That's because anything you've defined globally are accessible to the window object. The same goes for other inbuilt functions like `setTimeout();`, `clearTimeout();`, `setInterval();` and `clearInterval();` as well as variables you've made `const someVariableName = "some variable name"; `.

In Node we have the `global` object instead of the `window` object. Node is adding global onto your `console.logs` and such. 
```
global.console.log("something goes in here");
```
However Node does not recognise your variables. 
As such, the following code will return undefined. 

```
const someVariableName = "blah blah blah this is a string";
console.log(someVariableName)
```

This is a good thing though. Global variables are messy, when working on large projects with many people you don't want so many opportunities to break one another's code by defining global variables with the same variable names. 

Instead, Node.js does things *modularly*. 

Every file is a module, and the things we define within that file have global scope within that file and not without. They're *private*. When you want to use them outside of that file, you're going to have to `export it`. If you're familiar with React you've probably added `export default SomeTagName` to the bottom of many a files and `import SomeTagName from some/file/path` to the top of another. 

To take a look at the module object of a given file write the following. 
```
console.log(module);
```
Now if you run that file with node in the terminal you'll get a JSON object returned. It should have this shape.
```
Module {
  id: '.',
  path: '/Users/yourName/your/path/goes/here/your-app',
  exports: {},
  filename: '/Users/yourName/your/path/goes/here/first-app/app.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/yourName/your/path/goes/here/first-app/node_modules',
    '/Users/yourName/your/path/goes/node_modules',
    '/Users/yourName/your/path/node_modules',
    '/Users/yourName/your/node_modules',
    '/Users/yourName/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ]
}
```
#### Exporting
As previously mentioned if you want to use private variables in other files, you export them. That looks something like this.

In `hello.js` declare a variable, in this case for a function that says hello, and then export it. 
```
function sayHello(name){
    console.log(`hello ${name}`);
};

module.exports.sayHello = sayHello;
```
Now in `app.js` let's import it and then console.log the variable name to see what it returns.  
```
const hello = require('./logger');

hello.sayHello('Yasmin');
```
Now in terminal enter this command: `node app.js`
Look at the object returned.
```
{ sayHello: [Function: sayHello] }
```
However since we're exporting a single function, it makes more sense to export it as a function rather than as an Object. 

Do so like this. In `hello.js`
```
function sayHello(name){
    console.log(`hello ${name}`);
};

module.exports = sayHello;
```
While in `app.js`
```
const hello = require('./logger');

hello('Yasmin');
```
This is what's returned when we run `node app.js` in the terminal again `hello Yasmin`.

#### It's Complicated
Now to ruin all authority I garnered from writing this.
Things are more complicated than this blog post would suggest. As an entry level dev, don't worry your pretty little head about it yet. Learning things requires breaking them down and simplifying them, and so this information will be useful to you until it isn't anymore. Then more learning, on and on forever. Good luck. 

