# Table of contents

- [Implementation](#implementation)
- [Design based](#design-based)
- [Theoretical](#theoretical)

# Implementation

- In the react component, there is a prop `data` which is a long string containing some text along with custom xml tags (e.g. : `<div>this is some text<tag1>some text inside tag1</tag2><tag2>tag2</tag2></div>`). You need to render this on UI by rendering the tags. The tags can be html or non-html tags. In case of non-html tags, you have to convert them into div/span/p etc (mapping will be provided). What are the ways to do it avoiding possible security issues?

- Create a input type and a progress bar (or a loader). Initially the progress bar shouldn't be filled. Take the value from user in input and accordingly fill the progress bar in percentage. Bonus points if progress bar has css animation. You can assume that values will be in range 0-100. 

# Design based

- Design a website for user portfolio for stocks. It should have the following functionality:
  - User signin/signup functionality
  - A page showing the stocks owned by user along with functionality to buy and sell his stocks as well as allowing him to purchase new stocks
  Key points to focus:
    - What will be API end points and structure?
    - What will be the code and folder structure for frontend repository?
    - How will the react components be designed so that they can be re-used?
    - How will the redux store be designed?

# Theoretical

- What is virtual dom in react? How does react reconcilication works?
- List the life cycle methods with proper order in react.
- Why is componentWillReceiveProps unsafe to use?
- What are various ways in which you can avoid re-render in React?
- What is HOC?
- What are react hooks?
- How do you write custom hooks?
- What is Pure Component in React?
- How do you handle errors in React?
- const comp1 = new ReactComponent({name , age , address}). How to change states.    

[comment]: <> (comp1.setState comp1.setState comp1.setState all 3 in same lines)

- List some ways in which optimization can be done in React - pure component, should component update, memo, usememo.
- What is context API?
- Difference between JSX and HTML.
- What is Redux? Are there any other state management libraries out there? Give examples.
- Why do you use redux? Why can't you work using only react?
- Why immutability in Redux?
- Why use redux? Why not react/context APIs etc?
- Explain redux flow.
- What are key differences between redux saga and thunk. List some use cases where you will use them?
- If a component is rendering very slow in React, how will you go about debugging/optimizing it?  
