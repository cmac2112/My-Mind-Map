
2024-09-06 22:52

Status: in progress

Tags:[[Data Structure]], [[JavaScript]], [[Python]], [[C]]

# Arrays

# C 
good luck

# python
similar to [[JavaScript]] but not entirely
# Javascript arrays and methods

defined as 
let array = [];

Searching an array
The array methods indexOf() and lastIndexOf() search an array and return the index of the first found value or -1 if the value is not found. `indexOf()` searches from the beginning of the array to the end. `lastIndexOf()` searches from the end of the array to the beginning. Both functions take two arguments:

1. `searchValue` - The value to search for
2. `startingPosition` - Optional argument that indicates the index at which the search should begin (default is 0 for `indexOf()` and `array.length - 1` for `lastIndexOf()`)


The array method sort() sorts an array in ascending (increasing) order. `sort()`'s default behavior is to sort each element as a string using the string's Unicode values. Sorting by Unicode values may yield unsatisfactory results for arrays that store numbers. Ex: 10 is sorted before 2 because "10" is < "2" when comparing the Unicode values of "1" to "2".

The `sort()` method can sort elements in other ways by passing a comparison function to `sort()`. The comparison function returns a number that helps `sort()` determine the sorting order of the array's elements:

- Returns a value < 0 if the first argument should appear before the second argument.
- Returns a value > 0 if the first argument should appear after the second argument.
- Returns 0 if the order of the first and second arguments does not matter.
let numbers = [200, 30, 1000, 4];

// Sort based on Unicode values: [1000, 200, 30, 4]
numbers.sort();     

// Sort numbers in ascending order: [4, 30, 200, 1000]
numbers.sort(function(a, b) {
   return a - b;
});

javascript arrays can also hold a list of objects like

```
list = [{
x: 1, y:1
},
{
x:2, y:2
}]
etc
```