## Next.js란?

- `Next.js`는 react application에서 `Isomorphic Rendering`을 쉽게 해주는 React framwork입니다.
- csr(Client-Side-Rendering)을 하게되면 구글을 제외한 검색봇들이 csr application을 크롤링할 수 없어서 seo 문제가 생기며, 메타 데이터나 오픈 그래프 태그도 JS가 생성하기 때문에 SNS 공유하기에도 문제가 생깁니다.
- ssr(Server-Side-rendering)을 하게되면 서버의 리스폰스에 의존해서 페이지를 이동해야하기 때문에 페이지 이동시 fouc가 발생하며 spa에 비해 퍼포먼스가 떨어집니다.
- Isomorphic Rendering을 하게되면 최초 리퀘스트의 응답은 ssr하고 그이후에는 csr와 동일하게 동작해서 SEO와 UX 모두를 충족할 수 있습니다.

## getInitialProps

`getInitialProps` 함수는 `pages` 디렉토리 안에 있는 컴포넌트에서만 사용할 수 있는 스태틱 메소드입니다.

`Next.js`는 컴포넌트가 `getInitialProps`나 `getServerProps` 함수를 사용하고 있으면 build타임에서 ssr이 적용되게 빌드합니다. 

`getInitialProps` 함수의 인자로는 `context`객체가 전달되는데 해당 객체는 `pathname`, `query`, `req(ssr only)`, `res(ssr only)`, `err`등의 프로퍼티를 갖고 있습니다.

`getInitialProps` 함수의 리턴 값은 해당 컴포넌트의 인자로 전달됩니다.


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