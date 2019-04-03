# 연결 리스트(linked-list)

연결 리스트는 여러 개의 노드로 이루어진 리스트임 배열과 다르게 크기가 고정되어 있지 않음

연결 리스트는 2개의 프로퍼티를 가지며 head는 시작 노드를 가리키고 tail은 마지막 노드를 가리킴

## 연결 리스트 vs 배열

### 장점

- 데이터의 추가/삭제 연산의 시간복잡도가 연결 리스트는 어느 곳에 삽입하던지 O(n)의 시간이 소요되고 배열과 달리 기존 데이터를 한 칸씩 변경하는 추가과정이 필요없음, 만약 맨처음이나 맨 끝에 데이터를 삽입 한다면 O(1)의 시간이 소요(만약 배열에 할당된 공간이 남아있고 데이터를 맨 끝에 삽입한다면 배열 역시 O(1)의 시간이 소요)

- 배열의 경우 데이터 삽입시 모든 공간이 다 차버렸다면 새롭게 공간을 할당하여 메모리 공간 확장이 필요하지만 연결 리스트는 필요없음

### 단점

- n번째 노드 접근시 시간 복잡도가 O(1)인 배열과 달리 연결 리스트는 O(n)이 소요

- 각각의 노드가 다음 노드를 가리키는 포인터를 가지고 있기때문에 메모리가 낭비됨

### 결론

- 데이터의 추가/삭제가 번번이 이루어진다면 연결리스트가 좋음

- 데이터의 추가/삭제가 별로 이루어지지 않고 데이터의 접근이 자주 이루어진다면 배열이 좋음

## 종류

### 단일 연결 리스트

각 노드에 데이터와 한 개의 포인터 공간이 있고, 각 노드의 포인터는 다음 노드를 가리킨다 이전 노드에 대해서 참조가 불가능

<img src='https://camo.githubusercontent.com/37013b59008ed49a6701968da6b182eb6a9d24c8/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f362f36642f53696e676c792d6c696e6b65642d6c6973742e737667'/>

### 다중 연결 리스트

이중 연결 리스트의 구조는 단일 연결 리스트와 비슷하지만, 포인터 공간이 두 개가 있고 각각의 포인터는 앞의 노드와 뒤의 노드를 가리킨다 단일 연결 리스트와 달리 이전 노드에 대해서 참조가 가능

<img src='https://camo.githubusercontent.com/a77efae509d76b6329bf3752d5367aaa4d8905f0/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f352f35652f446f75626c792d6c696e6b65642d6c6973742e737667'/>

```javascript
// 단일 연결 리스트

function CreateNode(data) {
  this.data = data
  this.next = null
}

class LinkedList {
  constructor() {
    this.head = null
    this.tail = null
    this.length = 0
  }

  add(data) {
    const node = new CreateNode(data)
    // node가 아에 없을때 head에 node추가
    if (!this.head) {
      this.head = node
      this.tail = node
      this.length++
      return
    }
    // 기존에 node가 있을때 node 추가
    this.tail.next = node
    this.tail = node
    this.length++
  }

  remove(idx) {
    // head를 삭제할 때
    if (idx === 0) {
      let willRemoveHead = this.head
      this.head = willRemoveHead.next
      // node가 1개뿐일때 0번째 index의 node를 삭제했을때 tail도 같이 삭제
      if (!this.head.next) {
        this.tail = null
      }
      return
    }
    // 그냥 node를 삭제할 때
    let current = this.head
    let before
    let count = 0
    while (count < idx && current.next) {
      before = current
      current = current.next
      count++
    }
    if (idx !== count) {
      throw new Error('해당 idx에 해당하는 Node를 찾을 수 없습니다')
    }
    // 삭제할 노드가 마지막 노드가 아닐때
    if (current.next) {
      before.next = current.next
      // 삭제할 노드가 마지막 노드일때
    } else {
      before.next = null
    }
  }

  find(idx) {
    let current = this.head
    let count = 0
    while (count < idx && current.next) {
      current = current.next
      count++
    }
    if (idx !== count) {
      throw new Error('해당 idx에 해당하는 Node를 찾을 수 없습니다')
    }
    return current.data
  }
}

const list = new LinkedList()
list.add(2)
list.add(21)
list.add(1111)
list.remove(1)

console.log(list)
```
