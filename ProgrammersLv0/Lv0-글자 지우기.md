# Lv0: 세로 읽기

## 내 풀이

```Swift
import Foundation

func solution(_ my_string:String, _ indices:[Int]) -> String {
    var arr = Array(my_string)
    indices.forEach {
        arr[$0] = " "
    }
    return arr.map{String($0)}.filter{$0 != " "}.joined()
}
```

### 풀이내용

문자열을 문자 배열로 바꾸고 indices에 해당하는 부분을 공백으로 바꾼 후, 공백을 삭제하고 배열을 문자열로 변환

### 아쉬웠던 점

쉬운 문제

### 다른 풀이

다들 비슷비슷한 느낌
