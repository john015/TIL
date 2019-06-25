# 기본문법

sass와 동일

```javascript
const Button = styled.button`
  background-color: ${props => (props.danger ? 'red' : 'blue')};
  border-radius: 50px;
  &:focus {
    outline: none;
  }
`
```

## injectGlobal (styled-components v4에서 deprecated)

전역 css 선언시 사용

```javascript
import { injectGlobal } from 'styled-components' //import

injectGlobal`
body{
  margin: 0px;
  padding: 0px;
}
* {
  font-size: 30px;
}
`
```

## createGlobalStyle

v4 버전이후 전역 css 선언시 사용

```javascript
import { createGlobalStyle } from 'styled-components'
const GlobalStyle = createGlobalStyle`
  html {
    color: red;
  }
`
export default function App() {
  return (
    <div>
      <GlobalStyle />
      This is my app!
    </div>
  )
}
```

## mixin, extend, Extra Attribute

```javascript
import { css } from 'styled-components' //import

// mixin 값 설정
const mixin = css`
  background-color: ${props => (props.danger ? 'red' : 'blue')};
  border-radius: 50px;
  &:focus {
    outline: none;
  }
`

// 속성 설정
const Button = styled.button.attrs({
  attrs: true
})`
  ${mixin};
`

// extend, html tag 변경
const ExtendButton = Button.withComponent('a').extend`color: red;`
```

### theme

```javascript
// theme.js

const theme = {
container: `height: 100vh; width: 100%; background-color: pink; line-height: 10px;`;
mainColor: red;
};

export default theme;
```

```javascript
// app.js

import React, { Component, Fragment } from 'react'
import styled, { injectGlobal, ThemeProvider } from 'styled-components'
import theme from './theme'

class App extends Component {
  render() {
    return (
      <ThemeProvider theme={theme}>
        <Container />
      </ThemeProvider>
    )
  }
}

const Container = styled.div`
  ${({ theme }) => theme.container}
`
export default App
```

## typescript displayName 설정

- https://github.com/Igorbek/typescript-plugin-styled-components
- https://github.com/AustinBrunkhorst/react-app-rewire-styled-components-typescript
