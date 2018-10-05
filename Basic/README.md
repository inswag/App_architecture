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

### 여기까지 번역 완료.  아래는 공부는 되었지만 번역 중인 부분들.

<br>

* A good implementation of this design pattern in your application means that **each object falls into one of these groups**.

* The communication between View to Model through Controller can be best described with the following diagram:

(그림)

* The Model **notifies the Controller of any data changes**, and in turn, the Controller **updates the data in the Views**. The View **can then notify the Controller of actions the user** performed and the Controller **will either update the Model if necessary or retrieve any requested data**.

* You might be wondering why you can’t just ditch the Controller, and implement the View and Model in the same class, as that seems a lot easier.

* It all comes down to **code separation and reusability**. Ideally, the View should be completely separated from the Model. If the View doesn’t rely on a specific implementation of the Model, then it **can be reused with a different model to present some other data**.

* For example, if in the future you’d also like to add movies or books to your library, you **could still use the same AlbumView to display your movie and book objects**. Furthermore, if you **want to create a new project that has something to do with albums**, you could simply reuse your Album struct, because it’s not dependent on any view. That’s the strength of MVC!

<br>

## How to Use the MVC Pattern

* First, you need to ensure that **each class in your project is either a Controller, a Model or a View**; *don’t combine the functionality of two roles in one class*.

* Second, in order to ensure that you conform to this method of work **you should create three project groups to hold your code, one for each category**.

* Navigate to File\New\Group (or press on Command+Option+N) and **name the group Model**. *Repeat the same process to create View and Controller groups*.

* Now drag Album.swift to the Model group. Drag AlbumView.swift to the View group, and finally drag ViewController.swift to the Controller group.

(사진)

* Your project already looks a lot better without all those files floating around. Obviously you *can have other groups and classes*, but **the core of the application is contained in these three categories**.

* Now that your components are organized, you **need to get the album data from somewhere**. You’ll **create an API class to use throughout your code to manage the data** — which presents an opportunity to discuss your next design pattern — *the Singleton*.

## The Singleton Pattern

* The Singleton design pattern ensures that **only one instance exists for a given class and that there’s a global access point to that instance.** It usually uses **lazy loading to create the single instance when it’s needed the first time**.

> **Note** : Apple uses this approach a lot. For example: *UserDefaults.standard*, *UIApplication.shared*, *UIScreen.main*, *FileManager.default* all return a Singleton object.

* You’re likely wondering why you care if there’s more than one instance of a class floating around. Code and memory is cheap, right?

* There are some cases in which it makes sense to have exactly one instance of a class. For example, **there’s only one instance of your application and one main screen for the device, so you only want one instance of each. Or, take a global configuration handler class: it’s easier to implement a thread-safe access to a single shared resource, such as a configuration file, than to have many class modifying the configuration file possibly at the same time**.

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
