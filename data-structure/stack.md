## Stack

가장 늦게 추가된 항목이 가장 먼저 제거되는 LIFO(Last In First Out) 형식의 자료 구조

### stack overflow

스택에 더 이상 데이터가 추가될 공간이 없는데 추가(push)를 할 때 발생

### stack underflow

스택에 메모리가 비어있을 때 데이터를 꺼내려고(pop) 했을 때 발생

```javascript
function CreateNode(data) {
  this.data = data
  this.next = null
}

class Stack {
  constructor() {
    this.top = null
    this.count = 0
  }

  push(data) {
    const node = new CreateNode(data)
    node.next = this.top
    this.top = node
    this.count++
  }

  pop() {
    if (!this.top) {
      throw new Error('stack underflow!')
    }
    const data = this.top.data
    this.top = this.top.next
    this.count--
    return data
  }

  stackTop() {
    return this.top.data
  }
}

const stack = new Stack()
```
