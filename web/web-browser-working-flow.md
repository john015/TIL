# 웹 브라우저의 동작 원리

<img src="https://user-images.githubusercontent.com/32455422/59767121-91515e00-92dc-11e9-8501-a50da6436ee2.png" />

## 웹 페이지 렌더링 과정

- URL Entered: 사용자가 웹 브라우저에서 사이트 주소를 입력

- DNS Lookup: DNS서버로 접근하여 사이트 주소에 해당되는 Server IP를 획득

- Socket Connection: Client(브라우저)와 Server 간 접속을 위한 TCP 소켓 연결

- HTTP Request: Client에서 HTTP Header와 데이터가 서버로 전송

- Content Download: 해당 요청이 Server에 도달하면 사용자가 요청한 문서를 다시 웹 브라우저에 전송

- Browser Rendering: 전달된 문서를 웹 브라우저의 렌더링엔진에서 파싱이후 렌더링

## 브라우저의 기본 구조

- 사용자 인터페이스 - 주소 표시줄, 이전/다음 버튼, 북마크 메뉴 등. 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분이다.
- 브라우저 엔진 - 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어.
- 렌더링 엔진 - 요청한 콘텐츠를 표시. 예를 들어 HTML을 요청하면 HTML과 CSS를 파싱하여 화면에 표시함.
- 네트워킹 - HTTP 요청과 같은 네트워크 호출에 사용됨. 이것은 플랫폼 독립적인 인터페이스이고 각 플랫폼 하부에서 실행됨.
- UI 백엔드 - select / input 등 기본적인 위젯을 그림. 플랫폼에서 명시하지 않은 일반적인 인터페이스로서, OS 사용자 인터페이스 체계를 사용.
- 자바스크립트 파서 - 자바스크립트 코드를 해석하고 실행.
- 자료 저장소 - Cookie, Local storage등 local에 data를 저장하는 영역.

<img src="https://user-images.githubusercontent.com/32455422/59767397-32401900-92dd-11e9-845d-3d3512183b9e.png" />

## rendering-flow

- DOM Tree 생성
- CSSOM 생성
- Render Trre(DOM + CSSOM) 생성
- Render Tree reflow
- Render Tree painting

<img src = "https://user-images.githubusercontent.com/32455422/59767869-2f91f380-92de-11e9-9a4b-9077b4e3bf9f.png"/>

### DOM(Document Object Model) 생성

html파일을 서버로부터 불러오면, html파일을 파싱해서 DOM을 생성한다, html 파일을 파싱하는 도중 script 태그나, stylesheet link를 만나면 잠시 html 파싱을 멈추고 js나 css를 파싱한다.

다음 네 단계를 거쳐서, 트리 구조 모양의 DOM이 생성된다.

- Conversion(변환) : HTML의 raw bytes(원시 바이트)형태로 서버에서 받아온다. 해당 파일의 인코딩(예:UTF-8)에 따라 문자로 변환한다.
- 어휘 분석(토큰화) : 브라우저가 변환된 문자열을 HTML5 표준에 따라 고유 토큰으로 변환한다.
- 구문 분석(렉싱) : 이 토큰들은 다시 각각의 특성과 규칙을 정의한 object(객체) “노드”로 변환된다.
- DOM 생성 : HTML 마크업이 여러 태그 간의 관계를 나타내기 때문에 DOM은 트리 구조를 가진다. 따라서, DOM에 포함된 노드 또한 서로 관계를 가지게 된다. 다시 말해서, 노드의 상대적인 관계를 이용하면, 하나의 노드를 기준으로 모든 노드에 접근할 수 있다.

DOM 트리는 마크업과 1:1의 관계를 맺는다.

DOM 트리는 문서 마크업의 속성과 관계를 포함하지만, 렌더링될 때 표시되는 모습에 대해서는 CSSOM이 관여한다.

### CSSOM(CSS Object Model) 생성

- html 파일을 파싱하던 도중 stylesheet link를 만나면 DOM을 생성할 때 거쳤던 과정을 그대로 CSS에 반복한다. 그 결과로 브라우저가 이해하고 처리할 수 있는 형식(Style Rules)으로 변환된다.

- CSSOM 역시 트리 구조를 가지는데, 그 이유는, ‘하향식’으로 규칙을 적용하기 때문이다. 루트(body)부터 시작해서, 트리를 만들어 가는 방식이다. 모든 요소의 최종 스타일을 확정할 때 브라우저는 해당 노드에 적용 가능한 가장 일반적인 규칙으로 시작한 후에 더욱 구체적인 규칙을 적용한다.

### Render Tree(DOM + CSSOM)생성 - Attachment

- DOM 트리의 루트(html)에서 시작해서, 페이지에 표시되는 각각의 노드에 일치하는 CSSOM 규칙을 찾아 붙인다.

- 이때, 렌더링 트리에는 페이지를 렌더링하는 데 필요한 가시적인 노드만 포함된다.
  따라서, 메타 태그나 스크립트 태그 같은 노드나 display : none 으로 스타일이 지정된 노드는 제외된다.
  그러나, visibility : hidden 스타일이 적용된 노드는 보이지는 않지만 공간을 차지하므로, 렌더링 트리에 포함된다.

- DOM 트리와 렌더 트리의 노드는 서로 1:1로 대응되지 않는다.
- DOM 트리의 구성원 가운데 일부 노드(<head>, <title>, <script> 등)는 화면에 표현되는 노드가 아니므로 DOM 트리의 구성원이지만 렌더 트리의 구성원은 아닙니다.

### Layer Tree 생성(모던 브라우저에서 진행)

- 렌더링에 사용될 최종 Layer들을 계산 해서 생성 하는 과정

#### 레이어가 생성되는 조건

1. 페이지에서 root 객체이다.
2. CSS Position 프로퍼티가 relative or absolute이다.
3. CSS filter 프로퍼티를 가지고있다.
4. CSS 3D Transform, animations 프로퍼티를 가지고있다.
5. canvas나 video 태그 엘리먼트다.
6. will-change 프로퍼티를 가지고있다.

### Render Tree 배치 - layout(reflow)

- 지금까지의 과정을 요약하면, 브라우저가 화면에 표시할 노드와 해당 노드의 스타일을 계산하면서, 하나의 그룹으로 묶어서 렌더링 트리를 만든 것이다.

- reflow는 브라우저가 화면에 그리기 전에, 이 노드들을 정확한 위치와 크기로 나타내기 위해서 계산하는 과정이다. 이때, 모든 상대적인 값(예:%단위)은 절대적인 값(예:px단위)로 변환된다.

### Render Tree 그리기 - Painting

- UI 백엔드에서 렌더 트리의 각 노드를 순회하며 각 노드를 화면의 픽셀로 나타내는 작업이다.

### Composite Layers(모던 브라우저에서 진행)

- Compositing은 레이어들을 합성하여 1개의 bitmap으로 만드는 과정이다.
- 각 layer 별로 paint를 한다.

ps. 브라우저는 동기(Synchronous)적으로 HTML, CSS, Javascript을 파싱한다.

따라서 script 태그나 link 태그를 만나면 HTML파싱이 잠시 중단되고 CSS나 JS파싱이 진행된다.

그러므로 태그 위치에 따라 렌더 블로킹이 발생하여 DOM 생성이 지연될 수 있다.

만약 JS를 비동기적으로 불러오고싶을 때 defer나 async 어트리뷰트를 사용하면 비동기적으로 불러올 수 있다.
