## 힙 정렬(heap sort)

힙 정렬은 [힙(Heap)](https://github.com/john015/TIL/blob/master/data-structure/heap.md) 자료구조를 기반으로한 정렬 방식이다

최대 힙이면 오름차순 정렬이 되며, 최소 힙이면 내림차순 정렬이 된다.

root node와 맨 아래 노드를 스와핑을 한뒤 스와핑한 root node를 배제하고 맨 아래 노드를 siftDown 진행하는 방식을 반복해서 더이상 스와핑할 수 없으면 정렬이 완료된다.

시간 복잡도: O(nlog(n))

공간 복잡도: O(1)

```javascript
function swap(arr, indexA, indexB) {
  const temp = arr[indexA]
  arr[indexA] = arr[indexB]
  arr[indexB] = temp
}

function siftDown(arr, idx, length) {
  // left child node index
  const left = 2 * idx + 1
  // right child node index
  const right = 2 * idx + 2
  let largest = idx

  if (left < length && arr[left] > arr[largest]) {
    largest = left
  }
  if (right < length && arr[right] > arr[largest]) {
    largest = right
  }
  // child node들의 값이 현재 노드값 보다 크면
  if (largest !== idx) {
    swap(arr, idx, largest)
    siftDown(arr, largest, length)
  }
}

function heapSort(arr) {
  const length = arr.length

  // 자식있는 마지막 노드부터 siftDown해서 arr를 heap으로 변경
  for (let i = Math.floor(length / 2); i >= 0; i--) {
    siftDown(arr, i, length)
  }

  // root node와 마지막 노드를 swap한뒤 siftDown해서 heap sort 진행
  for (let j = length - 1; j > 0; j--) {
    swap(arr, 0, j)

    // swap한 root노드는 제외하기 때문에 length는 j + 1이 아니라 j
    siftDown(arr, 0, j)
  }
}

const list = [4, 2, -1, 3, 1, 5, 9, 30, 6]
heapSort(list)
console.log(list) // [ -1, 1, 2, 3, 4, 5, 6, 9, 30 ]
```
