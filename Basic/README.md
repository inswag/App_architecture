# Swift를 활용한 iOS 디자인 패턴

### from raywenderlich.com

### iOS 디자인 패턴 ?

* 디자인 패턴(Design Pattern)은 무엇을 의미하는가 ?
* 디자인 패턴이라는 것은 **재사용가능(Reusable)한 솔루션(Solution)**이라고 할 수 있어요. 
* **소프트웨어 디자인**에서의 일반적인 문제들에 대한 솔루션이죠.
* 여러분이 이해하기 쉽고 재사용하기에도 쉬운 코드를 짜도록 돕기 위해 고안된 **템플릿**.
* 디자인 패턴은 또 여러분들이 루즈하게 결합된 코드를 만들어 내도록 도와줌으로서, 여러분들이 혼란스러워 하지 않으면서 여러분이 짠 코드의 구성요소들(components)을 변화(Change)시키거나 대체(Replace)할 수 있도록 해줍니다. 

* 여러분은 이미 Cocoa 가 구축된 방식 + 사용하도록 권장되는 최고의 수 많은 사례들 덕분에 수많은 iOS 디자인 패턴을 사용하고 있을지도 모릅니다. 

<br>

## MVC – '디자인 패턴계의 킹'

<br>

* *Model-View-Controller (MVC)* 패턴은 의심할바 없이 가장 많이 사용되는 디자인 패턴입니다. MVC 패턴은 객체(object)를 어플리케이션 내에서 가지는 **일반적 규칙(general role)**에 따라서 객체를 분류하고, 규칙에 기반한 코드의 **깔끔한 분리(clean separation)** 를 지향합니다.  

<br>

>* **모델(Model)** : 애플리케이션 데이터(Application Data)를 가지고 있으며 데이터를 처리하는 방법을 정의하고 있는 객체
>* **뷰(View)** : 모델(Model)의 **시각적 표현(Visual representation)**을 담당하고 있는 객체이자 기본적으로, 유저가 모든 UIView 에서 파생된 객체와 상호작용할 수 있는 **제어 장치(controls)** (The objects that are in charge of **the visual representation of the Model and the controls** the user can interact with; basically, all the UIView-derived objects)
>* **컨트롤러(Controller)** : 컨트롤러는 **모든 작업을 조정하는 중재인(mediator)**입니다. 컨트롤러는 모델로부터 데이터에 접근(access)하고 그것을 뷰와 함께 표시(display)하고, 이벤트(events)를 수신하고 데이터를 필요에 따라 처리합니다. 

<br>
