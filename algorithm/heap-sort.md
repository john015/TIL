## 힙 정렬(heap sort)

```javascript
class Heap {
  constructor(arr = []) {
    this.arr = []
    arr.forEach((val, i) => {
      this.arr[i] = val
      this.reheapUp(i)
    })
  }

  reheapUp(idx) {
    if (!idx) {
      return
    }
    const parent = parseInt((idx - 1) / 2)
    if (this.arr[idx] > this.arr[parent]) {
      this.swap(idx, parent)
      this.reheapUp(parent)
    }
  }

  reheapDown(idx) {
    let left = 0
    let right = 0
    let large
    if (idx * 2 + 1 < this.arr.length) {
      left = this.arr[idx * 2 + 1]
      if (idx * 2 + 2 < this.arr.length - 1) {
        right = this.arr[idx * 2 + 2]
      }
      if (left > right) {
        large = idx * 2 + 1
      } else {
        large = idx * 2 + 2
      }
      if (this.arr[idx] < this.arr[large]) {
        this.swap(idx, large)
        this.reheapDown(large)
      }
    }
  }

  insert(number) {
    const last = this.arr.length
    this.arr[last] = number
    this.reheapUp(last)
  }

  delete() {
    if (this.arr.length === 0) {
      return false
    }
    const del = this.arr[0]
    this.arr[0] = this.arr.pop()
    this.reheapDown(0)
    return del
  }

  sort() {
    const sortedArr = new Array(this.arr.length).fill(0)
    return sortedArr.map(() => this.delete())
  }

  swap(target1, target2) {
    const temp = this.arr[target1]
    this.arr[target1] = this.arr[target2]
    this.arr[target2] = temp
  }
}

const heap = new Heap([1, 2, 3])
heap.insert(10)
heap.insert(5)
heap.insert(7)
heap.sort() // [ 10, 7, 5, 3, 2, 1 ]
```
