# React-Official-Doc-Study
This page provides a summary of React documentation study and some interesting facts that you may not have known while learning React.

`State` behaves more like a snapshot. Setting it does not change the state variable you already have, but instead triggers a re-render.

## **Rendering takes a snapshot in time**

- [“Rendering”](https://react-ko.dev/learn/render-and-commit#step-2-react-renders-your-components) means that React is calling your component
- Props, event handlers, and local variables were all calculated **using its state at the time of the render.**
- React executing the function → Calculating the snapshot → Updating the DOM tree
- **A state variable’s value never changes within a render,** even if its event handler’s code is asynchronous.


**React keeps the state values “fixed” within one render’s event handlers.** 

Don’t need to worry whether the state has changed while the code is running.

## **Recap**

- React stores state outside of your component, as if on a shelf.
- Every render (and functions inside it) will always “see” the snapshot of the state that React gave to *that* render.
