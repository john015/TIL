# SSR(Server Side Rendering)

ex) php, jsp, asp

## Flow

> 정적 페이지가 아니라 서버로부터 데이터를 패칭하는 페이지 기준으로 작성되어 있음.

- 사용자가 웹 페이지에 방문한다(request)
- `request`를 받은 서버는 해당 페이지에 필요한 데이터를 패칭 하기위해 REST API 엔드포인트에 다시 `request`를 보낸다.
- 엔드포인트에서 `response`가 오면, 서버는 `html` 파일에 응답받은 데이터 정보를 포함해서 사용자에게 `response` 해준다.
- 사용자가 페이지를 이동할 경우 위 동작을 반복한다.

## SSR의 장점

### SEO에 친화적이다

- 서버가 데이터를 다 그려서 응답해주기 때문에 검색 엔진이 웹 페이지 정보를 잘 수집해갈 수 있습니다.

### CSR에 비해 클라이언트에 부담이 덜하다

- 런타임에 `JavaScript`를 이용해 콘텐츠를 그리는 `CSR`과 달리 `SSR`은 서버가 콘텐츠를 그려서 `response` 해주기 때문에 기기 성능에 별 영향을 받지않고 웹 페이지를 제공할 수 있습니다.

## SSR의 단점

### 페이지 간의 TTFB(Time to First Byte)가 느리다

- 서버가 데이터를 패칭하고 해당 데이터를 기반으로 `html` 파일을 생성해서 사용자에게 `response` 해주기 때문에 CSR보다 TTFB가 느립니다.

### 서버 호스팅이 필요하다

- 클라이언트에서 `javaScript`를 이용해 렌더링하는 `CSR`와 미리 빌드 타임에 정적인 html파일을 생성하는 `Static Rendering`에 비해 `SSR`은 서버 사이드에서 `html`파일 안 내용을 생성하기 때문에 서버 호스팅이 필요합니다.

# Client Side Rendering

ex) react, vue, angular

## Flow

- 사용자가 웹 페이지에 방문한다(request)
- `script`, `meta`, `link`등의 태그를 포함하고 있는 빈 콘텐츠의 `index.html`을 `response`한다.
- 브라우저가 `index.html`에 있는 `javaScript` 번들 파일을 패칭한 뒤 파싱하고 실행해서 콘텐츠를 렌더링한다.
- 해당 페이지에 필요한 데이터를 패칭 하기위해 REST API/gql 엔드포인트에 `request`를 보낸다.
- 엔드포인트에서 `response`가 오면, 해당 데이터를 기반으로 콘텐츠를 브라우저에 렌더링한다.
- 사용자가 페이지를 이동할 경우 서버에 추가족안 `html`파일 요청 없이 이미 받은 `javaScript`를 이용해 렌더링합니다.

## CSR의 장점

### 페이지 간의 이동 속도(반응성)가 빠르다

- 라우팅시 추가적인 서버 요청 없이 클라이언트단에서 `javaScript`로 렌더링하기 때문에 `SSR`에 비해 라우팅 속도(반응성)가 빠릅니다.

## 별도의 웹용 서버가 필요없다

- 클라이언트단에서 라우팅을 처리하기 때문에 s3와 같은 버킷에 빌드된 파일만 올려놓으면 별도의 서버 호스팅 없이 웹 사이트를 사용자에게 제공 가능합니다.

## CSR의 단점

### 초기 로딩이 느리다

- `javaScript`로 웹 페이지를 렌더링하기 때문에 콘텐츠를 정상적으로 표시 해줄려면 추가적으로 `javaScript`를 이용해 콘텐츠를 렌더링하는 작업이 필요합니다.
- 별도의 코드 스플리팅을 하지 않으면 모든 페이지에서 사용되는 라이브러리와 소스를 불러오기 때문에 비 효율적입니다.

### SEO에 친화적이지 않다

- 크롤러가 요청을 보냈을 때 빈 콘텐츠의 `html` 파일을 response해주고 `javaScript`로 웹 페이지를 렌더링하기 때문에 구글을 제외한 나머지 검색 엔진들은 빈 페이지로 인식하게 됩니다.

### 사용자의 기기 성능에 영향 받는다

- 클라이언트에서 `javaScript`로 웹 페이지를 렌더링하기 때문에 저 성능 기기의 경우 성능 이슈가 있을 수 있습니다.

# Universal Rendering

ex) Next.js, Nuxt.js, Angular Universal

## Flow

- 사용자가 웹 페이지에 방문한다(request)
- `request`를 받은 서버는 해당 페이지에 필요한 데이터를 패칭 하기위해 REST API/GraphQL 엔드포인트에 다시 `request`를 보낸다.
- 엔드포인트에서 `response`가 오면, 서버는 `html` 파일에 응답받은 데이터 정보를 포함해서 사용자에게 `response` 해준다.
- 이 상태에서 초기 콘텐츠들은 다 렌더링 되었지만 아직 `javaScript` 번들이 패칭중이기 때문에 인터렉션이 불가능합니다.
- `javaScript` 번들이 다 패칭된 다음 파싱되면 그 이후에는 `CSR`와 동일하게 동작합니다.
- (라우팅에는 서버에 추가적인 `html`파일 요청 없이 `javaScript`를 이용해 렌더링 진행).

## Universal Rendering의 장점

- 초기 로딩시에는 `ssr`처럼 작동하고, 그 이후에는 `csr`처럼 작동해서 `ssr`과 `csr` 장단점을 보안할 수 있다.

## Universal Rendering의 단점

- Universal Rendering을 직접 구현하기보다는 프레임워크를 사용해야하는 경우가 많으므로, 해당 프레임워크에 대한 러닝커브가 있다.

# Static Rendering

ex) Gatsby, Next.js, Hugo, Jekyll

## Flow

- 빌드 타임에 REST API/GraphQL 엔드포인트에 `request`를 보내서 데이터를 받아온 뒤 `html`파일로 프리렌더링 해놓는다.
- 사용자가 웹 페이지에 방문한다(request)
- 미리 만들어 놓은 `html`파일을 제공해준다.

## Reference

- https://dev.to/kefranabg/demystifying-ssr-csr-universal-and-static-rendering-with-animations-m7d
- https://developers.google.com/web/updates/2019/02/rendering-on-the-web
