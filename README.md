# react-interview-questions

## Q-1. What is the virtual DOM (VDOM) and how does React use it to render to the DOM?
  
  React Virtual DOM is a representation of UI. This is basically object which has nested objects(fibers) to represent the actual structure of a DOM. 
  
  In react world, we do not need to manupulate DOM. Instead, we tell React the state of a component, which updates the virtual DOM. And then, react updates the actual DOM to make sure, the state of Virtual DOM and actual DOM states are same. 
  
  DOM manupulation is expensive. Because, each time DOM is modified, it re-creates RenderTree which involves Layout, Paint and Composite steps. 
  [I have explained Render tree creation in more details here.](https://github.com/mayukhr/parts_unknown)

## Q-2. What do you mean by prop drilling and how can you avoid it?

## Q-3. What are Higher-Order Components (HOC)?

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

