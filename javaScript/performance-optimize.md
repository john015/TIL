# 자바스크립트 성능 최적화

## requestIdleCallback

requestIdleCallback는 우리가 미리 콜백함수로 등록해놓은 함수를 브라우저가 할 일이 없을 때 실행해줍니다. 즉, 매 프레임마다 브라우저가 판단해서 남은 시간이 충분하다 싶으면 동록되어 있는 함수를 호출하는 것이다.

비교적 중요도가 떨어지는 작업들을 requestIdleCallback사용해서 등록해놓으면 브라우저가 할 일이 없을 때 실행된다.

### browser support

Edge: 76+, Firefox: 55+, Chrome: 47+, Opera: 34+

IE, Safari 미지원

## DocumentFragment

DOM 트리를 접근하는 건 상당히 속도가 느립니다. 따라서, 자바스크립트의 성능을 최적화하기 위해서는 DOM 객체 접근을 최소화하도록 코드를 작성해야 한다.

만약 DOM에 30개의 <li>태그를 추가해야 한다고 가정하면 30번의 접근이 필요하다.

이런경우에 DocumentFragment를 사용해서 추가하면 1번의 접근으로 추가가 가능하다.

```javascript
const ul = document.querySelector('ul')
const fragment = document.createDocumentFragment()

for(let i = 1; i < 31; i++) {
  const willInsertEl = document.createElement('li')
  willInsertEl.textContent = i
  fragment.appendChild(willInsertEl)
}
ul.appendChild(fragment)
```

DocumentFragment는 마치 하나의 가상 DOM 엘리먼트처럼 동작합니다. 따라서 fragment에 다른 엘리먼트를 추가하거나 제거할 수 있죠. 하지만 마지막에 DOM 트리에 fragment를 추가할 땐 좀 다른 결과가 나옵니다.

일반 DOM 엘리먼트와 동일하다면 ul 밑에 fragment가 들어가고 그 밑에 30개의 <li>태그가 생겼겠지만, DocumentFragment는 자신을 제외한 하위 엘리먼트들만 옮겨줍니다. 즉, ul 바로 밑에 30개의 <li>태그가 생기게 되는 것이죠. 결과는 동일하면서 속도는 개선되는 바람직한 방법이라 할 수 있습니다.


### browser support

IE: 9+, Firefox, Chrome, Opera등 전부 지원


## 지연평가(Lazy evaluation)

- 지연평가는 엄격한 평가(Strict evaluation)과 다르게 모든 값을 평가하지않고 1개의 값씩 순차적으로 평가한다.
- 주로 몇개의 값만 필터링 해야하는 상황에서 성능 최적화를 하기 위해 사용한다.

  ```javascript
  const arr = [1, 2, 5, 7, 8, 10];
  arr
    .map((val) => val ** 2)
    .filter((val) => val % 2)
    .slice(0, 2)
    .value(); // [1, 25] 12번 평가

  // lodash를 활용한 지연 평가

  // case1
  // _의 아규먼트로 지연 평가를 하고싶은 값을 넣어주면 그이후는 알아서 처리해줌
  const lazyArr = _(arr);
  lazyArr
    .map((val) => val ** 2)
    .filter((val) => val % 2)
    .slice(0, 2)
    .value(); // [1, 25] 6번 평가

  // case2
  // _.flow를 쓰면 알아서 지연평가가 되는 상황이면 지연평가 시키고 안되는 상황이면 엄격한 평가로 처리함
  _.flow(
    _.map((val) => val ** 2),
    _.filter((val) => val % 2),
    _.take(2)
  )(arr); // [1, 25] 6번 평가
  ```


