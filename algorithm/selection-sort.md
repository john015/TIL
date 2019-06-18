## 선택 정렬(selection sort)

오름차순 정렬 기준으로 배열을 처음부터 훑어서 가장 작은 값을 첫 번째 index에 놓습니다 다시 배열을 훑어서 두 번째로 작은 값을 두 번째 index에 놓습니다. 계속 끝까지 반복합니다

시간 복잡도: O(n²)

공간 복잡도: O(1)

```javascript
function swap(arr, target1, target2) {
  const temp = arr[target1]
  arr[target1] = arr[target2]
  arr[target2] = temp
}

// 오름차순
function ascSelectionSort(arr) {
  arr.map((_, idx) => {
    let minIdx = idx
    arr.slice(idx + 1).map((val, i) => {
      if (val < arr[minIdx]) {
        minIdx = i + idx + 1
      }
    })
    swap(arr, idx, minIdx)
  })
  return arr
}

//내림차순
function descSelectionSort(arr) {
  arr.map((_, idx) => {
    let maxIdx = idx
    arr.slice(idx + 1).map((val, i) => {
      if (val > arr[maxIdx]) {
        maxIdx = i + idx + 1
      }
    })
    swap(arr, idx, maxIdx)
  })
  return arr
}

ascSelectionSort([5, 1, 4, 7, 2, 6, 8, 3]) // [1, 2, 3, 4, 5, 6, 7, 8]
descSelectionSort([5, 1, 4, 7, 2, 6, 8, 3]) // [ 8, 7, 6, 5, 4, 3, 2, 1 ]
```
