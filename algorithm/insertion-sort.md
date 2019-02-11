## 삽입 정렬(insertion sort)

오름차순 정렬 기준으로 두 번째 값부터 이전 값 보다 크면 이전 값 오른쪽에, 작으면 왼쪽에 넣습니다 그다음 세 번째 값 앞의 두 값와 크기를 비교해서 알맞은 자리에 넣습니다 이렇게 마지막 index까지 반복 합니다

시간 복잡도: O(n²)

공간 복잡도: O(1)

```javascript 
// 오름차순
function ascInsertionSort(array) {
  let j
  for (let i = 1; i < array.length; i++) {
    const value = array[i]
    // j가 0보다 크거나 값고, value가 정렬된 값보다 작으면
    for (j = i - 1; j >= 0 && value < array[j]; j--) {
      array[j + 1] = array[j] // 한 칸씩 뒤로 밀어낸다
    }
    array[j + 1] = value // 마지막 빈 칸에 value를 넣어준다.
  }
  return array
}

// 내림차순

function descInsertionSort(array) {
  let j
  for (let i = 1; i < array.length; i++) {
    const value = array[i]
    // value < array[j]가 value > array[j]로 변경
    for (j = i - 1; j >= 0 && value > array[j]; j--) {
      array[j + 1] = array[j]
    }

    array[j + 1] = value
  }
  return array
}

ascInsertionSort([5, 6, 1, 4, 2, 3]) // [1, 2, 3, 4, 5, 6]
descInsertionSort([5, 6, 1, 4, 2, 3]) // [6, 5, 4, 3, 2, 1]
```
