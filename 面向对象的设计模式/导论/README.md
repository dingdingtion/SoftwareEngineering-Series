# Design Pattern

Creational Based on the concept of creating an object.
Class
Factory Method This makes an instance of several derived classes based on interfaced data or events.
Object
Abstract Factory Creates an instance of several families of classes without detailing concrete classes.
Builder Separates object construction from its representation, always creates the same type of object.
Prototype A fully initialized instance used for copying or cloning.
Singleton A class with only a single instance with global access points.
Structural Based on the idea of building blocks of objects.
Class
Adapter Match interfaces of different classes therefore classes can work together despite incompatible interfaces.
Object
Adapter Match interfaces of different classes therefore classes can work together despite incompatible interfaces.
Bridge Separates an object's interface from its implementation so the two can vary independently.
Composite A structure of simple and composite objects which makes the total object more than just the sum of its parts.
Decorator Dynamically add alternate processing to objects.
Facade A single class that hides the complexity of an entire subsystem.
Flyweight A fine-grained instance used for efficient sharing of information that is contained elsewhere.
Proxy A place holder object representing the true object.

Behavioral Based on the way objects play and work together.
Class
Interpreter A way to include language elements in an application to match the grammar of the intended language.
Template
Method Creates the shell of an algorithm in a method, then defer the exact steps to a subclass.
Object
Chain of
Responsibility A way of passing a request between a chain of objects to find the object that can handle the request.
Command Encapsulate a command request as an object to enable, logging and/or queuing of requests, and provides error-handling for unhandled requests.
Iterator Sequentially access the elements of a collection without knowing the inner workings of the collection.
Mediator Defines simplified communication between classes to prevent a group of classes from referring explicitly to each other.
Memento Capture an object's internal state to be able to restore it later.
Observer A way of notifying change to a number of classes to ensure consistency between the classes.
State Alter an object's behavior when its state changes.
Strategy Encapsulates an algorithm inside a class separating the selection from the implementation.
Visitor Adds a new operation to a class without changing the class.

[Cohesion](<https://en.wikipedia.org/wiki/Cohesion_(computer_science)>) characterizes the degree to which the elements of a module (namespace, class, method, block of code) belong together. The measurement of the cohesion is usually described as _high cohesion_ or _low cohesion_.

High cohesion is preferable because it suggests to design the elements of the module to focus solely on a single task. It makes the module:

- _Focused_ and _understandable_: easier to understand what the module does
- _Maintainable_ and _easier to refactor_: the change in the module affects fewer modules
- _Reusable_: being focusing on a single task, it makes the module easier to reuse
- _Testable_: you would easier test a module that's focused on a single task

![Components coupling and cohesion](https://rainsoft.io/content/images/2017/03/CouplingVsCohesion.svg)

High cohesion accompanied with [loose coupling](https://en.wikipedia.org/wiki/Loose_coupling) is the characteristic of a well designed system.

A code block by itself might be considered a small module. To profit from the benefits of high cohesion, you need to keep the variables as close as possible to the code block that uses them.

For instance, if a variable solely exists to form the logic of a block scope, then declare and allow the variable to live only within that block (using `const` or `let`declarations). Do not expose this variable to the outer block scope, since the outer block shouldn't care about this variable.

One classic example of unnecessary extended life of variables is the usage of `for` cycle inside a function:

```
function someFunc(array) {
  var index, item, length = array.length;
  // some code...
  // some code...
  for (index = 0; index < length; index++) {
    item = array[index];
    // some code...
  }
  return 'some result';
}
```

`index`, `item` and `length` variables are declared at the beginning of function body. However they are used only near the end. So what is the problem with such approach?

All the way between the declaration at the top and the usage in `for` statement the variables `item`, `index`, `item` are uninitialized and exposed to `undefined`. They have a long lifecycle in the entire function scope that has no reason.

A better approach is to move these variables as close as possible to their usage place:

```
function someFunc(array) {
  // some code...
  // some code...
  const length = array.length;
  for (let index = 0; index < length; index++) {
    const item = array[index];
    // some
  }
  return 'some result';
}
```

`index` and `item` variables exist only in the block scope of `for` statement. They don't have any meaning outside of `for`.
`length` variable is declared close to the source of its usage too.

Why is the modified version better than the initial one? Let's see:

- The variables are not exposed to uninitialized state, thus you have no risk of accessing `undefined`
- Moving the variables as close as possible to their usage place increases the code readability
- High cohesive chunks of code are easier to refactor and extract into separated functions when necessary

设计模式(Design pattern)是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。 毫无疑问，设计模式于己于他人于系统都是多赢的，设计模式使代码编制真正工程化，设计模式是软件工程的基石，如同大厦的一块块砖石一样。项目中合理的运用设计模式可以完美的解决很多问题，每种模式在现在中都有相应的原理来与之对应，每一个模式描述了一个在我们周围不断重复发生的问题，以及该问题的核心解决方案，这也是它能被广泛应用的原因。设计模式的解释如下：

> Descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.

总体来说设计模式分为三大类：

创建型模式，共五种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。

结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。

行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。

其实还有两类：并发型模式和线程池模式。用一个图片来整体描述一下：

![](http://img.my.csdn.net/uploads/201211/29/1354152786_2930.jpg)

## Comparison

(1)Bridge 模式 的用意是"将抽象化(Abstraction)与实现化(Implementation)脱耦，使得二者可以独立地变化"，因此可以将算法的使用者完全与算法的具体实现相解耦。(2)Observer 模式定义对象间的一对多的依赖关系,当一个对象的状态发生改变时, 所有依赖于它的对象都得到通知并被自动更新。  
(3)Strategy 模式 定义一系列算法，把他们封装起来，并使他们可以互相替换。  
将策略加以封装为一个物件，而不是将策略写死在某个类中，如此一来，策略可以独立于客户端，随时增加变化、增加或减少策略，即使是修改每个策略的内容，也不会对客户端程式造成影响。  
(4)Mediator 模式 用一个中介对象来封装一系列关于对象交互行为。

## Reference

### Blogs

- [架构设计基础知识整理](https://blog.dreamtobe.cn/2016/10/25/oo_architecture/)

[23 种设计模式](http://www.cnblogs.com/beijiguangyong/archive/2010/11/15/2302807.html#_Toc281750469)

### Practices & Resources

- [java-design-patterns](https://github.com/iluwatar/java-design-patterns)

### Books

- [Graphic Design Patterns](http://design-patterns.readthedocs.org/zh_CN/latest/read_uml.html):图解设计模式

# 设计原则

# 类关系

请看以下这个类图，类之间的关系是我们需要关注的：

![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_class_struct.jpg)

- 车的类图结构为`<<abstract>>`，表示车是一个抽象类；
- 它有两个继承类：小汽车和自行车；它们之间的关系为实现关系，使用带空心箭头的虚线表示；
- 小汽车为与 SUV 之间也是继承关系，它们之间的关系为泛化关系，使用带空心箭头的实线表示；
- 小汽车与发动机之间是组合关系，使用带实心箭头的实线表示；
- 学生与班级之间是聚合关系，使用带空心箭头的实线表示；
- 学生与身份证之间为关联关系，使用一根实线表示；
- 学生上学需要用到自行车，与自行车是一种依赖关系，使用带箭头的虚线表示；

## 泛化关系(generalization)

类的继承结构表现在 UML 中为：泛化(generalize)与实现(realize)：继承关系为 is-a 的关系；两个对象之间如果可以用 is-a 来表示，就是继承关系：(..是..)。eg：自行车是车、猫是动物。泛化关系用一条带空心箭头的直接表示；如下图表示(A 继承自 B)；
![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_generalization.jpg)
eg：汽车在现实中有实现，可用汽车定义具体的对象；汽车与 SUV 之间为泛化关系；
![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_generalize.jpg)
注：最终代码中，泛化关系表现为继承非抽象类；

## 实现关系(realize)

实现关系用一条带空心箭头的虚线表示；eg：”车”为一个抽象概念，在现实中并无法直接用来定义对象；只有指明具体的子类(汽车还是自行车)，才 可以用来定义对象(”车”这个类在 C++中用抽象类表示，在 JAVA 中有接口这个概念，更容易理解)
![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_realize.jpg)

注：最终代码中，实现关系表现为继承抽象类；

## 聚合关系

聚合关系用一条带空心菱形箭头的直线表示，如下图表示 A 聚合到 B 上，或者说 B 由 A 组成；

![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_aggregation.jpg)

聚合关系用于表示实体对象之间的关系，表示整体由部分构成的语义；例如一个部门由多个员工组成；与组合关系不同的是，整体和部分不是强依赖的，即使整体不存在了，部分仍然存在；例如， 部门撤销了，人员不会消失，他们依然存在；

## 组合关系(composition)

组合关系用一条带实心菱形箭头直线表示，如下图表示 A 组成 B，或者 B 由 A 组成；

![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_composition.jpg)

与聚合关系一样，组合关系同样表示整体由部分构成的语义；比如公司由多个部门组成；但组合关系是一种强依赖的特殊聚合关系，如果整体不存在了，则部分也不存在了；例如， 公司不存在了，部门也将不存在了；

## 关联关系(association)

关联关系是用一条直线表示的；它描述不同类的对象之间的结构关系；它是一种静态关系， 通常与运行状态无关，一般由常识等因素决定的；它一般用来定义对象之间静态的、天然的结构； 所以，关联关系是一种“强关联”的关系；比如，乘车人和车票之间就是一种关联关系；学生和学校就是一种关联关系；关联关系默认不强调方向，表示对象间相互知道；如果特别强调方向，如下图，表示 A 知道 B，但 B 不知道 A；

![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_association.jpg)
注：在最终代码中，关联对象通常是以成员变量的形式实现的；

## 依赖关系(dependency)

依赖关系是用一套带箭头的虚线表示的；如下图表示 A 依赖于 B；他描述一个对象在运行期间会用到另一个对象的关系；
![](http://design-patterns.readthedocs.org/zh_CN/latest/_images/uml_dependency.jpg)
与关联关系不同的是，它是一种临时性的关系，通常在运行期间产生，并且随着运行时的变化； 依赖关系也可能发生变化；显然，依赖也有方向，双向依赖是一种非常糟糕的结构，我们总是应该保持单向依赖，杜绝双向依赖的产生；注：在最终代码中，依赖关系体现为类构造方法及类方法的传入参数，箭头的指向为调用关系；依赖关系处理临时知道对方外，还是“使用”对方的方法和属性；

# 设计模式

## 结构型模式

结构型模式(Structural Pattern)描述如何将类或者对 象结合在一起形成更大的结构，就像搭积木，可以通过 简单积木的组合形成复杂的、功能更为强大的结构。结构型模式可以分为类结构型模式和对象结构型模式：类结构型模式关心类的组合，由多个类可以组合成一个更大的系统，在类结构型模式中一般只存在继承关系和实现关系。 - 对象结构型模式关心类与对象的组合，通过关联关系使得在一 个类中定义另一个类的实例对象，然后通过该对象调用其方法。 根据“合成复用原则”，在系统中尽量使用关联关系来替代继 承关系，因此大部分结构型模式都是对象结构型模式。
