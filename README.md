# JavaScript Objects, JSON and Constructors

### Objectives
*After this lesson, students will be able to:*

- Compare objects and key-value stores to arrays as data structures
- Explain the difference between object properties and methods
- Create empty objects and objects with multiple properties and methods using object literal syntax
- Compare adding and retreiving properties to an existing object using the dot and bracket notations
- Access properties of an object using keys and helper methods (.hasOwnProperty)
- Iterate over the keys of an object to return and manipulate values
- Identify the properties that are inherited by an object's prototype
- Use the `new ` operator with one or more arguments to set initial properties on a newly-constrcuted object

### Preparation
*Before this lesson, students should already be able to:*

- Create and manipulate variables with javascript
- Use the chrome dev tools console


We have seen that we can _encapsulate_:
* data via `arrays`
* code via `functions`

What if we want to _encapsulate_ both data and code into a single variable?

Objects in JavaScript
=====

## Opening

### What is an object?

* Objects are a type of data structure that is nearly universal across programming languages, although they may have different names in different languages
* Like arrays, objects can hold multiple pieces of data of varying types; but unlike arrays, objects use named keys rather than indices to order and access those pieces of data
* Objects in general are made up of two things – properties and methods. Properties are data attached to an object that describe it or are related to it in some way. Methods are just functions, but because they're attached to an object, you can think of them as actions that the object can invoke on itself
* In JavaScript, an object is a type of key-value store, or a way to group many pairs of keys and values together, so sometimes it's used like a hash (in Ruby) or a dictionary (in other languages)

Example: A car has properties, a type of engine, a color, a certain number of seats etc. Following the same logic, a JavaScript object may have **properties** and **values** for these properties.

Aside from the values `null` and `undefined`, **everything in Javascript is an object**.

### Collections of name-value pairs

Javascript objects work as lists of keys (**A property name**) and corresponding values (**A property value**).

This way of storing/reading data is widely used across programs and languages because it’s highly customisable and quick to implement.

A key can be either a name, a number or a string, the corresponding value to a key can be any value part of JavaScript, including arrays, `null` or `undefined`and even another object. Objects structures can therefore be nested (objects inside objects) and of any complexity.

## Creating Objects

There are 4 different ways to create an object, but we're gonna focus on two today:

- Object Literals
- Constructor Functions

### Object Literals

## Object Properties

Objects in Javascript **always** have properties associated with them.

You can think of a property on a JavaScript object as a type of variable that contains a value. The properties of an object can be accessed using "dot notation":

```javascript
var diesel = {
  name: "Diesel",
  type: "Terrier",
  age: 1
}

diesel.name
=> "Diesel"
```

You can define or re-assign a property by assigning it a value using `=` as you would a normal variable.

```javascript
diesel.name = "Schmitty"
diesel.name
=> "Schmitty"
```

## Creating an object with properties

We are going to create an object `classroom` that contains properties `name` and `campus`:

```javascript
var classroom = new Object();
=> undefined

classroom.name = "WDI ATL";
=> "WDI ATL"

classroom.campus = "Atlanta";
=> "Atlanta"

classroom
=> Object {name: "WDI ATL", campus: "Atlanta"}
```

#### Bracket notation

There is another way to set properties on a JavaScript object.

```javascript
classroom["name"]   = "WDI ATL";
classroom["campus"] = "Atlanta";
```

This syntax can also be used to read properties of an object:

```javascript
console.log(classroom["name"]);
=> "WDI ATL";

var property = "campus";

console.log(classroom[property]);
=> "Atlanta";
```

For more details see [MDN's Documentation on Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).

#### Deleting properties

If you want to delete a property of an object (and by extension, the value attached to the property), you need to use the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator:

The following code shows how to remove a property:

```js
var classroom = {name: "WDI ATL", campus: "Atlanta"};
delete classroom.campus;
classroom
=> {name: "WDI ATL"}
```

## Object methods

As we've said before, the value of a property can be anything in JavaScript, means we can also attach functions to objects properties. When a function is attached to a property, this function become a `method`. Methods are defined the exact same way than a function, except that they have to be defined as the property of an object.

```javascript
var classroom = {
  name: "WDI ATL",
  campus: "Atlanta",
  start: "July 2014",
  sayHello: function() {
    console.log("Hello from WDI!");
  }
};
```

To call the method, we add a pair of parentheses to execute it:

```js
classroom.sayHello();
=> Hello
```



##`this` for object references

In JavaScript, `this` is a keyword that refers to the current object. When used in a method on an object, it will always refer to the current object.

```javascript
var diesel = {
  name: "Diesel",
  species: "dog",
  age: 1,
  speak: function() { return this.name + " says woof."; }
};

console.log(diesel.name + ' is a ' + diesel.age + ' year old ' + diesel.species + '.');
diesel.speak();
```

Q: So why not just use Object Literals whenever we need to create an object?
A: How do we create another dog?

```javascript
var meisha = {
  name: "Meisha",
  species: "dog",
  age: 2,
  speak: function() { return this.name + " says woof."; }
};
```

That's *not* very DRY!!!


### EXERCISE YOU DO 

Create 3 Javascript Object Literals that contain the following:

- at least 3 different properties 
- a method that prints out a `String` using `this`

**BREAK**



## Constructors
#### What is a constructor function?

A constructor is any Javascript function that is used to return a new object. The language doesn’t make a distinction. A function can be written to be used as a constructor or to be called as a normal function, or to be used either way.

The syntax for creating Objects in Javascript comes in two forms:

- the **declarative (literal)** form
- and the **constructed** form

The literal syntax for an object looks like this:

```javascript
var myObj = {
  key: value
};
```

The constructed form looks like this:

```javascript
var myObj = new Object();
myObj.key = value;
```

If we wanted to simulate creating new instances of a person in JavaScript, we'd start with something like this:

```javascript
function Person(name){
  this.name = name;
}
```

#### What about the `new` operator?

The [`new`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) operator in Javascript creates a new instance of a user-defined object type or of one of the built-in object types that has a constructor function.

Now that we have a constructor function, we can use the `new` operator to create a `Person`:

```javascript
var jenny = new Person('Jenny');
// undefined
```

To be sure `jenny` is infact a `Person`, we can:

```javascript
jenny instanceof Person;
// true
```

**QUESTION** What if we wanted to require `age` (or some other property) when we first instantiate an object?

## Adding Properties and Methods to Objects - Codealong (15 mins)

Let's revisit the constructor function from earlier, and use it to create two people from the Person class:

```javascript
function Person(name){
  this.name = name;
}

var mum = new Person("mum");
var dad = new Person("dad");
```

Of course, we'll want to add information to our existing objects.  Super easy with dot notation:

```javascript
mum.nationality = "British";
// "British"
```

And dad will be unaffected:

```javascript
dad.nationality
// undefined
```

How about adding a method? Also easy:

```javascript
mum.speak = function() { alert("hello"); }
mum.speak()
```

Again, `dad` will not have this function, only `mum` will have it.


#### What if we wanted to change all instances of the Object? -- Use the Prototype

Using Prototype will enable us to easily define methods to all existing instances while saving memory. What's great is that the method will only be applied to the prototype of the object, so it is only stored in the memory once, because objects coming from the same constructor point to one common prototype object.

If we wanted to add a new property to both `mum` and `dad` after they've been instantiated, we can define a property on the shared prototype; and since the `mum` and `dad` objects have the same prototype, they will both inherit that property.

```javascript
Person.prototype.species = "Human";
// "Human"

mum.species
// Human

dad.species
// Human
```

Amazing!

In addition to that, all instances of Person will have access to that method.

```javascript
function Person(name){
   this.name = name;
}

Person.prototype.speak = function(){
  alert("My name is, " + name);
}

var mum = new Person("mum");
var dad = new Person("dad");

mum.speak == dad.speak;
// true
```

So if you have methods that are going to be shared by all instances of an Object, they can all have access to them. Otherwise, if we added a property or method to a constructor, we would have to manually update all the existing instantiated objects. Using `prototype` allows us to dynamically change our objects.

## Independent Monkey Exercise (20 minutes)

- Create a `monkey` object, which has the following properties:

  - `name`
  - `species`
  - `foodsEaten`

  And the following methods:

  - `eatSomething(thingAsString)`
  - `introduce`: producers a string introducing itself, including its name, species, and what it's eaten

- Create 3 monkeys total. Make sure all 3 monkeys have all properties set and methods defined.

- Exercise your monkeys by retrieving their properties and using their methods. Practice using both syntaxes for retrieving properties (dot notation and brackets).

## Independent Practice - LAB 2

Create a Pet Constructor Function that creates a Pet object with:
* pet’s name
* owner’s name
* pet’s age
* pet’s species
* toString method on prototype that returns a string like this:

    `Snoopy is Susan’s 3 year old dog`

Test your code with:

```javascript
var snoopy = new Pet(“Snoopy”, “Susan”, 3, “Dog”);
console.log(snoopy.toString());
```

## Conclusion (5 mins)

We will use objects in JavaScript every day, and you will have plenty of time to practice creating and using objects in Javascript. There are a lot of resources available on the web for you to dive deeper, but the most detailed and understandable one is probably MDN.

- [Javascript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [Intro to Object Orientate Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
- [Objects in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)