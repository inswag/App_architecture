## 앱 아키텍쳐(Application Architecture)
### Intro

<br>

Application Architecure 는 소프트웨어 디자인의 하나의 분야인데, 앱의 구조(Structure)와 관련이 있습니다. 더 구체적으로는 어플리케이션이 서로 다른 인터페이스(Different interfaces)와 층위(Conceptual layers)로 나누어지는 방법과, 이러한 여러 구성 요소들 사이에서 그리고 다른 구성 요소 내에서 서로 다른 작업이 수행하는 제어 흐름(Control flow)과 데이터 흐름 경로(Data flow paths)를 살펴보는 것입니다. 

<br>

예시로서 Apple 의 MVC(Model-View-Controller) 패턴은 3개의 계층(layer)을 설명하고 있습니다. 모델 계층, 뷰 계층, 컨트롤러 계층을 말합니다.

<br>

![MVC_Diagram](https://i.imgur.com/NFYdnX4.png)

<br>

위 그림의 도식(diagram) 안의 블록(block) 들은 패턴의 서로 다른 이름을 가진 계층(layer)을 보여주고 있어요. MVC 프로젝트에서 작성된 코드의 대부분은 이러한 계층(layer)들의 하나에 들어가게 됩니다. 화살표는 어떻게 층이 연결되어있는가를 보여주고 있구요.

<br>

그러나, 간단한 하나의 도식 블록은 패턴이 실제로 어떻게 작동할 것으로 예상되는지에 대해서는 설명하기가 힘듭니다. 앱 아키텍쳐는 얼만큼의 요소들(Components)이 구성될 지, 얼마나의 이벤트가 계층(layer)들을 통과할지, 요소들이 컴파일 혹은 런타입 시에 서로를 참조하고 있을지(혹은 아닐지), 서로 다른 요소들 내에서 얼마나의 데이터가 읽혀지거나 혹은 변형될지, 앱의 구조(Structure) 사이로 어떤 경로에서 상태 변화가 발생할지에 대한 수 많은 예상(expectation)들을 포함하고 있기 때문입니다.  

<br>

