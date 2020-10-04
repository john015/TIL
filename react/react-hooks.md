# Flow Diagram

![disgram](https://raw.githubusercontent.com/donavon/hook-flow/master/hook-flow.png)

## useState

- 값을 저장 할 때 사용, 값이 변경되면 리 렌더링이 일어남.

## useReducer

- reducer pattern을 사용하는 useState.

## useRef

- 값을 저장 할 때 사용, 값이 변경되면 리 렌더링이 일어나지않음.

## useEffect

- 사이드이펙트들을 핸들링 할 때 사용(class components에서 componentDidMount나 componentDidUpdate에 들어갔던 로직들)
- 브라우저에 React DOM이 페인팅 된 뒤 비동기적으로 useEffect의 콜백함수가 실행됨

## useLayoutEffect

- useEffect와 거의 동일하지만 React DOM이 변경 된 뒤 동기적으로 실행됨(실제 브라우저에 페인팅 하기 전 동기적으로 호출되기 때문에 헤비한 작업을 할 경우 일정 시간 렌더 블로킹이 발생함)
- DOM을 측정하거나 수정해야 할 때 useEffect 대신 사용

## useMemo

- 의존성 배열 안 요소들의 값이 바뀌기 전까진 동일한 reference의 return value를 반환함.

## useCallback

- 의존성 배열 안 요소들의 값이 바뀌기 전까진 동일한 reference의 함수를 반환함

## useContext

- 인자로 받은 context객체의 현재 값을 반환함.
