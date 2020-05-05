## 시간 복잡도

시간 복잡도는 수행되는 연산의 수를 나타냅니다.

알고리즘에서 중요하지 않는 값들은 최대한 무시합니다.(상수항 무시, 영향력 없는 항 무시)

### 예시

```javascript
function (n) {
  return n + n
}
// 덧셈 연산 1개 이므로 O(1)
```

```javascript
function (n) {
  for (let i = 1; i <= n; i++) {
    console.log(i)
  }
  for (let j = 1; j <= n; j++) {
    console.log(j)
  }
}
// 대입연산 1개가 n만큼 실행되는 구문이 2개 있으므로 O(2n)이지만 상수항을 무시하므로 O(n)
```

```javascript
function (n) {
  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
      console.log(j)
    }
  }
}
// 대입연산 1개가 n^2만큼 실행되므로 O(n^2)
```

## 공간 복잡도

공간 복잡도는 알고리즘이 메모리를 얼마나 필요로 하는지를 나타냅니다.

### 예시

```javascript
function (n) {
    let result = 1;
    for (let i = 1; i <= n; i++) {
        result = result * i;
    }
    return result;
}
// n 값에 상관없이 n과 i 그리고 result 변수가 메모리에 쌓이므로 O(1)
```

```javascript
function factorial(n) {
  if (n > 1) {
    return n * factorial(n - 1);
  }
  return 1;
}
// n의 값만큼 메모리에 factorial(n), factorial(n - 1), factorial(n -2), ... 값이 메모라에 쌓이므로 O(n)
```

## Big-O 표기법의 종류

O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!) < O(nⁿ)
