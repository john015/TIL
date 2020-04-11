
# 플래그

| Flag | Meaning                       |
| ---- | ----------------------------- |
| i    | 대소문자를 구별하지 않고 검색 |
| g    | 문자열 내의 모든 패턴을 검색  |
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

## \$

특정 단어로 끝나는지 검사

```javascript
// 'html'로 시작하는지 검사
const regexp = /html$/
console.log(regexp.test('index.html')) // true
console.log(regexp.test(test.mp4)) // false
```

## \*

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

## (x)

'x'에 대응되는것을 capture, capture된값은 exec나 match methods가 return하는 배열에 포함됨

```javascript
const regexp = /^(good).+/
console.log(regexp.exec('goodbye')) // ["goodbye", "good"]
console.log(regexp.exec('goo')) // null
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

## x|y

'x' 또는 'y'에 대응

```javascript
const regexp = /bye|hello/
console.log(regexp.test('bye')) // true
console.log(regexp.test('hello')) // true
console.log(regexp.test('good night')) // false
```

## {n}

앞 표현식이 n번 나타나는 부분에 대응, n은 반드시 양의 정수여야함

```javascript
const regexp = /hello{2}/
console.log(regexp.test('hellohello')) // true
console.log(regexp.test('hello')) // false
```

## {n,m}

앞 표현식이 n번 이상 나타나고 m번 이하 나타나는 부분에 대응, n, m은 반드시 양의 정수여야함

```javascript
const regexp = /hello{1,2}/
console.log(regexp.test('hellohello')) // true
console.log(regexp.test('hello')) // ture
```

## [xyz]

괄호 안의 문자셋과 대응

```javascript
const regexp = /^[a-c]/ // /^[abc]/와 동일
console.log(regexp.test('apple')) // true
console.log(regexp.test('banana')) // ture
console.log(regexp.test('melon')) // false
```

## [^xyz]

괄호 내부에 등장하지 않는 문자와 대응

```javascript
const regexp = /^[^a-c]/ // /^[^abc]/와 동일
console.log(regexp.test('apple')) // false
console.log(regexp.test('banana')) // false
console.log(regexp.test('melon')) // true
```

## [^xyz]

괄호 내부에 등장하지 않는 문자와 대응

```javascript
const regexp = /^[^a-c]/ // /^[^abc]/와 동일
console.log(regexp.test('apple')) // false
console.log(regexp.test('banana')) // false
console.log(regexp.test('melon')) // true
```

## \b

다른 '단어 문자'(\w와 동일)가 앞이나 뒤에 등장하지 않는 위치에 대응

```javascript
const regexp = /moon\b/
console.log(regexp.test('honeymoon')) // true
console.log(regexp.test('moonster')) // false
console.log(regexp.test('moon star')) // true
```

## \d

숫자 문자에 대응. [0-9]와 동일

```javascript
const regexp = /\d/
console.log(regexp.test('1')) // true
console.log(regexp.test('1st')) // true
console.log(regexp.test('first')) // false
```

## \D

숫자 문자가 아닌 문자에 대응. [^0-9]와 동일

```javascript
const regexp = /\d/
console.log(regexp.test('1')) // false
console.log(regexp.test('1st')) // true
console.log(regexp.test('first')) // true
```

## \s

스페이스, 탭, 폼피드, 줄 바꿈 문자등을 포함한 문자에 대응

```javascript
const regexp = /\s/
console.log(regexp.test('firstGoal')) // false
console.log(regexp.test('first goal')) // true
```

## \S

스페이스, 탭, 폼피드, 줄 바꿈 문자등을 제외한 하나의 공백 문자에 대응

```javascript
const regexp = /\S/
console.log(regexp.test(' ')) // false
console.log(regexp.test('first goal')) // true
```

## \w

밑줄 문자를 포함한 영숫자 문자에 대응. [A-Za-z0-9_] 와 동일

```javascript
const regexp = /\w/
console.log(regexp.test('안녕하세요')) // false
console.log(regexp.test('first')) // true
```

## \W

단어 문자가 아닌 문자에 대응. [^a-za-z0-9_] 와 동일합니다.

```javascript
const regexp = /\W/
console.log(regexp.test('안녕하세요')) // true
console.log(regexp.test('first')) // false
```

# Reference

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D

- https://regexone.com/

- https://poiemaweb.com/js-regexp
