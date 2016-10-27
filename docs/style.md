# Overview

All applicable styles should be colocated with their corresponding JavaScript component using [Aphrodite](https://github.com/Khan/aphrodite).

## Legacy

All legacy styles are processed with [Less](http://lesscss.org/) and can be found in the /less directory. These should still be maintained but all future CSS should be written in JavaScript and kept inside the appropriate component file.

## Example

Here is an example of a React component styled with Aphrodite.

Aphrodite will automatically create a single `<style>` tag in the document `<head>` to put its generated styles in.

```jsx
const React = require('react')
const ImmutableComponent = require('./immutableComponent')
const {StyleSheet, css} = require('aphrodite')

class Button extends ImmutableComponent {
  render () {
    return <span className={css(styles.browserButton)} 
      disabled={this.props.disabled}
      data-l10n-id={this.props.l10nId}
      data-button-value={this.props.dataButtonValue}
      onClick={this.props.onClick} />
  }
}

const styles = StyleSheet.create({
  browserButton: {
    cursor: 'default',
    display: 'inline-block',
    lineHeight: '25px',
    width: '25px',
    height: '25px',

    ':hover': {
      color: 'black'
    },

    '@media (min-width: 500px)': {
      width: '100px'
    }
  }
})

module.exports = Button
```

A few things to note:

1. All multi-word properties become camel cased (lineHeight instead of line-height).
2. Pseudo selectors and media queries can be given their own class or be nested within a selector.

## Passing Styles to Child Components

With Aphrodite, styles can be treated as props and passed down from parent to child. Here is an example:

```jsx
// addEditBookmarkHanger.js

const React = require('react')
const ImmutableComponent = require('../../../js/components/immutableComponent')
const Button = require('../../../js/components/button')
const {StyleSheet, css} = require('aphrodite')

class AddEditBookmarkHanger extends ImmutableComponent {
  render () {
    <Button styles={[styles.hangerButton, styles.hangerText]} />
  }
}

const styles = StyleSheet.create({
  hangerButton: {
    width: '50px',
    height: '25px',

    ':hover': {
      color: orange
    }
  },

  hangerText: {
    fontSize: '20px'
  }
})

// button.js

const React = require('react')
const ImmutableComponent = require('./immutableComponent')
const {StyleSheet, css} = require('aphrodite')

class Button extends ImmutableComponent {
  render () {
    return <span className={css(this.props.styles)} />
  }
}
```