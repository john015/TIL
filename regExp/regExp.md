
# 플래그

| Flag | Meaning          |
| ---- | ---------------- |
| i    | 대소문자를 구별하지 않고 검색 |
| g    | 문자열 내의 모든 패턴을 검색 |
| m    | 문자열의 행이 바뀌더라도 검색 |

# 특수 문자

## ^

특정 단어로 시작하는지 검사

```javascript
// 'http'로 시작하는지 검사
const regexp = /^http/
console.log(regexp.test('http://test.com')) // true
console.log(regexp.test('010-1234-5678')) // false
```

## $

특정 단어로 끝나는지 검사

```javascript
// 'html'로 시작하는지 검사
const regexp = /html$/
console.log(regexp.test('index.html')) // true
console.log(regexp.test(test.mp4)) // false
```

## *

앞의 표현식이 0회 이상 연속으로 반복되는 부분과 대응

```javascript
const regexp = /hi*/
console.log(regexp.test('h')) // true
console.log(regexp.test('hiiiii')) // true
console.log(regexp.test('good bye')) // false
```

## +

앞의 표현식이 1회 이상 연속으로 반복되는 부분과 대응

```javascript
const regexp = /hi+/
console.log(regexp.test('h')) // false
console.log(regexp.test('hiiiii')) // true
console.log(regexp.test('good bye')) // false
```

## ?

앞의 표현식이 0 또는 1회 등장하는 부분과 대응

```javascript
const regexp = /hi?/
console.log(regexp.test('h')) // true
console.log(regexp.test('hi')) // true
console.log(regexp.test('good bye')) // false
```

## .

개행 문자를 제외한 모든 단일 문자와 대응

```javascript
const regexp = /.oy/
console.log(regexp.test('boy')) // true
console.log(regexp.test('qo')) // false
console.log(regexp.test('oysho')) // false
```

## x(?=y)

오직 'y'가 뒤따라오는 'x'에만 대응

```javascript
const regexp = /good(?=bye)/
console.log(regexp.test('goodbye')) // true
console.log(regexp.test('good')) // false
console.log(regexp.test('bye')) // false
```

## x(?!y)

오직 'y'가 뒤따라오지 않는 'x'에만 대응

```javascript
const regexp = /good(?!bye)/
console.log(regexp.test('goodbye')) // false
console.log(regexp.test('good')) // true
console.log(regexp.test('bye')) // false
```

# Reference

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D

- https://regexone.com/

- https://poiemaweb.com/js-regexp
