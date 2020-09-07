## doctype이란?

- HTML의 버전을 명시하는 tag

## 커스텀 데이터 속성(data-\*)이란?

- HTML에서 기본적으로 제공되는 속성이 아닌, 개발자가 임의의 속성을 추가하고자 할 때 사용된다.
- 커스텀 데이터 속성은 html tag 상에서 별다른 작용을 하지 않는다.

## 쿠키(Cookies) vs 세션저장소(sessionStorage) vs 로컬저장소(localStorage)

- 셋 다 브라우저에 데이터를 저장하기 위한 기능들이다.
- 쿠키는 4kb까지만 데이터를 저장할 수 있고, 유효기간을 지정할 수 있다 또한 cookie에 데이터를 저장하면 무조건 서버에 request를 보낼 때 쿠키 정보도 같이 전달된다.
- localStorage는 5mb까지의 데이터를 저장할 수 있고. 데이터에 유효기간이 없고, localStorage를 설정한 도메인에서만 설정한 값을 읽을 수 있고 다른 도메인에서는 못 읽는다.
- sessionStorage는 localStorage와 동일하지만 sessionStorage에 저장된 데이터는 세션이 종료되면(해당탭이 종료되면)지워진다.

## script vs script async vs script defer

- 일반적으로 브라우저는 \<script\> tag를 만나면 웹 페이지 렌더링을 잠시 중단하고 js를 불러온 뒤 실행한다.
- 따라서 크기가 큰 script를 head에서 불러올 경우 렌더 블로킹이 발생한다.
- async와 defer 속성을 사용하게 되면 브라우저는 html 파싱을 중단하지 않고 비동기적으로 js파일을 불러온다.
- async와 defer의 차이점은 async의 경우 js 파일을 다 불러오는 즉시 실행하며 defer는 렌더링이 모두 완료된 뒤 script를 실행한다.

## img tag의 srcset 속성이란?

- srcset은 화면 해상도에 따라서 반응형 이미지를 제공하기 위한 속성이다.
- 최신 버전 기준 ie와 opera mini를 제외하고 모든 브라우저가 지원한다.

  ```html
  <!--
  width가 640px보다 큰경우 33.3vw을 기준으로 반응형 이미지를 제공하고 작은경우
  100vw을 기준으로 반응형 이미지를 제공함 <-->
  <img
    src="small.jpg"
    srcset="big.jpg 1024w, medium.jpg 640w, small.jpg 320w"
    sizes="(min-width: 640px) 33.3vw, 100vw"
  />
  ```

## 속성(Attribute) vs 요소(property)

### Attribute

- Attribute는 HTML 요소의 추가적인 정보를 표현하고 이름=”값”으로 표현된다
- 예를 들어 <div class="my-class"></div> 를 보면 class라는 attribute에 ‘my-class’라는 값이 할당 된것이다.

### Property

- Property는 attribute에 대한 HTML DOM 트리 내부에서의 표현이다

```html
<div class="my-class"></div>
<script>
  const myClassElement = document.querySelector(".my-class");
  console.log(myClassElement.class); // undefined
  console.log(myClassElement.className); // "my-class"
</script>
```

Attribute와 Property를 비교하면 Attributes는 HTML 문서에 있는 것이고 properties는 HTML DOM 트리에 있는 것이다.

## \<section\> vs \<article\> vs \<div\> vs \<aside\>

### Section

`<section>` 태그는 서로 관계가 있는 내용들을 그룹핑 하기위해 사용된다.

### Article

`<article>` 태그는 뉴스 기사나 블로그 글 같은 독립적인 내용을 표현할 때 사용한다.

### Div

`<div>` 태그는 아무 관계 없는 내용들을 그룹핑 할 때 사용한다.

### Aside

`<div>` 태그는 문서의 주요 내용과 간접적으로 연관된 부분을 나타낼 때 사용합니다.

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
