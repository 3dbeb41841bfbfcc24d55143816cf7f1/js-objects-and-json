# JavaScript Objects and JSON

We have seen that we can _encapsulate_:
* data via `arrays`
* code via `functions`

What if we want to _encapsulate_ both data and code into a single variable?

## Objects

Objects allow us to combine both data (properties) and functions (methods) into a single _object_ that can be stored in a single variable.

### Object Literals

```javascript
var miko = {
  name: "Miko",
  species: "dog",
  age: 3,
  speak: function() { return this.name + " says woof."; }
};

console.log(miko.name + ' is a ' + miko.age + ' year old ' + miko.species + '.');
miko.speak();
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

### Constructor Functions

```javascript
// Dog constructor
function Dog(name) {
  this.name = name;
  this.speak = function() { return this.name + “ says woof.”; };
}
```

```javascript
// Create some dogs
var miko = new Dog(“Miko”);
var meisha = new Dog(“Meisha”);

// Make them speak
console.log(miko.speak());    // Miko says woof.
console.log(meisha.speak());  // Meisha says woof.

// What does this do?
var snoopy = Dog(“Snoopy”);
```

### JavaScript Prototypes

```javascript
// Dog constructor
function Dog(name) {
  this.name = name;
//this.speak = function() { return this.name + “ says woof.”; };
}
// What is this???
Dog.prototype.speak = function() {
  return this.name + “ says woof.”;
};
```

```javascript
// Create some dogs
var miko = new Dog(“Miko”);
var meisha = new Dog(“Meisha”);

// Make them speak
console.log(miko.speak());    // miko says woof.
console.log(meisha.speak());  // meisha says woof.
```

### LAB 1

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

### LAB 1 - Alternate

Write a TrafficLight constructor function that creates a traffic light with the following properties:

* name:  // i.e. "4th and Peachtree"
* color: // i.e. red, yellow, green

Add the following Prototype methods to the TrafficLight prototype:

* goRed:      // function that changes the light to red
* goYellow:   // function that changes the light to yellow
* goGreen:    // function that changes the light to green
* toString:   // function that returns a string containing the light's name and color.

Then create some traffic lights using the `new` operator and make the lights change color by calling the methods.

#### Solution:

```javascript
function TrafficLight(name) {
  this.name = name;
  this.color = 'red';
}

TrafficLight.prototype.goGreen   = function() { this.color = 'green'; };
TrafficLight.prototype.goYellow  = function() { this.color = 'yellow'; };
TrafficLight.prototype.goRed     = function() { this.color = 'red'; };
TrafficLight.prototype.toString  = function() {
  return this.name + ' is ' + this.color;
};

var light1 = new TrafficLight('Peachtree and North Ave');
var light2 = new TrafficLight('1st and Main');

console.log(light1.toString());
console.log(light2.toString());

light1.goGreen();
console.log(light1.toString());
console.log(light2.toString());

light1.goYellow();
light2.goGreen();
console.log(light1.toString());
console.log(light2.toString());

light1.goRed();
light2.goYellow();
console.log(light1.toString());
console.log(light2.toString());

light2.goRed();
console.log(light1.toString());
console.log(light2.toString());
```

