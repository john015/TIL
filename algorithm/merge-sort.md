## 합병 정렬(merge-sort)

합병 정렬은 분할 정복 알고리즘(폰 노이만이 개발)이다. 분할 정복이란 어떤 문제를 그대로 해결할 수 없을 때, 작은 문제로 분할해서 푸는 방법이다.

합병 정렬은 배열을 두 개로 나누고, 나눈 것을 다시 두 개로 계속 나눠 더 이상 나눌수 없을때 나눈 배열의 첫번째 원소를 비교하며 합병(merge)한다

```javascript
function mergeSort(array) {
  if (array.length < 2) return array // 원소가 하나일 때는 그냥 return
  const pivot = Math.floor(array.length / 2) // 대략 반으로 분할
  const left = array.slice(0, pivot)
  const right = array.slice(pivot)
  return merge(mergeSort(left), mergeSort(right)) // 재귀적으로 분할하고 merge
}

function merge(leftArr, rightArr) {
  const result = []
  while (leftArr.length && rightArr.length) {
    // 두 배열의 첫 원소를 비교하여 더 작은 수를 결과에 넣어줍니다.
    const targetArr = leftArr[0] <= rightArr[0] ? leftArr : rightArr
    result.push(targetArr.shift())
  }

  // 어느 한 배열이 더 많이 남았다면 나머지를 다 넣어줍니다.
  if (leftArr.length) {
    while (leftArr.length) result.push(leftArr.shift())
  } else {
    while (rightArr.length) result.push(rightArr.shift())
  }
  return result
}

mergeSort([5, 2, 4, 7, 6, 1, 3, 8]) // [1, 2, 3, 4, 5, 6, 7, 8]
```
