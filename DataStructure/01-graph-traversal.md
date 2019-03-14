# 그래프 탐색 (Graph Traversal / Search)
> 19-03-18 (월)

<br>

## 순서
- DFS
- BFS

<br><br><br>


# 1. DFS
Depth First Search (깊이 우선 탐색)

그래프(트리를 포함한 개념)의 한 노드에서 탐색을 시작해, 가능한 깊이 들어간 후 더이상 들어갈 수 없을 때 
방문하지 않은 새로운 노드에서 같은 과정으로 탐색을 시작한다. 더이상 방문할 노드가 없다면 탐색을 종료한다.


<br>

### 1) 특징
  #### 장점
  - 저장 공간을 적게 사용한다.
  - 목표 노드가 깊은 곳에 있을 때 유용하다.

  #### 단점
  - 해가 없는 경로를 깊이 탐색해 낭비가 발생할 수 있다.
    - 따라서 실제로는 미리 지정한 임의 깊이까지만 탐색하고 목표 노드를 발견하지 못하면 다음 경로를 따라 탐색하는 방법이 유용할 수 있다.
  - 얻어진 해가 최단 경로가 된다는 보장이 없다.

<br>

### 2) 구현
일반적으로 recursion(재귀)를 사용한다.

기본적으로 다음과 같은 구조를 따르고, 문제에 따라 다양한 변형을 만들어낼 수 있다.
```java
void DoDFS(int v,boolean visited[])
{ 
    // 현재 노드를 방문한 것으로 표시하고 프린트한다.
    visited[v] = true; 
    System.out.print(v+" ");

    // 모든 인접한 노드를 방문한다.
    Iterator<Integer> i = adj[v].listIterator(); 
    while (i.hasNext()) 
    { 
        int n = i.next();
        if (!visited[n]) 
            DoDFS(n, visited); 
    } 
} 

// DFS의 main이 되는 메소드. DoDFS() 메소드를 호출한다.
void DFS(int v) 
{ 
    // 모든 노드를 방문하지 않은 것으로 초기화한다.
    // (java에서는 boolean 타입 생성시 default 값이 false이다.)
    boolean visited[] = new boolean[V];

    // DFS 탐색을 하기 위한 서브 메소드를 호출한다.
    DoDFS(v, visited); 
}
```


<br><br>


# 2. BFS
Breadth First Search (너비 우선 탐색)

트리의 경우 root 노드에서, 트리가 아닌 그래프의 경우 임의의 한 노드에서 시작해 인접한 노드를 모두 방문한 후 
그 다음 깊이에 있는 노드(방금 방문한 노드들의 자식 노드)들을 방문한다.

<br>
### 1) 특징
여러 갈래 중 무한한 길이를 가지는 경로가 존재하고 탐색 목표가 다른 경로에 존재하는 경우 
- DFS로 탐색할 시에는 무한한 길이의 경로에서 영원히 종료하지 못하지만,
- BFS의 경우는 모든 경로를 동시에 진행하기 때문에 탐색이 가능하다.

<br>

### 2) 구현
일반적으로 Queue를 사용한다. (현재 방문할 깊이에 있는 노드들을 순차적으로 Queue에 넣고 방문할 때 제거)

```java
void BFS(int s) 
{ 
    // 모든 노드들을 미방문 상태로 초기화.
    // (java는 boolean 타입 초기화시 deafult 값이 false)
    boolean visited[] = new boolean[V]; 

    // BFS를 위한 Queue 생성
    LinkedList<Integer> queue = new LinkedList<Integer>(); 

    // 주어진 현재 노드 s를 방문한 것으로 표시 후 큐에 넣는다.
    visited[s]=true; 
    queue.add(s); 

    while (queue.size() != 0) 
    { 
        // 방문할 노드를 큐에서 dequeue한다.
        // (확인을 위해 프린트도 함. 제거 가능)
        s = queue.poll();
        System.out.print(s+" ");

        // 현재 노드의 모든 인접한 노드를 가져오고, 그 인접 노드가 아직 방문하지 않은 상태라면 queue에 넣는다.
        Iterator<Integer> i = adj[s].listIterator(); 
        while (i.hasNext()) 
        { 
            int n = i.next(); 
            if (!visited[n]) 
            { 
                visited[n] = true; 
                queue.add(n); 
            } 
        } 
    } 
} 
```

### 언제 BFS를 써야 할까?
위의 `1) 특징`에서 확인할 수 있듯이, 
<a href="https://www.acmicpc.net/board/view/13899">가중치 없는 그래프의 최단 경로문제는 BFS로만 접근해야 한다</a>고 한다..



<br><br>
# References
- https://namu.wiki/w/DFS
- https://namu.wiki/w/BFS
- https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/
- https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
