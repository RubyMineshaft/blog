---
layout: post
title:      "React's State Hook"
date:       2019-08-25 00:45:33 +0000
permalink:  reacts_state_hook
---


State is an important aspect of React, and as of 16.8, managing state within your React app is even easier with the use of React hooks.  

Today we will take a brief look at the `React.useState` hook.

First, in order to use the state hook within our functional component we will need to import it:

```javascript
import React, { useState } from 'react';
```

`useState` returns two values:  the current state, and a function that can be used to update the state.

```javascript
import React, { useState } from 'react';

const PeopleList = props => {
  const [people, setPeople] = useState([]);
}
```

In this example, we are calling `useState` and passing it the initial state of an empty array.  `useState` returns the current state in a constant named *people* and can be updated with the function setPeople();

The fact that we are able to name our state constants anything we want and have multiple different states makes managing state very convenient. 



