# Lv0: 첫 번째로 나오는 음수

## 내 풀이

```Swift
import Foundation

func solution(_ num_list:[Int]) -> Int {
    for i in num_list {
        if i < 0 {
            return num_list.index(of: i)!
            break
        }
    }

    return -1
}
```

### 풀이내용

단순 배열을 탐색하는 문제

### 아쉬웠던 점

쉬운 문제, enumerated와 filter 고차함수를 사용했어도 됐을 것 같다.

### 다른 풀이

```swift
func solution(_ numList: [Int]) -> Int { numList.firstIndex(where: { $0 < 0 }) ?? -1 }
```

where절과 firstIndex를 사용한 풀이. where절을 아직 잘 사용하지 못하는데, 좀 더 연습이 필요하다.
