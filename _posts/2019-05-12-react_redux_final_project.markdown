---
layout: post
title:      "React/Redux Final Project"
date:       2019-05-12 16:30:27 -0400
permalink:  react_redux_final_project
---


For the Flatiron School final project, the assignment was to write an application using React/Redux with a Rails API back end.  I chose to make an application that pulls data from The Movie DB's API and displays that to the user.   

I must admit that as I started this project I was fairly confused about how state works with Redux and what that really meant for a React application.  However, this confusion quickly passed as I began to see the power that Redux offers in keeping the application's state all in one central store.  This is nothing short of amazing. 

With the applications state stored in a single store, it is fairly simple to pass that state down to the components which need it through props.  

I really enjoyed the fact that with the react-redux `connect()` function, one can be very specific in passing down data from state and assign that data to props in ways that make sense for the component in question. Let's take a look at this snippet from my TV Pal application:

```
const mapDispatchToProps = dispatch => {
  return {
    registrationDone: response => dispatch(authenticateUser(response)),
    displayErrors: response => dispatch(displayError(response)),
    dismissErrors: () => dispatch(dismissErrors())
  }
}

const mapStateToProps = state => {
  return {
    errors: state.user.errors
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(RegistrationContainer);
```

This shows exactly how easy it is to not only get the exact data you need from your Redux store but to also map dispatch actions to the component's props as well, giving a nice separation of concerns.  In the example above, the only bit of data my component cares about is any errors that have been returned when the form was submitted, so naturally, that's the only bit of data that should be pulled from the store.   In my `mapDispatchToProps` function I take care of dispatching actions from my action creators, and my component doesn't need to know about dispatching at all. It simply needs to know what it should do when it gets an error back from the back end and when a user submits the form. 

With all that said, it's very easy for me to see just how powerful and game-changing Redux could be, especially when an application scales to a much larger size.  Redux feels like a very helpful teammate, one that I wouldn't mind having around to help me out on my next project!  

![](https://media0.giphy.com/media/r2BtghAUTmpP2/giphy.gif?cid=790b76115cd8816675507a6b32018838&rid=giphy.gif)


