
2024-09-08 19:02

Status:

Tags:[[React Website]]

# UseState
usage:
const [var, setvar] = React.useState()
`useState` returns an array with exactly two values:

1. The current state. During the first render, it will match the `initialState` you have passed.
2. The [`set` function](https://react.dev/reference/react/useState#setstate) that lets you update the state to a different value and trigger a re-render.

why?
React works on renders, when a state is updated a rerender is triggered to update the variable
This wont happen if you use a static variable

such as 

let count = 0

and you have a button that increments the count variable
<button onClick={(count) => count + 1 }

the count WILL increment but since there is no rerender, the value will not appear on the page. If you console log it it will be correct.

here is how you would use it in React

const [count, setCount] = React.useState(0)

<button onClick={() => setCount((count) => count + 1)}> 

