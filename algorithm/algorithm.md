## 이분 검색

함수의 첫번째 아규먼트로 받은 배열에서 두번째 아규먼트로 받은 value의 index를 찾아서 반환 없을시 -1 반환

```javascript
function binarySearch(arr, value) {
  function solveFn(s, e) {
    if (s > e) {
      return -1
    }
    const m = Math.floor((s + e) / 2)
    if (arr[m] === value) {
      return m
    }
    if (arr[m] > value) {
      return solveFn(s, m - 1)
    }
    if (arr[m] < value) {
      return solveFn(m + 1, e)
    }
    return -1
  }
  return solveFn(0, arr.length - 1)
}
```
