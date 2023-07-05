# React-Official-Doc-Study
This page provides a summary of React documentation study and some interesting facts that you may not have known while learning React.

# Queuing a Series of State Updates

## **React batches state updates**

- **React waits until *all* code in the event handlers has run before processing your state updates.**
- This lets you update multiple state variables—even from multiple components—without triggering too many [re-renders.](https://react-ko.dev/learn/render-and-commit#re-renders-when-state-updates)

**React does not batch across *multiple* intentional events like clicks**—each click is handled separately.

## **Updating the same state multiple times before the next render**

1. React queues this function to be processed after all the other code in the event handler has run.
2. During the next render, React goes through the queue and gives you the final updated state.

**[What happens if you replace state after updating it](https://react-ko.dev/learn/queueing-a-series-of-state-updates#what-happens-if-you-replace-state-after-updating-it)**

- After the event handler completes, React will trigger a re-render.
- During the re-render, React will process the queue. ****
- **Updater functions run during rendering**, so **updater functions must be [pure](https://react-ko.dev/learn/keeping-components-pure) and only *return* the result.**

## **Naming conventions**

It’s common to name the updater function argument by the first letters of the corresponding state variable:

## **Recap**

React processes state updates after event handlers have finished running. This is called **batching**.
