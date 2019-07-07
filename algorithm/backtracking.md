# 백트래킹 알고리즘

백트래킹(퇴각검색) 알고리즘은 조건에 만족하는 모든 조합의 수를 살펴보는 알고리즘이다.

CSP(조건 만족 문제)을 해결하기 위해 사용한다.

일반적으로 DFS(깊이 우선탐색)을 사용해서 구현하며 순열을 구하거나, 괄호 쌍을 만들때 사용한다.

```javascript
// 정수 n이 주어질때 n쌍 괄호의 모든 조합을 배열에 담아 리턴하는 문제

/**
 * @param {number} n
 * @return {string[]}
 */
const generateParenthesis = function(n) {
  function backtrack(left, right, str) {
    if (str.length === limit) return arr.push(str)
    if (left) backtrack(left - 1, right, str + '(')
    if (right > left) backtrack(left, right - 1, str + ')')
  }
  const arr = []
  const limit = n * 2
  backtrack(n, n, '')
  return arr
}
```
