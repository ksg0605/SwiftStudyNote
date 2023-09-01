# Lv0: n개 간격의 원소들

## 내 풀이

```Swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    var ret: [Int] = []
    for index in 0..<num_list.count {
        if index % n == 0 {
            ret.append(num_list[index])
        }
    }
    return ret
}
```

### 풀이내용

배열에서 n개의 간격으로 배열을 다시 만드는것

### 아쉬웠던 점

stride를 왜 생각하지 못했을까

### 다른 풀이

```swift
import Foundation

func solution(_ num_list:[Int], _ n:Int) -> [Int] {
    return stride(from: 0, to: num_list.count, by: n).map { num_list[$0] }
}
```

`stride(from: , to: , by:)` 적극 활용해 보도록 하자
