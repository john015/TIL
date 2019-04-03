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
