# SSR(Server Side Rendering)

ex) php, jsp, asp

## Flow

- 사용자가 웹 페이지에 방문한다(request)
- `request`를 받은 서버는 해당 페이지에 필요한 데이터를 패칭하기위해 REST API 엔드포인트에 다시 `request`를 보낸다.
- 엔드포인트에서 `response`가 오면, 서버는 `html` 파일에 응답받은 데이터를 추가해서 사용자에게 `response`해준다.
- 사용자가 페이지를 이동할 경우 위 동작을 반복한다.

## SSR의 장점

### SEO에 친화적이다

- 서버가 데이터를 다 그려서 응답해주기 때문에 검색 엔진이 정보를 수집하기 편리합니다.

## CSR에 비해 클라이언트에 부담이 덜하다

- 런타임에 JS를 이용해 콘텐츠를 그리는 `CSR`과 달리 `SSR`은 서버가 콘텐츠를 그려서 `response` 해주기 때문에 기기 성능에 별 영향을 받지않고 웹 페이지를 제공할 수 있습니다.

## SSR의 단점

### 페이지 간의 TTFB(Time to First Byte)가 느리다

- 서버가 데이터를 패칭하고 해당 데이터를 기반으로 `html` 파일을 생성해서 사용자에게 `response` 해주기때문에 CSR보다 TTFB가 느립니다.

### 서버 호스팅이 필요하다

- 클라이언트에서 동적으로 콘텐츠를 그리는 `CSR`와 미리 빌드 타임에 정적인 html파일을 생성하는 `Static Rendering`랑 달리 `SSR`은 서버 사이드에서 `html`파일안 내용을 생성하기 때문에 서버 호스팅이 필요합니다.

# Client Side Rendering

ex) react, vue, angular

## Flow

- 사용자가 웹 페이지에 방문한다(request)
- `script`, `meta`, `link`등의 태그를 포함하고 있는 빈 콘텐츠의 `index.html`을 `response`한다.
- 브라우저가 `index.html`에 있는 `javaScript`를 응답 받은 뒤 파싱하고 실행해서 초기 콘텐츠를 렌더링한다.
- 해당 페이지에 필요한 데이터를 패칭하기위해 REST API/gql 엔드포인트에 `request`를 보낸다.
- 엔드포인트에서 `response`가 오면, 해당 데이터를 기반으로 콘텐츠를 브라우저에 렌더링한다.
- 사용자가 페이지를 이동할 경우 서버에게 추가 요청 없이 이미 받은 `javaScript`를 이용해 렌더링합니다.

## CSR의 장점

### 페이지 간의 TTFB(Time to First Byte)가 빠르다

## 서버 호스팅이 필요없다

## CSR의 단점

### 초기 로딩이 느리다

### SEO에 친화적이지 않다

### 사용자의 기기 성능에 영향 받는다

# Universal Rendering

# Static Rendering

<!--
### SPA

- SPA(Single Page Application)은 각 페이지에 접속할 때 마다 페이지를 요청하는게 아니라 최초 한번 페이지 전체를 로딩한뒤 데이터만 변경하여 사용할 수 있는 웹 애플리케이션이다.
- 전통적인 웹 방식(SSR)은 페이지를 변경할 때마다 서버로부터 리소스를 전달받아 해석하고 화면에 렌더링하는 방식이였기때문에 SPA보다 성능이 안좋았다.
- SPA는 트래픽을 감소시키고 사용자에게 더 나은 경험을 제공할 수 있다. SPA일경우 서버는 단지 JSON 파일만 보내주는 역할을 하면됐고, html을 그리는 역할은 클라이언트측의 자바스크립트가 수행하게 되었다.

#### SPA의 문제점

##### 초기 페이지 렌더링 속도가 느리다.

- SPA는 전통적인 SSR과 달리 맨처음 웹사이트에 접속했을 때 모든 페이지소스를 다 로딩하기 때문에 SSR에 비해 초기 렌더링 속도가 느리다.

##### 검색 엔진 최적화 문제(SEO)

- SPA는 JavaScript로 웹페이지를 렌더링하기때문에 구글은 제외한 나머지 포털 사이트들(네이버, 다음, 네이트, etc...)의 크롤러들은 빈 페이지로 인식하게된다.
- 또한 페이스북, 트위터, 카카오톡등의 미리보기도 각 페이지마다 미리보기를 설정할 수 없고 전체 페이지들에게 동일한 미리보기와 설명을 보여줘야한다.

이러한 문제들을 해결하기위해 next.js나 nuxt.js등의 라이브러리들을 활용하여 universal web app을 구현할 수 있다.

### SSR(universal web app)

- Universal Web App은 초기 렌더링은 전통적인 SSR방식을 사용해 서버에서 렌더링하여 보여주고 초기 페이지가 보여지는동안 페이지 전체를 로드하여 다른 페이지에 접근하면 SPA방식과 동일하게 동작하는 웹 애플리케이션이다.
- Universal Web App을 사용하면 초기 렌더링속도문제를 해결할 수 있고, SEO문제도 해결할 수 있다.
- 하지만 서버에 트래픽이 증가하고, 작성할 코드가 많아진다. -->

## Reference

- https://dev.to/kefranabg/demystifying-ssr-csr-universal-and-static-rendering-with-animations-m7d
- https://developers.google.com/web/updates/2019/02/rendering-on-the-web
