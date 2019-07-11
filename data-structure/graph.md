# Graph

노드(네트워크 또는 데이터 구조를 구성하는 각각의 개체)와 노드를 연결하는 간선(edge)을 하나로 모아 놓은 자료 구조

그래프는 여러 개의 고립된 부분 그래프로 구성될 수 있다 모든 정점간에 경로가 존재하는 그래프는 "연결 그래프"라고 부른다

사이클이 없는 그래프는 "비순환 그래프"라고 부른다

## 용어

- 정점(vertex): 네트워크 또는 데이터 구조를 구성하는 각각의 개체 (node 라고도 부름)
- 간선(arch): 버텍스를 연결하는 선 (edge 라고도 부름)
- 인접 정점(adjacent vertex): 아크에 의해 직접 연결된 버텍스
- 버텍스의 차수(degree): 무방향 그래프에서 하나의 버텍스에 인접한 버텍스의 수
- 진입 차수(in-degree): 다른 버텍스에서부터 오는 아크의 개수
- 진출 차수(out-degree): 다른 버텍스로 가는 아크의 개수
- 경로 길이(path length): 경로를 구성하는 데 사용된 아크의 수
- 단순 경로(simple path): 경로 중에서 반복되는 버텍스가 없는 경우
- 사이클(cycle): 단순 경로의 시작 버텍스와 종료 버텍스가 동일한 경우

## 그래프 표현

인접 리스트로 그래프를 표현하는 것이 가장 일반적인 방법이다

### 인접 행렬

<img src="https://t1.daumcdn.net/cfile/tistory/21029250584C0F2413">

인접 행렬은 그래프의 연결 관계를 2차원 배열로 나타내는 방식이다. matrix[i][j]가 1이면 i에서 j로의 간선이 있다는 뜻이고 0이면 간선이 없다는 뜻이다

장점으로는 구현하기 쉽고 두 점에 대한 연결 정보를 조회할 때 O(1) 의 시간 복잡도가 소요되지만

단점으로는 노드 i에 연결된 노드들의 갯수를 확인 해야할 경우 다른 모든 노드들을 모두 확인 해봐야 하기 때문에 O(V)의 시간이 소요되고 무조건 공간을 O(V²)차지한다 (V: 전체노드의 갯수)

### 인접 리스트

<img src="https://t1.daumcdn.net/cfile/tistory/2269874B584C17F301">

인접 리스트는 그래프의 연결 관계를 연결 리스트로 나타내는 방식이다

장점으로는 실제로 연결된 노드들에 대한 정보만 저장하기때문에 인접 행렬보다 메모리를 적게 차지하고 노드 i에 연결된 모든 노드들을 순회 해야할 경우 다른 모든 노드들을 확인해볼 필요없이 연결된 노드들만 확인해보면 된다

## 오일러 경로(Eulerian tour)

그래프에 존재하는 모든 아크을 한 번만 통과하면서 처음 버텍스으로 되돌아오는 경로를 말한다.
그래프의 모든 버텍스에 연결된 아크의 개수가 짝수일 때만 오일러 경로가 존재한다.

## 방향 그래프 vs 무방향 그래프

<img src="https://cdn.filepicker.io/api/file/ASqFe9MSQXqzoZthyThq"/>

왼쪽은 방향 그래프이고, 오른쪽은 무방향 그래프이다. 방향 그래프는 방향을 나타내는 화살표가 있지만 무방향 그래프는 없다 트리도 방향 그래프이다

트리의 노드가 하나의 In-degree만 가지는 반면, 그래프의 버텍스는 하나 이상의 In-degree를 가질 수 있다

## 완전 그래프

<img src='https://t1.daumcdn.net/cfile/tistory/99B299345B5408DA18' />

모든 버텍스가 아크로 연결된 그래프를 완전 그래프라고 부르고 그래프의 부분집합을 부분 그래프라고 부른다

## 그래프 탐색

DPS는 그래프에서 모든 노드를 방문하고자 할 때 주로 사용하고 BFS는 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾을때 주로 사용된다

### 깊이 우선 탐색(Depth first search)

- DFS는 a노드를 방문한 뒤 a와 인접한 노드를 차례로 순회하는 방식이다 a와 이웃한 노드 b를 방문하기전에 a와 인접한 모든 노드들을 다 방문해야한다

- DPS는 Stack 이나 재귀를 활용해서 탐색한다.
- Stack을 사용해서 탐색하는 방법은 첫번째 버텍스를 스택에 집어넣는다.
- 그이후 pop을 한뒤 pop을한 버텍스의 인접한 버텍스들중 방문하지않은 버텍스를 스택에 push하고 한번 방문한 버텍스들을 visited list에 저장해서 2번 방문하지 않게한다 이방법을 반복한다.
- DPS를 사용하면 그래프에서 싸이클이있는지 쉽게 확인할 수 있다(visited list에 중복된 버텍스가 있으면 그래프에 싸이클이 있음)

```javascript
// 재귀활용 트리 dfs
function dfs(node) {
    if(!node) {
        return 
    }
    console.log(node.val)
    dfs(node.left)
    dfs(node.right)
}

// stack 활용 트리 dfs
function dfs2(root) {
  const stack = [root]
  while(stack.length) {
    const current = stack.pop()
    if(current) {
      console.log(current.val)
      stack.push(current.right, current.left)
    }
  }
}

// stack 활용 graph dfs
function dfs3(root, adjacencyList) {
  const stack = [root]
  const visited = []
  while(stack.length) {
    const current = stack.pop()
    if(current) {
      console.log(current.val)
      adjacencyList[current].map(neighbor => {
        if (!visited[neighbor]) stack.push(neighbor)
      })
      visited.push(current)
    }
  }
}
```

### 너비 우선 탐색(Breadth first search)

- BFS는 a노드를 방문한 뒤 a와 이웃한 노드들을 차례로 순회하는 방식이다 a노드의 이웃 노드를 모두 방문한 다음에 이웃의 이웃 노드들을 방문한다
- BPS는 Queue을 사용해서 탐색한다.
- BFS는 Stack을 사용하는 DFS와 같지만 Stack대신 Queue를 사용한다

```javascript
// 트리 bfs
function bfs(root) {
  const queue = [root]
  while(queue.length) {
    const current = queue.shift()
    if(current) {
      console.log(current.val)
      queue.push(current.left, current.right)
    }
  }
}

// graph bfs
function bfs2(root, adjacencyList) {
  const queue = [root]
  const visited = []
  while(queue.length) {
    const current = queue.shift()
    if(current) {
      console.log(current.val)
      adjacencyList[current].map(neighbor => {
        if (!visited[neighbor]) queue.push(neighbor)
      })
      visited.push(current)
    }
  }
}
```

### 양방향 탐색(Bidirectional search)

- 양방향 탐색은 출발지와 도착지 사이에 최단 경로를 찾을 때 주로 사용된다 기본적으로 출발지와 도착지 두 노드에서 동시에 너비 우선 탐색을 수행한 뒤, 두 탐색 지점이 충돌하는 경우에 경로를 찾는 방식이다.
