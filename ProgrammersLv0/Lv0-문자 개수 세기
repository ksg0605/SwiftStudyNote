# Lv0: 세로 읽기

## 내 풀이

```Swift
import Foundation

func solution(_ my_string:String) -> [Int] {
    let stringArr = Array(my_string)
    var countArr = [Int](repeating: 0, count: 52)

    for char in stringArr {
        var asc = Int(char.unicodeScalars.first!.value)
        if asc <= 90 && asc >= 65 {
            countArr[asc - 65] += 1
        } else {
            countArr[asc - 71] += 1
        }
    }
    return countArr
}
```

### 풀이내용

조건을 대문자일 때와 소문자일 때를 나누어서 고려하였다. 이후 순서대로 배열에 저장하였다.

### 아쉬웠던 점

A는 65 a는 97 잊지말자....

### 다른 풀이

```Swift
import Foundation

func solution(_ my_string:String) -> [Int] {
    var answer = Array(repeating: 0, count: 52)
    my_string.forEach { answer[Int($0.asciiValue! - ($0.isUppercase ? 65 : 71))] += 1 }
    return answer
}
```

asciiValue!라는 함수를 사용하면 쉽게 풀 수 있다.
