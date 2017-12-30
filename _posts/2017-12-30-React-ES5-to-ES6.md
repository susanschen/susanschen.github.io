---
layout: post
title: "How to Convert React createClass to React Component"
date: 2017-12-30
---
## React Version 16 Deprecated CreateClass
React.createClass is deprecated and will be removed in version 16. 
Below is a guide on how to convert the old code to new standards.

## Functional Components
Functional components has only render method and no other methods. 
```javascript
var Simple = React.createClass({             
  render: function() { return ( // code ) }  // remove render function keyword
});
```

```javascript
function Simple(props) {
  return ( // code )
};
```

## React.createClass to React.Component
Change var to class, = to extends and createClass to Component

### ES5
```javascript
var Theme = React.createClass({        
  handleClick: function(e) { // code }, 
  render: function() { return ( // code ) },
});
```

### ES6+
```javascript
class Theme extends React.Component {
  handleClick(e) { . . . }
  render() { return ( // code ) }
}
```
## Initial States and Default Props
### ES5
```javascript
var Part = React.createClass({
  getDefaultProps: function() {                 // get function will be replaced with static properties
    return {
      prop1: "content",
      prop2: true,
    };
  },
  propTypes: {                                  // will become static property
    prop1: React.PropTypes.string.isRequired,
    prop2: React.PropTypes.bool.isRequired,
  },
  getInitialState: function() {                 // get function will be replaced with static properties
    return {
      state1: this.props.prop2,
    };
  },
});
```

### ES6
```javascript
class Part extends React.Component {
  static defaultProps = {                           // static property
    prop1: "content",
    prop2: true,
  }
  static propTypes = {                              // static property
    prop1: React.PropTypes.string.isRequired,
    prop2: React.PropTypes.bool.isRequired,
  }
  state = {                                         // a property
      state1: this.props.prop2,
  }
}
```

## Lifecycle Method ComponentWillMount to Constructor

### ES5
```javascript
componentWillMount: function() {  // code },
```

### ES6+
```javascript
 constructor(props) {
    super(props);
    // code
  }  
```

## Event Handle Binding
React.createClass does automatic binding to event handling. In new version, binding must be done manually

### ES5
```javascript
var Section = React.createClass({
  handleChange: function(data) { 
    this.setState({ currentInfo: data });
  }
});
```

### ES6+
```javascript
class Section extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);  // Important: Bind event handles
  }
  handleChange(data) {                                 // Event handler stays the same
    this.setState({ currentInfo: data });              
  }
}
```
### ES6 Alternate Binding with Arrow Functions

```javascript
class Section extends React.Component {
  handleChange = (data) => {                            // Use arrow function instead of bind(this)
    this.setState({ currentInfo: data });
  }
}
```


#### Credit Source
The above guide is my notes on what I learned today from Babel. See [Babel](https://babeljs.io/blog/2015/06/07/react-on-es6-plus) for more info.
