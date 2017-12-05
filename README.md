# Prototypes and Inheritance

## Learning objectives

* Explain what Prototypes are and demonstrate why they're an essential JavaScript feature
* Build a basic prototype and then a Constructor function, and show why Constructors are more efficient 
* ES6's major syntax change, and the new method of creating Constructors  
* Use the ```new``` keyword to create new objects with shared properties
* Create a class that inherits from another using ```extends``` and ```super``` keywords

## What are prototypes?
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
