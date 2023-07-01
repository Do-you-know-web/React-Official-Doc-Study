# React-Official-Doc-Study
This page provides a summary of React documentation study and some interesting facts that you may not have known while learning React.
# Quick Start

React apps are made out of *components*. A component is a piece of the UI (user interface) that has its own logic and appearance.

## ****Creating and nesting components****

**React components are JavaScript functions that return markup**

React component names **must always start with a capital letter**, while HTML tags must be lowercase

## ****Writing markup with JSX****

**Your component also can’t return multiple JSX tags.** You have to wrap them into a shared parent, like a `<div>...</div>` or an empty `<>...</>` wrapper:

```jsx
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```

## ****Conditional rendering****

If you prefer more compact code, you can use the [conditional `?` operator.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) Unlike `if`, it works inside JSX:

```jsx
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

```jsx
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

## ****Rendering lists****

```jsx
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);
```

For each item in a list, you should pass a string or a number that uniquely identifies that item among its siblings. Usually, a key should be coming from your data, such as a database ID. **React uses your keys to know what happened if you later insert, delete, or reorder the items.**

## ****Updating the screen****

you’ll want your component to “remember” some information and display it.

You’ll get two things from `useState`: the current state (`count`), and the function that lets you update it (`setCount`).

If you render the same component multiple times, each will get its own state.

## ****Using Hooks****

Functions starting with `use` are called *Hooks*.

You can only call Hooks *at the top* of your components (or other Hooks).

## ****Sharing data between components****

“lifting state up”. By moving state up, you’ve shared it between components.
