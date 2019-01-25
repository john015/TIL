# SMACSS

- 범주화로 패턴화 하고자 하는 방법론이다.
- 기본(base), 레이아웃(layout), 모듈(module), 상태(state), 테마(theme) 다섯가지의 범주를 제시한다.
- !important를 쓰지 않는다.

## Base

- 기본 스타일(Reset, Default, Variables, Mixins)

```css
body,
button ... {
  margin: 0;
  padding: 0;
}
```

## Layout

- 레이아웃과 관련된 스타일(ex header, footer …)
- id를 사용 할 수 있으며 Class명에는 suffix “l-”를 붙인다

```css
#header {
  width: 400px;
}
#aside {
  width: 30px;
}
.l-width #header {
  width: 600px;
  padding: 10px;
}
.l-width #aside {
  width: 100px;
}
```

## Module

- 스타일 재 사용을 위한 요소
- 재사용을 위해 id 셀렉터와 element를 사용하지 않는다.
- 만약, element 셀렉터를 사용해야 한다면, .container > p 처럼 child 셀렉터를 사용

```css
.folder > span {
  padding: 20px;
}
```

## State

- 상태를 나타내는 스타일
- active, hover 등의 상태에서 사용
- Class명에 suffix “is-” 또는 “s-”를 붙여서 사용

```css
.btn {
  display: inline-block;
  background: #ddd;
  border-radius: 4px;
}

.btn .is-active {
  background: #43f837;
}

.btn .is-hidden {
  display: none;
}
```

## Theme

- 색상이나 이미지를 분리, 기존 스타일을 재 선언하여 사용할 수 있다.
- 적용범위가 넓은 테마는 “theme-”를 suffix를 붙여 사용한다.

```css
.blue {
  color: blue;
}
.theme-red {
  color: red;
}
```
