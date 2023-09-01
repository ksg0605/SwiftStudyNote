# Lv0: 배열 만들기1

## 내 풀이

```Swift
import Foundation

func solution(_ n:Int, _ k:Int) -> [Int] {
    var arr: [Int] = Array(1...n)
    return arr.filter{$0 % k == 0}

}
```

### 풀이내용

단순히 k의 배수를 배열로 만드는 문제

### 아쉬웠던 점

그냥 한줄로 작성할 수 있는 문제 굳이 배열 변수를 만들지 않았어도 될 것 같다.

### 다른 풀이

```swift
import Foundation

func solution(_ n:Int, _ k:Int) -> [Int] {
    return (1...n).filter{$0 % k == 0}
}
```

stride()도 사용을 해보려고 노력해야겠다.
