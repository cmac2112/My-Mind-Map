
2024-10-10 17:20

Status:

Tags:[[React]], [[JavaScript]], [[Web dev book]]

# web dev book ch 11


# 11.1 Getting started with [[React]]

[[React]] is a front-end [[JavaScript]] library for creating interactive user interfaces. React allows developers to create custom [[HTML]] elements with behavior defined in [[JavaScript]] and styles defined in [[CSS]]. React automatically updates the UI when data within the [[HTML]] changes

1. `React.Dom.createRoot()` creates and returns a root [[DOM]] node inside the given element.
2. `Root.render()` renders a [[React]] element into the root [[DOM]] node. React uses a 'Virtual Dom', an in-memory copy of the browser's [[DOM]], to facilitate the rendering of the root [[DOM]] node into the browser's [[DOM]]

```
<!DOCTYPE html>
<html lang="en">
   <head>
      <title>Hello React!</title>
      <script src="https://unpkg.com/react/umd/react.development.js"></script>
      <script src="https://unpkg.com/react-dom/umd/react-dom.development.js"></script>
      <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
   </head>
   <body>
      <div id="root"></div>

      <script type="text/babel">
     
      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(<h1>Hello React!</h1>);
         
      </script>
   </body>
</html>
```
```
1. React requires multiple JavaScript files, including a library called Babel.
2. The React code appears in <script> tags using type="text/babel" so the Babel library can convert the code into plain JavaScript.
3. createRoot() creates a root DOM node inside the div element with id="root".
4. render() places the h1 element inside the root DOM node.
5. Changes to the virtual DOM cause React to update the browser's DOM. The browser displays: Hello React!
```

# 11.2 JSX

[[JSX]] ([[JavaScript]] [[XML]]) is an [[XML]]-like syntax extension to [[JavaScript]]. React uses [[JSX]] to create [[HTML]] that is inserted into a [[React]] webpage. A tool like babel transpiles or converts the [[JSX]] into standard [[JavaScript]]

```
Transpiler vs. compiler

Transpilers and compilers are both programs that convert one language into another. However, a compiler usually produces machine-executable code, and a transpiler produces code in a high-level language. Ex: Babel is a transpiler that converts JSX into JavaScript.

```

[[JSX]] Rules

writing [[JSX]] is like writing [[HTML]] but with some special rules

- A JSX expression may use {exp} to include a [[JavaScript]] expression. EX:`<h1> hello {name}</h1>` inserts the name variable's value into the JSX expression
- JSX attributes require quotes around the attribute values unless the value is specified with { }. EX: `<a href"http://google.com">Link</a>` and `<a href={url}>Link</a>` are valid
- The JSX attribute className must be used instead of class because class is a reserved [[JavaScript]] keyword. `<h1 className="special">Special heading</h1>`
- A JSX expression must start with an opening tag and end with a closing tag. Void elements may be use a self-closing tag. 

Multi Element expressions
a JSX expression composed of multiple lines is usually wrapped in parentheses (). If a JSX expression contains multiple elements, a single parent element must surround the child elements. A `fragment element <></>` may be used in place of a parent element, fragments are ignored when converting JSX into DOM nodes

# 11.3 Components
Function and Class Components

A [[React]] element is a single [[HTML]] element and is the smallest building block of a [[React]] app. [[React]] elements are combined into a component, which is responsible for rendering part of a [[React]] app's UI

Components can be implemented in 2 ways
1. a function component is a function that returns a React element
2. a class component is a class that extends `React.Component` and has a render() method that returns a [[React]] element
In recent updates to react, functions are typically used. Classes used to have more functionality but not much anymore


Props
component attributes are passed to components in an object called props (properties)
ex: `<Greeting name="Jasmine" />` creates the props object {name: "jasmine"}

the props object is passed as a parameter to a function component. 

![[Pasted image 20241010174555.png]]
Components in modules

Components may be organized into modules. A module is a JavaScript file that contains one or more variables, functions, or classes that are exported for use in another module. An export statement indicates which module contents are to be exported. An import statement indicates which module contents are to be imported.

# 11.4 Event handling 

Events and event handlers

A React Event is an action, usually caused by the user, that is similar to [[DOM]] events like click, key press, submit, etc. An event handler is specified on an element with "on" prefix using camelCase syntax

```
function Greeting(props) {
   function helloClick() {
      alert(`Hello, ${props.name}!`);
   }
 
   return (
      <button onClick={helloClick}>
         Say Hello
      </button>
   );
 }

function App() {
   return (
      <Greeting name="Jose" />
   );
}
1. The Greeting component is supplied the name Jose.
2. Greeting returns a button with a click event handler called helloClick.
3. When the user clicks the button, helloClick() is called. The function shows an alert saying hello to Jose.
```


React event parameter

An event handler has an optional React event parameter. The event parameter specifies additional information about the event. Ex: `event.target` is the widget that caused the event to occur

```
function Greeting(props) {
   function greetClick(event) {
      const greeting = event.target.id === "helloBtn" 
         ? "Hello" : "Hey";
            
      alert(`${greeting}, ${props.name}!`);
   }
 
   return (
      <div>
         <button id="helloBtn" onClick={greetClick}>
            Say Hello
         </button>
         <button id="heyBtn" onClick={greetClick}>
            Say Hey
         </button>
      </div>
   );
}

function App() {
   return (
      <Greeting name="Jose" />
   );


}
1. The Greeting returns two buttons, one with ID helloBtn and the other with ID heyBtn. Both buttons call greetClick() when clicked.
2. When the user clicks the "Say Hello" button, greetClick() is called with an event parameter representing the click event.
3. event.target is the button that was clicked, the "Say Hello" button, so event.target.id is "helloBtn". greeting is assigned "Hello", and the alert says hello to Jose.
4. If the user clicks the "Say Hey" button, event.target is the "Say Hey" button. event.target.id is "heyBtn", so greeting is assigned "Hey", and the alert says hey to Jose.
```

Passing arguments to event handlers

An event handler may be passed arguments by using an arrow function to call the event handler.

```
function Greeting(props) {
   function greetClick(greeting) {
      alert(`${greeting}, ${props.name}!`);
   }
 
   return (
      <div>
         <button onClick={() => greetClick("Hello")}>
            Say Hello
         </button>
         <button onClick={() => greetClick("Hey")}>
            Say Welcome
         </button>
      </div>
   );
}
```


# 11.5 State

Storing and changing state

A [[React]] component may need to remember the value of one or more variables as the variables change over time. The current values of a component's variables is called the component's state. The `useState()` function takes an initial state and returns an array containing the current state and a function that updates the state

Hooks

`useState()` is an example of a Hook. A Hook is a function that "hooks into" a React feature. Hooks were added in React 16.8 to allow function components to perform actions previously only available to class components. Older online sources use older methods to maintain state instead of using `useState()`.


### Multiple state variables

Most React apps require saving the state of multiple values. The Movie component in the example below stores the movie's title, rating, and release year in three separate variables. When the Change Movie button is clicked, the title, rating, and release year are changed to different values.

Ex
```
function Movie() {
   const [title, setTitle] = useState("Schindler's List");
   const [rating, setRating] = useState("R");
   const [releaseYear, setReleaseYear] = useState(1993);

   function changeMovie() {
      setTitle("Hidden Figures");
      setRating("PG-13");
      setReleaseYear(2016);
   }

   return (
      <>
         <h1>Favorite Movie</h1>
         <p>
            {title}, {rating}, {releaseYear}
         </p>
         <button onClick={changeMovie}>
            Change Movie
         </button>
      </>
   );
}
```

Objects in state

When multiple related values need to be stored in state, a [[React]] component may group the related values into a single object.

```
function Movie() {

   const [movie, setMovie] = useState({
      title: "Inception",
      rating: "PG-13",
      releaseYear: 2010
   });

   function changeTitle() {
      setMovie(prevState => ({
         ...prevState, title: "Titanic" 
      }));
   }

   return (
      <>
         <h1>Favorite Movie</h1>
         <p>
            {movie.title}, {movie.rating}, {movie.releaseYear}
         </p>
         <button onClick={changeTitle}>
            Change Title
         </button>
      </>
   );
}
1. useState() sets the initial state of movie to an object with a title, rating, and releaseYear.
2. The Movie component displays the initial movie title, rating, and releaseYear.
3. When the user clicks the Change Title button, changeTitle() calls setMovie() to change the movie title.
4. The prevState variable is the movie's previous state. The spread operator (...) adds the current movie properties to the new object. The title property is set to a new title, replacing "Inception" with "Titanic".
5. The new title is displayed in the webpage along with the previous rating and releaseYear.
```

# 11.6 Conditional Rendering

If-Else statement

A component may need to conditionally render different content based on the application state. Ex: A component could display one message to a logged in user and a different message to a guest user

``` example
function DaysRemaining(props) {
   if (props.days === 0) {
      return <p>No days remaining!</p>;
   }
   else if (props.days === 1) {
      return <p>One day remains.</p>;
   }
   else {
      return <p>{props.days} days remain.</p>
   }
}
```

[[Conditional (ternary) 

The ternary operator can be used to conditionally render content. The ternary operator has the form: `condition ? expression1 : expression2` After evaluating the condition, the operator returns the first expression if the condition is true and the second expression if false

```
function Light(props) {
   return (   
      <>
         { props.on ? 
            <p>Light is on!</p> 
         : 
            <p>Light is off.</p> 
         }      
      </>
   );
}
```

[[Logical && operator]] (and)

The logical `&&` operator may be used to render conditional content by placing an expression on the left side of `&&` and [[JSX]] to render on the right side of `&&`. When the expression is true, the [[JSX]] renders. When the expression is false, the [[JSX]] does not render

# Short-circuit evaluation

In JavaScript, `true && expression` evaluates to `expression` and `false && expression` evaluates to `false`. When the JavaScript interpreter ignores the expression on the right side of `&&` because the expression on the left is false, the interpreter is said to be "short-circuiting".

# 11.7 Lists [[React]]

Creating a list

In [[React]], lists are usually created in [[JSX]] with the `map()` method. The [[JavaScript]] array method `map()` uses a callback function that maps each array element to a new element, creating a new array

```
function CourseList() {
   const courseTitles = ["African History", "Greek II", 
      "Basic Chemistry"];

   return (
      <ol>
         {courseTitles.map(course => <li>{course}</li>)}
      </ol>
   );
}

function App() {
   return <CourseList />;
}

1. The CourseList component defines an array of course titles.
2. map() returns a new array where each course title appears in an li element.
3. CourseList returns the ordered list, which is rendered in the browser.
```

## Keys

When viewing the previous example, the browser's console will warn: `Each child in a list should have a unique "key" prop` A `key` property is an identifier assigned to each list items that helps [[React]] when list updates occur. If a list item is added, updates, or removed due to an event, [[React]] uses the keys to efficiently update just the modified list item instead of re-rendering the entire list

Typically a key is assigned with a unique Id. If no suitable Id exists, the key may be assigned with an array index. Keys must be unique among siblings but do not have to be globally unique.

```
function CourseList() {
   const courses = [
      { id: 1, title: "African History" },
      { id: 2, title: "Greek II" }, 
      { id: 3, title: "Basic Chemistry" }
   ];

   return (
      <ol>
         {courses.map(course => 
            <li key={course.id}>
               {course.title}
            </li>)}
      </ol>
   );
}

1. The CourseList component defines an array of course objects, each with a unique ID.
2. map() returns a new array where each li element's key property is assigned with the course id, and the course title appears inside the li element.
3. CourseList returns the ordered list, which is rendered in the browser.
```


# example, todo list

```
import { useState } from "react";
import "./App.css";

function TodoList() {

   const [task, setTask] = useState("");
   const [taskItems, setTaskItems] = useState([]);

   function addItem(event) {
      event.preventDefault();

      const newItem = {
         key: Date.now(),
         text: task
      };

      setTaskItems(prevItems => [...prevItems, newItem]);
   }

   return (
      <>
         <h1>Todo List</h1>
         <form onSubmit={addItem}>
            <label htmlFor="task">Task?</label>
            <input id="task" type="text" 
               value={task} onChange={(e) => setTask(e.target.value)} />
            <button type="submit">Add</button>
         </form>
      </>
   );
}

function App() {
   return <TodoList />;
}

export default App;
```

Example above has the functionality but lacks the means to display the items to the screen


```
function TodoItems(props) {

   const todoItems = props.items;

   return (
      <ol>
         {todoItems.map((item) =>
            <li key={item.key}>
               {item.text}
            </li>
         )}
      </ol>
   );
}
```

Deleting Tasks

The user should be able to delete completed tasks from the list.

```
function TodoItems(props) {

   const todoItems = props.items;

   return (
      <ol>
         {todoItems.map((item) =>
            <li key={item.key}>
               {item.text} &nbsp;
               <button onClick={() => props.delete(item.key)}>                  X               </button>            </li>
         )}
      </ol>
   );
}

function TodoList() {

   ...

   function deleteItem(key) {      setTaskItems(prevItems => prevItems.filter(         item => item.key !== key));   }
   return (
      <>
         <h1>Todo List</h1>
         ...
         <TodoItems items={taskItems}
            delete={deleteItem} />      </>
   );
}
```

# 11.10 Router

React router

Typically, changes in the browser's [[URL]] results in the browser loading a new webpage. But [[React]] apps often use changes in the [[URL]] to render different components or execute different programming statements

`React Router` is a library that allows [[React]] apps to display content based on the browser's [[URL]] path.

A typical react app imports three common React Router components:
1. BrowserRouter - the component that tracks changes to the browser's [[URL]] path
2. Routes - BrowserRouter's child component that contains one or more route components
3. Route - the Routes' child component that defined an element to display when the browser's URL path matches the specified path
```
import { BrowserRouter, Route, Routes } from "react-router-dom";

function App() {
   return (
      <BrowserRouter>
         <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/products" element={<Products />} />
            <Route path="*" element={<NotFound />} />
         </Routes>
      </BrowserRouter>         
  );
}
1. The BrowserRouter, Route, and Routes components are imported from react-router-dom.
2. The BrowserRouter component contains a Routes component, which contains four Route components.
3. Each Route specifies a path and corresponding element. Each element specifies a React component.
4. When the browser's URL path contains / only, the Home component renders.
5. When the path contains /about, the About component renders.
6. A URL path that doesn't match any other Route paths matches the * path and renders the NotFound component.
```

## Navigation

If an anchor element is used to create naviagation links for the React app's routes, clicking the links results in the entire webpage being reloaded

To prevent reloading, the React Router component `<Link>` produces a link that navigates to a route without reloading the webpage

```
import { 
   BrowserRouter, 
   Route, 
   Routes, 
   Link
} from "react-router-dom";

function App() {
   return (
      <BrowserRouter>
         <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/products" element={<Products />} />
            <Route path="*" element={<NotFound />} />
         </Routes>
         <NavBar />      </BrowserRouter>         
  );
}

function NavBar() {
   return (
      <nav>
         <ul>
            <li>
               <Link to="/">Home</Link>            </li>
            <li>
               <Link to="/products">Products</Link>            </li>
            <li>
               <Link to="/about">About</Link>            </li>
         </ul>
      </nav>
   );
}

function Home() {
   return <h1>Home</h1>;
}

function Products() {
   return <h1>Products</h1>;
}

function About() {
   return <h1>About</h1>;
}

function NotFound() {
   return <h1>Not Found</h1>;
}

export default App;
```

## url parameters

A React app may need to extract information from a URL path. 
A URL parameter may be specified in a Route path by placing a colon before the parameter name
ex: `path="products/:productID"` associates any string like "123" in the URL path "/products/123" with the parameter productId

The value of a URL parameter can be obtained with the `useParams()` hook, which returns an object of URL parameters and values

```
import { BrowserRouter, Route, Routes, Link, useParams } 
   from "react-router-dom";

function App() {
   return (
      <BrowserRouter>
         <Routes>
            ...
            <Route path="/products/:productId" 
               element={<ProductDetails />} />
         </Routes>
      </BrowserRouter>    
  );
}

const products = [
   { id: 111, name: "Blaze", desc: "About Blaze..." },
   { id: 222, name: "Comet", desc: "About Comet..." },
   { id: 333, name: "Doodle", desc: "About Doodle..." }
];

function ProductDetails() {
   const { productId } = useParams();
   const product = products.find(prod => prod.id == productId);

   return (      
      <>
         <h1>Product Details</h1>
         <p>Name: {product.name}</p>
         <p>Description: {product.desc}</p>
      </>
   );
}
1. The App component creates a Route with a URL parameter called productId.
2. When the browser's URL path contains "/products/222", the "222" part is assigned to the URL parameter productId.
3. ProductDetails calls useParams(), which returns an object of key/value pairs from the path. The productId variable is assigned with the "222" string from the path.
4. The find() function returns the product object in the products array that has the id 222.
5. ProductDetails renders details about the Comet product in the browser.
```

## Search Parameters

A react app may need to extract search parameters from a URL's query string. Ex: An app that supports product search may use "search?prod=test&limit=10" to search for a product containing the work "test" and limit the results to 10 items

ReactRouter provides the `useSearchParams()` hook to read and change a URL's search parameters

```
import { Link, useSearchParams } from "react-router-dom";
const products = [
   { id: 111, name: "Blaze", desc: "Keep warm on cold wintry nights." },
   { id: 222, name: "Comet", desc: "Light up the night without batteries." },
   { id: 333, name: "Doodle", desc: "Write on any surface." },
   { id: 444, name: "Bloom", desc: "Add a pleasing smell to any room." }
];

function ProductSearch() {
   const [searchParams, setSearchParams] = useSearchParams();

   let searchResults = [];

   // If user has entered search text, find what matches
   if (searchParams.get("prod")) {
      searchResults = products.filter(product => {
         const searchText = searchParams.get("prod").toLowerCase();
         return product.name.toLowerCase().includes(searchText);
      });
   }

   return (
      <>
         <h1>Product Search</h1>
         <input 
            type="search"
            placeholder="Search"
            value={searchParams.get("prod") || ""}
            onChange={(e) => setSearchParams({ "prod" : e.target.value })} />

         <ol>
            {searchResults.map(product => 
               <li key={product.id}>
                  <Link to={`/products/${product.id}`}>
                     {product.name}
                  </Link>
               </li>
            )}
         </ol>
      </>
   );
}

export default ProductSearch;
```

# 11.11 Styling

Stylesheets

A react component is usually styled with a [[CSS]] stylesheet in a .css file that matches the component name.

```
import "./Welcome.css";

function Welcome() {
   return <p className="para">Welcome!</p>;
}

export default Welcome;
```

### CSS modules

An alternative method for creating component CSS classes is to create a CSS module. A CSS module is a CSS file whose class names are accessible to only the component that imports the module. A CSS module's file is named _ComponentName_.module.css. Ex: Welcome.module.css for the Welcome component.

```
import styles from "./Welcome.module.css";

function Welcome() {
   return <p className={styles.para}>
      Welcome!</p>;
}

export default Welcome;
```

## bootstrap

Instead of creating CSS classes from scratch, a developer may choose to use CSS classes that others have created. Bootstrap covered elsewhere in this material, is a popular third-party library for styling a React app

```
function App() {
   return (
      <div className="m-3">
         <h1 className="display-1">Bootstrap Example</h1>
         <p className="text-primary">
            Bootstrap contains many CSS classes that make 
            styling a breeze! 
         </p>
         <blockquote className="border w-25 p-2 shadow">
            <p className="fs-4">"Learning never exhausts the mind."</p>
            <footer className="text-muted">Leonardo da Vinci</footer>
         </blockquote>
      </div>
   );
}

export default App;
```

# 11.13 Fetching Data

 Calling `fetch()`
A react component may need to retrieve data from a network request
the `fetch()` method is commonly used to send web API requests. Another option for sending web API requests is Axios, a third-party library.

```
async function fetchForecast() {
   const url = "https://wp.zybooks.com/weather.php?zip=90210";
   const response = await fetch(url);
   if (response.ok) {
      const result = await response.json();
      console.log("Day 1 high is " + result.forecast[0].high);
   }
};
1. The asynchronous function fetchForecast() defines a URL that asks the zyBooks web API for the five day forecast for ZIP code 90210.
2. fetch() sends an HTTP request to the zybooks.com web server.
3. The web server returns a JSON-encoded forecast for the 90210 ZIP code.
4. response.ok is true when the HTTP response has a 2xx status code. json() returns a JavaScript object containing the JSON-encoded data.
5. result.forecast is an array of objects containing the high, low, and general description for each day.
```

## The Effect Hook

The `Effect hook` is a React hook that allows a component to perform a "side effect". A side effect is code that changes something outside of the component, like manually updating [[DOM]] elements or fetching data with a web [[API]]. The effect hook is created by calling `useEffect()` with a function argument that, by default, always executes after the component renders

```
import { useEffect, useState } from "react";

function App() {
   const [forecast, setForecast] = useState([{ high: 0 }]);

   useEffect(() => {      
      async function fetchForecast() {
         const url = "https://wp.zybooks.com/weather.php?zip=90210";
         const response = await fetch(url);
         if (response.ok) {
            const result = await response.json();
            if (result.success) {
               setForecast(result.forecast);
            }
         }
      }

      fetchForecast();
   });

   return (
      <p>Day 1 high is {forecast[0].high}.</p>
   );
}

export default App;

1. useEffect is imported from the react library.
2. The forecast state variable is initialized with an array containing a single object: { high: 0 }.
3. App renders "Day 1 high is 0." in the browser.
4. Immediately after rendering, the useEffect() function argument executes.
5. fetchForecast() is called and fetches the weather forecast for 90210.
6. setForecast() sets the forecast state variable to an array of five objects obtained from the web API.
7. Changing the forecast state variable causes the App component to re-render, showing "Day 1 high is 82".
```

## useEffect's dependency array

The `useEffect()` function argument is called after every component render unless the function is supplied with a second argument, a dependency array that lists all variables used by the effect that may change over time. An empty array indicates the effect's function has no dependencies but should only execute only once after the first component render 
ex:
`useEffect(() => {code code code...}, []);`

Here is changed code from before,
1. the app component displays a form that allows the user to enter a zip code
2. the form's submit event handler sets the zip state variable with the value from the form
3. the call to `useEffect()` now takes a dependency array argument containing the zip state variable. When the zip changes, React executes the effect's function argument to fetch the weather for the new ZIP code
4. the app renders the full five-day forecase in a list
```
import { useEffect, useState } from "react";

function App() {
   const [forecast, setForecast] = useState([]);
   const [zip, setZip] = useState("90210");
   function handleSubmit(event) {
      event.preventDefault();
      setZip(event.target.zip.value);   }

   useEffect(() => {      
      async function fetchForecast() {
         const url = `https://wp.zybooks.com/weather.php?zip=${zip}`;         const response = await fetch(url);
         if (response.ok) {
            const result = await response.json();
            if (result.success) {
               setForecast(result.forecast);
            }
         }
      }

      fetchForecast();
   }, [zip]);
   return (
      <>
         <h1>Five Day Weather Forecast For {zip}</h1>         <form onSubmit={handleSubmit}>
            <input type="number" id="zip" />            <button type="submit">Submit</button>
         </form>
         <ol>
            {forecast.map((day, index) => (
               <li key={index}>
                  High: {day.high}, Low: {day.low}, Desc: {day.desc}
               </li>
            ))}
         </ol>
      </>
   );
}

export default App;
```
## loading and error messages

When the network is congested or the web server is busy, a web API request may result in a delayed response. Additionally, an error may occur when sending a web [[API]] request or when receiving back a response. The user should be informed when the app is waiting for a response and when errors occur

Two new state variables are added in the example

1. isLoading - indicates if app is waiting on the api response or now. When set to true, App renders a "Loading..." message. when set to false, App renders the forecast
2. errorMessage - indicates an error message to display. When set to an empty string, App renders no error message. Otherwise, App renders the error message
```
import { useEffect, useState } from "react";

function App() {
   const [forecast, setForecast] = useState([]);
   const [zip, setZip] = useState("90210");
   const [isLoading, setIsLoading] = useState(false);   const [errorMessage, setErrorMessage] = useState("");
   function handleSubmit(event) {
      event.preventDefault();
      setZip(event.target.zip.value);
   }
   
   useEffect(() => {      
      async function fetchForecast() {
         setForecast([]);
         setIsLoading(true);         setErrorMessage("");         
         const url = `https://wp.zybooks.com/weather.php?zip=${zip}`;
         const response = await fetch(url);
         if (response.ok) {
            const result = await response.json();
            if (result.success) {
               setForecast(result.forecast);
            }
            else {
               setErrorMessage(result.error);            }
         }
         else {
            setErrorMessage("Error in the response.");         }
         
         setIsLoading(false);      }

      fetchForecast();
   }, [zip]);

   return (
      <>
         <h1>Five Day Weather Forecast For {zip}</h1>
         <form onSubmit={handleSubmit}>
            <input type="number" id="zip" />
            <button type="submit">Submit</button>
         </form>
         
         {errorMessage.length > 0 && <p>{errorMessage}</p>}
         {isLoading ? (            <p>Loading...</p>         ) : (            <ol>
               {forecast.map((day, index) => (
                  <li key={index}>
                     High: {day.high}, Low: {day.low}, Desc: {day.desc}
                  </li>
               ))}
            </ol>
         )}      </>
   );
}

export default App;
```