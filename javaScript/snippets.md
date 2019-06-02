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
