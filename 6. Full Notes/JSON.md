
2024-09-14 13:32

Status:

Tags:[[JavaScript]][[web dev book ch 7]]

# JSON


JavaScript Object Notation or JSON is an efficient structured format for data based on a subset of the Javascript language

# Data types
1. string - unicode charactres enclosed within double quotes("). A few special characters must be escaped with a backslash: backslashes, double quotes, newlines, and tabs
2. Number - either an integer or decimal
3. [[Objects]] - unoerdered list of zero or more name/value pairs separated by commas and enclosed within braces ({}). A name in a Json object must be a string in double quotes. EX: { "Name": "Joe", "Age" : 35 }
4. [[Arrays]]- ordered list of zero or more JSON values separated by commas and enclosed within brackets []
5. [[Booleans]]
6. [[Null]]
Json structure is defiend recursively so that [[Objects]] can contain [[Arrays]] and [[Arrays]] can contain [[Objects]] to any arbitrary depth 

{
   "name": "John Doe",
   "vehicles": [
      {
         "make": "Ford",
         "model": "F-150",
         "color": "white"
      }, 
      {
         "make": "Toyota",
         "model": "Camry",
         "color": "red"
      }
   ],
   "married": false,
   "previous_customer": true,
   "known_associates": [],
   "notes": null
}

