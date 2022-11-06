# What the Heck does Object-Oriented Even Mean?

I dunno. Let's poke around on google together. 

#### Why Would I Care?
One of the powerful things about objects are in our ability to produce many instances of those objects. We can set up a factory of sorts to pop out many instances of a certain *class*. Object-oriented programming is a way that we can make our code modular and reusable, neatly boxing up or *encapsulating* relevant code within an object. 

#### Getting to know Objects, Classes, and Methods

You are a human, you have certain qualities. You look a certain way, you have a certain mass. You do things. You eat, you sleep, and a plethora of other things. You, a 100% unique beautiful little snowflake you, are much more than the things we just listed. That's because the category of human is a broad definition that encapsulates all of us, while you insertnamehere are an individual *instance* of humankind. 

Human is the class. You, insertnamehere, are an object. So the class is where we define the terms of the objects we produce with that definition. A class is a blue print, a cookie cutter, a factory! Within the class of human we get to ~encapsulate~ what it means to be a human. What do humans do, what do they look like? 

Here's a JavaScript example, but note that object-oriented programming isn't exclusively a JavaScript *thing*.
```js
class Human { 
        define your human here 
}

yasmin = new Human();
```
Notice the capitalisation on the class `Human`? This is a way we typically write class's to make it stick out a bit more and thus be easy to identify as a class instead of instances of a class or regular functions. Extra readable. It's kind of fun the way we humans have kept adding our own preferences for the languages we code with on top of built-in syntactical requirements. It's like our culture is mixing in with the needs of our machines. Hopefully, when super-intelligent ai take over the world this will help bridge the gap between us, and we can live a futurama future and not a Harlan Ellison one. 

```js
class Human { 
        eat() {
        console.log("yummy food I need this to live and also for enjoyment")
  }
}

yasmin = new Human();
yasmin.eat(); // "yummy food I need this to live and also for enjoyment"
```
See how we encapsulated what it means for a human to eat within the class definition? Now all instances of the class we generate will have the methods we defined. 

Read [this](https://processing.org/tutorials/objects) processing tutorial for a more in-depth example (still an easy entry-level one though). I also recommend [this](https://www.youtube.com/watch?v=T-HGdc8L-7w) Dan Shiffman youtube video.

#### Nitty-Gritty 

Now that we've played around with some examples, which in my view, are the best way to understand things as a beginner developer, let's get into the definition of object-oriented so you can talk about it more easily in interviews or things like that. 

According to [this](https://www.techtarget.com/searchapparchitecture/definition/object-oriented-programming-OOP#:~:text=Object%2Doriented%20programming%20(OOP)%20is%20a%20computer%20programming%20model,has%20unique%20attributes%20and%20behavior.) Object Oriented programming puts the what over the how. It's what you're tinkering with rather than how you're tinkering with it that matters. 

There are four fundamental categories to consider here. 
* Classes - datatypes that act as a blueprint for the following three
* Objects - instances of a class with their own specific data
* Methods - functions defined within a class which describe the behaviour of specific objects
* Attributes - defined within a class and describe the state of an object


To *do* object-oriented programming, you ought to

1. Encapsulate and Abstract. 

All important information is contained within an object. The information you expose should be on a need-to-know basis. Keep all your bits and pieces covered unless absolutely necessary. 

2. Recycle 

Classes can inherit code from other classes, and relationships and subclasses can be assigned so that common logic can apply from the top down. Like how all other classes in our crud app [adventures](https://yasmina95.hashnode.dev/ror-beginners-guide-crud-getting-started) inherent from ActiveRecord::Base

3. Be Poly, have babies 

Objects share behaviours, children extend the functionality of parent classes, and they're all a big happy family. 

#### Other Paradigms Exist

Object-oriented programming gets a lot of air time, but it's not the *only* paradigm out there. Functional programming is a popular example, and structured and imperative programming are some alternatives out there dying for more attention. They're not getting any more air time from me though heheh, losers. 

Next time (hopefully), a look into Object Oriented CSS. Not super popular anymore but a couple of smart older dev's have spoken of it fondly and I'm curious. 