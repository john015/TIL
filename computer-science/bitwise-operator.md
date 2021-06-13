# 비트 연산자

## & (AND)

피연산자를 비트로 바꿨을 때 각각 대응하는 비트가 모두 1이면 그 비트값에 1을 반환

```javascript
console.log(3 & 5) // 011 & 101 = 1
console.log(3 & 4) // 011 & 100 = 0
```

## | (OR)

피연산자를 비트로 바꿨을 때 각각 대응하는 비트가 모두 1이거나 한 쪽이 1이면 1을 반환.

```javascript
console.log(3 | 5) // 011 & 101 = 7
console.log(3 | 2) // 11 & 10 = 3
```

## ^ (XOR)

피연산자를 비트로 바꿨을 때 대응하는 비트가 서로 다르면 1을 반환.

```javascript
console.log(3 ^ 5) // 011 ^ 101 = 6
console.log(3 ^ 2) // 11 ^ 10 = 1
```

## ~ (NOT)

피연산자의 반전된 값을 반환.

```javascript
console.log(~-1) // 0
console.log(~3) // -4
console.log(~-5) // 4
```

## \<\< (부호 유지 왼쪽 시프트)

피연산자를 비트로 바꿨을 때 비트들을 값만큼 왼쪽으로 이동.

```javascript
console.log(4 << 1) // 8
console.log(4 << 2) // 16
console.log(-4 << 2) // -16
```

## \>\> (부호 유지 오른쪽 시프트)

피연산자를 비트로 바꿨을 때 비트들을 값만큼 오른쪽으로 이동.

```javascript
console.log(4 >> 1) // 2
console.log(4 >> 2) // 1
console.log(-4 >> 2) // -1
```

## \>\>\> (부호 버림 오른쪽 시프트)

피연산자를 비트로 바꿨을 때 비트들을 값만큼 오른쪽으로 이동.

```javascript
console.log(4 >>> 1) // 2
console.log(-1 >>> 1) // 2147483647
```
