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

## styled-components 동작 방식

- Tagged Template Literal을 파싱해서 문자열과 표현식을 분리시키고 함수인 표현식에는 props를 전달해서 스타일을 만든다.

- 고유한 componentId와 스타일을 더한 뒤 MurmurHash 알고리즘을 이용해 className을 만든다.

- 앞서 생성한 스타일을 stylis 라이브러리를 이용해 유효한 css로 변경시킨다.

- 미리 추가해놓은 head안 style 태그에 생성한 css를 삽입한다.

- 컴포넌트의 className에 componentId와 생성한 className을 넣어준 뒤 렌더링 한다.

## typescript displayName 설정

- https://github.com/Igorbek/typescript-plugin-styled-components
- https://github.com/AustinBrunkhorst/react-app-rewire-styled-components-typescript
