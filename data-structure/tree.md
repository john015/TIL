# Tree

그래프의 한종류로써 회로가 없고 서로 다른 두 노드를 잇는 길이 하나뿐이다

계층적 관계를 표현하는 비선형 자료구조이다

하나의 root 노드를 가지며 루트 노드는 0개 이상의 자식 노드를 갖고 있다

그 자식 노드들도 0개 이상의 자식 노드를 갖고 있고 이는 반복적으로 정의된다

## 용어

<img src='https://user-images.githubusercontent.com/32455422/53223669-71ef4f00-36b5-11e9-83fc-ffe3d1ea8eea.png'/>

- root node: 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
- leaf node: 자식이 없는 노드
- internal node: leaf node가 아닌 노드
- edge: 노드를 연결하는 선 (link, branch 라고도 부름)
- siblings: 같은 부모를 가지는 노드
- size: 자신을 포함한 모든 자손 노드의 갯수
- depth: 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 edge의 수
- level: 트리의 특정 깊이를 가지는 노드의 집합
- height: root node에서 가장 깊숙히 있는 노드의 깊이

## 특징

- 노드가 N개인 트리는 항상 N-1개의 edge을 가진다
- root node에서 어떤 노드로 가는 경로는 하나뿐이다
- 한 개의 root node만이 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가진다

## Graph vs Tree

<img src='https://gmlwjd9405.github.io/images/data-structure-graph/graph-vs-tree.png'>
