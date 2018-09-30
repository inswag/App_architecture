## 앱 아키텍쳐(Application Architecture)

<br>

Application Architecure 는 소프트웨어 디자인의 하나의 분야인데, 앱의 구조(Structure)와 관련이 있습니다. 더 구체적으로는 어플리케이션이 서로 다른 인터페이스(Different interfaces)와 층위(Conceptual layers)로 나누어지는 방법과, 이러한 여러 구성 요소들 사이에서 그리고 다른 구성 요소 내에서 서로 다른 작업이 수행하는 제어 흐름(Control flow)과 데이터 흐름 경로(Data flow paths)를 살펴보는 것입니다. 

<br>

예시로서 Apple 의 MVC(Model-View-Controller) 패턴은 3개의 계층(layer)을 설명하고 있습니다. 모델 계층, 뷰 계층, 컨트롤러 계층을 말합니다.

<br>

![MVC_Diagram](https://i.imgur.com/NFYdnX4.png)

<br>

위 그림의 도식(diagram) 안의 블록(block)들은 패턴의 서로 다른 이름을 가진 계층(layer)을 보여주고 있어요. MVC 프로젝트에서 작성된 코드의 대부분은 이러한 계층(layer)들의 하나에 들어가게 됩니다. 화살표는 어떻게 계층들이 연결되어있는가를 보여주고 있구요.

<br>

그러나, 간단한 하나의 도식 블록은 패턴이 실제로 어떻게 작동할 것으로 예상되는지에 대해서는 설명하기가 힘듭니다. 앱 아키텍쳐는 얼마 만큼의 요소들(Components)이 구성될 지, 얼마나의 이벤트가 계층(layer)들을 통과할지, 요소들이 컴파일 혹은 런타임 시에 서로를 참조하고 있을지(혹은 아닐지), 서로 다른 요소들 내에서 얼마나의 데이터가 읽혀지거나 혹은 변형될지, 앱의 구조(Structure) 사이로 어떤 경로에서 상태 변화가 발생할지에 대한 수 많은 예상(expectation)들을 포함하고 있기 때문입니다.  

<br>

## 모델과 뷰(Model and View)

<br>

가장 상위의 레벨에서, 앱 아키텍쳐는 서로 다른 요소(components)들이 나누어지는 카테고리(categories)의 기초적인 세트(basic set)라 할 수 있다. 여기서는 이러한 서로 다른 범주들을 *계층(layers)* 이라 부르기로 하겠습니다. 즉, 계층이란 몇 가지 기초적인 규칙과 책임을 따르고 있는 인터페이스들의 모음(collection) 및 기타 코드(other code)를 말합니다.

<br>

이 카테고리 중 가장 일반적인 것은 Model 계층과 View 계층 이죠.

<br>

*Model 계층* 은 어떠한 앱 프레임워크(예를 들면 UIKit)에도 의존하지 않는 어플리케이션 내용의 추상적 표현이라 할 수 있습니다. 그러므로 Model 계층은 프로그래머에게 전체적인 제어 권한을 부여합니다. Model 계층은 전형적으로 Model 객체(앞서 봤던 녹음 앱의 예시로 본다면, 폴더와 기록물을 포함한다)와 그리고 조정(coordinating) 객체(예를들면, 디스크 상에서 데이터를 계속해서 유지하는 객체) 둘 다 포함하고 있다. 디스크에서 유지(persisted)되는 Model 부분을 *문서 모델(document model)* 이라고 부릅니다.

<br>

*View 계층* 은 Model 계층을 어플리케이션으로 바꿈으로서 Model 계층을 가시적(visible)으로 만들고, 유저가 상호작용을 할 수 있도록 만드는 애플리케이션 프레임워크에 종속된(application framework-dependent) 부분이라 할 수 있어요. iOS 앱을 작성할 때, View 계층은 대부분의 경우에 항상 직접 UIKit 을 사용합니다. 하지만, 일부 아키텍쳐는 UIKit 을 둘러싸고 있는 다른 View 계층을 가지는데, 곧 보도록 살펴보도록 하죠. 그리고 일부 커스텀 앱에서(특히나 게임), View 계층은 UIKit 이나 AppKit 이 아닐 수 있어요. 그것은 SceneKit 또는 OpenGL 과 관련된 것이죠.

<br>

때때로, 모델 혹은 뷰 인스턴스들은 객체(Object)라기 보다는 오히려 구조체(structs)나 열거형(enums)으로 대표됩니다. 실제로 중요한건 차이점. 하지만 우리가 객체나, 구조체나, 열거형을 model 계층 내에서 이야기할 때, 우리는 이것들을 *모델 객체(model objects)* 라 부를 것입니다. 또한 객체, 구조체, 열거형을 view 계층 안에서 이야기할 때도 *뷰 객체(view objects)* 라 일컫는 것도 마찬가지 입니다.

<br>

뷰 객체들(View objects)은 일반적으로 단일 *뷰 계층* 을 형성합니다. 계층 내에는 모든 객체가 트리 구조로 연결되어 있습니다. in a tree structure with the screen at the trunk, windows within the screen, and increasingly smaller views at the branches and leaves. 한편, 뷰 컨트롤러들은 일반적으로 *뷰 컨트롤러 계층구조* 를 이룬다. 그 동안, 모델 객체들은 반드시 계층구조를 이루지는 않는다. 이 말은 모댈 객체들간의 연결을 가지고 있지 않은 프로그램 내의 모델들이 있을 수 있다는 것이다(there could be models in the program with no connection between them).

<br>

우리가 *뷰(view)* 를 작성할 때, 그 뷰는 단일 뷰 객체(Button 또는 label과 같은)를 의미해요. 우리가 *모델(model)* 을 작성할 땐, 그 모델은 단일 모델 객체(앞서 살펴본 앱에서, Recording 혹은 Folder 인스턴스)를 말하죠. 다루고 있는 주제(Model and View)에 대한 대부분의 문헌에서, "모델"은 문맥(Context)에 따라 의미가 달라집니다. 이것은 model 층을 의미한다. It could mean the model layer, the concrete objects that are in the model layer, the document model, or a discrete document within the model layer. 장황하더라도, 여기에서는 다른 의미들에 대해 명쾌하게 나타내고자 한다.

<br>

### Model 과 View 의 카테고리는 왜 근본적인 것으로 간주되는가 ?

<br>

모델 계층과 뷰 계층 둘 사이의 분리가 없는 애플리케이션을 작성하는 것은 분명 가능합니다. 예를 들면, 단순한 모달 대화 상자(modal dialog)에서, 별도의 모델 데이터(model data)가 없는 경우가 자주 있습니다. 대신에, "OK" 버튼을 탭했을 때, 유저 인터페이스 요소로부터 직접 상태를 읽어냅니다. 그럼에도 불구하고, 일반적으로 분리된 모델 계층 없이는 프로그램의 액션이 일관된 규칙에 따라 발생하도록 보증하는 것은 어렵습니다. 

<br> 

모델 계층을 정의하는 가장 중요한 이유는 우리 프로그램 안에서, 클린(Clean)하면서 잘 작동되고(Well behaved), 애플리케이션 프레임워크의 구현 세부 사항에 의해 통제되지 않는(not governed) 유니크한 진실의 소스(single source of truth)를 가지기 위함입니다. 

<br>

*애플리케이션 프레임워크(Application Framework)* 는 우리가 애플리케이션을 빌드 할 수 있는 토대(infrastructure)를 제공합니다. 여기서는, Cocoa(타겟 플랫폼에 따라서 UIKit, AppKit, WatchKit 과 같은 것들)를 애플리케이션 프레임워크로 사용합니다. 

<br>

만약 모델 계층이 애플리케이션 프레임워크로부터 분리되어 유지된다면, 우리는 모델 계층을 어플리케이션의 한계(bounds) 밖에서도 완전하게 사용할 수 있습니다. 우리는 쉽게 그것을 분리된 테스트 하네스 안에서 실행할 수 있거나, 우리는 새로운 뷰 계층을 다른 애플리케이션 프레임워크를 사용하여 작성하고 그리고 모델 계층을 타 OS의 애플리케이션에서도 사용할 수 있습니다. 

<br>

* 테스트 하네스(Testing Harness) 란?

<br>

시스템 및 시스템 컴포넌트를 시험하는 환경의 일부분으로 시험을 지원하는 목적하에 생성된 코드와 데이터. 시험 드라이버 (test driver)라고도 하며 일반적으로 단위 시험이나 모듈 시험에 사용하기 위해 코드 개발자가 만든다. 단순히 시험을 위한 사용자 인터페이스를 제공하거나 정교하게 제작된 경우, 코드가 변경되었을 때에도 항상 같은 결과를 제공하여 시험을 자동화시킬 수 있도록 디자인되어 있다.

<br>
