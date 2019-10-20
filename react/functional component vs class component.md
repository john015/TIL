# 함수형 컴포넌트 vs 클래스 컴포넌트

함수형 컴포넌트는 render 될 때의 값들을 유지하지만 클래스 컴포넌트는 유지 하지 않는다.

클래스 컴포넌트가 다시 렌더링 되면 `this.state`와 `this.props`도 따라서 업데이트된다.

따라서 요청이 진행되고 있는 상황에서 클래스 컴포넌트가 다시 렌더링 된다면 this.props 또한 업데이트 되기때문에 해당 메소드가 “새로운” props에 접근할 수 있다.

하지만 함수형 컴포넌트는 렌더링된 값들을 고정시키기 때문에 요청이 진행되고 있는 상황에서 함수형 컴포넌트가 다시 렌더링 된다면 새로운 props에 접근할 수 없다.

## Reference 

- https://overreacted.io/how-are-function-components-different-from-classes/