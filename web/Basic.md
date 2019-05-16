## 5가지 다른 stylesheet가 있을때, 최적화 하는방법

- css의 @import 문법을 사용해서 main stylesheet에 다른 4개의 스타일시트를 import하거나 webpack이나 gulp같은 번들러를 사용해서 5개의 스타일시트를 1개의 스타일시트로 변경

## 점진적 향상법(Progressive enhancement) vs 우아한 성능 저하법(graceful degradation)

### 점진적 향상법(Progressive enhancement)

- HTML, CSS, JS를 각각 분리하여 페이지를 계층적인 방식으로 표현해서 먼저 HTML로 마크업을하고 그뒤로 CSS로 스타일링을 한뒤 마지막으로 JS로 동적으로 사이트를 만들어 만약 CSS나 JS가 작동하지않아도 사이트가 동작하게 개발하는것

### 우아한 성능 저하법(graceful degradation)

- 먼저 최신 브라우저에서 잘 동작하게 만들어 놓고, 오래된 브라우저 혹은 오래된 기기에서도 유사하게 동작하도록 개발하는것

## 웹사이트에서 assets/resources를 최적화하는 방법

- webpack이나 gulp같은 번들러를 사용해서 여러개의 css, js파일을 하나의 파일로 만들어 http요청의 횟수를 줄인다
- css, js파일을 minify해서 파일 크기를 줄인다
- 서버 사이드 캐싱, 클라이언드 사이드 캐싱을 활용하여 통신횟수를 줄인다
