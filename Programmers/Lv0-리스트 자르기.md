# Lv0: 리스트 자르기

## 내 풀이

```Swift
import Foundation

func solution(_ n:Int, _ slicer:[Int], _ num_list:[Int]) -> [Int] {
    let a = slicer[0]
    let b = slicer[1]
    let c = slicer[2]

    switch n {
        case 1:
            return Array(num_list[0...b])
        case 2:
            return Array(num_list[a...])
        case 3:
            return Array(num_list[a...b])
        case 4:
            var arr = Array(num_list[a...b])
            var ret: [Int] = []
            for i in 0..<(b - a + 1) {
                if i % c == 0 {
                    ret.append(arr[i])
                }
            }
            return ret
        default:
            return [0]
    }
}
```

### 풀이내용

n을 매개변수로 switch를 사용, 서브스크립트와 범위 연산자를 사용하여 단순 케이스 나누기

### 아쉬웠던 점

쉬운 문제

### 다른 풀이

다들 비슷비슷한 느낌
