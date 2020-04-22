
## this

- this는 함수 선언 시점에 정해지는게 아니라 호출 시점에 정해짐.
- 일반적으로 함수실행 시점에서 객체의 method이면 부모객체를 가리킴 아니면 전역객체를 가리킴.
- 생성자 함수로 호출시 this는 새로 생성될 인스턴스 객체를 가리킴.
- 전역에서 this에 접근할경우 전역 객체를 가리킴.
- strict mode에서는 암묵적으로 this가 window 또는 global로 할당될경우 undefined가 할당됨.
- arrow function에서 this를 호출할 경우 this는 상위 객체를 가리킴.

## 참조형 타입 vs 원시형 타입

- 원시형 타입은 숫자(Number), 불리언(Boolean), null, undefined, 문자열(String), Symbol이 있고,

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

- 이벤트 위임(Event Delegation)이란 다수의 자식 엘리먼트에 각각 이벤트 핸들러를 바인딩하는 대신 부모 요소에 이벤트 핸들러를 바인딩하는 방법이다.
- 부모 Element에 이벤트 리스너를 바인딩 한 후 이벤트 버블링을 통해 전달받은 event 인자를 통해 event가 트리거된 Element를 확인한다.

## AMD와 CommonJS란?

- 둘다 모두 ES2015 module system이 등장하기 전까지 JavaScript에 기본적으로 존재하지 않는 module system을 구현하는 방법이다.
- CommonJS는 동기식으로 모듈을 로드하지만 AMD(Asynchronous Module Definition 비동기식 모듈 정의)는 비동기식으로 모듈을 로드한다.

## null vs undefined vs undeclared

### null

- null은 프로그래머가 의도적으로 변수에 값이 없음을 표현하고 싶을 때 할당하는 값이다.
- 또한 객체 참조 링크를 끊기 위해서도 사용할 수 있다, 해당 객체 변수를 null로 변경하면 가비지 컬렉션이 실행되며 해당 객체값을 메모리에서 제거한다.

### undefined

- 선언만 되어지고 특정 값이 할당되지 않는 경우 javascript 엔진에 의해 자동으로 할당되는 값이다.
- 특별히 할당된 값이 없는 경우 다른 언어들처럼 null이 아니고 undefiend가 할당된다.
- 또한 객체가 소유하지 않은 프로퍼티에 접근하게 될 경우에도 undefined가 반환된다.

### undeclared

- undeclared 변수란 선언하지 않은 식별자에 값을 할당한 변수이다.
- 예를 들어 undeclaredVar = ‘foo’ 와 같이 var, let, const keyword를 사용하지 않고 선언된 변수이다.
- undeclared 변수는 글로벌 변수로 생성 된다.

### null vs undefiend

- null은 프로그래머가 할당하는 것이며 변수에 값이 없음을 표현하고 싶을 때 사용한다.
- 반면 undefined는 javascript 엔진에 의해 자동으로 할당된다.

## 클로저(Closure)란?

- 클로저란 내부함수가 외부함수의 context에 접근하는것을 말한다.
- 내부함수가 외부함수의 지역변수에 접근할 수 있고, 외부함수는 내부함수의 지역변수에 접근할 수 없으며, 외부함수의 지역변수는 외부함수의 호출이 끝나도 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성이있다.
- 클로저는 반환된 내부함수가 자신이 선언됐을 때의 환경(Lexical environment)인 스코프를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 자신이 선언됐을 때의 환경(스코프)에 접근할 수 있는 함수이다.

```javascript
function generateCounter() {
  let count = 0
  return () => ++count
}

const counter = generateCounter()
counter() // 1
counter() // 2
```

## Host Object vs Native Object

- 호스트 객체(Host object)는 브라우저 환경에서 제공하는 window, XmlHttpRequest, HTMLElement 등의 DOM 노드 객체와 같이 호스트 환경에 정의된 객체를 말한다.
- 브라우저에서 동작하는 환경과 브라우저 외부에서 동작하는 환경의 자바스크립트(Node.js)는 다른 호스트 객체를 사용할 수 있다. ex) window, document, location, history, XMLHttpRequest, querySelectorAll, ...
- 네이티브 객체(Native Object)는 ECMAScript 명세서에 정의된 object로 Javascript의 모든 엔진에 구현된 표준객체이다.
- ex) Date, Math, parseInt, eval, ...

## 기능 검출(feature detection) vs 기능 추론(feature inference)

- 기능 검출은 자바스크립트를 호출하여 기능 X가 브라우저에 존재하는지 확인하는것이다.

```javascript
  if('localStorage' in window)
```

- 기능 추론도 기능 검출처럼 브라우저가 특정 기능을 지원하는지 체크하는 것이다. 하지만 'A기능을 지원하면 B기능도 지원할 것이다.'라는 추론이 바탕이 된다(비권장)

```javascript
if ('localStorage' in window) {
  sessionStorage.add('foo', 'bar') // localstorage가 있으면 sessionStorage도 있을것으로 기능 추론
}
```

## AJAX(Asynchronous JavaScript And XML)란?

- AJAX란 서버와 통신하기 위해 XMLHttpRequest 객체를 사용하는 것이다.
- JSON, XML, HTML 그리고 일반 텍스트 형식 등을 포함한 다양한 포맷을 서버와 주고 받을 수 있다.
- AJAX는 페이지 전체를 새로고침 하지 않고서도 수행 되는 비동기식 통신이다.
- 이러한 비동기성을 통해 사용자의 Event가 있으면 전체 페이지가 아닌 일부분만을 업데이트할 수 있게 해준다.

### 장점

- 웹페이지 전체를 다시 로딩하지 않아도 된다.
- 서버의 응답을 기다리지 않는 비동기 요청이 가능하다.
- 일부 데이터만 수신하기때문에 수신하는 데이터의 양을 줄일 수 있다.

### 단점

- 지원하는 Charset이 한정되어 있다.
- http요청을 남발하면 서버의 부하가 늘어날 수 있다.
- 동일 출처 정책(CORS issue)로 인해 다른 도메인과 통신이 불가능하다.

## JSONP란?

- JSONP는 AJAX와는 다르게 데이터를 요청하는 것이 아닌 \<script\>의 src로 호출하는 방식이다.
- AJAX은 Same Origin Policy에 의해 동일한 도메인에서만 호출이 가능하지만, JSONP는 \<script\>태그의 경우 동일 출처 원칙을 따르지 않아도 되기 때문에 이 원리를 바탕으로 통신이 가능하다.
- 주의 할 점은 JSONP 방식의 경우 GET 메서드만 호출 가능하다. 또한 현재(2019년) JSONP는 여러 보안상 이슈로 인하여 W3C에서는 2009년 채택된 CORS 방식의 HTTP 통신을 권장하고 있으며 JSONP방식은 거의 사용하지않는다.

```html
<!-- 서버에서 params로 받은 콜백함수명으로 반환할 데이터를 감싸서 반환해주면 해당 콜백함수의 인자로 데이터가 들어간다. -->
<script src="http://example.com/post/1?callback=콜백함수명"></script>
```

## “호이스팅(Hoisting)”이란?

- 호이스팅이란 함수나 변수가 해당 scope의 맨위로 올라가는 현상이다.
- 변수 호이스팅의 경우, var 키워드로 변수를 선언했을경우 변수 호이스팅이 일어나며 해당 변수의 선언이 scope의 맨위로 올라간다.
- let, const 키워드로 변수를 선언했을경우 변수 호이스팅이 일어나지않는다.
- 함수 호이스팅의 경우 "함수 선언식"으로 호출했을경우 일어나며 선언 및 할당되기 이전에 호출해도 호이스팅으로 인해 에러가 일어나지않는다.

## 이벤트 버블링(Event Bubbling)이란?

- 하위 엘리먼트에서 이벤트가 일어났을때 하위에서 상위 엘리먼트로 이벤트가 전달되는 방식이다.

## load event vs DOMContentLoaded event

### DOMContentLoaded event

- HTML 이 모두 로드되고, DOM 트리가 완성되었지만, 외부 리소스(img, etc...)가 아직 로드가 되지 않았을 때, DOM 노드를 제어할 수 있다.

### document load event

- 브라우저에 모든 리소스(img, style, script, etc...) 가 로드 되었을 때
- 모든 리소스가 로드된 시점이기에, 로드된 image 사이즈와 같은 것들을 얻을 수 있다.

## ==(동등 연산자) vs ===(일치 연산자)

- 동등 연산자은 비교하는 두 변수의 type이 다르면 형변환을 한뒤 비교한다.
- 일치 연산자는 비교하는 두 변수의 type이 달라도 무시하고 비교한다.

## Strict Mode란?

- Strict Mode는 ECMAScript 버전 5에서 새로 추가되었으며 "use strict;" 을 입력하면 해당 스코프의 다음 구문들부터 적용된다.
- 이전 버전의 JavaScript 인터프리터들은 use strict구문을 무시한다.
- Strict Mode에서는 암묵적 전역 변수 선언, 변수 함수 매개변수의 삭제, 매개변수 이름의 중복, with 문을 사용 하면 에러가 발생한다.
- 또한 일반 함수안에서 this를 호출하면 global객체가 return되는 대신, undefined가 return 된다.
- Strict Mode는 IE10이상부터 지원한다.

## SPA프로젝트에서 SEO(Search Engine Optimization)를 하는법

- SPA프로젝트의 경우 싱글 페이지이기 때문에 SPA프로젝트 크롤링이 가능한 구글을 제외하고 네이버, 다음, 네이트등의 포털사이트에서 검색결과가 나타나지않는다.
- SEO를 하기위해선 react기준으로 Next.js나 react-server를 사용하여 ssr을 하거나 prerender(빌드 시점에서 렌더링해서 정적 파일(.html)을 생성해 둔뒤 http 요청이 올때 미리 생성해둔 정적 파일을 전송)을 할 수있다.

## Promise의 장단점

### 장점

- 콜백 헬을 벗어날 수 있다.
- 메소드 체이닝을 통한 연속적인 코드 작성이 가능하다.
- Promise.all을 사용해서 동시에 여러개의 비동기 코드를 처리할 수 있다.

### 단점

- ES2015를 지원하지 않는 이전 브라우저(ie)에서 사용하기 위해서는 polyfill을 로드해야한다.

## immutable value vs mutable value

- 원시(primitive) 타입 값들은 변경 불가능한 값(immutable value)이며 원시 타입 이외의 모든 값들은 객체(Object) 타입이다. 객체 타입은 변경 가능한 값(mutable value)이다.
- 원시 타입 값들은 메모리에 저장되면 프로그래머가 의도적으로 값을 삭제하거나 재할당 하지않는이상 않는이상 메모리에 저장된 값이 변경되지않는다.

```javascript
const statement = 'I am an immutable value' // string은 immutable value
const slicedStr = statement.slice(8, 17)

console.log(otherStr) // 'immutable'
console.log(statement) // 'I am an immutable value' 원본값은 변경되지 않음
```

- 하지만 객체 타입값들은 메모리에 저장된 값이 변경될수있다.

```javascript
const arr = []
console.log(arr) // []

const arr2 = arr.push(2) // Array.prototype.push 메소드는 실행 후 arr의 length를 반환
console.log(arr) // [1] 원본 arr이 변경됌
```

## 함수 선언식 vs 함수 표현식

- 함수 선언식은 함수 호이스팅이 되지만 함수 표현식은 변수 호이스팅이된다.
- 함수 선언식은 브라우저가 자바스크립트를 해석할 때 스코프의 맨 위로 끌어 올려져 해석된다.
- 함수 표현식은 var 키워드를 사용하여 선언하면 선언만 스코프의 맨 위로 끌어올려지고 할당은 나중에되고, let이나 const 키워드로 선언하면 호이스팅이 일어나지않는다.

```javascript
fn1() // throw Error
fn2() // 2

// 함수 표현식
const fn1 = function() {
  return 1
}

// 함수 선언식
function fn2() {
  return 2
}
```

## var vs let vs const

- var로 선언된 변수는 함수 레벨 스코프를 가지고 let, const로 선언된 변수는 블록 레벨 스코프를 가진다.
- 또한 var는 변수 호이스팅이 일어나 변수의 선언이 스코프의 맨위로 올라가게된다.
- var 변수가 선언되기 전에 읽어도 에러가 발생하지 않지만, let과 const로 선언한 변수를 읽으면 에러가 발생한다.
- var를 사용하여 선언한 변수는 다시 선언해도 에러가 발생하지 않지만 ‘let’과 ‘const’는 에러가 발생합니다.
- var와 let로 선언된 변수는 값을 재할당할 수 있지만 const로 선언된 변수는 재할당 될수없다.

## Set, Map이란?

- 둘다 ES6에 추가됐으며, set은 array와 비슷하고 map은 object와 비슷하다.

### Map vs Object

- Object의 키에는 String과 Symbol을 사용할 수 있지만, Map은 함수, 객체, 원시 자료형 등 어떤 값도 사용할 수 있습니다.
- Map의 키는 삽입순으로 정렬되지만 Object의 키는 그렇지 않습니다. 따라서 Map을 순회하면 키를 삽입한 순서대로 반환합니다
- Map의 크기는 size 속성으로 쉽게 얻을 수 있지만 Object의 속성 수는 직접 판별해야 합니다.
- Map은 바로 순회할 수 있지만, Object를 순회하려면 어떤 방법이든 키의 배열을 얻고, 그 배열을 순회해야 합니다.
- Object는 프로토타입을 가지므로, 주의하지 않으면 키가 충돌할 수 있습니다.
- 잦은 키의 추가와 제거가 필요한 시나리오에서는 Map이 더 빠릅니다.

### Set vs Array

- Array는 중복된 값을 가질 수 있지만, Set은 중복된 값을 가질 수 없습니다.

## for of vs for in

- for in은 해당 컬렉션의 key값을 얻을 수 있고, for of는 value값을 얻을 수 있다.
- for in은 객체의 열거 가능한(Enumerable)프로퍼티의 값이 true인 프로퍼티만 순회한다.
- object.prototype.propertyIsEnumerable(propertyName)을 사용해서 해당 프로퍼티가 열거 가능한지 확인할 수 있다.
- for of은 컬렉션에서 [Symbol.iterator]값의 이터레이터를 끝까지 순회한다.

## Array.sort

- Array의 내장 prototype 메소드인 `sort`는 실행되는 엔진에 따라 다르지만, `v8` 엔진에서는 `Timsort`를 사용하고 있기 때문에 시간 복잡도는 `O(nlog(n))` 공간 복잡도는 `O(n)` 입니다.
- `sort`메소드는 인자로 아무것도 안 넘겨줄 경우 오름차순으로 정렬하며, 정렬 순서를 정의하고 싶으면 해당 메소드의 첫 번째 인자로 `compareFunction`를 넘겨주면 됩니다.
- `compareFunction(a, b)`의 인자로는 비교할 배열의 원소 값 2개가 제공됩니다. 
- 해당 함수의 리턴 값이 음수면 `a`를 `b`보다 낮은 인덱스로 정렬하고
- `0` 이면 두 원소의 순서를 변경하지 않고 유지합니다.
- 양수면 `b`를 `a`보다 낮은 인덱스로 정렬합니다. 

## Element.getBoundingClientRect란?

- 요소의 크기와 viewport에서의 상대적인 위치를 객체에 담아서 반환하는 메소드.
- browser support: ie9+

## requestAnimationFrame

- requestAnimationFrame이란 모니터의 주사율에 맞게 에니메이션을 표현할때 사용한다 requestAnimationFrame의 콜백함수는 초당 최대 모니터의 주사율만큼 호출된다.
- 또한 대부분의 최신 브라우저에서 브라우저를 백그라운드로 돌리게되면 requestAnimationFrame은 멈추게된다.

```javascript
let count = 0
const el = document.querySelector('.counter')
function counter() {
  if (count >= 1000) return
  count++
  el.textContent = count
  requestAnimationFrame(counter)
}
requestAnimationFrame(counter)
```
