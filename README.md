> This is a fork to the now unmaintained project [react-inline-edit](https://github.com/kaivi/ReactInlineEdit).
> Only minimal maintainance will be provided, and __no new features will be accepted__. 

# Inline Edit Component for React

[![npm version](https://badge.fury.io/js/react-edit-inplace.svg)](https://badge.fury.io/js/react-edit-inplace) 

This is a simple React component for in-place text editing. It turns into an `<input />` when focused, and tries to validate and save input on <kbd>Enter</kbd> or `blur`. <kbd>Esc</kbd> works as well for cancelling.

![Example animation gif](http://i.imgur.com/8vig5m1.gif)

Watch a [demo](http://htmlpreview.github.io/?https://github.com/dkwingsmt/ReactInlineEdit/blob/master/demo/index.html), then check out [demo/index.jsx](demo/index.jsx) for a quick example.

### Installation

`npm install --save react-edit-inplace`

### Required props
- `text`:`string` initial text
- `paramName`:`string` name of the parameter to be returned to `change` function
- `change`:`function` function to call when new text is changed and validated, it will receive `{paramName: value}`

### Optional props
- `className`:_string_ CSS class name
- `activeClassName`:_string_ CSS class replacement for when in edit mode
- `validate`:_function_ boolean function for custom validation, using this overrides the two props below
- `minLength`:_number_ minimum text length, **default** `1`
- `maxLength`:_number_ maximum text length, **default** `256`
- `editingElement`:_string_ element name to use when in edit mode (DOM must have `value` property) **default** `input`
- `staticElement`:_string_ element name for displaying data **default** `span`
- `editing`:_boolean_ If true, element will be in edit mode
- `tabIndex`:_number_ tab index used for focusing with TAB key **default** `0`
- `stopPropagation`:_boolean_ If true, the event onClick will not be further propagated.

### Usage example
```javascript
import React from 'react';
import InlineEdit from 'react-edit-inplace';

class MyParentComponent extends React.Component {

    constructor(props){
      super(props);
      this.dataChanged = this.dataChanged.bind(this);
      this.state = {
        message: 'ReactInline demo'
      }
    }

    dataChanged(data) {
        // data = { description: "New validated text comes here" }
        // Update your model from here
        console.log(data)
        this.setState({...data})
    }

    customValidateText(text) {
      return (text.length > 0 && text.length < 64);
    }

    render() {
        return (<div>
            <h2>{this.state.message}</h2>
            <span>Edit me: </span>
            <InlineEdit
              validate={this.customValidateText}
              activeClassName="editing"
              text={this.state.message}
              paramName="message"
              change={this.dataChanged}
              style={{
                backgroundColor: 'yellow',
                minWidth: 150,
                display: 'inline-block',
                margin: 0,
                padding: 0,
                fontSize: 15,
                outline: 0,
                border: 0
              }}
            />
        </div>)
    }
}
```
