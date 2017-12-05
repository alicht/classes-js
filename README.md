# Prototypes and Inheritance

## Learning objectives

* Explain what Prototypes are and demonstrate why they're an essential JavaScript feature
* ES6's major syntax change, and the new method of creating Constructors  
* Use the ```new``` keyword to create new objects with shared properties
* Create a class that inherits from another using ```extends``` and ```super``` keywords

## What are prototypes?

![Alt Text](https://media.giphy.com/media/3o6ZtjDNG2UXy7B3xK/giphy.gif)


Prototypes are the underlying blueprint of an object, and form the baseline from which other instances of an object can be created. 
* Every object in JavaScript has a special related object called the prototype. Through using Prototypes we can simply and efficiently share behavior and data between multiple objects.

* Let's look at an example to help us visualize how Prototypes work. We'll use 3 Objects: machine, vehicle, car.  
``` javascript
machine 
// ie just an example of a base object that we'll use here
```
^^ the base object

``` javascript
console.log(vehicle.prototype) // machine
// machine is the prototype of vehicle
```
and then
``` javascript
console.log(car.prototype) // vehicle
// vehicle is the prototype of car
```
This is a how a prototype chain works:
```
car -> vehicle -> machine
```
When JavaScript looks for a property that doesn't exist in a particular object (ie "car"), it will attempt to look for that property in each object on the prototype chain (ie first in vehicle, then in machine). It will walk along the chain until it finds the attribute or return undefined if it can't be found.

##### Let's explore some examples
 

## ES6 introduces new gamechanging syntax

Prior to ES6, the common way to build new objects in JavaScript was by using Constructor functions. However Function Constructors can be quite confusing to understand and to help alleviate this, ES6 introduced the ```class``` keyword. 

Classes in ES6 are honestly just syntactic sugar- they don't add any additional functionality to what we already had in the language (ie constructors), and are just a simpler syntax for building the same objects as we had before.

## Implementing JavaScript's new "class" keyword 

Let's take a look at what a constructor looks like when we use class:

``` javascript
class Pikachu {
  constructor(number, type, fastAttack, chargeAttack, hiddenPower){
    this.number = number;
    this.type = type;
    this.fastAttack = fastAttack;
    this.chargeAttack = chargeAttack;
    this.hiddenPower = hiddenPower;
  }
  walks(){
    return `I'll follow you wherever you go, and I can also do ${this.hiddenPower}!`
  }
}

class Snorlax {
  constructor(number, type, fastAttack, chargeAttack, weight){
    this.number = number;
    this.type = type;
    this.fastAttack = fastAttack;
    this.chargeAttack = chargeAttack;
    this.weight = weight;
  }
  eats(){
    return `Zzzzz! I am massively large and weigh ' + ${this.weight} +' pounds!`
  }
}
```


We see we have two classes: Pikachu and Snorlax. They have some things in common: number, type, fastAttack and chargeAttack. But they also have differences- Pikachu has a hiddenPower attribute and a walking function, whereas Snorlax has a weight attribute and an eats function.  

## Lab- refactor functional code into classes

# Pokemon will help us understand a deeper meaning to classes


#### This is fine except...

What if we wanted to create a number of other classes of Pokemon- like Gyarados, Dragonite, Farfetch'd, etc.- all of whom share some of the aforementioned properties but also have their own unique methods or attributes? 

How could we refactor this so that we don't have to keep writing out shared class properties and methods? 

A: Create a base class will abstract this: 
``` javascript
class Pokemon{
  constructor(number, type, fastAttack, chargeAttack){
    this.number = number;
    this.type = type;
    this.fastAttack = fastAttack;
    this.chargeAttack = chargeAttack;
  }
}
```

Here we've defined an Pokemon class. It contains the general properties and methods that can be found in just about all Pokemon. What's great about this is that Snorlax and Pikachu can now just reference this "parent" Pokemon class and thus the only things we'd need to put in their "child" class definitions are the properties and methods that are unique to them.


#### Now let's take our parent Pokemon class and apply it to its "children":

![Alt Text](https://media.giphy.com/media/12r4pHjvAOv48o/giphy.gif)

``` javascript
class Pikachu extends Pokemon {
  constructor(number, type, fastAttack, chargeAttack, hiddenPower){
    this.hiddenPower = hiddenPower;
  }
  walks(){
    return `I'll follow you wherever you go, and I can also do ${this.hiddenPower}!`
  }
}
``` 

![Alt Text](https://media.giphy.com/media/TFrE5CQ0oNqvu/giphy.gif)
``` javascript
class Snorlax extends Pokemon {
  constructor(number, type, fastAttack, chargeAttack, weight){
    this.weight = weight;;
  }
  eats(){
    return `Zzzzz! I am massively large and weigh ' + ${this.weight} +' pounds!`
  }
}
```
### Extends
The keyword "extends" plays a key role here. Whatever class is to the left of the extends keyword should inherit the properties and methods that belongs to the class to the right of the keyword. 

Let's test out our parent class (ie Pokemon). 
``` javascript
const magikarp = new Pokemon(129, "water", "splash", "struggle");
```
And now the children.
``` javascript
const yellowpikachu = new Pikachu(24, "electric", "thunder shock", "thunder", "hiddenPower");
console.log(yellowpikachu); // "this is not defined"
```
That didn't work out the way we expected, and that's because we forgot something: 

### Super
When creating an instance of a child class, we need to make sure it invokes the constructor of the parent (ie Pokemon) class.

We do this by using the keyword "super":
``` javascript
class Pikachu extends Pokemon {
  constructor(number, type, fastAttack, chargeAttack, hiddenPower){
    super(number, type, fastAttack, chargeAttack);
    this.hiddenPower = hiddenPower;
  }
  walks(){
    return `I'll follow you wherever you go, and I can also do ${this.hiddenPower}!`
  }
}
```
The super function calls the constructor of the parent class. In the above example, once super does what it needs to do, it then runs through the rest of Pikachu's constructor.

In order to give an instance of a child class context (i.e. to be able to use this), we must call super.


# Review
What are Prototypes and why are they useful?

What is a class? What is new? How are they related?

What does it mean to use "inheritance" when working with classes?

How do we indicate that one class inherits from another?

What does super mean?
#



![flat 800x800 075 f u3](https://user-images.githubusercontent.com/6153182/32067464-4fdf6e40-ba51-11e7-9f3f-30af6a9a0b36.jpg)










# see also 
[JavaScript Prototype in Plain Language](http://javascriptissexy.com/javascript-prototype-in-plain-detailed-language)

[ES6 Classes and Javascript Prototypes](https://reinteractive.com/posts/235-es6-classes-and-javascript-prototypes)

[Master the JavaScript Interview: What’s the Difference Between Class & Prototypal Inheritance?](https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9)
