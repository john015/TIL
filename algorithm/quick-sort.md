## 퀵 정렬(quick sort)

합병 정렬보다 평균 두 배 빠르다 하지만 best worst case에선 O(n²)이다

또 다른 단점으로 같은 숫자들을 정렬할 경우 순서가 섞일 수 있다 퀵 정렬은 합병 정렬처럼 분할 정복 기법을 사용한다

배열에 있는 한 원소를 선택(보통 맨 오른쪽 원소)한다 이렇게 고른 원소를 피벗(pivot) 이라고 한다.

피벗을 가장 오른쪽으로 보낸뒤 피벗을 제외한 가장 왼쪽과 오른쪽 값을 조작한다

왼쪽 값이 피벗보다 작으면 다음으로 넘어가고, 크면 가만히 유지 한다 오른쪽 값은 피벗보다 크면 다음으로 넘어가고, 작으면 가만히 유지한다 이렇게 넘어가다가 왼쪽 값은 피벗 보다 크고 오른쪽 값은 피벗보다 작으면 서로 바꿔준다.

가장 왼쪽과 오른쪽 수가 만나서 더 이상 비교할 수 없을때 만난 값과 피벗을 서로 바꿔준다.

피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다

분할된 리스트에 대하여 재귀를 하여 퀵 정렬을 반복한다

시간 복잡도: 평균 O(nlog(n)) 최악 O(n²)

공간 복잡도 O(log(n))

```javascript
function quickSort(array, left = 0, right = array.length - 1) {
  if (array.length < 1) {
    return []
  }
  const pivotIndex = partition(array, left, right - 1)

  if (left < pivotIndex - 1) quickSort(array, left, pivotIndex - 1) // 기준 왼쪽 부분 재귀
  if (pivotIndex + 1 < right) quickSort(array, pivotIndex + 1, right) // 기준 오른쪽 부분 재귀
  return array
}

function swap(arr, a, b) {
  const temp = arr[a]
  arr[a] = arr[b]
  arr[b] = temp
}

function partition(array, left, right) {
  const pivotIndex = right + 1
  const pivot = array[pivotIndex]
  while (left <= right) {
    // 왼쪽, 오른쪽 수를 피벗과 비교해 다음 수로 이동
    while (array[left] < pivot) left++
    while (array[right] > pivot) right--
    if (left <= right) {
      swap(array, left, right) // 서로 스왑
      left++
      right--
    }
  }
  swap(array, left, pivotIndex) // 피벗값과 left와 right가 만난 값을 스왑
  return left
}

quickSort([4, 1, 7, 6, 3, 8, 2, 5]) // [1,2,3,4,5,6,7,8]
```
