---
title: Learning to optimize ReactJS code
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

### 2. Inherit 'React.PureComponent'
The second way to avoid superfluous render is extending React.PureComponent. Nothing different between Pure component and component except Pure component implements 'shouldComponentUpdate' function automatically. They *shallow compare* old props/states with new props/states. But, one keynote when you consider using Pure component is: 'Use Pure Components, in case when the props and state changes are made to primitive type variable, state and props changes to reference variable may lead to incorrect results and inconsistent rendering'. 

### 3. Use 'React.Memo'

### 4. Don't change 'state' in 'render' function

### 5. Use less external library if them not neccessary

### 6. Profiling Components with the Chrome Performance Tab

### 7. Check Components are re-rendering with the Chrome Render Tab

### 8. Using Production Mode Flag in Webpack

## References:

1. Optiminzing Performance (@ReactJS.org): reactjs.org/docs/optimizing-performance.html

2. React.PureComponet (@ReactJS.org)

3. React.Memo (@ReactJS.org)

4. React Optimization (@codementor.io)
