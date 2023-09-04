# 앱의 생명주기

## 뷰컨트롤러의 생명주기 - 1

### 앱의 생명주기 기초

- 게임 중 -> 전화 옴 -> 화면 전환 -> 게임은 잠시 비활성화 상태로
- 데이터는 저장이 안되서 날아갈 수도 있음
- 앱의 실행(메모리에 올라감)부터 -> 앱이 백그라운드로 / 앱의 종료까지를 포괄적으로 표현하는 개념
- 앱이 실행되서 앱이 종료 (메모리에 올라가서 내려가기 까지)의 주기가 존재
- **(상태 변화의) 해당시점에 호출되는 함수들이 있음**

### 뷰컨트롤러의 생명주기의 컨셉

- viewDidLoad(): 앱의 화면에 들어오면, 가장 먼저 실행시키는 함수
- 내부적인 매커니즘: 운영체제에 의해서, 자동으로 호출되는 함수들이 있음
- 앱의 실행 중 화면이 감춰졌다가(다음 화면으로 넘어갔다가), 화면이 다시 보이기도 함
- **(화면 전환의) 해당시점에 호출되는 함수들이 있음**

> **전체적인 시점이 중요하다**

1. 특정 화면에 진입
2. 뷰를 메모리에 올리는 과정 loadView 뷰를 바꿀 수 있는 시점 (코드베이스)
3. **시점 중요** 스토리보드 상의 뷰들과의 연결이 끝난 시점 viewDidLoad 뷰가 생성되었을 때 한번만 호출
4. 실제 스크린에 뷰가 나타나기 전에 호출 (유저 눈에 보이기 전에 할 수 있는 것들 ex, 화면설정 관련 코드) viewWillApear 뷰가 화면에 나타날때마다 계속 호출
5. 추가 매커니즘 존재
6. 실제 스크린에 뷰가 나타난 후에 호출 (ex, 애니메이션 시작, 타이머 앱의 초 시작...) viewDidAppear
7. 실제 스크린에 뷰가 사라지기 전에 호출 (ex, 애니메이션 멈춤, 타이머 앱 - 초 멈춤...) viewWillDisappear
8. 실제 스크린에 뷰가 사라진 후에 호출 viewDidDisappear (메모르에서 없어진 것은 아님)
9. 4 - 8 반복

```swift
import UIKit

class ViewController: UIViewController {
    // 스토리보드 뷰와 연결된 후 (한번만 호출): 코드와 스토리보드의 뷰가 연결된 후
    override func viewDidLoad() {
        super.viewDidLoad()
        print("VC-1 viewDidLoad 호출됨")
    }

    // 뷰가 나타나기 전
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        print("VC-1 viewWillAppear 호출됨")
    }

    // 뷰가 나타난 후
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        print("VC-1 viewDidAppear 호출됨")
    }

    // 뷰가 사라지기 전
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        print("VC-1 viewWillDisappear 호출됨")
    }

    // 뷰가 사라지기 전
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        print("VC-1 viewDidDisappear 호출됨")
    }

    deinit {
        print("VC-1 메모리에서 내려감")
    }

}

import UIKit

class SecondViewController: UIViewController {


    // 스토리보드 뷰와 연결된 후 (한번만 호출): 코드와 스토리보드의 뷰가 연결된 후
    override func viewDidLoad() {
        super.viewDidLoad()
        print("====VC-2 viewDidLoad 호출됨")
    }

    // 뷰가 나타나기 전
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        print("====VC-2 viewWillAppear 호출됨")
    }

    // 뷰가 나타난 후
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        print("====VC-2 viewDidAppear 호출됨")
    }

    // 뷰가 사라지기 전
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        print("====VC-2 viewWillDisappear 호출됨")
    }

    // 뷰가 사라지기 전
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        print("====VC-2 viewDidDisappear 호출됨")
    }

    @IBAction func backButtonTapped(_ sender: UIButton) {
        dismiss(animated: true, completion: nil)
    }


    deinit {
        print("====VC-2 메모리에서 내려감")
    }

}

```

### 내부 매커니즘의 이해

- 앱의 생명 주기: 앱의 비활성화 / 다른앱 또는 백그라운드로 전환 / 종료 시점을 파악하기 위함
- 뷰컨트롤러의 생명 주기: 하나의 앱에서 화면 전환 시점을 파악하기 위함
- Drawing 주기: 하나의 화면에서 애니메이션 등을 다시 그리는 시점 파악

### 앱의 생명주기 본론

> **AppDelegate.swift (아래 1~6이 반복됨)**
>
> 1. Not running: 앱의 실행 전
> 2. Inactive: iOS가 관리 - 외부적인 요인에 의해 잠시 거쳐가는 영역
> 3. Active: 앱이 실행 중 (예: 푸시 알림으로 인해 잠시 앱 컨트롤 불가)
>    2~3영역을 Foreground(화면을 점유 중)이라고 함
> 4. Background running: 제한적인 실행만 가능하도록 OS에서 통제 (예: 멜론 백그라운드 플레이)
>    4영역을 Background(화면을 점유하고 있지 않음)이라고 함
> 5. Suspended: 다음 실행을 기다림/대기 상태
> 6. OS가 메모리 부족 시점으로 관리해서 종료시킴
>
> **Not running을 제외하고 아직 메모리에 올라가 있는 상태**

AppDelegate / SceneDelegate가 분리 -> 멀티태스킹으로 인함

- 1, 5, 6은 Appdelegate로 구현
- 2~4는 SceneDelegate로 구현

### Drawing Cycle

> 필요한 경우 1초에 60번씩 아래 메소드들이 자동 호출
>
> - 개발자 코드
> - `setNeedsUpdateConstraints() / updateConstraintsIfNeeded()`
>   - 다음 사이클에 오토레이아웃 조정 해줘 / 0.016초 못기다리겠으니까 지금 당장 오토레이아웃 조정 해줘
> - `updateConstraints (자동호출)` 제약: 오토레이아웃 업데이트
>   - 현재 기기의 앱 화면크기 기준으로 제약을 업데이트하는 과정
> - 개발자 코드
> - `setNeedsLayout() / layoutIfNeeded()`
>   - 다음 사이클에 위치 or 크기 조정 해줘 / 0.016초 못기다리겠으니까 지금 당장 조정해줘
> - `layoutSubviews (자동호출)` 하위뷰 레이아웃: 위치, 크기 재조정
>   - 하위 뷰들의 위치/크기를 계산하고 배치하는 과정
> - `setNeedsDisplay()/ displayIfNeeded()`
>   - 다음 사이클에 그림 다시 그려줘 / 없음
> - `draw (자동호출)`
>   - 그리기: 실제 내부 컨텐츠 그리기
