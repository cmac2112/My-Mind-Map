
2024-09-15 19:40

Status:

Tags:[[web dev book ch 8]], [[JavaScript]] [[class]],

# Inheritance


Inheritance creates a new child class that adopts properties of a parent class. 
	Ex: a student class (child) may inherit from a Person class (parent), so a student class has the same properties of a Person and may add even more properties
Implementing inheritence:
	1. the child class calls the parent class' constructor function from the child's constructor function using the call() method
	2. the `Object.create()` method copies the parent's prototype, and the new copy is assigned to the child's prototype to give the child class the same functionality as the parent class
	3. the child class's `prototype.constructor` is explicitly set to the child's constructor function

// Parent class
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log("Hello. My name is " + this.name);
};
Person.prototype.sayGoodbye = function() {
  console.log("Goodbye!");
};

// Child class
function Student(name, gpa) {   
  Person.call(this, name);
  this.gpa = gpa;
}

// Duplicate functionality of parent
Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

// Replace the parent's sayHello with a new method
Student.prototype.sayHello = function() {
  console.log("Hi, I'm " + this.name + " with a "
      + this.gpa + " GPA!");
}

let bob = new Student("Bob", 3.5);
bob.sayHello();
bob.sayGoodbye();

1. Constructor function Person takes a name parameter. Person.prototype is created with a constructor property that references the Person constructor function.
2. Methods sayHello() and sayGoodbye() are added to Person.prototype.
3. Constructor function Student takes a name and gpa parameter. Student.prototype is created with a constructor property that references the Student constructor function.
4. Object.create() creates a new Person.prototype object, and the new object is assigned to Student.prototype.
5. Student.prototype.constructor is reset back to the Student constructor function.
6. A new sayHello() method is defined that outputs the student's name and GPA.
7. Object bob is instantiated using the Student function constructor.
8. Person constructor function is called with "this" referencing the current object. Person constructor function initializes name property, and Student constructor function initializes gpa property.
9. bob's sayHello() and sayGoodbye() methods are called.

```
function Game(title) {
  this.title = title;  
}

Game.prototype.startPlaying = function() {
  console.log("Now playing " + this.title + "!");
};

Game.prototype.stopPlaying = function() {
  console.log("Taking a break.");
};

function VideoGame(title){
   Game.call(this, title)
   let totalPoints = 0;
   
   this.getScore = function(){
      return totalPoints;
      }
   this.addToScore = function(points){
      totalPoints += points
      }
   }
   
VideoGame.prototype = Object.create(Game.prototype)
VideoGame.prototype.constructor = VideoGame;

let game = new VideoGame("Pac-Man")
game.startPlaying()
console.log(game.getScore())
game.addToScore(20)
game.addToScore(50)
console.log(game.getScore())
game.stopPlaying()

```


# Inheritance ES6

class Person {
   constructor(name, age) {
      this.name = name;
      this.age = age;
   }
    
   sayHello() {
      console.log("Hello.  My name is " + this.name + ".");
   }
}

// Student inherits from Person
class Student extends Person {
   constructor(name, age, gpa) {
      super(name, age);     // Call parent constructor
      this.gpa = gpa;
   }

   // Override parent's sayHello method
   sayHello() {
      console.log("Hi, I'm " + this.name + " with a " + this.gpa + " GPA!");
   }
}