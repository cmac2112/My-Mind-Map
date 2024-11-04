
2024-09-10 10:45

Status:

Tags:[[Javascript]]

# Objects
An object is an unordered collection of properties. An object property is a name-value pair, where the name is an identifier and the value is any data type. Objects are often defined with an object literal. An object literal (also called an object initializer) is a comma-separated list of property name and value pairs.

let book = {};

book = {
   title: "Outliers",
   published: 2011,
   keywords: ["success", "high-achievers"]
};

# getters and setters

let rectangle = {
   width: 5,
   height: 8,
   get area() {
      return this.width * this.height;  
   },
   set area(value) {
      // Set width and height to the square root of the value
      this.width = Math.sqrt(value);
      this.height = this.width;
   }
};

let game = {
   firstOpponent: "Serena Williams",
   firstOpponentScore: 2,
   secondOpponent: "Garbine Muguruza",
   secondOpponentScore: 0,
   get winner() { 
      if (this.firstOpponentScore > this.secondOpponentScore) {
         return this.firstOpponent;
      }
      else if (this.secondOpponentScore > this.firstOpponentScore) {
         return this.secondOpponent;
      }
      else {
         return "Tie";
      }
   }
};