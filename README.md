# Front-End Cheat Sheet

### Design Patterns:

Design patterns are advanced object-oriented solutions to commonly occurring software problems.  Patterns are about reusable designs and interactions of objects.  Each pattern has a name and becomes part of a vocabulary when discussing complex design solutions.

The 23 Gang of Four (GoF) patterns are generally considered the foundation for all other patterns. They are categorized in three groups: Creational, Structural, and Behavioral

 
| Creational Patterns        |    Design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.    |
| ------------- |:-------------:|
| Prototype     |   A fully initialized instance to be copied or cloned |
| Singleton   | A class of which only a single instance can exist   |

--

| Structural Patterns|    Design Patterns that ease the design by identifying a simple way to realize relationships between entities.    |
| ------------- |:-------------:|
| Decorator     |  Add responsibilities to objects dynamically|
| Facade   | A single class that represents an entire subsystem   |

--

| Behavioral Patterns |    Design patterns that identify common communication patterns between objects and realize these patterns. By doing so, these patterns increase flexibility in carrying out this communication.    |
| ------------- |:-------------:|
| Mediator     | Defines simplified communication between classes |
| Observer   | A way of notifying change to a number of classes   |

### SOLID principles:

#### 1. Single Responsibility Principle
A class should have one and only one reason to change, meaning that a class should only have one job.
#### 2. Open-Closed Principle
Objects or entities should be open for extension, but closed for modification.
#### 3. Liskov Substitution Principle
Every subclass/derived class should be substitutable for their base/parent class.
In other words, as simple as that, a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.
#### 4. Interface Segregation
A client should never be forced to implement an interface that it doesn’t use or clients shouldn’t be forced to depend on methods they do not use.
#### 5. Dependency Inversion Principle
Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.


### JavaScript Concepts

#### Scope 

There are two types of Scopes in JavaScript

* #### Block Scope
JavaScript does NOT have block scope (think if blocks and the like). Variables used before assignment will be undefined and variables used after assignment will yield the expected value.

```javascript
function a() {
    var hi = 'hi';
    console.log(hi);  //hi
    console.log(bye); //undefined

    if (true) {
        var bye = 'bye';
        console.log(hi);  //hi
        console.log(bye); //bye
    }
    console.log(hi);  //hi
    console.log(bye); //bye
}
```
* #### Function Scope
JavaScript DOES have function scope. Variables defined in inner function scope and used in outer function scope will result in an error because the variable has not been defined in scope.
```javascript
function a() {
    var hi = 'hi';
    console.log(hi);  //hi
    console.log(bye); //error

    function b() {
        var bye = 'bye';
        console.log(hi);
        console.log(bye);
    }
    b();
    console.log(hi);
    console.log(bye);
}
```

#### Hoisting

* When var is not used, variables are made global
* Variable names take precedence over function names (in the case of duplicates)
* Variable declarations (e.g. var myObj) are hoisted to the top of function scope; however, assignment is NOT hoisted
* Function declarations (e.g. function myFunc() { }) are hoisted to the top of function scope
* Function expressions (e.g. var myFunc = function someFunc() { }) are NOT hoisted to the top of function scope
* They are treated like variable declarations–the variable definition is hoisted, but the assignment is not hoisted
* someFunc cannot be called outside of its assignment; someFunc is undefined (ReferenceError); must use myFunc
* Immediately executing function declarations has no effect on hoisting–the function will still be hoisted to the top of function scope

#### Closure

Closure is when a function has access to its original context. 
A closure is a special kind of object that combines two things: a function and the environment in which that function was created. The environment consists of any local variables that were in-scope at the time that the closure was created.

A closure is a function having access to the parent scope, even after the parent function has closed.

#### Memoization
Is a programming technique which attempts to increase a function’s performance by caching its previously computed results.

### Invocation patterns

#### Method Invocation Pattern
A method is a function tied to a property on an object. For methods, this is bound to the object upon invocation. For example:

```javascript
var person = {
    name: 'Calvin',
    age: 25,
    greet: function () {
        alert('My name is ' + this.name + '.');
    }
};
person.greet(); //My name is Calvin.
```

In this example, this is bound to the person object upon invoking greet because greet is a method of person.

#### Function Invocation Pattern
For functions that are not properties on objects, this is bound to the global object. This is not very intuitive and is often considered one of the ‘bad parts’ of JavaScript–a mistake in language design. Naturally, you’d think this would be bound to the parent function, and that would have been much more helpful. Regardless, most developers overcome this problem by assigning this to a variable in the parent function. For example:

```javascript
// Add a new method to person
person.calculateAge = function (yearsFromNow) {
    var self = this;

    function yearsOld() {
        return self.age + yearsFromNow;
    }

    alert('I will be ' + yearsOld() + ' years old ' + yearsFromNow + ' years from now.');
}
person.calculateAge(10); //I will be 35 years old 10 years from now.
```
In this example, I maintain a reference to the context of this by assigning it to the variable self. At the time of assignment, this is bound to the person object. As a result, I can access the property age on the person object from within the yearsOld function. self and that are common names for variables that maintain the context of this.

What if I had used this instead of self?

```javascript
person.calculateAgeWrong = function (yearsFromNow) {
    function yearsOld() {
        return this.age + yearsFromNow; //NaN
    }

    alert('I will be ' + yearsOld() + ' years old ' + yearsFromNow + ' years from now.');
}
person.calculateAgeWrong(10);
```

#### Constructor Invocation Pattern
In JavaScript, functions can be invoked with the new prefix similar to the way objects are constructed in other languages. When this happens, this is bound to the new object. In addition, the resulting object is created with a link to the hidden prototype property of the function. This is what makes JavaScript a prototypal inheritance language as opposed to a classical inheritance language. There are no classes, but objects can inherit properties from other objects.

Functions that are designed to be called with the new prefix are by definition constructors. These functions are distinguished from others by using PascalCase as opposed to camelCase.

```javascript
var Person = function (name) {
    this.name = name;
};

Person.prototype.greet = function () {
    return this.name + ' says hi.';
};

alert(new Person('Calvin').greet()); //Calvin says hi.
```

Notice the greet function uses this to access the name property. this is bound to Person.

#### Apply Invocation Pattern

As a functional object-oriented language, JavaScript makes it possible for functions to have methods as well. The apply function is a method on the Function.prototype–the prototype for all JS functions. apply makes it possible to use one object’s method in the context of another. We can do so by supplying an array with the correct number arguments and and the object to which this will be bound, also known as the context. Therefore, apply can take two arguments: (1) a context for this and (2) an array of arguments that will be applied to the method at hand.

```javascript
var calvin = new Person('Calvin');
var hobbes = {name: 'Hobbes'};
alert(calvin.greet.apply(hobbes)); //Hobbes says hi.
```
Even though hobbes does not have a greet method, we can still apply the greet method from calvin because hobbes has a name property. If hobbes didn’t have a name property, the invocation would fail. This example demonstrates the invocation of the apply function with only one argument. greet doesn’t have any parameters so we didn’t provide apply an array of arguments.

Let’s say we have a method greetFriends that takes two arguments–two objects with a name property.

```javascript
Person.prototype.greetFriends = function (friendA, friendB) {
    return this.name + ' says hi to ' + friendA.name + ' and ' + friendB.name + '.';
};

var bill = {name: 'Bill Watterson'};

alert(calvin.greetFriends.apply(bill, [calvin, hobbes]));
//Bill says hi to Calvin and Hobbes.
```

In this example, we supply two arguments to the apply function: bill as the context for this and an array with our two person objects. calvin and hobbes become the parameters friendA and friendB in greetFriends.

### CSS

#### Specificity

Is the means by which browsers decide which CSS property values are the most relevant to an element and, therefore, will be applied. Specificity is based on the matching rules which are composed of different sorts of CSS selectors.

Specificity is a weight that is applied to a given CSS declaration, determined by the number of each selector type in the matching selector. When multiple declarations have equal specificity, the last declaration found in the CSS is applied to the element. Specificity only applies when the same element is targeted by multiple declarations. As per CSS rules, directly targeted elements will always take precedence over rules which an element inherits from its ancestor.

### Thanks to:

 * [Markdown-editor](https://jbt.github.io/markdown-editor) for Markdown parsing
 * [Taylor Mcgann](http://blog.taylormcgann.com) for strong concepts on JS
 * [Medium](https://medium.com/@cramirez92/s-o-l-i-d-the-first-5-priciples-of-object-oriented-design-with-javascript-790f6ac9b9fa) For SOLID concepts
