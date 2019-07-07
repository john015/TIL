# redux-saga

`redux-saga`는 리액트/리덕스 애플리케이션의 사이드 이펙트, 예를 들면 데이터 fetching이나 브라우저 캐시에 접근하는 순수하지 않은 비동기 동작들을 쉽게 처리해주는 라이브러리이다.

saga는 애플리케이션에서 사이드 이펙트만을 담당하는 별도의 쓰레드와 같다.

## redux store와 연결

```javascript
import { createStore, applyMiddleware } from 'redux'
import createSagaMiddleware from 'redux-saga'

import reducer from './reducers'
import mySaga from './sagas'

function configureStore() {
  // saga 미들웨어를 생성합니다.
  const sagaMiddleware = createSagaMiddleware()
  // 스토어에 mount 합니다.
  const store = createStore(reducer, applyMiddleware(sagaMiddleware))

  // 그리고 saga를 실행합니다.
  sagaMiddleware.run(mySaga)

  return store
}
```

## Effects

### take

액션이 디스패치 되기를 기다린다.

takeEvery의 경우 여러번 dispatch되길 기다리며 take의 경우는 1번 트리거되면 그이후 dispatch는 무시한다.

takeLatest의 경우 여러개의 action들이 동시에 트리거될 경우 마지막 action만 처리한다.

```javascript
    yield take(SIGN_UP_SUCCESS)
    console.log('ok')

    yield takeEvery(SIGN_UP_SUCCESS, () => console.log('ok'))
```

### put

redux 스토어에 액션을 디스패치한다.

```javascript
    yield put(SIGN_UP_SUCCESS) // SIGN_UP_SUCCESS action을 dispatch
```

### select

셀렉터를 사용하여 기존 애플리케이션 상태의 일부를 얻어온다.

```javascript
const getCart = state => state.cart

yield select(getCart) // cart를 get
```

### call

다른 saga들이나 promise등을 동기적으로 호출.

```javascript
const loginAPI = () => axios.get('https://test.com/users/john')
const result = yield call(loginAPI) // 서버에서 응답이 오기전 success가 콘솔에 표시되지 않음.
console.log('success')
```

### fork

다른 saga들이나 promise등을 비동기적으로 호출.

```javascript
const loginAPI = () => axios.get('https://test.com/users/john')
const result = yield fork(loginAPI) // 서버에서 응답이 오기전 success가 콘솔에 표시됨.
console.log('success')
```

### cancel

fork됐던 서브 프로세스를 취소한다.

```javascript
  const initialAction = yield take (['LOGIN', 'LOGOUT'])
        if (initialAction.type === 'LOGIN') {
            const { username, password } = initialAction.payload
            const authTask = yield fork(
                authorizeWithRemoteServer,
                { username: username, password: password }
            )
            const action = yield take(['LOGOUT', 'LOGIN_FAIL'])
            if (action.type === 'LOGOUT') {
                yield cancel(authTask)
                yield call(unauthorizeWithRemoteServer)
            }
        } else {
            yield call(unauthorizeWithRemoteServer)
        }
```

### cancelled

해당 제너레이터 함수가 취소되었는지 여부를 반환한다. 일반적으로 finally 블록에서 이 Effect를 사용하여 취소 특정 코드를 실행한다.

```javascript
function* saga() {
  try {
    // ...
  } finally {
    if (yield cancelled()) {
      console.log('cencelled')
    }
  }
}
```

### race

여러 task들중 가장 먼저 resolve(혹은 reject)된 task를 제외하고 나머지 task는 취소시킴.

```javascript
  const {posts, timeout} = yield race({
    posts: call(fetchApi, '/posts'),
    timeout: call(delay, 1000) // limit 1초
  })
```

### delay

다음 구문으로 이동하기 전에 주어진 ms동안 대기하며, setTimeout과 동일하다. promise를 리턴한다.

```javascript
yield delay(1000) // 1초뒤 ok 출력
console.log('ok')
```
