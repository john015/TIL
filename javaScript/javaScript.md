# Basices

## this

일반적으로 함수실행 시점에서 객체의 method이면 부모객체를 가리킴 아니면 전역객체를 가리킴
생성자 함수에서 this는 새로 생성될 객체를 가리킴
전역에서 this에 접근할경우 전역객체를 가리킴
strict mode에서는 암묵적으로 this가 window 또는 global로 할당될경우 undefined가 된다

## substr() , slice() 차이

substr()은 시작부터 추출 길이
slice()은 시작 부터 끝 인덱스
substring()은 slice()랑 동일하지만 음수 아규먼트가 안됨

```javascript
const target = 'hello world'
const substring = target.substring(2, 5) // 2 부터 5 전까지 "llo"
const slice = target.slice(2, 5) // 2 부터 5 전까지 "llo"
const substr = target.substr(2, 5) // 2 부터 5 글자 "llo w"
```

## function 유효범위

javascript function 은 렉시컬 스코프를 가지고 있어 소스코드가 작성된 그 문맥에서 결정된다.

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
b() //global
```

## apply vs call vs bind

**apply**

1번째 아규먼트로 this에 바인딩할 값을 받고 2번째 아규먼트로 배열을 받아서 함수의 아규먼트로 뿌려줌

**call**

1번째 아규먼트로 this에 바인딩할 값을 받고 2번째 아규먼트부터 함수의 1번째 아규먼트가 됨

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

# Tip

## javascript typecheck 할때

```javascript
toString.call(check 하고싶은거)
```

call대신 apply해도 동일

# Code

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
  if (!obj) {
    obj = this
  }
  return (...closureFnArgs) => {
    this.apply(obj, args.concat(closureFnArgs))
  }
}
```
