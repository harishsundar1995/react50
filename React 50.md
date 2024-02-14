---


---

<p><strong>1. What is React Fiber and how does it improve performance?</strong></p>
<p>React Fiber is a reimplementation of the React core algorithm. It’s designed to improve the way React schedules, prioritizes, and renders updates to the DOM. Fiber introduces the concept of asynchronous rendering, allowing React to split the rendering work into smaller chunks and prioritize high-priority updates, thus making the user interface more responsive.<br>
For example:</p>
<pre><code>// React Fiber example
// Before Fiber
function render() {
  // perform entire rendering process
}
// After Fiber
function render() {
  // perform a small amount of work
  // yield to allow other tasks to run
  // resume work later
}
</code></pre>
<p><strong>2. Explain the concept of virtual DOM and how React utilizes it.</strong></p>
<p>The virtual DOM is a lightweight copy of the actual DOM. React uses it to improve performance by minimizing direct manipulation of the DOM. Instead, React updates the virtual DOM in response to state changes, compares it with the previous version, and then efficiently updates only the parts of the actual DOM that have changed.<br>
For example:</p>
<pre><code>// Virtual DOM example
// Before updating the actual DOM
const element = &lt;div&gt;Hello, world!&lt;/div&gt;;
// After updating the actual DOM
ReactDOM.render(element, document.getElementById('root'));
</code></pre>
<p><strong>3. What are controlled and uncontrolled components in React? Provide examples.</strong></p>
<p>Controlled components are React components whose state is controlled by React, typically through state management like useState or Redux. Uncontrolled components, on the other hand, manage their own state internally, usually using refs.<br>
For example:</p>
<pre><code>// Controlled component example
function ControlledComponent() {
  const [value, setValue] = useState('');

  function handleChange(event) {
    setValue(event.target.value);
  }

  return &lt;input type="text" value={value} onChange={handleChange} /&gt;;
}

// Uncontrolled component example
function UncontrolledComponent() {
  const inputRef = useRef(null);

  function handleSubmit(event) {
    event.preventDefault();
    console.log('Input value:', inputRef.current.value);
  }

  return (
    &lt;form onSubmit={handleSubmit}&gt;
      &lt;input type="text" ref={inputRef} /&gt;
      &lt;button type="submit"&gt;Submit&lt;/button&gt;
    &lt;/form&gt;
  );
}
</code></pre>
<ol start="4">
<li><strong>How does React handle forms and form validation?</strong></li>
</ol>
<p>React handles forms by maintaining the form state within its components and updating it via controlled inputs. Form validation can be achieved by adding validation logic to the input change handlers or form submission handlers. Libraries like Formik and Yup can also be used for more complex form handling and validation. For example:</p>
<pre><code>    `import React, { useState } from 'react';
    
    function FormExample() {
      const [formData, setFormData] = useState({
        username: '',
        password: '',
      });
    
      function handleChange(event) {
        const { name, value } = event.target;
        setFormData({ ...formData, [name]: value });
      }
    
      function handleSubmit(event) {
        event.preventDefault();
        // Form validation logic here
        console.log('Form submitted:', formData);
      }
    
      return (
        &lt;form onSubmit={handleSubmit}&gt;
          &lt;input
            type="text"
            name="username"
            value={formData.username}
            onChange={handleChange}
            placeholder="Username"
          /&gt;
          &lt;input
            type="password"
            name="password"
            value={formData.password}
            onChange={handleChange}
            placeholder="Password"
          /&gt;
          &lt;button type="submit"&gt;Submit&lt;/button&gt;
        &lt;/form&gt;
      );
    }` 
</code></pre>
<ol start="5">
<li>
<p><strong>What is the significance of keys in React lists? How do you use them correctly?</strong></p>
<p>Keys in React lists help React identify which items have changed, are added, or are removed. They should be unique among siblings and stable across re-renders. Keys aid in efficient re-rendering and updating of lists.</p>
</li>
</ol>
<p>For example:</p>
<pre><code> `function ListExample({ items }) {
      return (
        &lt;ul&gt;
          {items.map((item) =&gt; (
            &lt;li key={item.id}&gt;{item.name}&lt;/li&gt;
          ))}
        &lt;/ul&gt;
      );
    }` 
</code></pre>
<ol start="6">
<li><strong>Discuss the differences between React class components and functional components.</strong></li>
</ol>
<p>React class components are ES6 classes that extend React.Component and have access to lifecycle methods and state. Functional components are simple functions that take props as input and return JSX. With the introduction of hooks, functional components can also manage state and have access to lifecycle equivalents.</p>
<p>For example:</p>
<pre><code>    `// Class component example
    class ClassComponent extends React.Component {
      render() {
        return &lt;div&gt;Hello, {this.props.name}!&lt;/div&gt;;
      }
    }
    
    // Functional component example
    function FunctionalComponent({ name }) {
      return &lt;div&gt;Hello, {name}!&lt;/div&gt;;
    }` 
</code></pre>
<ol start="7">
<li><strong>What are hooks in React? How do they change the way we write components?</strong></li>
</ol>
<p>Hooks are functions that allow functional components to use state and other React features without writing a class. They provide a simpler and more concise way to manage state and side-effects within functional components. Hooks like useState and useEffect are commonly used in React.</p>
<p>For example:</p>
<pre><code>    import React, { useState, useEffect } from 'react';
    
    function ExampleComponent() {
      const [count, setCount] = useState(0);
    
      useEffect(() =&gt; {
        document.title = `You clicked ${count} times`;
      }, [count]);
    
      return (
        &lt;div&gt;
          &lt;p&gt;You clicked {count} times&lt;/p&gt;
          &lt;button onClick={() =&gt; setCount(count + 1)}&gt;Click me&lt;/button&gt;
        &lt;/div&gt;
      );
    }`` 
</code></pre>
<ol start="8">
<li><strong>Explain the useEffect hook and its dependencies parameter.</strong></li>
</ol>
<p>The useEffect hook in React is used for side effects in functional components, such as data fetching, subscriptions, or manually changing the DOM. The second parameter of useEffect is an array of dependencies. If any of the dependencies change between renders, the effect will re-run. If the dependencies array is empty, the effect will only run once after the initial render.</p>
<p>For example:</p>
<pre><code>    import React, { useState, useEffect } from 'react';
    
    function TimerComponent() {
      const [seconds, setSeconds] = useState(0);
    
      useEffect(() =&gt; {
        const intervalId = setInterval(() =&gt; {
          setSeconds((prevSeconds) =&gt; prevSeconds + 1);
        }, 1000);
    
        return () =&gt; clearInterval(intervalId);
      }, []); // Empty dependencies array means the effect runs once after initial render
    
      return &lt;div&gt;Seconds: {seconds}&lt;/div&gt;;
    }` 
</code></pre>
<ol start="9">
<li><strong>Describe the useContext hook and provide a use case for its usage.</strong></li>
</ol>
<p>The useContext hook in React allows functional components to consume values from a Context without nesting. It provides a cleaner and more readable way to access global state or values throughout the component tree.</p>
<p>For example:</p>
<pre><code>    import React, { useContext } from 'react';
    import ThemeContext from './ThemeContext';
    
    function ThemedButton() {
      const theme = useContext(ThemeContext);
    
      return (
        &lt;button style={{ background: theme.background, color: theme.text }}&gt;
          Themed Button
        &lt;/button&gt;
      );
    }` 
</code></pre>
<ol start="10">
<li><strong>How does React handle state management? Compare local state, Context API, Redux, and MobX.</strong></li>
</ol>
<p>React handles state management through various methods. Local state is managed within individual components using the useState hook. The Context API provides a way to pass data through the component tree without having to pass props manually at every level. Redux and MobX are external state management libraries. Redux follows a centralized store pattern with actions and reducers, while MobX allows for more granular reactivity with observable data. Each approach has its pros and cons depending on the complexity and requirements of the application.</p>
<ol start="11">
<li><strong>What is Redux middleware? Provide examples of popular middleware.</strong></li>
</ol>
<p>Redux middleware provides a third-party extension point between dispatching an action and the moment it reaches the reducer. It’s commonly used for logging, asynchronous actions, and routing. Examples of popular middleware include Redux Thunk for handling asynchronous actions, Redux Saga for more complex asynchronous flows, and Redux Logger for logging actions and state changes.</p>
<ol start="12">
<li><strong>Explain React Router and its core components.</strong></li>
</ol>
<p>React Router is a library for routing in React applications. Its core components include BrowserRouter, HashRouter, Route, Switch, Link, and NavLink. BrowserRouter and HashRouter are different types of routers for handling navigation. Route defines a mapping between a URL path and a React component. Switch renders the first child Route or Redirect that matches the current location. Link and NavLink are used for navigation between routes, with NavLink providing additional styling options for active links.</p>
<ol start="13">
<li><strong>What are higher-order components (HOCs) in React? How do you create one?</strong></li>
</ol>
<p>Higher-order components (HOCs) are functions that take a component and return a new component with enhanced functionality. They are commonly used for code reuse, logic abstraction, and cross-cutting concerns like authentication and logging. To create a HOC, you typically define a function that accepts a component as an argument, creates a new component that wraps the original component, and returns it.</p>
<p>For example:</p>
<pre><code>function withAuthentication(WrappedComponent) {
  return function WithAuthentication(props) {
    // Add authentication logic here
    return &lt;WrappedComponent {...props} /&gt;;
  };
}` 
</code></pre>
<ol start="14">
<li><strong>Discuss the advantages and disadvantages of using Redux in a large-scale application.</strong></li>
</ol>
<p>Advantages:<br>
-   Centralized state management simplifies data flow and makes it easier to reason about application state.<br>
-   Time-travel debugging and hot reloading enhance developer productivity and debugging capabilities.<br>
-   Middleware support enables handling of complex asynchronous operations and side-effects.</p>
<p>Disadvantages:<br>
-   Boilerplate: Redux requires writing additional code for actions, reducers, and connecting components.<br>
-   Learning curve: Understanding Redux concepts like actions, reducers, and the store can be challenging for beginners.<br>
-   Overhead: For smaller applications, Redux might introduce unnecessary complexity and overhead.</p>
<ol start="15">
<li><strong>How does React handle routing on the server-side?</strong></li>
</ol>
<p>React can handle routing on the server-side using server-side rendering (SSR). SSR involves rendering React components on the server and sending the fully rendered HTML to the client. Libraries like React Router support SSR by providing components and utilities for server-side routing. SSR improves performance and SEO by sending HTML content to search engines and clients with disabled JavaScript.</p>
<ol start="16">
<li><strong>What are fragments in React? When and why would you use them?</strong></li>
</ol>
<p>Fragments in React are used to group multiple children elements without adding extra nodes to the DOM. They provide a cleaner syntax and improve performance by reducing unnecessary div wrappers. Fragments are especially useful when returning multiple elements from a component’s render method or when rendering lists of elements without a parent wrapper.</p>
<p>For example:</p>
<pre><code>function FragmentExample() {
  return (
    &lt;&gt;
      &lt;ChildComponent1 /&gt;
      &lt;ChildComponent2 /&gt;
    &lt;/&gt;
  );
}` 
</code></pre>
<ol start="17">
<li><strong>Explain code-splitting in React and why it is important.</strong></li>
</ol>
<p>Code-splitting in React involves splitting your code bundle into smaller chunks that are loaded asynchronously. This improves initial page load times by only loading the necessary code for the current route or component, rather than loading the entire application upfront. Code-splitting is crucial for large-scale applications to reduce the initial load time, improve performance, and optimize resource usage. React provides built-in mechanisms like dynamic import() and React.lazy() to achieve code-splitting.</p>
<ol start="18">
<li><strong>Discuss React’s reconciliation process and how it impacts performance.</strong></li>
</ol>
<p>React’s reconciliation process is the mechanism by which it updates the DOM to match the virtual DOM. It recursively compares elements in the virtual DOM with those in the real DOM and applies the necessary updates efficiently. React uses a diffing algorithm during reconciliation to minimize DOM updates and improve performance. However, inefficient component structures or frequent updates can impact performance negatively, so it’s important to optimize component rendering and minimize unnecessary re-renders.</p>
<ol start="19">
<li><strong>What is the role of PropTypes in React? How do you use them?</strong><br>
PropTypes are a type-checking mechanism provided by React for runtime type validation of props passed to components. They help catch bugs early by providing warnings in the console when unexpected props are passed. PropTypes are defined using the propTypes object on the component and specifying the expected types for each prop.</li>
</ol>
<p>For example:</p>
<pre><code>import PropTypes from 'prop-types';

function MyComponent({ name, age }) {
  return &lt;div&gt;{name} is {age} years old&lt;/div&gt;;
}

MyComponent.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};
</code></pre>
<ol start="20">
<li><strong>Explain error boundaries in React. How do they help in handling errors gracefully?</strong></li>
</ol>
<p>Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the entire application. They help in handling errors gracefully by isolating them to specific components and preventing the entire application from crashing. Error boundaries are defined using special lifecycle methods like componentDidCatch().</p>
<p>For example:</p>
<pre><code>class ErrorBoundary extends React.Component {
  state = { hasError: false };

  componentDidCatch(error, errorInfo) {
    this.setState({ hasError: true });
    console.error('Error:', error);
  }

  render() {
    if (this.state.hasError) {
      return &lt;div&gt;Something went wrong...&lt;/div&gt;;
    }
    return this.props.children;
  }
}

&lt;ErrorBoundary&gt;
  &lt;MyComponent /&gt;
&lt;/ErrorBoundary&gt;
</code></pre>
<ol start="21">
<li><strong>Discuss the concept of lazy loading in React and how it improves performance.</strong></li>
</ol>
<p>Lazy loading in React involves deferring the loading of non-critical resources or components until they are needed. This improves performance by reducing the initial load time of the application and deferring the download of large JavaScript bundles or assets. React.lazy() and Suspense are used to implement lazy loading of components, while dynamic import() is used for lazy loading other resources. Lazy loading is particularly beneficial for optimizing the initial page load time of applications with large codebases or complex UIs.</p>
<ol start="22">
<li><strong>What is server-side rendering (SSR) in React? How do you implement it?</strong></li>
</ol>
<p>Server-side rendering (SSR) in React involves rendering React components on the server and sending the fully rendered HTML to the client. This improves performance by reducing the time-to-content and enables better SEO as search engines can crawl the rendered HTML. SSR can be implemented using libraries like Next.js, which provide built-in support for SSR, or by setting up custom server-side rendering using Node.js and React libraries like ReactDOMServer.</p>
<ol start="23">
<li><strong>What is the significance of PureComponent in React? How does it differ from regular components?</strong></li>
</ol>
<p>PureComponent is a class component provided by React that implements a shallow comparison of props and state to determine if a component should re-render. It automatically implements the shouldComponentUpdate() method with a shallow comparison of props and state, resulting in performance optimizations by preventing unnecessary re-renders. PureComponent is useful when the component’s render output is determined solely by its props and state, without any deep nested data structures.</p>
<ol start="24">
<li><strong>Discuss the differences between useMemo and useCallback hooks.</strong></li>
</ol>
<p>useMemo and useCallback are both memoization hooks in React used to optimize performance by caching the results of expensive computations. useMemo is used to memoize the result of a function or computation, while useCallback is used to memoize the function itself. The main difference is that useMemo memoizes the result value, while useCallback memoizes the function instance. useMemo is useful for optimizing expensive computations, while useCallback is useful for optimizing expensive callback functions to prevent unnecessary re-renders of child components.</p>
<ol start="25">
<li><strong>How do you optimize performance in React applications?</strong></li>
</ol>
<p>Performance optimization in React applications can be achieved through various techniques such as:<br>
-   Using PureComponent or React.memo for optimizing component re-renders.<br>
-   Implementing shouldComponentUpdate or using hooks like useMemo and useCallback for memoization.<br>
-   Splitting large components into smaller ones and using code-splitting for lazy loading.<br>
-   Optimizing network requests and data fetching with techniques like caching, pagination, and debounce.<br>
-   Minimizing unnecessary re-renders and DOM manipulations by optimizing component lifecycle methods and avoiding unnecessary state updates.<br>
-   Profile and analyze performance using browser developer tools and performance monitoring libraries like React Profiler and Lighthouse.</p>
<ol start="26">
<li><strong>Explain the useReducer hook and provide a practical example of its usage.</strong></li>
</ol>
<p>The useReducer hook in React is used for state management similar to Redux. It is a more powerful alternative to useState when the state logic is complex and involves multiple sub-values or when the next state depends on the previous state. useReducer takes a reducer function and an initial state as arguments and returns the current state and a dispatch function to update the state.</p>
<p>For example:</p>
<pre><code>import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    &lt;div&gt;
      Count: {state.count}
      &lt;button onClick={() =&gt; dispatch({ type: 'increment' })}&gt;+&lt;/button&gt;
      &lt;button onClick={() =&gt; dispatch({ type: 'decrement' })}&gt;-&lt;/button&gt;
    &lt;/div&gt;
  );
}
</code></pre>
<ol start="27">
<li><strong>What are portals in React? Provide a scenario where portals are useful.</strong></li>
</ol>
<p>Portals in React provide a way to render children into a DOM node that exists outside the parent component’s DOM hierarchy. They are useful for scenarios where a child component needs to be rendered outside its parent’s container, such as modals, tooltips, and overlays. Portals enable developers to manage the z-index and positioning of elements more flexibly and avoid issues like overflow clipping and CSS constraints.</p>
<p>For example:</p>
<pre><code>function Modal({ children }) {
  return ReactDOM.createPortal(
    children,
    document.getElementById('modal-root')
  );
}

function App() {
  return (
    &lt;div&gt;
      &lt;h1&gt;My App&lt;/h1&gt;
      &lt;Modal&gt;
        &lt;p&gt;This is a modal&lt;/p&gt;
      &lt;/Modal&gt;
    &lt;/div&gt;
  );
}
</code></pre>
<ol start="28">
<li><strong>Discuss the differences between Shallow rendering and Full DOM rendering in React testing.</strong></li>
</ol>
<p>Shallow rendering in React testing involves rendering only the component under test without rendering its children. It provides a faster and more focused way to test a component’s behavior without dealing with its children. Full DOM rendering, on the other hand, involves rendering the entire component tree and its children. It provides a more comprehensive testing environment but can be slower and less isolated than shallow rendering. Both shallow rendering and full DOM rendering have their use cases depending on the complexity of the component and the testing requirements.</p>
<ol start="29">
<li><strong>How do you handle authentication and authorization in a React application?</strong></li>
</ol>
<p>Authentication and authorization in a React application can be handled using various techniques such as:<br>
-   Storing authentication tokens in browser cookies or local storage.<br>
-   Implementing protected routes using React Router and checking authentication status before rendering components.<br>
-   Using higher-order components (HOCs) or custom hooks to wrap components with authentication logic.<br>
-   Communicating with a server-side authentication service or API endpoints for user authentication and authorization.<br>
-   Managing user roles and permissions to control access to certain routes or components based on user privileges.<br>
-   Handling authentication errors and redirects to login pages or error pages.</p>
<ol start="30">
<li><strong>Explain the React Context API and when you should use it over Redux.</strong></li>
</ol>
<p>The React Context API provides a way to pass data through the component tree without having to pass props manually at every level. It’s useful for sharing global data, such as theme preferences, user authentication status, or language preferences, with multiple components in a React application. While Redux is a more powerful state management library suitable for large-scale applications with complex state logic and actions, the Context API is simpler and more lightweight, making it suitable for smaller applications or cases where Redux might introduce unnecessary complexity.</p>
<ol start="31">
<li><strong>Discuss the differences between server-side rendering (SSR) and client-side rendering (CSR).</strong></li>
</ol>
<p>Server-side rendering (SSR) involves rendering React components on the server and sending the fully rendered HTML to the client, while client-side rendering (CSR) involves rendering components in the browser using JavaScript. SSR improves performance by reducing time-to-content and enabling better SEO, but it requires more server-side processing and can be slower for initial page loads. CSR provides a more interactive user experience and allows for dynamic updates without full page refreshes, but it can lead to slower perceived performance and SEO challenges.</p>
<ol start="32">
<li><strong>What are the advantages of using TypeScript with React?</strong></li>
</ol>
<p>Advantages of using TypeScript with React include:<br>
-   Static type checking: TypeScript helps catch type-related errors at compile time, reducing bugs and improving code quality.<br>
-   Improved developer experience: TypeScript provides features like code completion, type inference, and automatic refactoring, enhancing developer productivity and code readability.<br>
-   Better code documentation: TypeScript’s type annotations serve as self-documenting code, making it easier to understand and maintain complex React applications.<br>
-   Enhanced tooling support: TypeScript integrates well with popular development tools like Visual Studio Code, offering advanced features like type-aware linting, debugging, and IntelliSense.</p>
<ol start="33">
<li><strong>Explain the concept of code splitting and lazy loading in React. How do they improve performance?</strong></li>
</ol>
<p>Code splitting and lazy loading in React involve splitting the application’s code bundle into smaller chunks and loading them on-demand instead of loading everything upfront. This improves performance by reducing the initial load time of the application, as only the necessary code for the current route or component is loaded when it’s needed. React provides built-in mechanisms like dynamic import() and React.lazy() to achieve code splitting and lazy loading of components, allowing developers to optimize performance and resource usage.</p>
<ol start="34">
<li><strong>Discuss the significance of the shouldComponentUpdate() method in React.</strong></li>
</ol>
<p>The shouldComponentUpdate() method in React is a lifecycle method that determines if a component should re-render when its props or state change. By default, React re-renders a component whenever its parent component re-renders, regardless of whether the component’s props or state have changed. Implementing shouldComponentUpdate() allows developers to optimize performance by preventing unnecessary re-renders when the component’s props or state haven’t changed. By returning false from shouldComponentUpdate(), React skips the re-rendering process for that component, resulting in performance improvements.</p>
<ol start="35">
<li><strong>How do you handle memory leaks in React applications?</strong></li>
</ol>
<p>Memory leaks in React applications can be handled by following best practices such as:<br>
-   Proper cleanup: Ensure that event listeners, timers, subscriptions, and other resources are properly cleaned up when components unmount to prevent memory leaks.<br>
-   UseEffect cleanup: Utilize the cleanup function returned by useEffect to clean up any resources created during the component’s lifecycle.<br>
-   Avoid circular references: Be mindful of creating circular references or closures within event handlers or state updates that prevent components from being garbage collected.<br>
-   Profile and analyze: Use browser developer tools like Chrome DevTools or React Profiler to profile memory usage and identify potential memory leaks or performance bottlenecks.<br>
-   Monitor performance: Regularly monitor performance metrics and memory usage to detect any anomalies or regressions and take corrective actions as needed.</p>
<ol start="36">
<li><strong>What is the role of the ReactDOM library in React?</strong></li>
</ol>
<p>ReactDOM is a library in React used for rendering React components into the DOM. It provides methods for mounting React components into the DOM, updating them with new props or state, and unmounting them when they are no longer needed. ReactDOM.render() is the primary method used to render a React element into the DOM, while other methods like ReactDOM.hydrate(), ReactDOM.unmountComponentAtNode(), and ReactDOM.createPortal() provide additional functionality for working with React components and the DOM.</p>
<ol start="37">
<li><strong>Discuss the importance of immutable data structures in React applications.</strong></li>
</ol>
<p>Immutable data structures in React applications are important for several reasons:<br>
-   Predictable state management: Immutable data ensures that state changes are predictable and consistent, making it easier to reason about the application’s behavior and debug issues.<br>
-   Performance optimizations: Immutable data allows React to perform shallow comparisons to determine if a component needs to re-render, improving performance by reducing unnecessary re-renders.<br>
-   Avoiding side effects: Immutable data prevents unintentional side effects caused by mutating state directly, leading to more predictable and maintainable code.<br>
-   Enforcing purity: Immutable data encourages a functional programming style where functions are pure and free of side effects, promoting better code organization and testability.</p>
<ol start="38">
<li><strong>Explain how to optimize images in a React application for better performance.</strong></li>
</ol>
<p>Images can be optimized in a React application for better performance by following these best practices:<br>
-   Use appropriate image formats: Choose the most suitable image format (e.g., JPEG, PNG, SVG, WebP) based on the image content and desired quality to reduce file size and loading time.<br>
-   Resize and compress images: Resize images to the required dimensions and compress them using tools like ImageMagick, TinyPNG, or Squoosh to reduce file size without sacrificing quality.<br>
-   Lazy loading: Implement lazy loading for images that are not immediately visible on the screen to defer their loading until they enter the viewport, reducing initial page load time.<br>
-   Responsive images: Use responsive image techniques like srcset and sizes attributes or the  element to serve appropriately sized images based on the user’s device and screen size, improving performance and user experience.<br>
-   CDN usage: Serve images from a content delivery network (CDN) to leverage caching and reduce latency, improving image loading speed for users across different geographical locations.</p>
<ol start="39">
<li><strong>What are hooks rules in React? Discuss the rules of hooks.</strong></li>
</ol>
<p>Hooks rules in React are guidelines that ensure consistent and correct usage of React hooks in functional components. The rules of hooks are:<br>
-   Only call hooks at the top level: Hooks should be called at the top level of a functional component or custom hook and not within loops, conditions, or nested functions.<br>
-   Only call hooks from React functions: Hooks should only be called from functional components or custom hooks, not from regular JavaScript functions, class components, or event listeners.<br>
-   Follow the naming convention: Hooks should start with the prefix “use” to indicate that they are hooks (e.g., useState, useEffect, useContext).<br>
-   Don’t call hooks conditionally: Hooks should be called unconditionally in the same order on every render to ensure consistent behavior and avoid bugs.</p>
<ol start="40">
<li><strong>How does React ensure that the UI remains responsive during long-running computations?</strong></li>
</ol>
<p>React ensures that the UI remains responsive during long-running computations by leveraging its asynchronous rendering model and event loop. The reconciliation process in React is divided into small units of work called “fiber” that can be interrupted and resumed to allow for interleaving of rendering and other tasks. This prevents the UI from becoming unresponsive or freezing during long-running computations by allowing React to pause rendering, handle user input, and schedule updates in a non-blocking manner. Additionally, React provides features like asynchronous rendering, suspense, and concurrent mode to further improve responsiveness and performance in modern web applications.</p>
<ol start="41">
<li><strong>Discuss the benefits of using PureComponent in React applications.</strong></li>
</ol>
<p>PureComponent in React applications provides several benefits:<br>
-   Automatic optimization: PureComponent implements a shallow comparison of props and state to determine if a component needs to re-render, reducing unnecessary re-renders and optimizing performance.<br>
-   Simplified code: PureComponent eliminates the need to manually implement shouldComponentUpdate() for optimizing component re-renders, resulting in cleaner and more concise code.<br>
-   Improved performance: By preventing unnecessary re-renders, PureComponent reduces the CPU and memory overhead associated with rendering components, resulting in improved application performance and responsiveness.<br>
-   Better developer experience: PureComponent helps developers focus on building features and functionality without worrying about performance optimizations, leading to a more enjoyable development experience and faster time-to-market.</p>
<ol start="42">
<li><strong>What are the differences between Redux and MobX? When would you choose one over the other?</strong></li>
</ol>
<p>Redux and MobX are both state management libraries for React applications with different approaches:<br>
-   Redux follows a centralized store pattern with actions, reducers, and a single immutable state tree. It is suitable for large-scale applications with complex state logic and actions that require strict immutability and predictable state changes.<br>
-   MobX adopts a more decentralized approach with observable data and reactive programming principles. It is suitable for smaller applications or cases where simplicity and flexibility are preferred over strict patterns and conventions.<br>
-   When to choose Redux: Choose Redux for large-scale applications with complex state management requirements, predictable state changes, time-travel debugging, and middleware support for handling asynchronous actions.<br>
-   When to choose MobX: Choose MobX for smaller applications, rapid prototyping, or cases where simplicity, flexibility, and minimal boilerplate are desired. MobX is also well-suited for cases where reactivity and automatic updates are important, such as real-time applications or data-driven UIs.</p>
<ol start="43">
<li><strong>Explain the concept of “lifting state up” in React and when it is beneficial.</strong></li>
</ol>
<p>“Lifting state up” in React refers to the practice of moving state from child components to their nearest common ancestor in the component tree. This allows multiple child components to share the same state and synchronize their behavior based on that shared state. Lifting state up is beneficial when:<br>
-   Multiple components need access to the same state or need to synchronize their behavior based on shared data.<br>
-   There is a need to maintain a single source of truth for state management to avoid inconsistencies and bugs.<br>
-   State changes in one component should propagate to other related components in the component tree.</p>
<ol start="44">
<li><strong>What are the advantages and disadvantages of using React’s Context API?</strong></li>
</ol>
<ul>
<li>Advantages:
<ul>
<li>Simplified state management: Context API provides a simple and convenient way to share global data across components without the need for prop drilling.</li>
<li>Avoids prop drilling: Context API eliminates the need to pass props through intermediate components, leading to cleaner and more maintainable code.</li>
<li>Supports component composition: Context API supports nesting and composition of multiple contexts, allowing for fine-grained control over data sharing and isolation.</li>
</ul>
</li>
<li>Disadvantages:
<ul>
<li>Performance concerns: Context API may have performance implications, especially when used with deeply nested components or when the context value changes frequently.</li>
<li>Limited to simple use cases: Context API is suitable for simple state management scenarios but may not be suitable for complex state logic or large-scale applications.</li>
<li>Complexity of usage: Context API introduces additional complexity and boilerplate, especially when managing multiple contexts or when using context consumers in class components.</li>
</ul>
</li>
</ul>
<ol start="45">
<li><strong>Explain the purpose of the componentDidCatch() lifecycle method in React.</strong></li>
</ol>
<p>The componentDidCatch() lifecycle method in React is used to handle errors that occur within a component’s subtree during rendering. It catches JavaScript errors thrown by child components in their lifecycle methods, event handlers, or render methods and allows the parent component to gracefully handle the error by displaying a fallback UI or logging the error for debugging purposes. componentDidCatch() is primarily used for error boundaries, which are special components in React that capture errors and prevent them from propagating up the component tree, thereby preventing the entire application from crashing due to unhandled errors.</p>
<ol start="46">
<li><strong>Discuss the differences between React.memo() and PureComponent.</strong></li>
</ol>
<p>React.memo() and PureComponent are both used to optimize functional components and prevent unnecessary re-renders, but they differ in their usage and behavior:<br>
-   React.memo() is a higher-order component for functional components that memoizes the result of rendering based on the component’s props. It performs a shallow comparison of props to determine if the component should re-render and only re-renders when props change. React.memo() is suitable for optimizing functional components and preventing unnecessary re-renders when props remain the same.<br>
-   PureComponent is a class component provided by React that implements shouldComponentUpdate() with a shallow comparison of props and state. It prevents re-renders when props or state remain the same and is suitable for optimizing class components with complex rendering logic. PureComponent is automatically applied to class components to optimize performance, whereas React.memo() must be explicitly applied to functional components.</p>
<ol start="47">
<li><strong>Explain the concept of synthetic events in React and how they differ from native DOM events.</strong></li>
</ol>
<p>Synthetic events in React are wrapper objects around native DOM events that provide a cross-browser interface for handling events in React components. Synthetic events mimic the behavior of native DOM events but are normalized to ensure consistent behavior across different browsers and platforms. Unlike native DOM events, which can have different properties and behaviors depending on the browser implementation, synthetic events have a consistent API and behavior in all environments. Synthetic events also have performance optimizations, such as event pooling and automatic event delegation, to improve performance in React applications.</p>
<ol start="48">
<li><strong>What is the purpose of React.Fragment and when would you use it?</strong></li>
</ol>
<p>React.Fragment is a built-in component provided by React that allows grouping multiple elements without adding extra nodes to the DOM. It provides a cleaner syntax for rendering lists of elements, fragments, or components without the need for a parent wrapper element like a </p><div>. React.Fragment is useful when:<br>
-   Rendering multiple elements or components without introducing additional DOM elements.<br>
-   Avoiding unnecessary wrappers or divs that clutter the DOM and CSS styles.<br>
-   Improving performance by reducing the number of nodes in the DOM and optimizing rendering efficiency.</div><p></p>
<pre><code>import React from 'react';

function MyComponent() {
  return (
    &lt;React.Fragment&gt;
      &lt;ChildComponent1 /&gt;
      &lt;ChildComponent2 /&gt;
    &lt;/React.Fragment&gt;
  );
}
</code></pre>
<ol start="49">
<li><strong>Explain how you can prevent default behavior in React event handlers.</strong></li>
</ol>
<p>In React event handlers, you can prevent the default behavior using the preventDefault() method of the event object. This method prevents the default action associated with the event from occurring, such as submitting a form, following a link, or scrolling the page. You can call preventDefault() within event handlers like onClick, onSubmit, or onKeyDown to prevent the default behavior of the event. Preventing default behavior is useful for implementing custom behavior or validation logic in response to user interactions without triggering the browser’s default actions.</p>
<pre><code>function handleClick(event) {
  event.preventDefault();
  // Custom logic here
}

&lt;button onClick={handleClick}&gt;Click me&lt;/button&gt;
</code></pre>
<ol start="50">
<li><strong>What are the key differences between React functional components and class components?</strong></li>
</ol>
<p>React functional components and class components are both used to define UI components in React, but they differ in their syntax, features, and usage:<br>
-   Functional components are defined as simple JavaScript functions that take props as input and return JSX elements as output. They are lightweight, easier to read and write, and support React hooks for managing state and side effects.<br>
-   Class components are defined as ES6 classes that extend React.Component and have access to lifecycle methods, state, and instance methods. They are more powerful, support more features like lifecycle methods and state management, and are suitable for complex UI logic and legacy codebases.<br>
-   Functional components are recommended for new development and modern React applications, while class components are still used in legacy codebases or when migrating existing code to functional components and hooks.</p>

