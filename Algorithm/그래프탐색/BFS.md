# <em> BFS </em>

- 너비 우선 탐색(Breadth First Search)
- 그래프의 각 노드를 탐색할 때 주로 사용한다.
  - 가까운 노드부터 탐색한다.
- 너비 우선 탐색(Breadth First Search)에서는 큐(Queue)자료 구조를 사용한다.
  - DFS에서는 스택과 재귀를 이용한다.

## <em> Process 방식 </em>

1.  Graph에서 탐색 시작 노드를 큐에 삽입하고 방문처리 한다.
2.  큐에서 노드를 꺼내 해당 노드의 인접 노드중에서 방문처리가 되어 있지 않은 노드를 모두 큐에 삽입하고 방문처리 한다.
3.  위와 같은 방식으로 반복수행

## <em> 시간 복잡도 </em>

- O(n)
- DFS보다 실제 수행시간은 좋은편이다.
