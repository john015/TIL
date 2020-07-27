# Snippets

## customBind

```javascript
Function.prototype.customBind = function (obj, ...args) {
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

## 조건에 따른 프로퍼티 삽입문 축약

```javascript
const keyword = document.querySelector('.input').value
const user = { name: 'lee', gender: 'male' }

const query = {
  collection: 'Cats',
  sort: 'asc',

  ...(keyword && { keyword }), // keyword가 있으면 keyword: keyword 없으면 무시
  ...(user.gender === 'male' && user), // user.gender가 male이면 user객체의 프로퍼티를 삽입 없으면 무시
}
```
