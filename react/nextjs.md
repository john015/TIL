<details>
<summary>Index</summary>

- [Next.js란?](#nextjs란)
- [getInitialProps](#getinitialprops)
- [Routing](#routing)
- [Dynamic Import](#dynamic-import)
- [Custom Error Page](#custom-error-page)
- [_app과 _document의 차이점](#_app과-_document의-차이점)

</details>

## Next.js란?

- `Next.js`는 react application에서 `Isomorphic Rendering`을 쉽게 해주는 React framwork입니다.
- csr(Client-Side-Rendering)을 하게되면 구글을 제외한 검색봇들이 csr application을 크롤링할 수 없어서 seo 문제가 생기며, 메타 데이터나 오픈 그래프 태그도 JS가 생성하기 때문에 SNS 공유하기에도 문제가 생깁니다.
- ssr(Server-Side-rendering)을 하게되면 서버의 리스폰스에 의존해서 페이지를 이동해야하기 때문에 페이지 이동시 fouc가 발생하며 spa에 비해 퍼포먼스가 떨어집니다.
- Isomorphic Rendering을 하게되면 최초 리퀘스트의 응답은 ssr하고 그이후에는 csr와 동일하게 동작해서 SEO와 UX 모두를 충족할 수 있습니다.

## getInitialProps

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

## _app과 _document의 차이점