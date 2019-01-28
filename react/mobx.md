# mobx Basices

## observable

- 넘겨받은 객체나 값 등을 observe(관찰)하게 만듦

```javascript
class CounterState {
  @observable
  number = 0
}
```

## computed

- 연산된 값을 사용해야 할 때 사용
- 값이 바뀔 때 미리 값을 계산해놓고 조회 할 때는 캐싱된 데이터를 사용함

```javascript
class MarketStore {
  @observable
  selectedItems = []

  @computed
  get totalPrice() {
    // 총합 계산
    return this.selectedItems.reduce((previous, { price }) => {
      return previous + price
    }, 0)
  }
}
```

## action

Observable State를 변경할때 사용

```javascript
class CounterState {
  @observable
  number = 0

  @action
  increase = () => {
    this.number++
  }

  @action
  decrease = () => {
    this.number--
  }
}
```

# mobx-react Basices

## observer

- observable state 를 추적 할때 사용
- 만일 observable state를 사용하는데 observer로 매핑 하지않으면 observable state가 변경될시 rerendering이 안일어남

```javascript
@inject("userStore")
@observer
class MyComponent extends React.Component<IProps, {}> {
  get injected() {
    return this.props as InjectedProps;
  }

  render() {
    const { userStore, router } = this.injected;
    ...
  }
}
```

## inject

mobx state를 props로 주입 할때 사용 함수형태로 파라미터를 전달해주면 특정 값만 주입도 가능

```javascript
// example store을 props에 주입
@inject('example')

//함수형태
// foo, bar를 props에 주입
@inject(stores => ({
  foo: stores.example.foo,
  bar: stores.example.bar
}))
```

# typescript props type error 해결방법

https://github.com/mobxjs/mobx-react#strongly-typing-inject
또는 위 링크 처럼 하는 방법도 있음

```javascript
@inject("userStore")
@withRouter
@observer
class MyComponent extends React.Component<IProps, {}> {
  get injected() {
    return this.props as InjectedProps;
  }

  render() {
    const { name, countryCode } = this.props;
    const { userStore, router } = this.injected;

  }
}
```

참고 https://github.com/mobxjs/mobx-react/issues/256
