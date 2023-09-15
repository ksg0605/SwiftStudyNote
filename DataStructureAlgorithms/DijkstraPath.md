# [알고리즘] 10. Dijkstra : 다익스트라 (Swift)

> 그래프의 특정 노드에서 출발하여 다른 노드까지의 최단 경로를 구하는 단일 경로 알고리즘  
> 가중치 그래프에서 간선의 가중치 합이 최소가 되도록 하는 것이 목적

![Dijkstra](https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif)

## 생각한 로직

1. 우선순위 큐를 사용한다.
   1. 가장 짧은 거리를 가진 노드 정보를 꺼내게 된다.
2. 거리 저장 배열을 사용한다. (최종 리턴이 될 정보를 저장)
3. HashMap을 사용하여 하나의 노드(key)에서 갈 수 있는 Edge(노드와 가중치)(ArrayList)를 그래프로 저장한다.
4. 우선순위 큐에서 맨 앞에 있는 값을 poll()하고 현재 값과 갈 수 있는 값들을 비교하여 현재 값보다 작으면 거리 저장 배열에 저장한다.

## 코드 구현 (Swift)

```Swift
var graph : [String: [(String,Int)]] = [:]
graph.updateValue([("B",8),("C",1),("D",2)], forKey: "A")
graph.updateValue([], forKey: "B")
graph.updateValue([("B",5),("D",2)], forKey: "C")
graph.updateValue([("E",3),("F",5)], forKey: "D")
graph.updateValue([("F",1)], forKey: "E")
graph.updateValue([("A",5)], forKey: "F")

for items in graph {
    for item in items.value {
        print("\(items.key) -> \(item.0) : \(item.1)")
    }
}
print(dijkstra(graph,"A"))

func dijkstra(_ graph : [String: [(String,Int)]], _ start : String) -> [String:Int] {

    var distances : [String:Int] = [:]
    for item in graph {
        distances.updateValue(Int.max, forKey: item.key)
    }

    distances[start] = 0

    var pq : [(Int,String)] = [(distances[start]!,start)]


    while pq.count != 0 {
        print(pq)
        pq.sort{ $0 > $1 }
        let dequeued = pq.removeLast()

        let currentDistance = dequeued.0
        let currentNode = dequeued.1

        if distances[currentNode]! < currentDistance {
            continue
        }

        for (adjacent,weight) in graph[currentNode]! {
            print(pq)
            let distance = currentDistance + weight
            if distance < distances[adjacent]! {
                distances[adjacent] = distance
                pq.append((distance,adjacent))
            }
        }
    }
    return distances
}
```

## 고민한 부분

- 머리로 하나하나 생각하다가 터질 뻔 했기 때문에 그림을 그려가면서,
- 글로 써내려가면서 직접 반복되는 패턴을 파악해야 한다.
- 무조건 그림과 글로 파악하기
