# MVC(Model-View-Controller)패턴

MVC 패턴은 소프트웨어 개발에서 많이 사용됨(안드로이드 앱 개발에서도 많이 사용)
MVC 패턴은 3가지 주요 컴포넌트로 나누어 관리함
### Model
* 데이터와 데이터 관련 로직을 포함한 컴포넌트 임 (데이터는 앱의 핵심 데이터나 상태)
* 안드로이드 앱에서의 Model은 데이터베이스나 네트워크 요청 결과, 앱의 상태 등을 포함 가능'
* 주로 데이터를 가져오고 저장하며, 데이터의 유효서 검증을 가공

### View
* UI(User Interface)를 나타내고 화면에 데이터를 표시, 사용자 입력을 처리
* 안드로이등 앱에서는 xml레이아웃 파일로 정의 되거나 코드를 직접 생성(Jetpack Compose)될수 있음
* 주로 사용자에게 정보, Modle 의 상태를 표시, 사용자 입력을 받아 Controller에 전달
* xml 컴포넌트에 입력이 있을때 onClick 속성을 통하여 어떤 함수가 호출되어야하는지 정도 설정이 가능(실제 동작 처리 구현은 컨트롤러의 함수에서 이루어짐)

### Controller
* Model과 View의 중간 역할, 가교 역할을 수행.
  사용자 입력을 처리하고 Model 에서 데이터를 가져와 View에 전달
* 안드로이드 앱에서는 Activity나 Fragment임
* 사용자 상호작용 감지, 해당 이벤트 처리하여 Model과 View를 업데이트
* View가 사용자 입력을 받으면 Controller에 알림, Controller는 적절한 조치를 취하려고 동작함
* View와 연결되고 onClicklistener 등을 통해 입력을 입력받으면 처리할 동작을 구현

# MVP(Model-View-Presenter)

Controller 를 View 에서 정의하던 기존의 MVC 패턴과 다르게 Presenter가 그곳을 대신함

### Model 
* MVC 에서의 Model 과 동일한 역할을 함
* View 또는 Presenter 등 다른 어떤 요소에도 의존적이지 않은 독립적인 영역

### View 
* UI 를 담당하며 xml 과 Activity, Fragment 가 View 임. (MVC 에서의 Activity, Fragment 가 View 로 넘어옴)
* Model 에서 처리된 데이터를 Presenter 를 통해 받아서 유저에게 보여줌
* 사용자의 Action 및 액티비티/프래그먼트 상태 변경을 주시하며 Presenter 에게 보내는 역할
* View 는 사용자 입력 이벤트를 Presenter 에 전달하고 Presenter 에게 데이터를 표시하도록 요청 (Presenter 에 매우 의존적임)
  
### Presenter - MVP
* Model 과 View 사이의 매개체 역할
* Controller 처럼 View 에 직접 연결되어 상호작용하는 것이 아닌,  인터페이스와 연결
* 뷰에게 표시할 내용(데이터)만 전달함. 어떻게 보여줄 지는 View 가 담당 (View 가 인터페이스를 구현해서)
* Presenter 에서 비즈니스 로직이 처리










