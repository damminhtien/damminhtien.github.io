---
title: Learning to optimize ReactJS app by avoiding redundant re-render
tags: ReactJS, Optimization, Web-development, Front-end
mode: immersive
header:
  theme: dark
article_header:
  type: cover
  image:
    src: /assets/images/reactjs.png
---

@**Author**: damminhtien :whale:

@**CreatedAt**: 07/10/2019

@**LastUpdate**: 04/01/2020

*Writing ReactJS code to run can be easy but writing ReactJS code efficiently is more difficult*. While better performance will lead to better UI, UX; React API provides massive clever techniques to minimize the number of costly DOM operations required to update the interface.  A list below contains a few key-words that might help you run React apps smoothly. Each one just was described simple and short, if you need to known more details, you can get addition information in [References](#references) part.

### 1. Use 'shouldComponentUpdate' function to avoid superfluous re-render
If you prefer class-based components than function-based components, you should try 'shouldComponentsUpdate' function. This function is a event in React life cycle:
![reactlifecycle](/assets/images/reactlifecycle.png)
We all known that components always re-render when a state or prop is changed. So, if the new state/ prop 's value doesn't change, it is redundant. The shouldComponentUpdate() method is the first real life cycle optimization method that we can leverage in React. We can look at our current and new props & state and make a choice if we should move on. It prevent your components re-render if they are unneccessary.

But, you are fan of React hook and similar with function-based components :confused: ? Dont worry, you can easily implement **shouldComponentUpdate' just by passing an array as an optional second argument.
```javascript
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```
 
### 2. Inherit 'React.PureComponent'
The second way to avoid superfluous render is extending React.PureComponent. Nothing different between Pure component and component except Pure component implements 'shouldComponentUpdate' function automatically. They *shallow compare* old props/states with new props/states. But, one keynote when you consider using Pure component is: 'Use Pure Components, in case when the props and state changes are made to primitive type variable, state and props changes to reference variable may lead to incorrect results and inconsistent rendering'. 
Example: instead of extend React.Component, we extends React.PureComponent
```javascript
class MyComponent extends PureComponent {...}
```

### 3. Use 'React.Memo', useMemo
A rule of thumb in React: when a parent component re-renders, all child components will re-render as well. But sometime we need only one child component change, re-rendering of other child components are unneccessary. At that time, **React.memo** is our hero. React.memo is a higher order component, used with functional components. React.memo will compare the previous props to the next props, and if different, will re-render the component. Like the comparison in React.PureComponent is **shallow comparison**, it work fine when compares (string, number, boolean. However, arrays, objects, and functions being passed as a prop will not work with React.memo alone. We will need to use hooks like useMemo around the Array or Object. In a functional component, every re-render will cause everything in the function body to be "re-created". So arrays, objects, and functions will be new and different on every re-render. When these are passes to the child Component, it will cause the child to re-render. Wrapping arrays and objects with the useMemo hook will solve this problem. Better yet, if the dependency array is empty, you should just hoist it out of the function body.

### 4. Don't change **state** in **render** function
This is a default warning in React. If we change **state** in render function, it make the function re-call -> state change -> render function re-call -> ...
We create a loop of render HTML DOM, making waste!

## Conclusion
Donald Knuth wrote that “premature optimization is the root of all evil” years before JavaScript was even imagined, but that does not make it any less relevant today.

Of course, us JavaScript programmers are not known for learning things the easy way, and a number of you are probably now asking “but some things are less evil than others, right?” After all, how much can a short three-line function really hurt when it isn’t even going to slow things down? Actually, my experience is that it can be downright painful.

## Other techniques without coding
* Use less external library if them not neccessary

* Profiling Components with the Chrome Performance Tab

* Check Components are re-rendering with the Chrome Render Tab

* Using Production Mode Flag in Webpack

## References:

1. Optiminzing Performance (@ReactJS.org): reactjs.org/docs/optimizing-performance.html

2. React.PureComponet (@ReactJS.org)

3. React.Memo (@ReactJS.org)

4. React Optimization (@codementor.io)
