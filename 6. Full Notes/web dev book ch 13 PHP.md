
2024-10-25 18:17

Status:

Tags:[[PHP]], [[Web dev book]]

# web dev book ch 13 PHP


Full stack development ([[PHP]])

# 13.2 Getting started with [[PHP]]

[[PHP]] is a popular server side scripting language used to create web applications. Rasmus Lerdorf created [[PHP]] in 1994 and named his creation Personal Home Page. [[PHP]] has evolved over the years and now stands for PHP: Hpyertext Preprocessor

[[PHP]] is relatively easy to learn, free to use, and ships with the apache web server.


Php script is a file composed of [[HTML]] tags and php code inserted between `<?php and />` tags. When the browser requests a php script, the ber server starts the php engine, which compiles the requested php script and executes the code. The php script uses the `echo` statement to produce output that is sent to the browser in an [[HTTP]] response

# 13.3 Arithmetic and comparisons

[[PHP]] arithmetic operators perform arithmetic computations. When multiple arithmetic operators appear in a single arithmetic expression, the precedence of rules of basic arithmetic apply, and expressions surrounding by parentheses are evaluated first. 
arithmetic eval order
1. **
2. *,/,%
3. +, -


|Arithmetic operator|Name|Example|
|---|---|---|
|`+`|Add|// $x = 3<br>$x = 1 + 2;|
|`-`|Subtract|// x = 1<br>$x = 2 - 1;|
|`*`|Multiply|// $x = 6<br>$x = 2 * 3;|
|`/`|Divide|// $x = 0.5<br>$x = 1 / 2;|
|`%`|Modulus (remainder)|// $x = 0<br>$x = 4 % 2;|
|`**`|Exponentiation|// $x = 8<br>$x = 2 ** 3;|
|`++`|Increment|// Same as $x = $x + 1<br>$x++;|
|`--`|Decrement|// Same as $x = $x - 1<br>$x--;|
|Assignment operator|Description|Example|
|---|---|---|
|`+=`|Add to|// Same as $x = $x + 2<br>$x += 2;|
|`-=`|Subtract from|// Same as $x = $x - 2<br>$x -= 2;|
|`*=`|Multiply by|// Same as $x = $x * 3<br>$x *= 3;|
|`/=`|Divide by|// Same as $x = $x / 3<br>$x /= 3;|
|`%=`|Mod by|// Same as $x = $x % 4<br>$x %= 4;|
|`.=`|Concatenation|// Same as $x = $x . "test"<br>$x .= "test";|

Comparison

## 

Table 13.3.3: PHP comparison operators.

|Comparison operator|Name|Example|
|---|---|---|
|`==`|Equality|2 == 2          // true<br>"bat" == "bat"  // true|
|`!=`  <br>`<>`|Inequality|2 != 3          // true<br>"bat" <> "zoo"  // true|
|`===`|Identical|2 === 2     // true<br>"2" === 2   // false|
|`!==`|Not identical|2 !== 2     // false<br>"2" !== 2   // true|
|`<`|Less than|2 < 3          // true<br>"bat" < "zoo"  // true|
|`<=`|Less than or equal|2 <= 3          // true<br>"bat" <= "bat"  // true|
|`>`|Greater than|3 > 2          // true<br>"zoo" > "bat"  // true|
|`>=`|Greater than or equal|3 >= 2          // true<br>"zoo" >= "zoo"  // true|
|`<=>`|Spaceship (introduced in PHP 7)|1 <=> 1   // 0<br>1 <=> 2   // -1<br>2 <=> 1   // 1|

When a string is compared to a number with any comparison operator besides the identical and non-identical operators, the string is first converted into a number and then compared. 
When two strings are compared, [[PHP]] compares the [[ASCII]] values of each character in the strings from left to right.

[[PHP]] logic operators perform [[AND]] (&&) and [[OR]] (||) logic between two expressions. [[PHP]] also includes and, or, and xor operators that operate with different precedence and are not widely used
## 

Table 13.3.4: PHP logical operators.

|Logical operator|Name|Description|Example|
|---|---|---|---|
|`&&`|And|True if both sides are true|(1 < 2 && 2 < 3)  // true|
|`\|`|Or|True if either side is true|(1 < 2 \| 2 < 0)  // true|
|`!`|Not|True if expression is not true|!(2 == 2)  // false|

![[Pasted image 20241028192330.png]]
# 13.4 Conditionals

If else and elseif statements

an If-else statement execues a block of statements if the statement's condition is true.



# 13.5 loops

Three general purpose looping structures exist: while, do-white, and for statements.

```
while (condition) {
   body
}
```

## 

"Jump" statements in loops.

Three "jump" statements alter the normal execution of a loop:

1. `break` statement - Breaks out of a loop or switch statement immediately
2. continue statement - Causes a loop to iterate again without executing the remaining statements in the loop
3. goto statement - Jumps to another section in the program
```

for ($c = 1; $c <= 5; $c++) {
   if ($c == 4) {
      break;   // Leave the loop   }
   echo $c;   // 1 2 3 (missing 4 and 5)
}

for ($c = 1; $c <= 5; $c++) {
   if ($c == 4) {
      goto end;   // Jump to "end" section   }
   echo $c;   // 1 2 3 (missing 4 and 5)
}
end:
for ($c = 1; $c <= 5; $c++) {
   if ($c == 4) {
      continue;   // Iterate again immediately   }
   echo $c;   // 1 2 3 (missing 4) 5
}

Some developers use jump statements to write short and concise code, but others avoid using jump statements on the grounds that jump statements may introduce subtle logic errors that are difficult to find. This material avoids using jump statements.

```

# 13.6  Arrays

Indexed and associative arrays

A [[PHP]] array is an ordered collection of key/value pairs, They key may be an integer or a string, but the value may be any data type. An array with integer keys is often called an indexed array. An array with string keys is called an associative array.

The `foreach` loop iterates over an indexed array or associative array
```
// Iterates over an indexed array
foreach ($indexedArray as $value) {
   // body
}

// Iterates over an associative array
foreach ($assocArray as $key => $value) {
   // body
}
```

## multidimensional arrays

Indexed and associative arrays may contain arrays as values. A multidimensional array is an array of arrays

```
// Multidimensional array
$courses = [
   "123" => [
      "instructor" => "Cruz",
      "title" => "Intro to Computing"        
   ],
   "444" => [
      "instructor" => "Wang",
      "title" => "Western Civilization"
   ],
   "761" => [
      "instructor" => "Pratt",
      "title" => "English Composition"
   ]
];

// Who is teaching Western Civilization?
echo "<p>", $courses["444"]["instructor"], "</p>\n";

// Display all course titles
echo "<ul>";
foreach ($courses as $courseId => $course) {
   echo "<li>", $course["title"], "</li>\n";   
}
echo "</ul>";
1. $courses is an associative array where the keys are the course IDs of each course, and the values are an associative array containing the instructor and title of each course.
2. Western Civilization is stored in key "444", and the instructor's name is stored in key "instructor".
3. A foreach loop iterates over all the courses and displays each title.
```

# 13.7 Functions [[PHP]]

A function is a named group of statements, php functions are declared with the `function` keyword


# 13.8 Includes

the include statement inserts the contents of a file into a [[PHP]] script as the script is executing. Includes can save development time by ecapsulating frequently used code into a file that can be included in multiple scripts.

```
<!DOCTYPE html>   <!-- index.php -->
<html>
  <title>Super Drug Store</title>
  <link rel="stylesheet" href="styles.css">
  <body>
    <?php include "header.php"; ?>        
    <p>Come visit us in downtown Boulder!</p>
    <?php include "footer.php"; ?>
  </body>
</html>
```

## require statement
the require statement is identical to `include` except that require produces a fatal error and terminates the script immediately if the file is missing, whereas include produces a warning and continues executing the script

# 13.10 string, day/time, math

```
  

function countCapitalLetters($str) {
   $upperTotal = 0;
   $length = strlen($str);

   for ($i = 0; $i < $length; $i++) {
      $asciiValue = ord($str[$i]);
      if ($asciiValue >= 65 && $asciiValue <= 90) {
         $upperTotal++;
      }
   }

   return $upperTotal;
}

echo countCapitalLetters("HelP") . "\n";
echo countCapitalLetters(strtoupper("Help"));
1. countCapitalLetters() is called with "HelP" string.
2. strlen() returns the number of characters in "HelP".
3. The for loop iterates $i from 0 to 3.
4. ord() returns the ASCII value of the given character.
5. $upperTotal is only incremented when $asciiValue is between 65 (for "A") and 90 (for "Z"). 2 is returned because "HelP" has 2 capital letters.
6. strtoupper() capitalizes "Help" and returns "HELP". So, countCapitalLetters() is passed "HELP" and returns 4.
```

|Function|Description|Example|
|---|---|---|
|strcmp(string1, string2)|Returns 0 if both strings are equal, < 0 if `string1` < `string2`, and > 0 if `string1` > `string2`|// $result is < 0<br>$result = strcmp("Cat", "Dog");|
|strpbrk(string, charlist)|Returns the string starting from the first occurrence of one character from `charlist` in the `string` or FALSE if no characters are found|// $str will be "is is a test" ("i" is found first)<br>$str = strpbrk("This is a test", "aeiou");|
|strpos(string, search)|Returns the position of the first occurrence of `search` in the `string` or FALSE if the string is not found|// $pos will be 2 <br>$pos = strpos("This is a test", "is");|
|str_replace(search, replace, string)|Returns a string where `search` is replaced with `replace` in `string`|// $str will be "Thwas was a test"<br>$str = str_replace("is", "was", "This is a test");|
|substr(string, start, length)|Returns a substring beginning at position `start` in `string` that is `length` number of characters|// $str will be "is"<br>$str = substr("This is a test", 5, 2);|