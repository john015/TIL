# Stack

<img src="https://www.geeksforgeeks.org/wp-content/uploads/gq/2013/03/stack.png"/>

가장 늦게 추가된 항목이 가장 먼저 제거되는 LIFO(Last In First Out) 형식의 자료 구조

stack에 데이터를 추가하는걸 push라고 부르고 데이터를 꺼낼때 pop이라고 부른다

stack에는 제일 위 데이터를 가리키는 top가 있다

## stack overflow

스택에 더 이상 데이터가 추가될 공간이 없는데 추가(push)를 할 때 발생

## stack underflow

스택에 메모리가 비어있을 때 데이터를 꺼내려고(pop) 했을 때 발생

## 사용 사례

- 역순 문자열 만들기
- 재귀 알고리즘
- 웹 브라우저 방문기록 (뒤로가기, 앞으로 가기)
- 실행 취소 (undo)
-

## Stack으로 Queue만들기

- 1. mainStack와 subStack를 만든다
- 2. 데이터가 enqueue가 되면 mainStack의 데이터를 pop해서 subStack에 push한다
- 3. subStack에 enqueue할 데이터를 push한다
- 4. 다시 subStack에서 데이터들을 pop해서 mainStack에 push한다

```javascript
class Queue {
  constructor() {
    this.mainStack = []
    this.subStack = []
  }

  push(data) {
    while (this.mainStack.length) {
      this.subStack.push(this.mainStack.shift())
    }
    this.subStack.push(data)
    while (this.subStack.length) {
      this.mainStack.push(this.subStack.shift())
    }
  }
  pop() {
    return this.mainStack.shift()
  }
  peak() {
    return this.mainStack[this.mainStack.length - 1]
  }
  isEmpty() {
    return !this.mainStack.length
  }
}
```

## 구현

```javascript
function Node(data) {
  this.data = data
  this.next = null
}
class Stack {
  constructor() {
    this.top = null
  }
  push(data) {
    const n = new Node(data)
    n.next = this.top
    this.top = n
  }

  pop() {
    if (!this.top) {
      throw new Error('stack underflow')
    }
    const item = this.top
    this.top = item.next
    return item.data
  }

  peek() {
    if (!this.top) {
      throw new Error('stack underflow')
    }
    return this.top.data
  }

  isEmpty() {
    return !this.top
  }
}

const stack = new Stack()
```
