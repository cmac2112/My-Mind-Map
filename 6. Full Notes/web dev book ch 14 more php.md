
2024-10-29 19:46

Status:

Tags:[[PHP]], [[Programming Language]], [[web dev book ch 13 PHP]]

# web dev book ch 14 more php

# 14.1 Regular expressions

[[PHP]] applications often need to determine if a string conforms to a pattern. 

A [[regular expression]] often shortened to regex is a string pattern that is matched against a string.

regular expressions is defined between two forward slashes EX: `$regex = "/abc/";` defines a regex with the pattern "abc", which matches an string that contains "a" followed by "b" followed by "c"

The [[PHP]] function preg_match(regex, string) returns 1 if the regex matches the string and 0 if no match is found

```
$words = ["ban", "babble", "make", "flab"];
$regex = "/ab/";

foreach ($words as $word) {
   if (preg_match($regex, $word)) {
      echo "<p>$word matches!</p>";
   }
}
1. Define a regular expression that matches words containing "ab".
2. Loop through each word in the words array.
3. preg_match() returns 0 (which evaluates to false) because "ban" does not contain "ab".
4. preg_match() returns 1 (which evaluates to true) because "babble" contains "ab".
5. preg_match() returns 0 because "make" does not contain "ab".
6. preg_match() returns 1 because "flab" contains "ab".
```


### Special characters

Regular expressions use characters with special meaning to create more sophisticated patterns. The + character matches the preceding character at least once. Ex: `/ab+c/` matches one "a" followed by at least one "b" and one "c", so "abc" and "abbbbc" both match. However, "ac" does not match because the required "b" is missing.

## 

Table 14.1.1: Selected special characters in regex patterns.

|Character|Description|Example|
|---|---|---|
|`*`|Match the preceding character 0 or more times.|`/ab*c/` matches "abc", "abbbbc", and "ac".|
|`+`|Match the preceding character 1 or more times.|`/ab+c/` matches "abc" and "abbbbc" but not "ac".|
|`?`|Match the preceding character 0 or 1 time.|`/ab?c/` matches "abc" and "ac", but not "abbc".|
|`^`|Match at the beginning.|`/^ab/` matches "abc" but not "cab".|
|`$`|Match at the end.|`/ab$/` matches "cab" but not "abc".|
|`\|`|Match string on the left OR string on the right.|`/ab\|cd/` matches "abc" and "bcd".|

A metacharacter is a character or character sequence that matches a class of characters in a regular expression. Ex: The period character matches any single character except the newline character. So `/ab.c/` matches "abZc" and "ab2c", but not "abc" since the period must match a single character. Other metacharacters begin with a backslash.

## 

Table 14.1.2: Selected metacharacters in regex patterns.

| Metacharacter | Description                                                        | Example                                          |
| ------------- | ------------------------------------------------------------------ | ------------------------------------------------ |
| `.`           | Match any single character except newline.                         | `/a.b/` matches "aZb" and "a b".                 |
| `\w`          | Match any word character (alphanumeric and underscore).            | `/a\wb/` matches "aAb" and "a5b" but not "a b".  |
| `\W`          | Match any non-word character.                                      | `/a\Wb/` matches "a-b" and "a b" but not "aZb".  |
| `\d`          | Match any digit.                                                   | `/a\db/` matches "a2b" and "a9b", but not "aZb". |
| `\D`          | Match any non-digit.                                               | `/a\Db/` matches "aZb" and "a b", but not "a2b". |
| `\s`          | Match any whitespace character (space, tab, form feed, line feed). | `/a\sb/` matches "a b" but not "a4b".            |
| `\S`          | Match any non-whitespace character.                                | `/a\Sb/` matches "a!b" but not "a b".            |

# 14.2 [[Error Handling]]

Displaying Error messages

Developers normally enable PHP error reporting to send error messages (parse errors, fatal errors, warnings, and notices) to the browser when developing PHP scripts. But, PHP error reporting should be turned off in a production environment (`display_errors = 0` in php.ini) to avoid showing messages that users will not understand or messages that could be exploited to compromise the web server.

`$file = fopen("suspects.txt", "r") or die("Can't open suspects.txt");`

## Logging errors

[[PHP]] sends error to an error log, a file that is named by the `error_log` setting in php.ini

A developer may send custom messages to the error log using the [[PHP]] function `error_log(message)` 

## 

Figure 14.2.3: Logging an error and emailing an error.
```

// Log the error
if (!connectToDatabase()) {
   error_log("Failed to connect to the database");
}

// Email the system admin
if (systemResourcesLow()) {
   error_log("Warning: System resources are critically low!", 1, "admin@example.com");
}
```

## User defined error handlers

Developers can create user-defined error handlers that are automatically called when an error occurs. The `set_error_handler("errorHandler")` function registers an `errorHandler` function that is called when an error occurs. The error handler is a function wit the following parameters

- `errno` - Error report level(integer)
- `errstr` - Error description
- `errfile` - Filename that contains the error
- `errline` - line number of the error
- `errcontext` - Array of all variables that existed in the scope when the error occurred

Errors can be triggered with `trigger_error(message, errorno)` using one of the following error numbers  `E_USER_ERROR`, `E_USER_WARNING`, `E_USER_NOTICE`.

Error reporting levels

|Value|Constant|Description|Example|
|---|---|---|---|
|2|E_WARNING|Run-time warnings|// Opening non-existing file<br>$file = fopen("suspects.txt", "r");|
|8|E_NOTICE|Possible run-time logic error|// Outputting uninitialized variable<br>echo $homeRuns;|
|256|E_USER_ERROR|User-generated error that halts script execution|trigger_error("Value must be positive", E_USER_ERROR);|
|512|E_USER_WARNING|User-generated warning|trigger_error("Disk quota exceeded", E_USER_WARNING);|
|1024|E_USER_NOTICE|User-generated notice|trigger_error("Indicators are unusually high", E_USER_NOTICE);|

```
<?php

set_error_handler("errorHandler");

function errorHandler($errno, $errstr) {
   echo "<p>Error $errno: $errstr</p>";
}

$file = fopen("batting-average.txt", "r");
if ($file) {
   $battingAve = fread($file, filesize($file));
   fclose($file);
}

if ($battingAve < 0.1) {
   trigger_error("Batting average is too low.",
      E_USER_WARNING);
}
?>
1. set_error_handler() names a function called "errorHandler" to be called when an error occurs.
2. errorHandler() function outputs the error report level and description when an error occurs.
3. Trying to open batting-average.txt causes an E_WARNING error because batting-average.txt does not exist.
4. errorHandler() is called with $errno set to E_WARNING and $errstr set to the error description.
5. Because batting-average.txt was not opened, $battingAve was not initialized. Comparing an uninitialized variable with 0 causes an E_NOTICE error.
6. The uninitialized $battingAve is treated as 0, so the trigger_error() function generates an E_USER_WARNING error.
```


## Exception handling

Exception handling is the process of responding to an exception. An [[exception]] is an error that disrupts the normal flow of program execution. When an exception occurs, a program may need to execute code to handler the error, like displaying an error message or logging the error.

the `throw` statement throws an `Exception` object. Syntax: `throw new Exception("error message");` A thrown exception causes a fatal error that halts the script unless a try-catch statement is used to catch and handle the exception.
```
function findSum($numbers, $startIndex, $endIndex) {
   if ($startIndex < 0) {
      throw new Exception("startIndex is less than 0.");
   }
   else if ($endIndex >= count($numbers)) {
      throw new Exception("endIndex is too large.");
   }
        
   $sum = 0;
   for ($i = $startIndex; $i <= $endIndex; $i++) {
      $sum += $numbers[$i];
   }
   return $sum;
}

$nums = [1, 2, 3, 4];
echo findSum($nums, 0, 2);
echo findSum($nums, 3, 4);

echo "<p>Done!</p>";

sum = 0 + 1 + 2 + 3 = 6

6

Fatal error: Uncaught exception 'Exception' with message 'endIndex is too large.' in script.php:8

try {
   echo findSum($nums, 3, 4);
}
catch (Exception $e) {
   echo $e->getMessage();
}

echo "<p>Done!</p>";

1. findSum() function called to add the numbers in the nums array from index 0 to index 2.
2. findSum() function called to add the numbers in the nums array from index 3 to index 4.
3. $endIndex (4) is equal to count($numbers) (4), so the throw statement throws an Exception object, indicating a problem with the endIndex value.
4. The code does not handle the exception, so a fatal error results, the exception message is displayed in the browser, and the program halts prematurely.
5. Using a try-catch statement, the catch block handles the exception and uses the getMessage() method to output the exception message.
6. After the catch block executes, the program execution continues.
```

Finally block

A finally block may folllow a try or catch block and executes regardless of whether an exception was thrown or not. Developers use the finally block for any operations that must be executed, whether or not an exception was thrown.