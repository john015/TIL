# react 16.3 이후 라이프 싸이클

## componentDidMount

```javascript
componentDidMount() {
  // 외부 라이브러리 연동: D3, masonry, etc
  // 컴포넌트에서 필요한 데이터 요청: Ajax, GraphQL, etc
  // DOM 에 관련된 작업: 스크롤 설정, 크기 읽어오기 등
}
```

- 컴포넌트가 mount됐을 때 호출된다.

## getDerivedStateFromProps

```javascript
static getDerivedStateFromProps(nextProps, prevState) {
  // 설정하고 싶은 state 값을 리턴하는 형태로 사용
  /*
  if (nextProps.value !== prevState.value) {
    return { value: nextProps.value } // props의 value를 State의 value로 동기화
  }
  return null; // null 을 리턴하면 따로 업데이트 할 것은 없다라는 의미
  */
}
```

- 이 메소드는 컴포넌트가 mount되기전에 또는 state나 props가 변경되어 리렌더링 되기전에 호출된다.

- props로 받아온 값을 state로 동기화 하는 작업을 해줘야 하는 경우에 사용.

## shouldComponentUpdate

```javascript
shouldComponentUpdate(nextProps, nextState) {
  // return false 하면 업데이트를 안함
  return true
}
```

- state나 props가 변경됐을때 호출된다.
- 아직 props나 state가 변경되지않았다.
- 기본적으로 true를 반환 false 반환시 리렌더링 x

## getSnapshotBeforeUpdate

```javascript
getSnapshotBeforeUpdate(prevProps, prevState) {
  return window.scrollY // componentDidUpdate 에서 3 번째 파라미터로 들어옴
}
```

- state나 props가 변경되어 DOM 변화가 일어나기 직전에 호출된다.
- 리턴 값은 componentDidUpdate 에서 3 번째 파라미터로 받아올수 있음.
- componentDidUpdate를 사용하지않고 getSnapshotBeforeUpdate만 사용하면 console에 warning이 뜸.
- 주로 DOM을 업데이트하기 직전의 값들을 참고할 때 사용한다.(ex 스크롤바 위치 유지)

## componentDidUpdate

```javascript
componentDidUpdate(prevProps, prevState, snapshot) {
  console.log(`prev scroll y: ${snapshot}`)
}
```

- state나 props가 변경되어 DOM 변화가 발생한 뒤 발생.

## componentWillUnmount

```javascript
componentWillUnmount() {
  // 이벤트, setTimeout, 외부 라이브러리 인스턴스 제거
}
```

- 컴포넌트가 언마운트 되기전에 호출.

## componentDidCatch(error, info)

- 에러 발생시 호출
