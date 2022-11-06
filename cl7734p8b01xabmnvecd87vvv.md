# Cryptid.js ~ Rare JavaScript ~

#### JavaScript is Weird Sometimes

In this circumstance especially. For the context under which this rare JavaScript cryptid appears, we're going to talk about closures. 

#### Closures are Weird

You've used them before, whether you know it or not. The good news you can take from that is that you don't *need* to know what they are so long as you notice the pattern subconsciously and accept it. Unfortunately, though, you're reading this. Which means you're about to think about it way too hard.  
```
function helloMaker() {
      const greeting = "Hello World";
       return function() {
                console.log(greeting);
       };
};

const hey = helloMaker();
hey();
```
The variable `greeting` here is a closure. That means the greeting variable is in 'function scope' even to the nested function. Basically, a closure gives the nested functions access to that which is accessible to the top layer function. It's sorta like an instance variable in Ruby. 

#### The Cryptid

If we run the file we made for our previous example in node, we can call our helloMaker function and its nested function in one line.
```
> helloMaker()()
Hello World
``` 
Weeeeeird. 

