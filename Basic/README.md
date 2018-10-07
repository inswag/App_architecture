# Swift를 활용한 iOS 디자인 패턴

### Ref. [Raywenderlich's iOS Design Pattern](https://www.raywenderlich.com/477-design-patterns-on-ios-using-swift-part-1-2)

### iOS 디자인 패턴 ?

* 디자인 패턴(Design Pattern)은 무엇을 의미하는가 ?
* 디자인 패턴 : **재사용가능(Reusable)한 솔루션(Solution)** 
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
>* **뷰(View)** : 모델(Model)의 **시각적 표현(Visual representation)**을 담당하고 있는 객체이자 기본적으로, 유저가 모든 UIView 에서 파생된 객체와 상호작용할 수 있는 **제어 장치(controls)** (원문 : The objects that are in charge of **the visual representation of the Model and the controls** the user can interact with; basically, all the UIView-derived objects)
>* **컨트롤러(Controller)** : 컨트롤러는 **모든 작업을 조정하는 중재인(mediator)**입니다. 컨트롤러는 모델로부터 데이터에 접근(access)하고 그것을 뷰와 함께 표시(display)하고, 이벤트(events)를 수신하고 데이터를 필요에 따라 처리합니다. 

<br>

* MVC 패턴을 여러분의 어플리케이션에서 잘 구현한다는 것은 무엇을 의미할까요? 바로 **각각의 객체(object)가 M-V-C 그룹 중 하나에 속하는 것입니다**

* 컨트롤러를 통해서 뷰와 모델이 통신하는 것은 다음 그림처럼 표현해 볼 수 있어요.

![MVC Diagram](https://i.imgur.com/IRc8Wh1.png)

* 모델은 **임의의 데이터의 변화를 컨트롤러에게 알려주고**, 반대로 **컨트롤러는 뷰에 데이터를 업데이트합니다**. 그리고 뷰는 **유저가 실행한 액션을 컨트롤러에게 알려주며**, 컨트롤러는 **만약 필요하다면 모델을 업데이트 할 것이거나, 혹은 어떤 요청된 데이터를 검색할(retrieve) 것입니다.**

* 여러분은 왜 컨트롤러를 버릴 수 없고 같은 클래스 내에 뷰와 모델을 구현할 수 없는지 궁금할 것입니다. 훨씬 그게 쉬어 보이는데 말이죠.

* 그것은 코드의 분리와 재사용성으로부터 나온다고 볼 수 있어요. 이상적으로는 뷰는 모델로부터 완전히 분리되어야 합니다. **만약 뷰가 특정 모델의 구현에 의존한다면, 몇몇의 다른 데이터를 표현하기 위해서 다른 모델과 함께 뷰가 재 사용될 수 없게 됩니다.**

<br>

## MVC 패턴 간단 사용법

<br>

* 첫째, 프로젝트 내에서 **각각의 클래스는 Controller 나 Model 이나 View 가 되도록 할 필요가 있습니다**. *하나의 클래스 안에 두 역할의 기능이 들어있지 않아야 합니다.* 

* 둘째, 3개의 프로젝트 그룹을 만들어야 합니다. 각각의 카테고리에 하나씩 여러분의 코드를 붙잡아 두기 위함이죠.

* 셋째, 각 그룹의 이름을 *Model*, *View*, *Controller* 로 지정해줍니다.

* 넷째, 각각의 폴더에 역할에 맞는 파일을 생성해줍니다.

* 다섯째, AppDelegate 파일, Asset 폴더, .plist, 스토리보드 파일은 그냥 두세요 ! 

* 애플리케이션의 핵심은 이 3개의 카테고리 안에 포함되어 있다고 보시면 됩니다.

<br>

## 싱글톤 패턴

<br>

* 싱글톤 디자인 패턴은 **해당 클래스에 오직 단 하나의 인스턴스만 존재하도록 보장해주며, 그 인스턴스에 대해 전역 접근 포인트(global access point)가 있도록 보장해줍니다**. 이 패턴은 일반적으로 **지연 로딩(lazy loading)을 사용하는데, 처음 필요할 때에 단 하나의 인스턴스를 생성하기 위함입니다**. 

<br>

**Ref. 전역 접근 지점(Global access point)** : 모든 클래스에서 접근해서 사용할 수 있게끔 싱글톤을 구현하였기 때문에, 전역 접근 지점이라고 할 수 있다.

<br>

**Ref. 지연 로딩(lazy loading)** : 필요한 순간에서 사용할 수 있도록, 메모리 상에 올리지 않고 있다가 사용하는 순간에 메모리에 올라갈 수 있도록 'lazy' 키워드를 변수 앞에 사용한다. 

<br>

> **주목** : 애플은 싱글톤을 많이 사용합니다. 예를 들면 *UserDefaults.standard*, *UIApplication.shared*, *UIScreen.main*, *FileManager.default* 까지 얘내 들은 모든 싱글톤 객체를 리턴하죠.

<br>

* Q. 왜 이렇게 해야할까요? 코드와 메모리가 비싼 것도 아닌닐텐데요.. 

* A. 좋은 질문입니다. 몇 가지 케이스가 있어요. 예를 들면 **여러분의 애플리케이션과 디바이스에 대한 하나의 메인 스크린에는 단지 하나의 인스턴스가 존재하죠. 그래서 여러분의 단지 각각에 대해 하나의 인스턴스만을 원하게 되는 거에요. 또 동시에 가능한 구성 파일을 많은 클래스가 수정하는 것보다, 단 하나의 공유된 리소스에 대해 *thread-safe* 한 접근을 구현하게 위함이죠. (멀티스레드 환경에서는 스레드간 충돌 문제가 일어날 수 있는데, 싱글톤 패턴을 활용하면 이러한 문제로부터 안전할 수 있어서 *thread-safe* 하다고 이야기 합니다.)**

<br>

## 싱글톤을 사용할 때, 주의할 점.

<br>

>* **주목** : 싱글톤 패턴은 주니어나 시니어나 관계 없이 과다 사용의 역사를 가지고 있습니다. 그래서 과다 사용의 예시를 많이 살펴보는 것은 중요합니다.

* **Singleton pattern 은 이 패턴의 남용에 매우 주의를 기울여야 합니다.**

* 여러분이 싱글톤을 사용할 유혹을 받는다면 먼저 다른 방법을 고려해보세요.

* 예를 들어, **하나의 뷰 컨트롤러에서 다른 뷰 컨트롤러로 단순히 정보를 보내려고 시도하는 경우에는 싱글톤은 부적절합니다. 대신에, 이니셜라이저나 프로퍼티를 통해 모델을 보내는 것을 고려해보세요**.

* 여러분이 만약 싱글톤이 필요하다고 결정했다면, **싱글톤이 정말 더 적절한 것인지 아닌지 고려해보세요.**

* Will having more than one instance **cause problems?** Will it ever be useful to have custom instances? Your answers will determine whether its better for you to use a true singleton or singleton plus.

* 싱글톤이 문제가 많은 가장 일반적인 이유는 **테스팅** 입니다. **전역 객체에 만약 상태가 저장되어 있는 경우(싱글톤처럼) 테스트 순서가 중요할 수 있으며**, 이를 무시하기에는 어렵습니다. 이러한 이유들은 테스팅을 고통스럽게 만들게 됩니다. 

* 마지막으로 'Code smell' 에 주의하세요. 여러분의 유스 케이스(Use case)가 싱글톤으로는 적합하지 않음을 나타냅니다. 예를 들어 **만약 여러분이 종종 많은 커스텀 인스턴스들을 필요로 한다면, 여러분의 유스 케이스는 아마도 일반 객체(regular object)로서 아마 더 나을 것입니다.** 

<br>

* **Ref. 유스케이스(Use case)**

>* 시스템 사이에서 교환되는 메시지의 중요도에 의해 클래스나 시스템에 제공되는 고유 기능 단위이며, 상호 행위자 밖의 하나 혹은 그 이상의 것이 시스템에 의해서 실행되는 행위를 함께 함
>* 시스템이 제공하는 서비스 혹은 기능
>* 시스템이 액터에게 제공하는 사용자 관점의 기능단위
>* 액터의 요청에 반응하여 원하는 처리를 수행하거나 정보를 제공
>* 액터와 한번 이상의 상호 작용을 통한 의미 있는 묶음의 시스템 행위
>* 의미 있는 자기완결형의 서비스 단위
>* 사용자관점에서의 정의가 필요 

<br>

* Ref. [**Definition of Code Smell** from wikipedia](https://ko.wikipedia.org/wiki/코드_스멜)

<br>

## 싱글톤 패턴 만드는 방법

<br>

* 오직 단 하나의 인스턴스를 갖는 싱글톤을 구현하기 위해서, 여러분은 **다른 누군가가 인스턴스를 만드는 것을 절대로 불가능하게 해야합니다**. 스위프트에서는 여러분에게 **private 키워드가 들어간 이니셜라이져**를 정의함으로서 이것을 가능하게 만들어 줍니다. 그리고 여러분은 **클래스 내에서 초기화되는 공유되는 인스턴스를 위한 정적(Static) 프로퍼티를 만들 수 있습니다**. 

* 여러분은 모든 데이터를 관리하기 위한 **싱글턴 클래스를 생성**함으로서 이 패턴을 구현할 것입니다.

* 맨 위의 참고 사이트의 튜토리얼을 통해서 여러분은 앨범을 관리하기 위한 시작 지점으로서 싱글톤 객체를 가지게 되었습니다. 튜토리얼을 통해, 여러분의 데이터의 지속성을 다루기 위해서 클래스를 생성하게 될 것입니다. 

* 과정 번역은 생략 !

<br>

## The Facade Design Pattern

* The Facade design pattern provides **a single interface(단일 인터페이스) to a complex subsystem(하위 시스템).** Instead of exposing the user to a set of classes and their APIs, **you only expose one simple unified API.**

* The following image explains this concept:

* 그림 (유저 -> API -> Remote Server / Database / File System / Memory)

* The user of the API is completely unaware of the complexity that lies beneath. This pattern is **ideal when working with a large number of classes, particularly when they are complicated to use or difficult to understand**.

* (번역 해야함) **The Facade pattern decouples the code that uses the system from the interface and implementation of the classes you’re hiding; it also reduces dependencies of outside code on the inner workings of your subsystem. This is als    o useful if the classes under the facade are likely to change, as the facade class can retain the same API while things change behind the scenes**.

* For example, if the day comes when you want to replace your backend service, **you won’t have to change the code that uses your API, just the code inside your Facade.**

### How to Use the Facade Pattern

* Currently you have *PersistencyManager* to save the album data locally and *HTTPClient* to handle the remote communication. The other classes in your project should not be aware of this logic, as they will be hiding behind the facade of *LibraryAPI.*

* To implement this pattern, only *LibraryAPI* should hold instances of *PersistencyManager* and *HTTPClient*. Then, *LibraryAPI* will expose a simple API to access those services.

* The design looks like the following:

* (그림 : [Other code] -> [LibraryAPI] ..

* *LibraryAPI* will be exposed to other code, but will hide the *HTTPClient* and *PersistencyManager* complexity from the rest of the app.

* Open LibraryAPI.swift and add the following constant properties to the class:

* *isOnline* determines **if the server should be updated** with any changes made to the albums list, such as added or deleted albums. The HTTP client **doesn’t actually work with a real server** and is only here to **demonstrate the usage of the facade pattern**, so isOnline will always be **false**.

* Next, add the following three methods to LibraryAPI.swift:

* ...

* Take a look at *addAlbum(_:at:)*. The class **first updates the data locally**, and then **if there’s an internet connection, it updates the remote server.** This is the **real strength of the Facade**; when some class outside of your system adds a new album, it(some class) doesn’t know — and doesn’t need to know — of **the complexity that lies underneath**.

>* **Note** : When designing a Facade for classes in your subsystem, (번역필요)remember that **unless you’re building a separate module and are using access control, nothing prevents the client from accessing these “hidden” classes directly**. Don’t be stingy with defensive code and don’t assume that all the clients will necessarily use your classes the same way the Facade uses them.

* Build and run your app. You’ll see two empty views, and a toolbar. The top view will be used to display your album covers, and the bottom view will be used to display a table of information related to that album.

## The Decorator Design Pattern

* The Decorator pattern **dynamically adds behaviors and responsibilities to an object without modifying its code**. It’s an **alternative to subclassing where you modify a class’s behavior by wrapping it with another object**.

* In Swift there are two very common implementations of this pattern: **Extensions** and **Delegation**.

### Extensions

* Adding **extensions is an extremely powerful mechanism** that allows you to add new functionality to existing classes, structures or enumeration types without having to subclass. What’s also really awesome is you can extend code you don’t have access to, and enhance their functionality. **That means you can add your own methods to Cocoa classes** such as *UIView* and *UIImage* !

* Swift extensions are slightly different from the classic definition of a decorator, because **a extension doesn’t hold an instance of the class it extends**.

### How to Use Extensions

* Imagine a situation in which you have an *Album* instance that you want to present inside a table view:

* (그림)

* Where will the album titles come from? *Album* is a Model, so it doesn’t care how you present the data. You’ll **need some external code to add this functionality to the Album struct**.

* You’ll create a extension of the *Album* struct; it will define a new method that returns a data structure which can be used easily with *UITableView*.

* Go to Album.swift and add the following code at the end of the file:

* (그림)

* This typealias defines a tuple which contains **all of the information** that the table view needs to display **a row of data**. Now add the following extension to access this information:

* (그림)

* An array of AlbumData will be much easier to display in a table view!

<br>

> **Note** : Classes can of course **override a superclass’s method, but with extensions you can’t**. Methods or properties in an extension **cannot have the same name as methods or properties in the original class**.

<br>

* Consider for a moment how powerful this pattern can be:

* You’re using properties **directly** from Album.
* You have added to the Album struct **but you haven’t modified it.**
* This simple addition lets you return a *UITableView*–ish representation of an *Album*.

### Delegation 

* The other implementation of the Decorator design pattern, **Delegation**, is a mechanism in which one object acts on behalf of(~을 대신하여), or in coordination with(~와 합동하여), another object. UITableView is greedy(욕심쟁이) – it has two delegate-type properties, one called **a data source**, and one called **a delegate**. They do slightly different things – for example, the table view asks its data source **how many rows should be in a particular section, but it asks its delegate what to do when a row is selected.**

* You can’t expect the UITableView to know how many rows you want to have in each section, as this is application-specific. Therefore, the task of calculating the amount of rows in each section is passed on to the data source. This allows the UITableView class to be independent of the data it displays.
