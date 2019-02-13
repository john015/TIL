## 버블 정렬(bubble sort)

오름차순 정렬 기준으로 첫 번째 값과 두 번째 값을, 두 번째 값과 세 번째 값을, ..., (마지막 - 1)번째 값과 마지막 값을 비교하여 큰 값을 뒤로 보내면서 배열을 정렬한다

처음 정렬 한뒤 가장 큰 값이 맨 뒤로 이동하므로 그다음 정렬에서는 맨 끝에 있는 값은 정렬에서 제외되고, 두 번째 정렬을 한뒤 끝에서 두 번째 값은 정렬에서 제외된다. 이렇게 끝 까지 반복한다

시간 복잡도: O(n²)

공간 복잡도: O(1)

```javascript
// 오름차순
function ascBubbleSort(array) {
  // 순차적으로 비교하기 위한 반복문
  for (let i = 0; i < array.length - 1; i++) {
    // 끝까지 돌았을 때 다시 처음부터 비교하기 위한 반복문
    for (let j = 0; j < array.length - 1 - i; j++) {
      // array[j]값이 arrat[j + 1]값보다 크면 변경
      if (array[j] > array[j + 1]) {
        // 두 수를 서로 바꿔줌
        const temp = array[j]
        array[j] = array[j + 1]
        array[j + 1] = temp
      }
    }
  }
  return array
}

// 내림차순
function descBubbleSort(array) {
  // 순차적으로 비교하기 위한 반복문
  for (let i = 0; i < array.length - 1; i++) {
    // 끝까지 돌았을 때 다시 처음부터 비교하기 위한 반복문
    for (let j = 0; j < array.length - 1 - i; j++) {
      // array[j]값이 arrat[j + 1]값보다 크면 변경
      if (array[j] < array[j + 1]) {
        // 두 수를 서로 바꿔줌
        const temp = array[j]
        array[j] = array[j + 1]
        array[j + 1] = temp
      }
    }
  }
  return array
}

ascBubbleSort([7, 1, 5, 4, 6, 3, 2, 8]) // [ 1, 2, 3, 4, 5, 6, 7, 8 ]
descBubbleSort([7, 1, 5, 4, 6, 3, 2, 8]) // [ 8, 7, 6, 5, 4, 3, 2, 1 ]
```
