## 힙 정렬(heap sort)

힙 정렬은 [힙(Heap)](https://github.com/john015/TIL/blob/master/data-structure/heap.md) 자료구조를 기반으로한 정렬 방식이다

최대 힙이면 오름차순 정렬이 되며, 최소 힙이면 내림차순 정렬이 된다.

root node와 맨 아래 노드를 스와핑을 한뒤 스와핑한 root node를 배제하고 맨 아래 노드를 siftDown 진행하는 방식을 반복해서 더이상 스와핑할 수 없으면 정렬이 완료된다.

시간 복잡도: O(nlog(n))

공간 복잡도: O(1)

