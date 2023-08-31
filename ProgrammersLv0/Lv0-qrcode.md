# Lv0: qr code

## 내 풀이

```Swift
import Foundation

func solution(_ q:Int, _ r:Int, _ code:String) -> String {
    var arr = [Character]()

    for i in 0..<code.count {
        if i % q == r {
           arr.append(code[code.index(code.startIndex, offsetBy: i)])
        }

    }

    return arr.map{String($0)}.joined()
}
```

### 풀이내용

조건에 맞는 문자를 for문으로 찾아 `arr: [Character]` 배열에 추가하고 `map`으로 `String`으로 변환 후 `joined()`로 합쳐주는 식으로 구현

### 아쉬웠던 점

for문을 고차함수로 구현했으면 더 좋지 않았을까?

### 다른 풀이

```Swift
func solution(_ q: Int, _ r: Int, _ code: String) -> String {
    return code.enumerated().filter { $0.offset % q == r }.map { String($0.element) }.joined()
}
```

`enumerated()`는 배열의 인덱스를 가져오는 함수로 (n, x)로 이루어진 쌍을 튜플 형태로 리턴  
n은 0부터 x까지의 연속적 숫자, x는 해당 요소의 순서
