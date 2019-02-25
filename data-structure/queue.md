# Queue

<img src="https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/02/Queue.png"/>

가장 먼저 추가된 항목이 가장 먼저 제거되는 FIFO(First In First Out) 형식의 자료 구조

queue에 데이터를 추가하는걸 enqueue라고 부르고 데이터를 꺼낼때 dequeue이라고 부른다

queue에는 제일 위 데이터를 가리키는 head와 맨 끝 데이터를 가리키는 rear이 있다

```javascript
function CreateNode(data) {
  this.data = data
  this.next = null
}
class Queue {
  constructor() {
    this.head = null
    this.rear = null
    this.count = 0
  }

  enqueue(data) {
    const node = new CreateNode(data)
    // queue에 아무 data가 없을때
    if (!this.head) {
      this.head = node
      // queue에 data가 있을때
    } else {
      this.rear.next = node
    }
    this.rear = node
    this.count++
  }

  dequeue() {
    if (!this.head) {
      throw new Error('data가 없습니다')
    }
    const data = this.head.data
    // queue에 data가 1개밖에 없을때
    if (this.head.next === null) {
      this.rear = null
      this.head = null
      // queue에 data가 1개이상 일때
    } else {
      this.head = this.head.next
    }
    this.count--
    return data
  }

  front() {
    return this.head && this.head.data
  }
}

const queue = new Queue()
```
