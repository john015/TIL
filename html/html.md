## doctype이란?

- HTML의 버전을 명시하는 tag

## 표준모드(standards mode) vs 호환모드(quirks mode)

- 일반적으로 브라우저는 표준모드로 웹페이지를 렌더링하며, 오래된 웹페이지의 경우 최신 버전의 브라우저에서 깨지지 않도록 렌더링하는 것이 호환 모드입니다.
- 브라우저가 html의 doctype을 읽고 해당 페이지가 최신 버전이라고 판단하면 표준 모드(standard mode)로 웹페이지를 렌더링합니다.
- 반면 브라우저가 해당 페이지를 구 버전 이라고 판단을 하면 호환 모드(quirks mode)로 렌더링을 하게 되며 이 모드에서는 해당 버전에 맞는 비표준 문법을 적용합니다.

## 커스텀 데이터 속성(data-\*)이란?

- HTML에서 기본적으로 제공되는 속성이 아닌, 개발자가 임의의 속성을 추가하고자 할 때 사용된다.
- 커스텀 데이터 속성은 html tag 상에서 별다른 작용을 하지 않는다.

## 쿠키(Cookies) vs 세션저장소(sessionStorage) vs 로컬저장소(localStorage)

- 셋 다 브라우저에 데이터를 저장하기 위한 기능들이다.
- 쿠키는 4kb까지만 데이터를 저장할 수 있고, 동일한 도메인의 페이지를 요청할 때마다 서버로 함께 전송되며, 변조가 쉬워 보안이 취약하다.
- 또한 유효기간을 지정할 수 있음.
- localStorage는 5mb까지의 데이터를 저장할 수 있고, 자동으로 서버에 데이터가 전송되지 않는다.
- 또한 데이터에 유효기간이 없고, localStorage를 설정한 도메인에서만 설정한 값을 읽을 수 있고 다른 도메인에서는 못 읽는다.
- sessionStorage는 localStorage와 동일하지만 sessionStorage에 저장된 데이터는 세션이 종료되면(해당탭이 종료)지워진다.

## IE 조건부 주석

```html
//ie 9미만
<!--[if lt IE 9]> <script src="./src/demo.js"> <![endif]-->

//ie 10이하
<!--[if lte IE 10]> <script src="./src/demo.js"> <![endif]-->
```

### !

- 아니다(not)
- 예) [if !ie] ie 가 아니라면

### lt

- 작다(less than)
- 예) [if lt ie 9] ie9 보다 작다면

### lte

- 작거나 같다(less than equal)
- 예) [if lte ie 8] ie8 보다 작거나 같다면

### gt

- 크다(greater than)
- 예) [if gt ie 6] ie6 보다 크다면

### gte

- 크거나 같다(greater than equal)
- 예) [if gte ie 7] ie7 보다 크거나 같다

### &

- 그리고(and)
- 예) [if (gte ie 7)&(lt ie 9)] ie7 이상이고 ie9 미만이라면

### |

- 또는(or)
- 예) [if (ie 7)|(ie 8)] ie7 이거나 ie8 이라면
