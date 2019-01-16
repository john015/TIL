# mobx Basic

## observable

넘겨받은 객체나 값 등을 observe(관찰)하게 만듦

## computed

연산된 값을 사용해야 할 때 사용
값이 바뀔 때 미리 값을 계산해놓고 조회 할 때는 캐싱된 데이터를 사용함

## action

Observable State를 변경할때 사용

## asyncAction

비동기로 Observable State를 변경할때 사용

# mobx-react Basic

## observer

observable state 를 rerendring 할때 사용

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

# typescript props error 해결방법

참고 https://github.com/mobxjs/mobx-react/issues/256

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
    ...
  }
}
```
