## 선택 정렬(selection sort)

오름차순 정렬 기준으로 배열을 처음부터 훑어서 가장 작은 값을 첫 번째 index에 놓습니다 다시 배열을 훑어서 두 번째로 작은 값을 두 번째 index에 놓습니다. 계속 끝까지 반복합니다

시간 복잡도: O(n²)

공간 복잡도: O(1)

```javascript
// 오름차순
function ascSelectionSort(array) {
  const length = array.length
  for (let i = 0; i < length - 1; i++) {
    let minIndex = i
    // 최솟값의 위치를 찾음
    for (let j = i + 1; j < length; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j
      }
    }
    // 최솟값을 앞으로 두 수를 서로 바꿔줌
    const temp = array[minIndex]
    array[minIndex] = array[i]
    array[i] = temp
  }
  return array
}

//내림차순
function descSelectionSort(array) {
  const length = array.length
  for (let i = 0; i < length - 1; i++) {
    let maxIndex = i
    // 최댓값의 위치를 찾음
    for (let j = i + 1; j < length; j++) {
      if (array[j] > array[maxIndex]) {
        maxIndex = j
      }
    }
    // 최댓값을 앞으로 두 수를 서로 바꿔줌
    const temp = array[maxIndex]
    array[maxIndex] = array[i]
    array[i] = temp
  }
  return array
}

ascSelectionSort([5, 1, 4, 7, 2, 6, 8, 3]) // [1, 2, 3, 4, 5, 6, 7, 8]
descSelectionSort([5, 1, 4, 7, 2, 6, 8, 3]) // [ 8, 7, 6, 5, 4, 3, 2, 1 ]
```
