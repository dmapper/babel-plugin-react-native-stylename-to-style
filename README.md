# babel-plugin-react-native-stylename-to-style

[![NPM version](http://img.shields.io/npm/v/babel-plugin-react-native-stylename-to-style.svg)](https://www.npmjs.org/package/babel-plugin-react-native-stylename-to-style)
[![Build Status](https://travis-ci.org/kristerkari/babel-plugin-react-native-stylename-to-style.svg?branch=master)](https://travis-ci.org/kristerkari/babel-plugin-react-native-stylename-to-style)
[![Build status](https://ci.appveyor.com/api/projects/status/1040mtj6qyu9vkg8/branch/master?svg=true)](https://ci.appveyor.com/project/kristerkari/babel-plugin-react-native-stylename-to-style/branch/master)
[![Coverage Status](https://coveralls.io/repos/github/kristerkari/babel-plugin-react-native-stylename-to-style/badge.svg?branch=master)](https://coveralls.io/github/kristerkari/babel-plugin-react-native-stylename-to-style?branch=master)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github)

Transform JSX `styleName` property to `style` property in react-native. The `styleName` attribute and syntax are based on [babel-plugin-react-css-modules](https://github.com/gajus/babel-plugin-react-css-modules#conventions).

## Usage

### Step 1: Install

```sh
yarn add --dev babel-plugin-react-native-stylename-to-style
```

or

```sh
npm install --save-dev babel-plugin-react-native-stylename-to-style
```

### Step 2: Configure `.babelrc`

You must give one or more file extensions inside an array in the plugin options.

```
{
  "presets": [
    "react-native"
  ],
  "plugins": [
    ["react-native-stylename-to-style", {
      "extensions": ["css"]
    }]
  ]
}
```

## Syntax

## Anonymous reference

Anonymous reference can be used when there is only one stylesheet import.

### Single class

```jsx
import "./Button.css";

<View styleName="wrapper">
  <Text>Foo</Text>
</View>;
```

↓ ↓ ↓ ↓ ↓ ↓

```jsx
import Button from "./Button.css";

<View style={Button.wrapper}>
  <Text>Foo</Text>
</View>;
```

### Multiple classes

```jsx
import "./Button.css";

<View styleName="wrapper red-background">
  <Text>Foo</Text>
</View>;
```

↓ ↓ ↓ ↓ ↓ ↓

```jsx
import Button from "./Button.css";

<View style={[Button.wrapper, Button["red-background"]]}>
  <Text>Foo</Text>
</View>;
```

### with `styleName` and `style`:

```jsx
import "./Button.css";

<View styleName="wrapper" style={{ height: 10 }}>
  <Text>Foo</Text>
</View>;
```

↓ ↓ ↓ ↓ ↓ ↓

```jsx
import Button from "./Button.css";

<View style={[Button.wrapper, { height: 10 }]}>
  <Text>Foo</Text>
</View>;
```

## Named reference

Named reference is used to refer to a specific stylesheet import.

### Single class

```jsx
import foo from "./Button.css";

<View styleName="foo.wrapper">
  <Text>Foo</Text>
</View>;
```

↓ ↓ ↓ ↓ ↓ ↓

```jsx
import foo from "./Button.css";

<View style={foo.wrapper}>
  <Text>Foo</Text>
</View>;
```

### Multiple classes

```jsx
import foo from "./Button.css";
import bar from "./Grid.css";

<View styleName="foo.wrapper bar.column">
  <Text>Foo</Text>
</View>;
```

↓ ↓ ↓ ↓ ↓ ↓

```jsx
import foo from "./Button.css";
import bar from "./Grid.css";

<View style={[foo.wrapper, bar.column]}>
  <Text>Foo</Text>
</View>;
```
