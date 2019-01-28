# SMACSS

- 기본(base), 레이아웃(layout), 모듈(module), 상태(state), 테마(theme) 다섯가지의 범주로 구분한다.
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

# BEM

- block--element\_\_modifier 규칙으로 작명한다.
- 여러단어의 조합은 하이픈(-)으로 연결하여 작명한다.

## Block(블록)

- 재사용 할 수 있는 기능적으로 독립적인 페이지 구성 요소
- 목적에 맞게 결정해야 한다.(logo, form, etc...)
- 블록은 환경에 영향을 받지 않아야 한다. 즉, 여백이나 위치를 설정하면 안된다.
- 블록은 중첩해서 작성 할 수 있다.

```css
.form {
  color: blue;
}
.header {
  font-size: 20px;
}
.footer {
  color: red;
}
```

## Element(요소)

- 블록안에서 특정 기능을 담당하는 부분
- Element는 중첩해서 작성 할 수 있다.
- 모든 블록에서 Element는는 필수가 아닌 선택적으로 사용한다

```css
.form__label {
  font-weight: bold;
}
.header__title {
  color: white;
}
.footer__image {
  margin: 10px;
}
```

## Modifier(수식어)

- 블록이나 요소의 모양, 상태
- 수식어는 단독으로 사용할 수 없다.
- 수식어에는 boolean 타입과 key-value 타입이 있다.
- boolean 타입: 값이 true 라고 가정한다. (form\_\_button-—disabled)
- key-value 타입 : key, value를 하이픈으로 연결하여 표시한다. (form\_\_button--color-red)

```css
.form__label--disabled {
  opacity: 0.4;
}
.header__title--color-gray {
  color: gray;
  font-size: 32px;
}
.footer__image--size-big {
  width: 400px;
  height: 350px;
  margin: 20px;
}
```

# OOCSS

## 기본 규칙

- 반복적인 시각적 코드(background, border, etc..)을 별도의 스킨으로 정의하여 중복 코드를 줄인다.
- 위치에 의존적인(부모 자식, 형제 자매 셀렉터 등) 스타일을 정의하지 않는다 (.object h2)

## 네이밍 방법

- 짧고 간결하게 작성한다.
- 동작과 형태가 예상 가능하도록 명확하게 작성한다.
- 어떻게 생겼는지 보다는 어떤 목적인지 알 수 있도록 작성한다.
- 지나치게 구체적 이지 않게 일반적으로 사용 가능 하도록 작성한다.

```html
<!-- 기존 방식 -->
<button class="google_btn">Google Login</button>
<button class="github_btn">Github login</button>
<!-- OOCSS 방식 -->
<button class="btn google">Facebook</button>
<button class="btn github">Twitter</button>
```
