# Queue

<img src="https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/02/Queue.png"/>

가장 먼저 추가된 항목이 가장 먼저 제거되는 FIFO(First In First Out) 형식의 자료 구조

queue에 데이터를 추가하는걸 enqueue라고 부르고 데이터를 꺼낼때 dequeue이라고 부른다

queue에는 제일 위 데이터를 반환하는 peek과 queue가 비어있는지 불리언으로 반환하는 isEmpty 메소드가 있다

## Queue로 Stack만들기

- 1. mainQueue와 subQueue를 만든다
- 2. 데이터가 push 되면 mainQueue의 데이터를 dequeue해서 subQueue에 enqueue한다
- 3. mainQueue에 push할 데이터를 enqueue한다
- 4. 다시 subQueue에서 dequeue한다음 mainQueue에 enqueue한다

```javascript
class Stack {
  constructor() {
    this.mainQueue = []
    this.subQueue = []
  }

  push(data) {
    while (this.mainQueue.length) {
      this.subQueue.push(this.mainQueue.shift())
    }
    this.mainQueue.push(data)
    while (this.subQueue.length) {
      this.mainQueue.push(this.subQueue.shift())
    }
  }
  pop() {
    return this.mainQueue.shift()
  }
  top() {
    return this.mainQueue[0]
  }
  isEmpty() {
    return !this.mainQueue.length
  }
}
```

## 구현

```javascript
function CreateNode(data) {
  this.data = data
  this.next = null
}
class Queue {
  constructor() {
    this.head = null
    this.rear = null
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
  }

  dequeue() {
    if (!this.head) {
      throw new Error('queue에 data가 없습니다')
    }
    const item = this.head.data
    this.head = this.head.next
    // queue에 data가 없을때
    if (!this.head) {
      this.rear = null
    }
    return item
  }

  peek() {
    return this.head.data
  }

  isEmpty() {
    return !this.head
  }
}

const queue = new Queue()
```
