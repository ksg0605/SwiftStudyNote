# Lv0: 세로 읽기

## 내 풀이

```Swift
import Foundation

func solution(_ my_string:String, _ m:Int, _ c:Int) -> String {
    var arr = ""
    my_string.enumerated().forEach{
        if m == 1 {
            arr = my_string
        }

        if ($0+1) % m == c {
            arr += String($1)
        }

        if m == my_string.count {
            arr = String(my_string[my_string.index(my_string.startIndex, offsetBy: c-1)])
        }
    }
    return arr
}
```

### 풀이내용

조건을 `my_string`을 `1로 나누는 경우`, `my_string의 크기로 나누는 경우`, `일반적인 경우` 총 세가지로 나누어서 풀이하였다.  
친절한 테스트케이스 덕분에 풀 수 있었다.
처음에는 나 자신으로 나누는 경우의 수를 생각하지 못해 18번 테스트케이스를 틀렸기 때문

### 아쉬웠던 점

항상 경우를 잘 나누기

### 다른 풀이

```Swift
func solution(_ myString: String, _ m: Int, _ c: Int) -> String {
    return myString.enumerated()
        .filter { $0.offset % m == c - 1 }
        .map { String($0.element) }
        .joined()
}
```

`offset, element` enumerated()를 사용하면 $0.0은 offset, $0.1은 element로 사용할 수 있다. 이 부분 한번 더 생각하기
