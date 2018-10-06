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

MVC 패턴을 여러분의 어플리케이션에서 잘 구현한다는 것은 무엇을 의미할까요? 바로 **각각의 객체(object)가 M-V-C 그룹 중 하나에 속하는 것입니다**

* 컨트롤러를 통해서 뷰와 모델이 통신하는 것은 다음 그림처럼 표현해 볼 수 있어요.

![MVC Diagram](https://i.imgur.com/IRc8Wh1.png)

* 모델은 **임의의 데이터의 변화를 컨트롤러에게 알려주고**, 반대로 **컨트롤러는 뷰에 데이터를 업데이트합니다**. 그리고 뷰는 **유저가 실행한 액션을 컨트롤러에게 알려주며**, 컨트롤러는 **만약 필요하다면 모델을 업데이트 할 것이거나, 혹은 어떤 요청된 데이터를 검색할(retrieve) 것입니다.**

* 여러분은 왜 컨트롤러를 버릴 수 없고 같은 클래스 내에 뷰와 모델을 구현할 수 없는지 궁금할 것입니다. 훨씬 그게 쉬어 보이는데 말이죠.

* 그것은 코드의 분리와 재사용성으로부터 나온다고 볼 수 있어요. 이상적으로는 뷰는 모델로부터 완전히 분리되어야 합니다. **만약 뷰가 특정 모델의 구현에 의존한다면, 몇몇의 다른 데이터를 표현하기 위해서 다른 모델과 함께 뷰가 재 사용될 수 없게 됩니다.**

<br>

## MVC 패턴 간단 사용법

<br>

* 프로젝트 내에서 **각각의 클래스는 Controller 나 Model 이나 View 가 되도록 할 필요가 있습니다**. *하나의 클래스 안에 두 역할의 기능이 들어있지 않아야 합니다.* 

* 3개의 프로젝트 그룹을 만들어야 합니다. 각각의 카테고리에 하나씩 여러분의 코드를 붙잡아 두기 위함이죠.

* 각 그룹의 이름을 *Model*, *View*, *Controller* 로 지정해줍니다.

* 각각의 폴더에 역할에 맞는 파일을 생성해줍니다.

* AppDelegate 파일, Asset 폴더, .plist, 스토리보드 파일은 그냥 두세요 ! 

* 애플리케이션의 핵심은 이 3개의 카테고리 안에 포함되어 있다고 보시면 됩니다.

<br>

### 여기까지 번역 완료.  아래는 공부는 되었지만 번역 중인 부분들.

<br>

## 싱글톤 패턴

<br>

* 싱글톤 디자인 패턴은 **해당 클래스에 오직 단 하나의 인스턴스만 존재하도록 보장해주며, 그 인스턴스에 대해 전역 접근 포인트(global access point)가 있도록 보장해줍니다**. 이 패턴은 일반적으로 **지연 로딩(lazy loading)을 사용하는데, 처음 필요할 때에 단 하나의 인스턴스를 생성하기 위함입니다**. 

<br>

> **주목** : 애플은 이러한 접근을 많이도 사용해요. 예를 들면 *UserDefaults.standard*, *UIApplication.shared*, *UIScreen.main*, *FileManager.default* 까지 얘내 들은 모든 싱글턴 객체를 리턴하죠.

<br>

* 왜 이렇게 해야할까요? 코드와 메모리가 비싼 것도 아닌데요...

* 좋은 질문입니다. 몇 가지 케이스가 있어요. 예를 들면 **여러분의 애플리케이션과 디바이스에 대한 하나의 메인 스크린에는 단지 하나의 인스턴스가 존재하죠. 그래서 여러분의 단지 각각에 대해 하나의 인스턴스만을 원하게 되는 거에요. 또 동시에 가능한 구성 파일을 많은 클래스가 수정하는 것보다, 단 하나의 공유된 리소스에 대해 *thread-safe* 한 접근을 구현하게 위함이죠. (멀티스레드 환경에서는 스레드간 충돌 문제가 일어날 수 있는데, 싱글톤 패턴을 활용하면 이러한 문제로부터 안전할 수 있어서 *thread-safe* 하다고 이야기 합니다.)**

<br>

## What Should You Be Careful About?

<br>

>* **Note from Ray**: This pattern has a history of **being overused (or otherwise misused)** by both beginner and experienced developers, so we are including this brief excerpt from our book Design Patterns by Tutorials by Joshua Greene that explains some things to be careful about with this pattern.

* **The singleton pattern is very easy to overuse.**

* If you encounter(접하다) a situation where you’re tempted to use a singleton, first consider other ways to accomplish your task.

* For example, singletons are **not appropriate if you’re simply trying to pass information from one view controller to another.** Instead, **consider passing models via an initializer or property.**

* If you determine you actually do need a singleton, **consider whether a singleton plus makes more sense**.

* Will having more than one instance **cause problems?** Will it ever be useful to have custom instances? Your answers will determine whether its better for you to use a true singleton or singleton plus.

* The most common reason why singleton’s are problematic is **testing**. If you have **state being stored in a global object like a singleton then order of tests can matter**, and it can be painful to mock them. Both of these reasons make **testing a pain**.

* Lastly, beware of “code smell”, indicating your use case isn’t appropriate as a singleton at all. For example, **if you often need many custom instances, your use case may be better as a regular object.**

<br>

> **Code Smell ** : Anything in a program's source code that suggests the presence of a design problem.

<br>

## How to Use the Singleton Pattern

<br>

* To ensure there is only one instance of your singleton, you **must make it impossible for anyone else to make an instance**. Swift allows you to do this by marking the **initializers as private**. You can then add **a static property for the shared instance, which is initialized inside the class**.

* You’ll implement this pattern by creating a singleton class to manage all the album data.

* You’ll notice there’s a group called API in the project; this is where you’ll put all the classes that will provide services to your app. Create a new file inside this group by right-clicking the group and selecting New File. Select iOS > Swift File. Set the file name to LibraryAPI.swift and click Create.

* Xcode 프로젝트에 코드 구현(LibraryAPI.swift)

* You now have a Singleton object as the entry point to manage the albums. Take it a step further and create a class to handle the persistence of your library data.

* Now within the group API create a new file. Select iOS > Swift File. Set the class name to PersistencyManager.swift and click Create.
Open PersistencyManager.swift and add the following code.

* Xcode 프로젝트에 코드 구현(PersistencyManager.swift)

* These methods allow you to **get, add, and delete albums.**

* Build your project just to make sure everything still compiles correctly.

* At this point, you might wonder where the *PersistencyManager* class comes in since it’s not a Singleton. You’ll see the relationship between *LibraryAPI* and *PersistencyManager* in the next section where you’ll look at the **Facade** design pattern.

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
