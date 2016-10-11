#Inline Styles

There are many different ways to use styles in React.

An inline style is a style that's written as an attribute, like this:
```js
<h1 style={{ color: 'red' }}>Hello world</h1>
```
Notice the double curly braces. The outer curly braces inject JavaScript into JSX. They say, "everything between us should be read as JavaScript, not JSX."

The inner curly braces create a JavaScript object literal. They make this a valid JavaScript object:
```js
{ color: 'red' }
```
If you inject an object literal into JSX, and your entire injection is only that object literal, then you will end up with double curly braces. There's nothing unusual about how they work, but they look funny and can be confusing.

```js
var React = require('react');
var ReactDOM = require('react-dom');

var styleMe = <h1 style={{ background: 'lightblue', color: 'darkred' }}>Please style me!  I am so bland!</h1>;

ReactDOM.render(
	styleMe,
	document.getElementById('app')
);
```
#Make A Style Object Variable

One problem with this approach is that it becomes obnoxious if you want to use more than just a few styles. An alternative that's often nicer is to store a style object in a variable, and then inject that variable into JSX.
```js
var React = require('react');

var styles = {
  color: 'darkcyan',
  background: 'mintcream'
};

var StyledClass = React.createClass({
  render: function () {
    return (
      <h1 style={styles}>
        Hello world
      </h1>
    );
  }
});

module.exports = StyledClass;
```
Defining a variable named style in the top-level scope would be an extremely bad idea in many JavaScript environments! In React, however, it's totally fine.

Remember that every file is invisible to every other file, except for what you choose to expose via module.exports. You could have 100 different files, all with global variables named style, and there could be no conflicts.

#Style Name Syntax

In regular JavaScript, style names are written in hyphenated-lowercase:
```js
var styles = {
  'margin-top':       "20px",
  'background-color': "green"
};
```
In React, those same names are instead written in camelCase:
```js
var styles = {
  marginTop:       "20px",
  backgroundColor: "green"
};
```
This has zero effect on style property values, only on style property names.

#Style Value Syntax

Style values are slightly different in React than they are in regular JavaScript.

In regular JS, style values are almost always strings. Even if a style value is numeric, you usually have to write it as a string so that you can specify a unit. For example, you have to write "450px" or "20%".

In React, if you write a style value as a number, then the unit "px" is assumed.

How convenient! If you want a font size of 30px, you can write:
```js
{ fontSize: 30 }
```
If you want to use units other than "px," you can use a string:
```js
{ fontSize: "2em" }
```
Specifying "px" with a string will still work, although it's redundant.

A few specific styles will not automatically fill in the "px" for you. These are styles where you aren't likely to use "px" anyway, so you don't really have to worry about it. Here is a list of styles that don't assume "px". https://facebook.github.io/react/tips/style-props-value-px.html

#Share Styles Across Multiple Components

What if you want to reuse styles for several different components?

One way to make styles reusable is to keep them in a separate JavaScript file. This file should export the styles that you want to reuse, via module.exports. You can then require your styles into any component that wants them.
