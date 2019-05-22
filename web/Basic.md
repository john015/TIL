## 5가지 다른 stylesheet가 있을때, 최적화 하는방법

- css의 @import 문법을 사용해서 main stylesheet에 다른 4개의 스타일시트를 import하거나 webpack이나 gulp같은 번들러를 사용해서 5개의 스타일시트를 1개의 스타일시트로 변경

## Progressive enhancement vs graceful degradation

### 점진적 향상법(Progressive enhancement)

- HTML, CSS, JS를 각각 분리하여 페이지를 계층적인 방식으로 표현해서 먼저 HTML로 마크업을하고 그뒤로 CSS로 스타일링을 한뒤 마지막으로 JS로 동적으로 사이트를 만들어 만약 CSS나 JS가 작동하지않아도 사이트가 동작하게 개발하는것

### 우아한 성능 저하법(graceful degradation)

- 먼저 최신 브라우저에서 잘 동작하게 만들어 놓고, 오래된 브라우저 혹은 오래된 기기에서도 유사하게 동작하도록 개발하는것

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

- 간단한 애니메이션의 경우 CSS 애니메이션은 사용하기 쉽지만 JS 애니메이션보다 성능이 더 안좋다.
- 복잡한 에니메이션의 경우 CSS 애니메이션으로는 구현하기어렵고 JS 애니메이션을 사용해야한다.

## CORS란?

- CORS(Cross Origin Resource Sharing)란 서로 다른 도메인끼리 http Request을 가능하게하는 표준 규약이다.
- 기본적으로 Same Origin Policy에 의해 동일한 도메인끼리만 http Request가 가능하지만, CORS를 사용하게 된다면 다른 도메인으로 HTTP Request가 가능해진다.
- 이를 해결하기 위해선 여러가지 방법이 있는데, 프록시 서버를 사용하거나 JSONP방식을 사용하거나 서버측에서 http header에 Access control값을 설정하면 된다.

## i18n 지원하는 방법

- 웹페이지를 언어별로 작성한다음 보여준다(비추천)
- html tag의 dataset에 언어별 텍스트를 넣어놓고 보여준다.
- JSON파일에 언어별 텍스트를 입력해놓고 해당 JSON파일 값을 읽어서 보여준다.
- i18n 라이브러리를 사용해서 보여준다(react-intl, react-i18next, etc..)
