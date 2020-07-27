## Progressive enhancement vs graceful degradation

### 점진적 향상법(Progressive enhancement)

- 구식 기술 환경에서 동작할 수 있는 기능을 구현하고, 최신 기술을 사용할 수 있는 환경에서는 더 나은 사용자 경험을 제공할 수 있는 최신 기술을 제공하는 방법

### 우아한 성능 저하법(graceful degradation)

- 먼저 최신 브라우저에서 잘 동작하게 만들어 놓고, 오래된 브라우저 혹은 오래된 기기에서도 유사하게 동작하도록 개발하는 것
- ex) img 태그에 alt 속성을 지정함으로써 이미지를 보여주지 못하는 환경에서 이미지를 텍스트로 대체하는 것

## 웹사이트에서 assets/resources를 최적화하는 방법

- webpack같은 번들러를 사용해서 여러개의 css, js파일을 하나의 파일로 만들어 네트워크 요청의 횟수를 줄인다
- css, js파일을 minify해서 파일 크기를 줄인다
- 서버 사이드 캐싱, 클라이언드 사이드 캐싱을 활용하여 통신횟수를 줄인다

## HTTP/1.0 프로토콜 기준 브라우저가 한 번에 1개의 도메인에서 내려받을수 있는 resource수

- http/1.0 기준
- ie 8 ~ 9, chrome, firefox, opera: 6개
- ie 10 ~ 11: 8개
- HTTP/2.0 프로토콜 사용하면 제한 없음

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
