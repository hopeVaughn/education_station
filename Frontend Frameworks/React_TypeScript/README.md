# React with TypeScript Basics

An introduction to using React with TypeScript, covering fundamental concepts, syntax, and patterns.

## Table of Contents

1. [TypeScript Basics](#typescript-basics)
2. [React Basics](#react-basics)
3. [TypeScript with React](#typescript-with-react)
4. [Hooks](#hooks)
5. [React Component Lifecycle](#react-component-lifecycle)
6. [Event Handling](#event-handling)
7. [Conditional Rendering](#conditional-rendering)
8. [Lists and Keys](#lists-and-keys)
9. [Forms](#forms)
10. [CSS in React](#css-in-react)

## TypeScript Basics

TypeScript adds static typing to JavaScript. This means that you can define the type of a variable, function argument, or return value, and TypeScript will check that the types match at compile time. Here are some examples of TypeScript syntax:

### Types <sup><sub>[top](#table-of-contents)</sub></sup>

TypeScript supports several basic types:

```typescript
let num: number = 42;
let str: string = 'hello';
let bool: boolean = true;
let arr: number[] = [1, 2, 3];
let tuple: [string, number] = ['hello', 42];
let anyType: any = 'hello';
```

### Interfaces <sup><sub>[top](#table-of-contents)</sub></sup>

Interfaces define a contract for an object's shape:

```typescript
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: 'Alice',
  age: 30,
};
```

### Enums <sup><sub>[top](#table-of-contents)</sub></sup>

Enums allow you to define a set of named constants:

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let color: Color = Color.Red;
```

### Functions <sup><sub>[top](#table-of-contents)</sub></sup>

Functions in TypeScript can have typed arguments and return values:

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

### Classes <sup><sub>[top](#table-of-contents)</sub></sup>

Classes in TypeScript can have typed properties and methods:

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name}.`;
  }
}
```

These are just a few examples of TypeScript syntax. TypeScript has many other features, such as type unions, type intersections, and type aliases, that can help you write more expressive code.

## <a id="react-basics"></a>React Basics <sup><sub>[top](#table-of-contents)</sub></sup>

To use TypeScript with React.js, you'll need to install the TypeScript compiler and set up a tsconfig.json file. Here's an example tsconfig.json file:

```json
{
  "compilerOptions": {
    "target": "es6",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react"
  },
  "include": ["./src/**/*"]
}
```

This configuration sets the target version of ECMAScript to ES6, enables strict type checking, and sets up support for JSX syntax.

Once you have TypeScript set up, you can create React components with typed props and state. Here is an example of a React class component and React functional component written in TypeScript:

## <a id="functional-components-and-class-components"></a>Functional Components and Class Components <sup><sub>[top](#table-of-contents)</sub></sup>

### W/ Class Components <sup><sub>[top](#table-of-contents)</sub></sup>

```typescript
interface MyComponentProps {
  name: string;
}

interface MyComponentState {
  count: number;
}

class MyComponent extends React.Component<MyComponentProps, MyComponentState> {
  constructor(props: MyComponentProps) {
    super(props);
    this.state = { count: 0 };
  }

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Hello, {this.props.name}!</p>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

### W/ Functional Components <sup><sub>[top](#table-of-contents)</sub></sup>

```typescript
import React, { useState } from 'react';

interface MyComponentProps {
  name: string;
}

interface MyComponentState {
  count: number;
}

const MyComponent: React.FC<MyComponentProps> = ({ name }) => {
  const [state, setState] = useState<MyComponentState>({ count: 0 });

  const handleClick = () => {
    setState({ count: state.count + 1 });
  };

  return (
    <div>
      <p>Hello, {name}!</p>
      <p>Count: {state.count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
};
```

## <a id="typescript-with-react"></a>TypeScript with React <sup><sub>[top](#table-of-contents)</sub></sup>

- Components
- JSX
- Props
- State
- Hooks

### Components <sup><sub>[top](#table-of-contents)</sub></sup>

Components are the building blocks of React applications. A component is a self-contained unit of UI that can be reused across your application. Components can be either functional or class-based.

Here's an example of a functional component:

```typescript
import React from 'react';

interface GreetingProps {
  name: string;
}

const Greeting: React.FC<GreetingProps> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

This component takes a name prop and displays a greeting using the h1 HTML element.

### JSX/TSX <sup><sub>[top](#table-of-contents)</sub></sup>

JSX is a syntax extension for JavaScript that allows you to write HTML-like code within your JavaScript. JSX is used to define the structure and content of your React components. TSX is the same as JSX, but for TypeScript.

Here's an example of how we would use the Greeting component from above using TSX:

```typescript
import React from 'react';

const App: React.FC = () => {
  return (
    <div>
      <Greeting name='Alice' />
      <Greeting name='Bob' />
    </div>
  );
};
```

In this example, we're using TSX to create an App component that renders two instances of the Greeting component, passing in the name prop with different values.

### Props <sup><sub>[top](#table-of-contents)</sub></sup>

Props are the inputs to your React components. Props are passed to a component as an object and can be accessed within the component using the destructuring syntax.

Here's an example of a component that takes a name prop:

```typescript
interface GreetingProps {
  name: string;
}

const Greeting: React.FC<GreetingProps> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

In this example, we've defined the GreetingProps interface to type-check the props passed to the Greeting component. We've also destructured the name prop from the props object and used it to render the greeting.

### State <sup><sub>[top](#table-of-contents)</sub></sup>

State is the internal data of your React components. State is managed within the component and can be updated using the setState method. State can be either functional or class-based.

Here's an example of a class-based component that uses state:

```typescript
interface CounterState {
  count: number;
}

class Counter extends React.Component<{}, CounterState> {
  state = { count: 0 };

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

In this example, we've defined the CounterState interface to type-check the state of the Counter component. The handleClick function updates the count state value when the button is clicked.

## <a id="hooks"></a>Hooks <sup><sub>[top](#table-of-contents)</sub></sup>

Hooks are a way to use state and other React features in functional components. React provides several built-in hooks, such as the useState hook for managing state and the useEffect hook for performing side effects.

Here's an example of a functional component that uses the useState hook:

```typescript
import React, { useState } from 'react';

const Counter: React.FC = () => {
  const [count, setCount] = useState<number>(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
};
```

In this example, we're using the useState hook to manage the component's state. The useState hook returns an array with two values: the current state value (count in this case), and a function to update the state value (setCount in this case).

The handleClick function uses setCount to update the count state value when the button is clicked. The rest of the component is similar to the class component version, with the count state value being displayed in the JSX.

React provides several other hooks that you can use to manage state, perform side effects, and more. Hooks can be a powerful tool for building functional components that are easy to read, write, and maintain.

## TypeScript with React <sup><sub>[top](#table-of-contents)</sub></sup>

- Type annotations
- Props validation
- State management

## Type Annotations <sup><sub>[top](#table-of-contents)</sub></sup>

Type annotations can be used to add type information to your React components. Type annotations can help catch errors before runtime and make code more maintainable. Here's an example of a component with type annotations:

```typescript
import React from 'react';

interface GreetingProps {
  name: string;
  age: number;
}

const Greeting: React.FC<GreetingProps> = ({ name, age }) => {
  return (
    <h1>
      Hello, {name}! You are {age} years old.
    </h1>
  );
};
```

In this example, we're using the interface keyword to define the GreetingProps interface, which specifies that the name prop should be a string and the age prop should be a number. We're also using the React.FC type to indicate that this component is a functional component.

## Props Validation <sup><sub>[top](#table-of-contents)</sub></sup>

Props validation can be used to ensure that the props passed to your components are valid. Props validation can help catch errors before runtime and make code more maintainable. React provides a built-in way to validate props using the propTypes property.

Here's an example of a component with props validation:

```typescript
import React from 'react';
import PropTypes from 'prop-types';

interface GreetingProps {
  name: string;
  age: number;
}

const Greeting: React.FC<GreetingProps> = ({ name, age }) => {
  return (
    <h1>
      Hello, {name}! You are {age} years old.
    </h1>
  );
};

Greeting.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};
```

In this example, we're using the propTypes property to specify that the name prop should be a string and the age prop should be a number, and that both props are required.

## State Management <sup><sub>[top](#table-of-contents)</sub></sup>

State management can be used to manage the internal data of your React components. State management can help catch errors before runtime and make code more maintainable. React provides a built-in way to manage state using the useState hook.

Here's an example of a component with state management using Class Components:

```typescript
import React from 'react';

interface CounterProps {
  initialCount: number;
}

interface CounterState {
  count: number;
}

class Counter extends React.Component<CounterProps, CounterState> {
  constructor(props: CounterProps) {
    super(props);
    this.state = { count: props.initialCount };
  }

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

In this example, we're using the interface keyword to define the CounterProps interface, which specifies that the initialCount prop should be a number. We're also using the interface keyword to define the CounterState interface, which specifies that the count state value should be a number.

In the constructor method, we're initializing the component's state with the initialCount prop value. The handleClick method updates the count state value when the button is clicked.

Here's an example of a component with state management using Functional Components:

```typescript
import React, { useState } from 'react';

interface CounterProps {
  initialCount: number;
}

const Counter: React.FC<CounterProps> = ({ initialCount }) => {
  const [count, setCount] = useState<number>(initialCount);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleClick}>Increment</button>
    </div>
  );
};
```

In this example, the useState hook is used to declare the count state variable, and the setCount function is used to update the state. The handleClick function remains the same, and is called when the button is clicked. The initialCount prop is destructured from the CounterProps interface in the function parameter. The Counter component is declared as a functional component using the React.FC type, which takes the CounterProps interface as its generic argument.

## Functional Components and Class Components <sup><sub>[top](#table-of-contents)</sub></sup>

- Syntax
- Lifecycle methods
- Hooks

### Functional Components <sup><sub>[top](#table-of-contents)</sub></sup>

Functional components are a simpler way to define components in React. They are typically shorter and easier to read than class components.

Here's an example of a functional component:

```typescript
import React from 'react';

interface GreetingProps {
  name: string;
}

const Greeting: React.FC<GreetingProps> = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

In this example, we're using the React.FC type to define a functional component that takes a name prop and displays a greeting using the h1 HTML element.

Functional components don't have a render method like class components do. Instead, they simply return JSX.

Functional components don't have lifecycle methods like class components do. However, they can use hooks to perform side effects and manage state. We'll cover hooks in more detail later.

### Class Components <sup><sub>[top](#table-of-contents)</sub></sup>

Class components are the traditional way to define components in React. They offer more features and flexibility than functional components.

Here's an example of a class component:

```typescript
import React from 'react';

interface GreetingProps {
  name: string;
}

interface GreetingState {
  message: string;
}

class Greeting extends React.Component<GreetingProps, GreetingState> {
  constructor(props: GreetingProps) {
    super(props);
    this.state = { message: `Hello, ${props.name}!` };
  }

  componentDidMount() {
    console.log('Component mounted!');
  }

  componentDidUpdate(prevProps: GreetingProps) {
    if (prevProps.name !== this.props.name) {
      this.setState({ message: `Hello, ${this.props.name}!` });
    }
  }

  componentWillUnmount() {
    console.log('Component unmounted!');
  }

  render() {
    return <h1>{this.state.message}</h1>;
  }
}
```

In this example, we're using the class keyword to define a class component that takes a name prop and displays a greeting using the h1 HTML element. We're also using the interface keyword to define the GreetingState interface, which specifies that the message state value should be a string.

Class components have several lifecycle methods that can be used to perform side effects and update the component's state. In this example, we're using the componentDidMount method to log a message when the component is mounted, the componentDidUpdate method to update the message state value when the name prop changes, and the componentWillUnmount method to log a message when the component is unmounted.

## Hooks <sup><sub>[top](#table-of-contents)</sub></sup>

Hooks are a way to use state and other React features in functional components. React provides several built-in hooks, such as the useState hook for managing state and the useEffect hook for performing side effects.

Here's an example of a functional component that uses the useState and useEffect hooks:

```typescript
import React, { useState, useEffect } from 'react';

interface GreetingProps {
name: string;
}

const Greeting: React.FC<GreetingProps> = ({ name }) => {
const [message, setMessage] = useState<string>(`Hello, ${name}!`);

useEffect(() => {
  console.log('Component mounted!');
  return () => {
    console.log('Component unmounted!');
  };
}, []);

useEffect(() => {
  setMessage(`Hello, ${name}!`);
}, [name]);

return <h1>{message}</h
```

In this example, we're using the useState hook to manage the message state value, and the useEffect hook to perform side effects. The useEffect hook takes a callback function that is called when the component is mounted or updated. In the first useEffect call, we're logging a message when the component is mounted, and returning a cleanup function that is called when the component is unmounted. In the second useEffect call, we're updating the message state value when the name prop changes.

Hooks are a powerful tool for managing state and performing side effects in functional components. They can make your code more concise and easier to understand.

## React Component Lifecycle <sup><sub>[top](#table-of-contents)</sub></sup>

React component lifecycle can be divided into three phases:

- **Mounting** - When a component is first created and added to the DOM.
- **Updating** - When a component's state or props change and the component needs to be re-rendered.
- **Unmounting** - When a component is removed from the DOM.

Each phase of the lifecycle has a corresponding set of lifecycle methods that can be used to perform actions at specific points in the component's lifecycle.

## Mounting

The mounting phase of a component's lifecycle happens when the component is first created and added to the DOM. The following lifecycle methods are called in order during the mounting phase:

1. `constructor(props: P)` - This method is called when the component is first created. It is used to initialize the component's state and bind event handlers.
2. `static getDerivedStateFromProps(props: P, state: S)` - This method is called right before the component is mounted. It is used to update the component's state based on changes to its props.
3. `render()` - This method is called to render the component's UI.
4. `componentDidMount()` - This method is called after the component is mounted in the DOM. It is used to perform side effects, such as fetching data from a server or setting up event listeners.

## Updating

The updating phase of a component's lifecycle happens when a component's state or props change and the component needs to be re-rendered. The following lifecycle methods are called in order during the updating phase:

1. `static getDerivedStateFromProps(props: P, state: S)` - This method is called right before the component is re-rendered. It is used to update the component's state based on changes to its props.
2. `shouldComponentUpdate(nextProps: P, nextState: S)` - This method is called to determine whether the component should be re-rendered. It is used to optimize performance by preventing unnecessary re-renders.
3. `render()` - This method is called to render the component's UI.
4. `getSnapshotBeforeUpdate(prevProps: P, prevState: S)` - This method is called right before the component is updated in the DOM. It is used to capture information about the current DOM state, such as scroll position or input focus.
5. `componentDidUpdate(prevProps: P, prevState: S, snapshot: any)` - This method is called after the component is updated in the DOM. It is used to perform side effects, such as updating the DOM based on changes to the component's props or state.

## Unmounting

The unmounting phase of a component's lifecycle happens when a component is removed from the DOM. The following lifecycle method is called during the unmounting phase:

1. `componentWillUnmount()` - This method is called right before the component is removed from the DOM. It is used to perform cleanup, such as removing event listeners or canceling pending network requests.

### Using TypeScript with Component Lifecycle Methods

## useState and useEffect Hooks <sup><sub>[top](#table-of-contents)</sub></sup>

- State management
- Side effects
- Cleanup

## Event Handling <sup><sub>[top](#table-of-contents)</sub></sup>

- onClick
- onChange
- onSubmit
- Event types

## Conditional Rendering <sup><sub>[top](#table-of-contents)</sub></sup>

- If/else
- Ternary operators
- Short-circuit evaluation

## Lists and Keys <sup><sub>[top](#table-of-contents)</sub></sup>

- Mapping
- Key prop
- Indexing

## Forms <sup><sub>[top](#table-of-contents)</sub></sup>

- Controlled components
- Validation
- Event handling

## CSS in React <sup><sub>[top](#table-of-contents)</sub></sup>

- Inline styles
- CSS modules
- Styled-components
