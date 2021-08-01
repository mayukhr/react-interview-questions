# react-interview-questions

## Q-1. What is the virtual DOM (VDOM) and how does React use it to render to the DOM?
  
  React Virtual DOM is a representation of UI. This is basically object which has nested objects to represent the actual structure of a DOM. 
  
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

If we are using Class Components in react, there are multiple methods, which help us control the behavior of the component. React lifecycle is basically: Mount, Update, Unmount(Similar to human: Birth, GrowUp, Death :)). And, to control things around these cycles, we use lifecycle methods.

This can look like:
```
class ASimpleComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
  }
  
  // This is a lifecycle method.
  componentDidMount() {
   this.setState({color: "yellow"})
  }
  
  render() {
    return (
      <h1>Component Color is {this.state.color}</h1>
    );
  }
}
```
There are lifecycle methods like: `componentDidMount`(Mount), `componentDidUpdate`(Update), `componentWillUnmount`(Unmount), which we use heavily.
There are other lifecycke methods too, like: `getDerivedStateFromProps`, `shouldComponentUpdate` 


## Q-5. What is Refs in React?
A Ref is a leash to a react component. Let me explain:
In react, if we want to access/change a component directly, without using Props, we can use refs. 

As an example, If we need to set a focus to a Text input field, we can use ref.
```
import { useRef, useEffect } from 'react';

function TextInputWithFocus() {
  const inputRef = useRef();

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return (
    <input 
      ref={inputRef} 
      type="text" 
    />
  );
}
```

## Q-6. What is Forwarding Refs in React?
If a ref needs to be passed to a child component, we need to pass that ref to child. However, Refs can not be passed as props. To achieve this, `forwardRef` is uesd.

```
import React, {useRef, forwardRef} from 'react';

// Parent component with ref
export function Parent() {
    const nodeRef = useRef();
    return (
       <Child ref={nodeRef}
       )
};

// Child component using forwardRef
export function Child forwardRef((props, ref) {
    return (
        <div ref={ref}>
        </div>
    )
});

```


## Q-7. What is Keys in React?
When populating a list or a group of components, `keys` must be used in react to identify each an every item.
Lets take an example:

```
const brothers = ['Rama', 'Laxmana', 'Bharata', 'Shatrughna'];
const listOfBrothers = brothers.map((brother) =>
  <li key={brother}>
    {brother}
  </li>
);
```
It is important to provide an unique key for each item. That is how react knows which part of the list needs to be re-rendered. A better understanding of react keys help in the app performance.

## Q-8. What do you mean by Props Validation in React?
React components can check the props passed to them and validate if those were of right types or not. If a prop with wrong type is sent to a component, react can show an warning.

As an example(with custom validation):
```
import PropTypes from 'prop-types';

function Component({fullname, date, custom}) {
  return (
    <p> 
      Ok! this is {fullname} on {date} doing {custom} work!
    </p>
  );
}

// This will create a warning saying: "Warning: Failed prop type: Invalid prop!"
const isValidCustom = function() {
    return new Error('Invalid prop!');
  }
}

Component.propTypes = {
  custom: isValidCustom, // Custom validation
  fullname: PropTypes.string,
  date: PropTypes.instanceOf(Date)
}
```

## Q-9. What is the key difference between state and props?
Well, state and props are 2 entirely different concepts in react:

state: Application/Component's current state is this. We can use `setState`(for class components) and `useState` hook for functional component to set a state of component. A state represents what should a component look like in a perticular point of time.

props: Props are properties/variables passed to a Component. Lets say, `<Component name='Mayukh' surname='Roy'/>` has two props: name and surname.

## Q-10. What are Pure Components in React?

PureComponent in react is similar to `React.Component`, with an intention of performance improvement. The idea is, if nothing has been changed(in props), a component should not re-render. Hence, a PureComponent has a shallow-compare method written in it's `shouldComponentUpdate` method. 

```
class Component extends React.PureComponent { 

}
```
To optimize a functional component same as above, we use an HOC called 'memo':

```
export default const FunctionalComponent = React.memo(function FunctionalComponent(props) {
  /* render using props */
});

```

## Q-11. What are React Events?

To handle events in react, we use 'React Events'. React Events are syntactically very similar to the DOM events, with a slight difference: it uses camelCasing.

As an example:
```
DOM Events | React Events
-------------------------
onclick    | onClick
onchange   | onChange
onsubmit   | onSubmit

```

One small thing to notice here: `return false;` does not work to prevent default behavior in react events. We need to use preventDefault() method:

HTML:
```
<form onsubmit="return false">
  <button type="submit">Submit</button>
</form>
```
REACT:
```
function ReactForm() {
  function handleSubmit(e) {
    e.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit Button</button>
    </form>
  );
}
```

## Q-12. Can parent components change value in States and Props?

Yes, surely.

## Q-13. Can changes be made inside the component?

Yes, surely.

## Q-14. Can we make changes inside child components?

Yes, surely.

## Q-15. What is a Stateful component?
A stateful component(typically refered to class components) are Class components in react with a state. As an example:

```
class Main extends Component {
 constructor() {
   super()
   this.state = {
     movies: ['Pather Panchali', 'Enemy at the gates', 'The Godfather', 'Back to the future'];
   }
 }
 render() {
   <MovieList movies={this.state.movies} />
 }
}
```

## Q-16. Define Synthetic Events in React?

When we use any react event(like onChange), React actually uses a wrapper method on top of the browser event. This makes every event-listner work same way in every browser. This wrapped events are called 'Synthetic' events.
However, we can access `event.nativeEvent`, which will let us use browser's unwrapped native event.

## Q-17. What is JSX?

JSX is a syntactic extension of JavaScript, which comes with full power of JavaScript. JSX stands for JavaScript XML. This can represent HTML while writing code in JavaScript.
As an example:
```
// this is a simple jsx containing nested html elements
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);

```

Also, JSX code can be saved in `.jsx` files, so that it could be identified(however, writing it in a `.js` file also works).

