# [알고리즘] 8. BFS : 너비우선탐색 (Swift)

> 그래프 혹은 트리를 너비 우선으로 탐색하는 알고리즘이다.
> 쉽게 말해 가로로 탐색한다고 생각

![BFS](https://upload.wikimedia.org/wikipedia/commons/4/46/Animated_BFS.gif)

## 생각한 로직

1. 그래프를 만든다
2. 방문할 예정인 리스트를 만든다.
3. 방문했던 노드들의 리스트를 만든다.
4. 시작 노드의 값을 방문할 예정 리스트에 저장
5. 방문했던 노드 리스트에 현재 노드값이 존재하는지를 확인한다.
6. 시작 노드의 인접 노드들을 방문할 예정 리스트에 저장한다.
7. 시작 노드를 방문할 예정 리스트에서 제거하고 방문헀던 노드 리스트에 저장한다.
8. 방문할 예정 리스트의 크기가 0이 될 때까지 반복한다.

## 코드 구현 (Swift)

```Swift
func bfs(graph: [[Int]], start: Int, visited: inout [Bool]){
    var queue = [start]
    //현재 노드 방문 처리
    visited[start] = true

    //큐가 빌 때까지 반복
    while !queue.isEmpty{
        //큐에서 하나의 원소 뽑아 출력
        let v = queue.removeFirst()
        print(v, terminator: " ")
        //방문하지 않은 인접한 원소들을 큐에 추가
        for i in graph[v]{
            if !visited[i]{
                queue += [i]
                visited[i] = true
            }
        }
    }
}

```

## 고민한 부분

- 큐를 사용해야 한다는 것을 떠올리기가 생각보다 힘들었다.
- 직접 그림을 그려보면서 코드를 작성하면 생각보다 용이하다.
- 작년 초에 그래프 부분에서 학습을 종료했는데 다시보니까 생각보다 할 만 했다는 점
