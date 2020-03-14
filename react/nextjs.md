<details>
<summary>Index</summary>

- [Next.js란?](#nextjs란)
- [getInitialProps(Next.js 9.3 버전이후 부터는 권장 하지않음)](#getinitialpropsnextjs-93-버전이후-부터는-권장-하지않음)
- [getStaticProps](#getstaticprops)
- [getStaticPaths](#getstaticpaths)
- [getServerSideProps](#getserversideprops)
- [Routing](#routing)
- [Dynamic Import](#dynamic-import)
- [Custom Error Page](#custom-error-page)
- [Custom Document](#custom-document)

</details>

## Next.js란?

- `Next.js`는 react application에서 `Isomorphic Rendering`을 쉽게 해주는 React framwork입니다.
- csr(Client-Side-Rendering)을 하게되면 구글을 제외한 검색봇들이 csr application을 크롤링할 수 없어서 seo 문제가 생기며, 메타 데이터나 오픈 그래프 태그도 JS가 생성하기 때문에 SNS 공유하기에도 문제가 생깁니다.
- ssr(Server-Side-rendering)을 하게되면 서버의 리스폰스에 의존해서 페이지를 이동해야하기 때문에 페이지 이동시 fouc가 발생하며 spa에 비해 퍼포먼스가 떨어집니다.
- Isomorphic Rendering을 하게되면 최초 리퀘스트의 응답은 ssr하고 그이후에는 csr와 동일하게 동작해서 SEO와 UX 모두를 충족할 수 있습니다.

## getInitialProps(Next.js 9.3 버전이후 부터는 권장 하지않음)

`getInitialProps` 함수는 `pages` 디렉토리 안에 있는 컴포넌트에서만 사용할 수 있는 스태틱 메소드입니다.
`Next.js`는 컴포넌트가 `getInitialProps`나 `getServerProps` 함수를 사용하고 있으면 build타임에서 ssr이 적용되게 빌드합니다.

`getInitialProps` 함수의 인자로는 `context`객체가 전달되는데 해당 객체는 `pathname`, `query`, `req(ssr only)`, `res(ssr only)`, `err` 등의 프로퍼티를 갖고 있습니다.

`getInitialProps` 함수의 리턴 값은 해당 컴포넌트의 첫 번째 인자로 전달됩니다.

```javascript
import fetch from 'isomorphic-unfetch'

function Page({ stars }) {
  return <div>Next stars: {stars}</div>
}

Page.getInitialProps = async ctx => {
  const res = await fetch('https://api.github.com/repos/zeit/next.js')
  const json = await res.json()
  return { stars: json.stargazers_count }
}

export default Page
```

## getStaticProps

`getInitialProps` 함수는 빌드 타임에 데이터를 가져오고 싶을 때 사용할 수 있습니다

`getInitialProps` 함수는 빌드 될 때 서버 사이드에서 한번만 호출됩니다.

`getServerSideProps, getInitialProps`와 달리 해당 함수를 사용해도 `Next.js`는 페이지를 ssr하지 않습니다.

```javascript
import fetch from 'node-fetch'

function Blog({ posts }) {
  return (
    <ul>
      {posts.map(post => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}

export async function getStaticProps() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  return {
    props: {
      posts
    }
  }
}

export default Blog
```

## getStaticPaths

`getStaticPaths` 함수는 다이나믹 라우팅을 하면서 `getStaticProps` 를 사용하는 페이지가 빌드 타임에 어떤 `params`에 해당하는 페이지를 프리 렌더링 할지 결정할려고 사용합니다.

`getStaticPaths` 함수를 사용하는 이유는 `Next.js` 입장에서는 해당 함수를 이용해 `paths`를 전달 해주지 않으면 `params`에 어떤 값이 들어올지 모르기 때문에 프리 렌더링을 하기위해 필수로 사용해야 합니다.

`getStaticPaths` 함수는 `paths`와 `fallback` 프로퍼티를 갖고있는 객체를 리턴해야합니다.

`fallback` 프로퍼티가 `true`면 `paths` 에 없는 경로에 방문 했을 때 `fallback` 페이지를 보여주고, 백그라운드로 `getStaticProps`와 같이 `params`에 해당 하는 페이지를 생성해서 사용자에게 보여줍니다.

해당 프로퍼티가 `false` 일 경우 `paths` 에 없는 경로에 방문 했을 때 그냥 404 페이지를 보여줍니다.

```javascript
import fetch from 'node-fetch'

const Post = () => {
  ...
}

export async function getStaticPaths() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  const paths = posts.map(post => ({
    params: { id: post.id },
  }))

  return { paths, fallback: false }
}

export async function getStaticProps({ params }) {
  ...
}

export default Post
```

## getServerSideProps

`getServerSideProps` 함수는 ssr을 할려고 할 때 사용합니다.

`getServerSideProps` 함수는 `getStaticProps` 와 달리 해당 페이지 경로로 리퀘스트가 올 때 마다 호출됩니다.

`getServerSideProps` 함수는 항상 서버 사이드에서만 호출됩니다.

```javascript
function Page({ data }) {
  ...
}

export async function getServerSideProps({ params }) {
  const res = await fetch(`https://.../${params.id}`)
  const data = await res.json()

  return { props: { data } }
}

export default Page
```

## Routing

`pages` 디렉토리 안에 파일을 생성하면 자동으로 파일명에 해당하는 주소로 접속할 수 있습니다.

- `pages/index.js` → `/`
- `pages/blog/first-post.js` → `/blog/first-post`
- `pages/blog/[id].js` → `/blog/[id]`
- `pages/blog/[...all].js` → `/blog/*`

### Dynamic Routing

만약 동적으로 라우팅을 해야할 경우 파일명을 `[id]`와 같이 대괄호로 묶어서 생성하면 다이나믹 라우팅 기능을 이용할 수 있습니다.

해당 `id` 값은 `router` 객체나 `context` 객체의 `query` 파라미터로 조회할 수 있습니다.

`Link` 컴포넌트에서 다이나믹 라우팅을 사용할려면 `href` prop에 파일명을 넣고 `as` prop에 이동할 주소를 넣어야합니다. 굳이 `href`를 넘겨주는 이유는 `Next.js`가 사전에 컴포넌트를 `preload` 하기위해 넘겨줘야 합니다.

```javascript
import Link from 'next/link'

const index = () => (
  <Link href="/blog/[id]" as="/blog/test-post">
    test-post link
  </Link>
)
```

위 예시의 `pages/blog/first-post.js`와 `pages/blog/[id].js`처럼 미리 정의된 주소가 동적 라우팅 주소에도 해당 될 수 있을 경우, 미리 정의된 주소(`first-post.js`)가 우선 순위를 갖습니다.

또한 라우트 파라미터와 쿼리 파라미터가 동일하다면 라우트 파라미터가 우선 순위를 갖습니다.

```javascript
import Router from 'next/router'

// query 파라미터의 프로퍼티로는 2가 아니라 "second-post"가 들어감
// push메소드는 첫 번째 인자로 href를 받고 두 번째 인자로 as 마지막 세 번째 인자로 option를 받습니다
Router.push('/blog/[id]', '/blog/second-post?id=2')
```

### Shallow Routing

동일한 `pathname`에서 리렌더링 하지않고 쿼리 스트링만 바꾸고 싶을 때는 `Router.push`메소드에 `shallow` 옵션을 `true`로 전달하면 `Shallow Routing`을 진행합니다.

```javascript
import Router from 'next/router'

Router.push('/blog/first-post?id=5', null, { shallow: true })
```

`Shallow Routing`을 할 경우 `getInitialProps` 함수는 실행되지 않습니다.

## Dynamic Import

`Dynamic Import` 를 할려면 `next/dynamic` 모듈에서 `default export`된 `dynamic` 함수를 이용하면 됩니다.

```javascript
import dynamic from 'next/dynamic'

// default export된 컴포넌트를 다이나믹 임포트
const DynamicComponent = dynamic(() => import('../components/hello'), {
  loading: <Loader />
})

// Hello라는 이름으로 named default된 컴포넌트를 다이나믹 임포트
const DynamicNamedComponent = dynamic(() =>
  import('../components/hello').then(module => module.Hello)
)

function Home() {
  return (
    <>
      <DynamicComponent />
      <DynamicNamedComponent />
    </>
  )
}

export default Home
```

## Custom Error Page

### Customizing The 404 Page

기본적으로 `Next.js`가 제공해주는 404 에러 페이지를 커스터마이징 할려면 `/pages` 디렉토리에 `404.js` 파일을 생성하면 됩니다.

```javascript
// pages/404.js
export default function Custom404Page() {
  return <h1>페이지를 찾을 수 없습니다.</h1>
}
```

### Customizing The Error Page

404 에러외에도 다양한 에러를 표시해주는 페이지를 커스터마이징 할려면 `/pages` 디렉토리에 `_error.js` 파일을 생성하면 됩니다.

만약 `_error.js`와 `404.js`파일이 둘다 존재하면 `404.js`파일이 우선 순위를 갖습니다.

```javascript
function Error({ statusCode }) {
  return (
    <p>
      {statusCode
        ? `An error ${statusCode} occurred on server`
        : 'An error occurred on client'}
    </p>
  )
}

Error.getInitialProps = ({ res, err }) => {
  const statusCode = res?.statusCode ?? err?.statusCode ?? 404
  return { statusCode }
}

export default Error
```

## Custom Document

일반적인 SPA `React.js`앱과 다르게 `Next.js` 앱에서는 `index.html` 파일이 없기때문에

Custom Document는 `Next.js`가 마운트(Server-Side) 되는 지점을 커스터마이징 할려고 사용합니다.

Custom Document는 주로 애플리케이션의 `<html>`, `<body>`, `<head>` 태그를 마크업하는 용도나 서버 사이드 렌더링 환경에서 `css-in-js` 동작을 구현하기 위해 사용합니다.

Custom Document는 `pages/_document.js`경로에 파일을 생성해서 만들 수 있습니다.

주의할 점으로는 custom Document에서는 `<title>` 태그를 가질 수 없고, `Data Fetching`과 `Lifecycle`을 사용할 수 없습니다.

```javascript
import Document, { Html, Head, Main, NextScript } from 'next/document'

class MyDocument extends Document {
  render() {
    return (
      <Html lang="ko">
        <Head>
          <meta
            name="viewport"
            content="initial-scale=1.0, width=device-width"
            key="viewport"
          />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}

export default MyDocument
```

### Custom App

`Next.js`는 페이지를 초기화할 때 `App` 컴포넌트를 사용합니다. 

그래서 `Document`와 달리 `App` 컴포넌트는 페이지가 이동될 때 마다 사용됩니다.

해당 `App` 컴포넌트를 커스터마이징 할려면 `pages/_app.js` 경로에 Custom App를 생성해서 커스터마이징할 수 있습니다.

Custom App는 주로 모든 페이지들의 공용 레이아웃을 정의하거나, Global CSS를 추가할 때 사용합니다.

만약 Custom App에 `getInitialProps` 함수를 사용하면 [Automatic Static Optimization](https://nextjs.org/docs/advanced-features/automatic-static-optimization) 기능이 비활성화 됩니다.

```javascript
// component: 현재 페이지 컴포넌트
// pageProps: getInitialProps, getServerSideProps등으로 preloaded된 페이지 props
function MyApp({ Component, pageProps }) {
  return (
    <div>
      hello world!
      <Component {...pageProps} />
    </div>
  )
}

export default MyApp
```