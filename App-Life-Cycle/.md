# 앱의 현제 상태
언제든지 수행할수 있는 작업,수행할수 없는 작업을 결정

# 생명주기
앱이 처음 시작하고 종료되기 까지 앱이 가지는 상태와 그 상태들 사이의 전이를 뜻하고 앱이 어떤걸 할수있는가를 결정

# 앱의 생명주기(App's Life Cycle)
앱이 실행/종료 및 앱이 Background/Foreground에 있을 때, 시스템이 발생시키는 이벤트에 의해 앱의 상태가 전환되는 인련의 과정

# 앱의 상태
1. NotRunning
  * 시작되지 않았거나 종료되어 동작하지 않는 상태

2. Foreground-Inactive
  * Inactive 상태는 앱이 실행중인 상태지만 이벤트를 받아오지 못하는 상태로, 멀티테스킹 윈도우로 진입하거나 앱 실행중 전화, 알림 등의 이유로 앱 사용이 불가해지면 이상태로 돌입

3. Foreground-Active
  *  Active 상태는 실행되고 있는 상태로, 이벤트를 받아 상호작용이 가능한 상태임 바로 Active상태로 돌입은 안되고 Inactive 상태를 거쳐야지 Active 상태가 됨
    
4.  Background-Running
  * 다른 앱으로 전환되어 앱이 실질적인 동작을 하지 않는 상태로 앱을 사용하지 않는동안 서버와 데이터를 동기화 해야하때 이상태에서 실행

5.  Background-Suspended
  * 엡을 다시 실행했을떄 최근 작업으로 빠르게 로드 하기위해서 메모리 관련 데이터만 저장된 상태임( Background 상태에서 다른 작업 안하면 Suspended 상태로 진입)
  * Suspended의 앱은 iOS의 메모리가 부족해지면 먼저 메모리가 해제되서 종료한적이 없더라도 앱을 종료하고 다시 실행 시킨다.

# scene
앱을 새로 시작하고 scene을 요청하면 UIKit은 scene을 생성하고 unattached 상태로 설정함
사용자가 요청한 scene은 Foreground로 빠르게 이동하여 보여지며
시스템이 요청한 scene은 이벤트를 처리할 수 있도록 Background로 이동

## 1. 앱 실행
앱을 실행하면 화면을 보여주기 위한 준비가 끝난후 아래 메소드가 출력
```swift
application(_: didFinishLaunchingWithOptions:)

```

## 2. scene 연결
```swift
application(_:configurationForConnecting:options:)

* 새로운 scene 만들고 UIKit와 연결하기 위한 configuration 지정
* configuration은 scene을 연결하기 위한 정보가 들어있는 UISecneConfiguration 객체임

scene(_:willConnecTO:options: )

* scene이 연결될 것임을 delegate에 알려줌
* application(_:didFinishLaunchingWithOptions:)에서 했던 UIWindow 작업을 메소드로 가능

sceneDidBecomeActive(_:)

* 앱이 Inactive에서 Active 상태로 전환되었을때 호출

```

## 3. 앱 실행 후 홈 화면으로 나가면
앱 실행 후 홈 화면으로 나가면 Active - Inactive - Background 상태로 전환되는데 이떄
Scenedelegate는 scene 다음의 순서 대로 메소드들 호출
```swift
sceneWillResignActive(_:)

* 앱이 Active 상태에서 Inactive 상태로 전환할때 호출

sceneDidEnterBackground(_:)

* 앱이 Background 상태로 전환됬을때 호출

```

## 4. Background 상태에서 있는 앱을 다시 실행하면
Background 상태에 있는 앱을 다시 실행하면 Background - Inactive - Active 상태로 전환되는데 이때 SceneDelegate는 시스템에 다음 메소드를 출력하라고 요청

```swift
sceneWillEnterForeground(_:)

* 앱이 Background에서 Inactive로 상태 변환

sceneDidBecomeActive(_:)

* 앱이 Inactive에서 Active로 상태 전환

```

## 5. Scene 연결 해제
scene 사용시 Multi Window를 지원하지 않아 앱이 둘이 이상의 Scene Window를 가질 경우 swift-up 제스처는 앱을 종료하지 않고 scene에서 해제 시킴(모든 scene이 해제되면 앱 종료)

```swift
sceneDidDisconnected(_:)

* delegate에 UIKit에 연결된 scene의 연결 헤제할것을 요청

application(_: didDiscardSceneSessions :)

* 사용자가 멀티태스킹 창 (app Switcher)에 한개 이상의 scene룰 종료했을때 호출

applicationWillTerminate(_:)

* 앱이 사용자의 의해 종료될때 호출 (얘가차 못한 상황에서 종료될때는 호출 X)









