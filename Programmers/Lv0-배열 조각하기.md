# Lv0: 배열 조각하기

## 내 풀이

```Swift
import Foundation

func solution(_ arr:[Int], _ query:[Int]) -> [Int] {
    var ret = arr
    for i in 0..<query.count {
        if i % 2 == 0 {
            ret = Array(ret.prefix(query[i]+1))
        } else {
            ret = Array(ret.suffix(ret.count-query[i]))
        }
    }
    return ret
}
```

### 풀이내용

query의 짝수 인덱스에서는 `arr[query[i]]` 이전의 요소들을 가져오고
query의 홀수 인덱스에서는 `arr[query[i]]` 이후의 요소들을 가져온다

### 아쉬웠던 점

suffix 숫자 계산으로 조금 골머리를 앓았다.

### 다른 풀이

```swift
import Foundation

func solution(_ arr:[Int], _ query:[Int]) -> [Int] {
    var left = 0, right = arr.count - 1
    query.enumerated().forEach {
        if $0.offset % 2 == 0 { right = left + $0.element }
        else { left += $0.element }
    }
    let arr = Array(arr[left..<right])
    return arr.isEmpty ? [-1] : arr
```

enumerate를 사용했으면 더 보기 좋았을지도 모르겠다.
