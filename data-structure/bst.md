# 이진 검색 트리(binary search tree)

이진 탐색 트리는 "모든 왼쪽 자식들 <= n < 모든 오른쪽 자식들"이라는 정의가 모든 노드 n에 대해서 참인 트리를 말한다.

바로 아래 자식뿐만 아니라 내 밑에 있는 모든 자식 노드들에 대해서 참이어야 한다.

시간 복잡도: 검색, 삭제, 삽입 O(log n)

```javascript
function Node(data, left = null, right = null) {
  this.data = data
  this.left = left
  this.right = right
}

class BinarySearchTree {
  constructor() {
    this.root = null
  }

  insertNode(node) {
    // root node가 없으면 root에 node 삽입
    if (!this.root) {
      this.root = node
      return
    }

    let currentNode = this.root
    while (currentNode) {
      // 만약 node data가 현재 노드의 data보다 작다면
      if (node.data < currentNode.data) {
        // 만약 current node가 left subtree 없는 leaf node라면 left에 node삽입후 종료
        if (!currentNode.left) {
          currentNode.left = node
          return
        }
        // left subtree가 있으면 current node를 왼쪽 subtree로 이동
        currentNode = currentNode.left
        continue
      }
      // 만약 node data가 현재 노드의 data보다 크다면
      if (node.data > currentNode.data) {
        // 만약 current node가 right subtree 없는 leaf node라면 right에 node삽입
        if (!currentNode.right) {
          currentNode.right = node
          return
        }
        // right subtree가 있으면  current node를 오른쪽 subtree로 이동
        currentNode = currentNode.right
        continue
      }
      // 만약 node data가 현재 노드의 data와 동일하다면
      console.error(
        '이미 해당 data가 BST에 존재합니다 다른 data를 삽입해주세요.'
      )
      return
    }
  }

  inOrderTraversal(node = this.root) {
    if (node !== null) {
      this.inOrderTraversal(node.left)
      console.log('visit node: ' + node.data)
      this.inOrderTraversal(node.right)
    }
  }
}

const bst = new BinarySearchTree()
bst.insertNode(new Node(24))
bst.insertNode(new Node(20))
bst.insertNode(new Node(30))
bst.insertNode(new Node(26))
bst.insertNode(new Node(22))
bst.insertNode(new Node(14))
bst.inOrderTraversal() // 정렬된 node들
```
