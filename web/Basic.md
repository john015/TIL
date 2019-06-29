## 5가지 다른 stylesheet가 있을때, 최적화 하는방법

- css의 @import 문법을 사용해서 main stylesheet에 다른 4개의 스타일시트를 import하거나 webpack이나 gulp같은 번들러를 사용해서 5개의 스타일시트를 1개의 스타일시트로 변경

## Progressive enhancement vs graceful degradation

### 점진적 향상법(Progressive enhancement)

- 구식 기술 환경에서 동작할 수 있는 기능을 구현하고, 최신 기술을 사용할 수 있는 환경에서는 더 나은 사용자 경험을 제공할 수 있는 최신 기술을 제공하는 방법이다

### 우아한 성능 저하법(graceful degradation)

- 먼저 최신 브라우저에서 잘 동작하게 만들어 놓고, 오래된 브라우저 혹은 오래된 기기에서도 유사하게 동작하도록 개발하는것
- ex) img 태그에 alt 속성을 지정함으로써 이미지를 보여주지 못하는 환경에서 이미지를 텍스트로 대체하는 것

## 웹사이트에서 assets/resources를 최적화하는 방법

- webpack이나 gulp같은 번들러를 사용해서 여러개의 css, js파일을 하나의 파일로 만들어 http요청의 횟수를 줄인다
- css, js파일을 minify해서 파일 크기를 줄인다
- 서버 사이드 캐싱, 클라이언드 사이드 캐싱을 활용하여 통신횟수를 줄인다

## 브라우저가 한 번에 1개의 도메인에서 내려받을수 있는 resource수

- ie 8 ~ 9, chrome, firefox, opera: 6개
- ie 10 ~ 11: 8개

## 페이지 로드 시간을 줄이는 방법

- gzip
- Resource prefetching
- 이미지 스프라이트

## Flash of Unstyled Content(FOUC)이란? FOUC를 피하기 위한 방법

- FOUC란 CSS 코드를 불러오기 전 스타일이 적용되지 않은 페이지가 잠시 나타나는 현상이다. 특히 IE에서 자주 발생하는 현상으로, UX을 저하시킨다.
- FOUC를 피하기 위해선 head tag 안에 CSS를 link하고 @import의 사용을 자제해야 한다. 또한 JavaScript로 styling을 한다면 head tag 안에서 js를 load할수도있다.

## ARIA와 screenreader이란?

- ARIA(Accessible Rich Internet Applications)이란 웹페이지를 작성할 때 장애인이 웹페이지를 잘 식별할 수 있도록 하는 접근성 명세 이다.
- ARIA 속성들은 [링크](https://github.com/lezhin/accessibility/blob/master/aria/README.md#html)를 참고
- screenreader란 시각장애인이 컴퓨터를 사용할 때 나타나는 정보들을 음성으로 출력해주는 프로그램이다.

## CSS 애니메이션과 JavaScript 애니메이션의 차이점

- 자바스크립트는 메인 쓰레드가 무거운 작업을 하고 있을 때 애니메이션 처리의 우선순위를 미뤄두는 반면 CSS는 독립적인 쓰레드가 애니메이션을 처리해준다. 때문에 CSS 애니메이션은 최적화가 쉽다.
- 하지만 복잡한 에니메이션의 경우 CSS 애니메이션으로는 구현하기 어렵고 JS 애니메이션을 사용 해야한다.

## CORS란?

- CORS(Cross Origin Resource Sharing)란 서로 다른 도메인끼리 http Request을 가능하게하는 표준 규약이다.
- 기본적으로 Same Origin Policy에 의해 동일한 도메인끼리만 http Request가 가능하지만, CORS를 사용하게 된다면 다른 도메인으로 HTTP Request가 가능해진다.
- 이를 해결하기 위해선 여러가지 방법이 있는데, 프록시 서버를 사용하거나 JSONP방식을 사용하거나 서버측에서 http header에 Access control값을 설정하면 된다.
- 보통 서버측에서 데이터의 http header에 Access control값을 설정하는걸 권장한다.

|           HTTP Header            |          Description           |
| :------------------------------: | :----------------------------: |
|   Access-Control-Allow-Origin    |     접근 가능한 `url` 설정     |
| Access-Control-Allow-Credentials |    접근 가능한 `쿠키` 설정     |
|   Access-Control-Allow-Headers   |    접근 가능한 `헤더` 설정     |
|   Access-Control-Allow-Methods   | 접근 가능한 `http method` 설정 |

```javascript
res.header('Access-Control-Allow-Origin', '*')
res.header('Access-Control-Allow-Methods', 'GET, POST, DELETE, PUT, PATCH')
res.header(
  'Access-Control-Allow-Headers',
  'Origin, X-Requested-With, Content-Type, Accept'
)
res.header('Access-Control-Allow-Credentials', true)
```

## i18n 지원하는 방법

- 웹페이지를 언어별로 작성한다음 보여준다(비추천)
- html tag의 커스텀 데이터 속성에 언어별 텍스트를 넣어놓고 보여준다.
- JSON파일에 언어별 텍스트를 입력해놓고 해당 JSON파일 값을 읽어서 보여준다.
- i18n 라이브러리를 사용해서 보여준다(react-intl, react-i18next, etc..)

## 크로스 브라우징 지원하는법

polyfill이나 babel을 사용하거나 ie8이하를 지원해야한다면 기능 검출(feature detection)를 해서 하위브라우저를 지원해준다.

```javascript
function addHandler(el, type, handler) {
  // chrome
  if (el.addEventListener) {
    el.addEventListener(type, handler)
    return
  }
  // ie
  if (el.attachEvent) {
    el.attachEvent('on' + type, handler)
    return
  }
  // old broswer
  element['on' + type] = handler
}
```

## SPA vs SSR(universal web app)

### SPA

- SPA(Single Page Application)은 각 페이지에 접속할 때 마다 페이지를 요청하는게 아니라 최초 한번 페이지 전체를 로딩한뒤 데이터만 변경하여 사용할 수 있는 웹 애플리케이션이다.
- 전통적인 웹 방식(SSR)은 페이지를 변경할 때마다 서버로부터 리소스를 전달받아 해석하고 화면에 렌더링하는 방식이였기때문에 SPA보다 성능이 안좋았다.
- SPA는 트래픽을 감소시키고 사용자에게 더 나은 경험을 제공할 수 있다. SPA일경우 서버는 단지 JSON 파일만 보내주는 역할을 하면됐고, html을 그리는 역할은 클라이언트측의 자바스크립트가 수행하게 되었다.

#### SPA의 문제점

하지만 SPA는 마냥 장점만 있는것만은 아니다.

##### 초기 페이지 렌더링 속도가 느리다.

- SPA는 전통적인 SSR과 달리 맨처음 웹사이트에 접속했을 때 모든 페이지소스를 다 로딩하기 때문에 SSR에 비해 초기 렌더링 속도가 느리다.

##### 검색 엔진 최적화 문제(SEO)

- SPA는 JavaScript로 웹페이지를 렌더링하기때문에 구글은 제외한 나머지 포털 사이트들(네이버, 다음, 네이트, etc...)의 크롤러들은 빈 페이지로 인식하게된다.
- 또한 페이스북, 트위터, 카카오톡등의 미리보기도 각 페이지마다 미리보기를 설정할 수 없고 전체 페이지들에게 동일한 미리보기와 설명을 보여줘야한다.

이러한 문제들을 해결하기위해 next.js나 nuxt.js등의 라이브러리들을 활용하여 universal web app을 구현할 수 있다.

### SSR(universal web app)

- Universal Web App은 초기 렌더링은 전통적인 SSR방식을 사용해 서버에서 렌더링하여 보여주고 초기 페이지가 보여지는동안 페이지 전체를 로드하여 다른 페이지에 접근하면 SPA방식과 동일하게 동작하는 웹 애플리케이션이다.
- Universal Web App을 사용하면 초기 렌더링속도문제를 해결할 수 있고, SEO문제도 해결할 수 있다.
- 하지만 서버에 트래픽이 증가하고, 작성할 코드가 많아진다.

## 브라우저의 layout, painting, compositing

### layout(reflow)

레이아웃 너비, 높이, 왼쪽 또는 상단 위치 등 요소의 기하학적 형태에 영향을 주는 'layout' 속성을 변경하면 브라우저가 다른 모든 요소를 확인하고 페이지에 대해 '리플로우'를 수행해야 합니다. 영향을 받은 영역이 있으면 다시 페인트해야 하고 최종적으로 페인트한 요소는 다시 합성해야 합니다.

### painting

페이지의 레이아웃에 영향을 주지 않는 배경 이미지, 텍스트 색상 또는 그림자 등의 'paint only' 속성을 변경하면, 브라우저가 레이아웃을 건너뛰되 페인트 작업은 여전히 수행합니다.

### compositing

transform, opacity등의 속성을 변경하면 composite작업만 수행합니다.

각 painting된 레이어들을 병합한후 화면을 출력합니다.

ps. 주어진 CSS 속성을 변경하는 위의 세 가지 버전 중 어느 버전이 트리거될지 알고 싶은 경우 [CSS 트리거](https://csstriggers.com/)를 참조하세요.

## Synchronous vs Asynchronous vs Blocking vs NonBlocking

### Synchronous/Asynchronous는 호출되는 함수의 작업 완료 여부를 누가 신경쓰냐가 관심사

- 호출되는 함수의 작업 완료를 호출한 함수가 신경쓰면 Synchronous
- 호출되는 함수의 작업 완료를 호출된 함수가 신경쓰면 Asynchronous

### Blocking/NonBlocking은 호출되는 함수가 바로 리턴하느냐 마느냐가 관심사

- 바로 리턴하지 않으면 Blocking
- 바로 리턴하면 NonBlocking

<img src="http://i.imgur.com/gKDoKbs.png">

- [참고](https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
