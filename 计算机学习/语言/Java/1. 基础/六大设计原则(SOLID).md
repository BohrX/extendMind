#### 一、SOLID

**设计模式的六大原则有：**

-   Single Responsibility Principle：单一职责原则
-   Open Closed Principle：开闭原则
-   Liskov Substitution Principle：里氏替换原则
-   Law of Demeter：迪米特法则
-   Interface Segregation Principle：接口隔离原则
-   Dependence Inversion Principle：依赖倒置原则

把这六个原则的首字母联合起来（两个 L 算做一个）就是 SOLID （solid，稳定的），其代表的含义就是这六个原则结合使用的好处：建立稳定、灵活、健壮的设计。下面我们来分别看一下这六大设计原则。

#### 二、单一职责原则（Single Responsibility Principle）

一个类应该只有一个发生变化的原因

> There should never be more than one reason for a class to change.

[六大设计原则之单一职责原则（SRP）](https://www.jianshu.com/p/526a70f24ac5)

#### 三、开闭原则（Open Closed Principle）

一个软件实体，如类、模块和函数应该对扩展开放，对修改关闭

> Software entities like classes, modules and functions should be open for extension but closed for modification

[六大设计原则之开闭原则（OCP）](https://www.jianshu.com/p/55c3482d6e00)

#### 四、里氏替换原则（Liskov Substitution Principle）

所有引用基类的地方必须能透明地使用其子类的对象

> Functions that use use pointers or references to base classes must be able to use objects of derived classes without knowing it.

[六大设计原则之里氏替换原则（LSP）](https://www.jianshu.com/p/dfcdcd5d9ece)

#### 五、迪米特法则（Law of Demeter）

只与你的直接朋友交谈，不跟“陌生人”说话

> Talk only to your immediate friends and not to strangers

其含义是：如果两个软件实体无须直接通信，那么就不应当发生直接的相互调用，可以通过第三方转发该调用。其目的是降低类之间的耦合度，提高模块的相对独立性。

[六大设计原则之迪米特法则（LOD）](https://www.jianshu.com/p/98761ad06de6)

#### 六、接口隔离原则（Interface Segregation Principle）

1、客户端不应该依赖它不需要的接口。  
2、类间的依赖关系应该建立在最小的接口上。

> Clients should not be forced to depend upon interfaces that they don\`t use.  
> The dependency of one class to another one should depend on the smallest possible.

注：该原则中的接口，是一个泛泛而言的接口，不仅仅指Java中的接口，还包括其中的抽象类。

[六大设计原则之接口隔离原则（ISP）](https://www.jianshu.com/p/3232c9891403)

#### 七、依赖倒置原则（Dependence Inversion Principle）

1、上层模块不应该依赖底层模块，它们都应该依赖于抽象。  
2、抽象不应该依赖于细节，细节应该依赖于抽象。

> High level modules should not depend upon low level modules. Both should depend upon abstractions.  
> Abstractions should not depend upon details. Details should depend upon abstractions.

[依赖倒置原则(DIP)](https://www.jianshu.com/p/c3ce6762257c)
