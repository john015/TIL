# Basices

## this

- 일반적으로 함수실행 시점에서 객체의 method이면 부모객체를 가리킴 아니면 전역객체를 가리킴.
- 생성자 함수로 호출시 this는 새로 생성될 객체를 가리킴.
- 전역에서 this에 접근할경우 전역객체를 가리킴.
- strict mode에서는 암묵적으로 this가 window 또는 global로 할당될경우 undefined가 된다.
- arrow function에서 this를 호출할 경우 this는 상위 객체를

## 참조형 타입 vs 원시형 타입

- 원시형 타입은 숫자(Number), 불리언(Boolean), null, undefined, 문자열(String)이 있고,

- 참조형 타입은 객체(Object), 배열(Array), 함수(function), 정규 표현식(regExp)등이 있다.

- 원시형 타입은 pass by value이기 때문에 값이 변경 되거나 복사되면 새로운 메모리에 할당 된다.

- 참조형 타입은 pass by reference이기 때문에 값이 변경 되거나 복사되어도 새로운 메모리에 할당 되지않고 기존 메모리를 참조 하게 된다.

- 기존 메모리를 참조하기때문에 만약 복사한 값의 프로퍼티를 변경했을시 복사된 값도 같이 변경된다.

- 참조형 타입을 원시형 타입처럼 pass by value로 사용할려면 전개연산자나 Object.assign으로 얕은 복사가 아닌 깊은 복사를 해야한다.

```javascript
let str = 'str'
let copiedStr = string

let obj = { foo: '1', bar: '2' }
let copiedObj = obj

console.log(str, copiedStr) // 'str str'
copiedStr = 'string'
console.log(str, copiedStr) // 'str string'

console.log(obj, copiedObj) // '{ foo: '1', bar: '2' } { foo: '1', bar: '2' }'
copiedObj.foo = 3
console.log(obj, copiedObj) // '{ foo: '3', bar: '2' } { foo: '3', bar: '2' }'

const deepCopiedObj = { ...obj } // 전개 연산자를 사용하여 깊은 복사

console.log(obj, deepCopiedObj) // '{ foo: '3', bar: '2' } { foo: '3', bar: '2' }'
deepCopiedObj.foo = 30
console.log(obj, deepCopiedObj) // '{ foo: '3', bar: '2' } { foo: '30', bar: '2' }'
```

## Lexical scope란?

javascript function는 렉시컬 스코프를 가지고 있어 호출된 시점이 아니라 함수가 작성된 상황에서 스코프가 결정된다.

```javascript
const x = 'global'

function a() {
  console.log(x)
}

function b() {
  const x = 'local'
  a()
}
a() //global
b() //local이 아니라 global
```

## substring vs substr vs slice

**substring**

첫번째 파라미터: 시작 index 두 번째 파라미터: 마지막 index

**substr**

첫번째 파라미터: 시작 index 두 번째 파라미터: 길이

**slice**

substring와 동일하지만 파라미터에 음수를 입력할 수 없음

```javascript
const target = 'hello world'
const substring = target.substring(2, 5) // 2번째 인덱스 부터 5 인덱스 전까지 return: "llo"
const slice = target.slice(2, -6) // 2번째 인덱스 부터 뒤에서 6번째 인덱스 전까지 return: "llo"
const substr = target.substr(2, 5) // 2번째 인덱스 부터 5 글자 return: "llo w"
```

## apply vs call vs bind

**apply**

1번째 파라미터로 this에 바인딩할 값을 받고 2번째 파라미터로 배열을 받아서 함수의 파라미터로 뿌려줌

**call**

1번째 파라미터로 this에 바인딩할 값을 받고 2번째 파라미터부터 함수의 1번째 파라미터가 됨

**bind**

call과 똑같지만 함수 실행이 안됨

```javascript
var val1 = 30
var val2 = 50
const obj = {
  val1: 40,
  val2: 90,
  sum(a, b) {
    return this.val1 + this.val2 + a + b
  }
}
console.log(obj.sum(0, 100)) //230
console.log(obj.sum.call(window, 0, 100)) //180
console.log(obj.sum.apply(window, [0, 100])) //180
```

## throttle vs debounce

throttle: 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 것

debounce: 연속되어 호출되는 함수 중 호출된 마지막 함수만 호출하도록 하는 것

throttle은 맨처음 함수가 실행된후 일정 시간전 까진 다시 호출되지 않지만 debounce는 일정 시간동안 호출되지 않아야지 호출된 마지막 함수가 실행된다

throttle은 스크롤 이벤트 처리시 주로 사용하고 debounce는 ajax 검색에 주로 사용한다

## 이벤트 위임(Event Delegation)이란?

- 이벤트 위임(Event Delegation)이란 다수의 자식 엘리먼트에 각각 이벤트 핸들러를 바인딩하는 대신 부모 요소에 이벤트 핸들러를 바인딩하는 방법입니다.
- 부모 Element에 이벤트 리스너를 바인딩 한 후 이벤트 버블링을 통해 전달받은 event 인자를 통해 event가 트리거된 Element를 확인합니다.

## AMD와 CommonJS란?

- 둘다 모두 ES2015 module system이 등장하기 전까지 JavaScript에 기본적으로 존재하지 않는 module system을 구현하는 방법이다.
- CommonJS는 동기식으로 모듈을 로드하지만 AMD(Asynchronous Module Definition 비동기식 모듈 정의)는 비동기식으로 모듈을 로드한다.

# Snippets

## Infinite scroll

```javascript
_.throttle(() => {
  // 사용자의 화면에 보여지는 높이
  const { innerHeight } = window
  // body의 화면에 보이지 않는 부분까지 포함한 높이
  const { scrollHeight } = document.body
  // 스크롤된 높이 ie의 경우는 document.body.scrollTop으로 구해야함
  const scrollTop =
    (document.documentElement && document.documentElement.scrollTop) ||
    document.body.scrollTop

  // body 전체높이 - 화면에 보여지는 높이 - 스크롤된 높이가 80보다 작으면 데이터 추가
  if (scrollHeight - innerHeight - scrollTop < 80) {
    // data fetch 로직
  }
}, 100)
```

## customBind

```javascript
Function.prototype.customBind = function(obj, ...args) {
  if (obj == null) {
    obj = this
  }
  return (...closureFnArgs) => {
    this.apply(obj, args.concat(closureFnArgs))
  }
}
```

## 숫자 천단위마다 콤마 찍기

```javascript
const num = 10203040
const num2 = 10203040.12345

console.log(num.toLocaleString()) // 10,203,040
console.log(num2.toLocaleString()) // 기본으로 소수점 3자리에서 끊김 10,203,040.123
console.log(num2.toLocaleString(undefined, { maximumFractionDigits: 5 })) // 10,203,040.12345
```
