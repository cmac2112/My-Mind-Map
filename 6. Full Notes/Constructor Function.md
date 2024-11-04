
2024-09-15 19:04

Status:

Tags:[[Web dev book]] [[class]]

# Constructor Function

# Javascript
is a function that initializes a new object whe n an object is instantiated with the `new` operator

`function Person(name, age) {
  this.name = name;
  this.age = age;

  this.sayHello = function() {
     console.log("Hello, " + this.name);
  };
};

let bob = new Person("Bob", 21);
let sue = new Person("Sue", 40);

bob.sayHello();
sue.sayHello();