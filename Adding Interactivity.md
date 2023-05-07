
## **State: a component’s memory**

- Components often need to change what’s on the screen as a result of an interaction.
- Components need to “remember” things: the current input value, the current image, the shopping cart. In React, this kind of component-specific memory is called *`state`.*

You can add state to a component with a `[useState](https://react-ko.vercel.app/reference/react/useState)` Hook

```tsx
const [index, setIndex] = useState(0);
const [showMore, setShowMore] = useState(false);
```

## **Render and commit**

1. **Triggering** a render (delivering the diner’s order to the kitchen)
2. **Rendering** the component (preparing the order in the kitchen)
3. **Committing** to the DOM (placing the order on the table)

## **State as a snapshot**

Unlike regular JavaScript variables, **React state behaves more like a snapshot**.

```tsx
console.log(count);  // 0
setCount(count + 1); // Request a re-render with 1
console.log(count);  // Still 0!
```

**React state works like a snapshot** because **it captures the current values of the state variables at a particular point in time**. When the state is updated, React takes a new snapshot of the updated state and **compares it with the previous snapshot to determine what has changed**. Based on this comparison, React updates the UI to reflect the changes in state.

The value of a state variable never changes during rendering, even if the event handler is asynchronous. Looking at the onClick function in the code snippet below:

```tsx
const [number, setNumber] = useState(0);
// ...
return(
  <button onClick={() => {
        setNumber(number + 5);
        setTimeout(() => {
          alert(number);
        }, 3000);
      }}>+5</button>
)
```

The value of **`number`** remains 0 even after the call to **`setNumber(number + 5)`**. **This is because React takes a snapshot of the component's state when it renders, and the value of the state variable is fixed at that point in time**.

## **Queueing a series of state updates**

Setting state requests a new re-render, **but does not change it in the already running code**.

```tsx
// Before
 <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
```

`props`, `event handlers`, and `local variables` were all calculated **using its state at the time of the render.**

[each render’s state values are fixed](https://react-ko.vercel.app/learn/state-as-a-snapshot#rendering-takes-a-snapshot-in-time)

### If you want to update the state with the same value multiple times before the next render

You can pass a function to the state updater instead of the new value. This function can use the previous state value to calculate the next state.

You can fix this by passing an *updater function* when setting state. Notice how replacing `setScore(score + 1)` with `setScore(s => s + 1)`

For example, instead of calling **`setNumber(number + 1)`** multiple times, you can use the following code:

```tsx
// After
<button onClick={() => {
  setNumber(prevNumber => prevNumber + 1);
  setNumber(prevNumber => prevNumber + 1);
  setNumber(prevNumber => prevNumber + 1);
}}>+3</button>
```

In this way, each call to **`setNumber`** receives the **previous value of `number` as an argument and returns a new value based on that previous value**. This allows you to **update the state multiple times with the same value before the next render**.

## **Updating objects in state & Updating arrays in state**

State can hold any kind of JavaScript value, including objects. **But you shouldn’t change objects and arrays that you hold in the React state directly**. Instead, when you want to update an **object and array**, **you need to create a new one (or make a copy of an existing one)**, and then update the state to use that copy.

```tsx
export default function Form() {
  const [person, setPerson] = useState({
    name: 'Niki de Saint Phalle',
    artwork: {
      title: 'Blue Nana',
      city: 'Hamburg',
      image: 'https://i.imgur.com/Sd1AgUOm.jpg',
    }
  });

  function handleNameChange(e) {
    setPerson({
      ...person,
      name: e.target.value
    });
  }
```

### The reason why immutability is important is how React performs state updates

When updating state in React, it performs a **shallow comparison**. This means that it compares the **previous and current reference values of an object**, rather than comparing each individual property of an object or array. To detect state changes, **React needs to have a new object or array with a new reference value, which is why it is important to maintain immutability when updating state, such as creating a new array or object** with the updated values using methods like `setState([...state, newState]) or setState({...state, [key]: value})`.

Maintaining immutability also helps prevent side effects, as it **avoids directly modifying original data and instead creates a copy of the data to use**. This can help **prevent unexpected errors**, as modifying data outside of the React component could lead to side effects and potential issues. Ultimately, **by maintaining immutability, React can benefit from efficient state updates and prevent side effects**.

**Efficient state updates through shallow comparison**
Shallow comparison only checks whether the reference value of an object has changed, rather than comparing each property of an object. This helps reduce computational resources and allows React to update state efficiently.
