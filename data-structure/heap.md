# Heap

<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/480px-Max-Heap.svg.png'/>

- 힙이란 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전 트리(노드가 왼쪽부터 순서대로 들어있는 트리)구조의 자료구조

- 데이터를 삽입할 때 힙의 밑바닥 가장 오른쪽 위치에 이어서 삽입한뒤 부모 노드들과 서로 교환하여 최대 힙 또는 최소 힙을 만든다

- 데이터를 제거할 때 가장 위의 루트 노드를 제거하고 힙의 마지막 노드를 가져와서 힙을 재구성한다

시간 복잡도 = 힙을 생성할 때: O(nlogn) 데이터를 삽입, 제거할 때: O(logn) 최대, 최소값을 구할 때: O(1)

## 종류

### 최대 힙(max heap)

![max heap img](https://camo.githubusercontent.com/cf3c66d0d2ed67af70a8bc500fc215526d266a0d/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f332f33382f4d61782d486561702e737667)

부모 노드의 값이 자식 노드의 값보다 크거나 같은 힙

### 최소 힙(min heap)

![min heap img](https://camo.githubusercontent.com/16e4220b69a866f97cc20d934c4b16fe5b9147de/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f362f36392f4d696e2d686561702e706e67)

부모 노드의 값이 자식 노드의 값보다 작거나 같은 힙

```javascript
// 최대 힙
class Heap {
  constructor(list = []) {
    this.list = list

    for (let i = Math.floor(list.length / 2); i >= 0; i--) {
      this.siftDown(i, list.length)
    }
  }

  heapify(idx) {
    const parent = Math.floor((idx - 1) / 2)
    if (this.list[idx] > this.list[parent]) {
      this.swap(idx, parent)
      this.heapify(parent)
    }
  }

  siftDown(idx, length) {
    const left = idx * 2 + 1
    const right = idx * 2 + 2
    let largest = idx

    if (left < length && this.list[left] > this.list[largest]) {
      largest = left
    }
    if (right < length && this.list[right] > this.list[largest]) {
      largest = right
    }
    if (idx !== largest) {
      this.swap(largest, idx)
      this.siftDown(largest, length)
    }
  }

  insert(data) {
    const length = this.list.length
    this.list[length] = data
    this.heapify(length)
  }

  delete() {
    if (!this.list.length) {
      return false
    }
    const item = this.list[0]
    this.list[0] = this.list.pop()
    this.siftDown(0, this.list.length)
    return item
  }

  peek() {
    return this.list
  }

  swap(indexOne, indexTwo) {
    const temp = this.list[indexOne]
    this.list[indexOne] = this.list[indexTwo]
    this.list[indexTwo] = temp
  }
}

const heap = new Heap([1, 2, 3, 4, 9, 6, 7, 8, 0])
heap.insert(99)
heap.insert(10)
heap.delete()
heap.peek() // [ 10, 9, 7, 4, 8, 6, 3, 1, 0, 2 ]
```
