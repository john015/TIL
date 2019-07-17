## 이진 탐색

함수의 첫번째 파라미터로 받은 배열에서 두번째 파라미터로 받은 value의 index를 찾아서 반환 없을시 -1 반환

시간 복잡도: O(log(n))

```javascript
// s = startIdx, e = endIdx, m = middleIdx
// dp
function binarySearch(arr, value) {
  return recur (s, e) {
    if (s > e) {
      return -1
    }
    const m = Math.floor((s + e) / 2)
    if (arr[m] === value) {
      return m
    }
    if (arr[m] > value) {
      return recur(s, m - 1)
    }
    if (arr[m] < value) {
      return recur(m + 1, e)
    }
    return -1
  }(0, arr.length - 1)
}

function binarySearch2(arr, val) {
  let start = 0
  let end = arr.length - 1
  while(start <= end) {
    const middle = Math.floor((start + end) / 2)
    if(arr[middle] === val) return middle
    if(arr[middle] > val) {
      end = middle - 1
    } else {
      start = middle + 1
    }
  }
  return - 1
}
```
