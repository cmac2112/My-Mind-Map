
2024-08-27 09:30

Status:

Tags:[[C]], [[Python]], [[JavaScript]], 

# for loop

the for statement is a loop, a generalization of the [[While loop]].
The for loop is usually appropriate for loops in which the initialization and increment are single statements and logically related, since it is more compact than a while and it keeps the loop control statements in one place.

For loop in [[C]]:
	for (int i = 0; i <= 100; i = i + 1){
		printf(%d, i)
	}
This will print i 100 times


# Python
couple of different ways

for i in arr:
	will print every element of arr directly

for i in range(len(arr))
	same as other normal for loops in other languages
	initalizes i to a number, so you can access elements in a structure like
		arr[i]

# Javascript
for(let i=0; i < arr.length; i ++)


The `Array` method forEach() also loops through an array. The `forEach()` method takes a function as an argument. The function is called for each array element in order, passing the element and the element index to the function.

let groceries = ["bread", "milk", "peanut butter"];

// Display all elements in groceries array
groceries.forEach(function(item, index) {
   console.log(index + " - " + item);
});

The for-of loop is a simplified for loop that loops through an entire array. The array name is placed after the `of` keyword in a for-of loop. Each time through the loop, the next array element is assigned to the variable in front of the `of` keyword.
let groceries = ["bread", "milk", "peanut butter"];

// Display all elements in groceries array
for (let item of groceries) {
   console.log(item);
}

The `Array` method forEach() also loops through an array. The `forEach()` method takes a function as an argument. The function is called for each array element in order, passing the element and the element index to the function.

## 

Figure 6.8.3: Looping through an array with the forEach() method.

let groceries = ["bread", "milk", "peanut butter"];

// Display all elements in groceries array
groceries.forEach(function(item, index) {
   console.log(index + " - " + item);
});

### For-in loop

The for-in loop iterates over an object's properties in arbitrary order and is ideal for looping through an object map's elements. The for-in loop declares a variable on the left side of the `in` keyword and an object on the right. In each iteration, the variable is assigned with each of the object's properties.


# for each

```javascript
actors.forEach((value, key) => {
    console.log(`Actor: ${key}, Role: ${value.role}`);
});
```