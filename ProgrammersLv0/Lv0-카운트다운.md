# Lv0: 카운트다운

## 내 풀이

```Swift
import Foundation

func solution(_ start:Int, _ end_num:Int) -> [Int] {
    var ret: [Int] = []
    for num in end_num...start {
        ret.append(num)
    }
    return ret.reversed()
}
```

### 풀이내용

내림차순으로 배열을 정렬하는 문제

### 아쉬웠던 점

초기에 푼 문제라 swift스럽지 않다.

### 다른 풀이

```swift
import Foundation

func solution(_ start:Int, _ end_num:Int) -> [Int] {
    return (end_num...start).sorted(by: >)
}
```
