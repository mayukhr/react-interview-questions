# react-interview-questions

## Q-1. What is the virtual DOM (VDOM) and how does React use it to render to the DOM?
  
  React Virtual DOM is a representation of UI. This is basically object which has nested objects(fibers) to represent the actual structure of a DOM. 
  
  In react world, we do not need to manupulate DOM. Instead, we tell React the state of a component, which updates the virtual DOM. And then, react updates the actual DOM to make sure, the state of Virtual DOM and actual DOM states are same. 
  
  DOM manupulation is expensive. Because, each time DOM is modified, it re-creates RenderTree which involves Layout, Paint and Composite steps. 
  [I have explained Render tree creation in more details here.](https://github.com/mayukhr/parts_unknown/blob/main/README.md)

## Q-2. What do you mean by prop drilling and how can you avoid it?
In React we pass properties(we often call these `props`) to the components below(or children). Now, if these children have child components of their own, which requires these `props`, we pass those down.
In simple words, the above scenario may look like this:
`ParentComponent() -aParentProp-> ChildComponent({aParentProp}) -aParentProp-> GrandChildComponent({aParentProp})` and so on.

Now, is it a bad thing which we should avoid? 
Maybe not! Actually it is great. It lets a developer avoid polluting global scope. If we were using global scope, everytime a dev has to think: "Can I change something without breaking something else in the app?". But, with prop-drilling, it is not the case.

When it becomes bad(or difficult to work with)?
Well, when the chain of components is really long.

How to avoid prop-drilling?
There are two main ways:
1. Using ContextAPI:
```
// Create this UsefulContext inside the ParentComponent from above
const UsefulContext = React.createContext({aParentProp: 0})

// use the UsefulContext in all other components(ChildComponent and GrandChildComponent) like:
const {aParentProp} = React.useContext(UsefulContext)

```
2. Using connect(), when used with Redux: 

Connect method will connect a component to the global store, where all the state variables are present.

## Q-3. What are Higher-Order Components (HOC)?

HOCs are a design pattern used in React. To reuse a function/logic in multiple components, we use HOC pattern. 
As an example, a Facebook `like` can happen both on a post and a comment below the post. `Like` is a simple counter which is needed for both Post and Comment.
We can simply have an HOC which can wrap around both Like and Comment components and reuse it's counter logic.

[I have created a simple implementation in CodeSandbox for above scenario. It's Up and Running here!](https://codesandbox.io/s/hoc-example-try-00oqh?file=/src/hoc/hoc.js)


## Q-4. Life cycle methods of React.

## Q-5. What is Refs in React?

## Q-6. What is Forwarding Refs in React?

## Q-7. What is Keys in React?

## Q-8. What do you mean by Props Validation in React?

## Q-9. What is the key difference between state and props?

## Q-10. What are Pure Components in React?

## Q-11. What are React Events?

## Q-12. Can parent components change value in States and Props?

## Q-13. Can changes be made inside the component?

## Q-14. Can we make changes inside child components?

## Q-15. What is a Stateful component?

## Q-16. Define Synthetic Events in React?

## Q-17. What is JSX?

