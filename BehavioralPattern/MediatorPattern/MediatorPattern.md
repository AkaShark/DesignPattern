# 中介者模式

中介者模式 用一个中介对象来封装一系列对象的交互，中介者使各个对象不需要显示的相互引用，从而是的其耦合松散，而且可以独立的改变他们之前的交互。 通过中介者进行消息的转发**将原本网状结构变成以中介者为中心的星型结构**

尽管将一个系统分割成很多对象通常可以增加其复用性，但是对象间相互连接的激增又会降低其可复用性 大量的连接是的一个对象不可能在没有其他对象的支持下工作，系统表现为一个不可分割的整体，所以 对系统的行为进行任何比较大的改动就十分困难

## 使用场景

中介者模式一般应用于一组对象以定义良好但是复杂的方式进行通信的场合以及想制定一个分布在多个类中的行为，而又不想生成太多的子类的场合

## 优点

中介者模式很容易在系统中应用，也很容易在系统中误用，当系统出现多对多交互复杂的对象群的时候，不要急于使用中介者模式，而要先反思你的系统在设计上是不是合理

优点 中介者的出现减小各个关联对象之间的耦合，使得可以独立的修改对象复用对象，同时由于把对象如何协作进行了抽象，将中介者作为一个独立的概念并将其封装在一个对象中，这样关注的对象就从对象和各自本身的行为转移到了他们之间的交互上来，就站在了一个更加宏观的角度上看待问题

缺点 由于中介者类需要知道所有关联的对象，控制集中化，于是就把交互复杂性变成了中介者的复杂性，这就是的中介者变得很复杂不方便维护

## 模式动机

在用户与用户直接聊天的设计方案中，用户对象之间存在很强的关联性，将导致系统出现如下问题： 系统结构复杂：对象之间存在大量的相互关联和调用，若有一个对象发生变化，则需要跟踪和该对象关联的其他所有对象，并进行适当处理。 对象可重用性差：由于一个对象和其他对象具有很强的关联，若没有其他对象的支持，一个对象很难被另一个系统或模块重用，这些对象表现出来更像一个不可分割的整体，职责较为混乱。 系统扩展性低：增加一个新的对象需要在原有相关对象上增加引用，增加新的引用关系也需要调整原有对象，系统耦合度很高，对象操作很不灵活，扩展性差。 在面向对象的软件设计与开发过程中，根据“单一职责原则”，我们应该尽量将对象细化，使其只负责或呈现单一的职责。 对于一个模块，可能由很多对象构成，而且这些对象之间可能存在相互的引用，为了减少对象两两之间复杂的引用关系，使之成为一个松耦合的系统，我们需要使用中介者模式，这就是中介者模式的模式动机。

## 模式定义

中介者模式(Mediator Pattern)定义：用一个中介对象来封装一系列的对象交互，中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。中介者模式又称为调停者模式，它是一种对象行为型模式。

## 模式结构

角色

* Mediator: 抽象中介者
* ConcreteMediator: 具体中介者
* Colleague: 抽象同事类
* ConcreteColleague: 具体同事类

![](https://img-blog.csdnimg.cn/img\_convert/580f0feb22163e86925e19dd32c77b41.png) ![](https://img-blog.csdnimg.cn/img\_convert/ff6ce1be7a6dc4d50390411e5eb50ba2.png)

## 模式分析

中介者模式可以使对象之间的关系数量急剧减少 中介承担两个方面的职责:

* 中转作用(结构性): 通过中介者提供的中转作用，各个同时对象就不再需要显示引用其他同事，当需要和其他同事通信的时 候，通过中介者即可，该中转作用属于中介者在结构上的支持
* 协调作用(行为性): 中介者可以更进一步的对同事之间的关系进行封装，同事可以一致地和中介者进行交互，而不需要指明中 介者具体需要做什么，中介者根据封装在自身内部的协调逻辑，对同事请求进行进一步处理，将同事成员 之间的关系行为进行分离和封装。该协作作用属于中介者在行为上的支持。

某论坛系统欲增加一个虚拟聊天室，允许论坛会员通过该聊天室进行信息交流，普通会员(CommonMember)可以给其他会员发送文本信息，钻石会员(DiamondMember)既可以给其他会员发送文本信息，还可以发送图片信息。该聊天室可以对不雅字符进行过滤，如“日”等字符；还可以对发送的图片大小进行控制。用中介者模式设计该虚拟聊天室。

&#x20;![](https://img-blog.csdnimg.cn/img\_convert/b1b97ea3f60ba04f9aab519c18f3d694.png) ![](https://img-blog.csdnimg.cn/img\_convert/f52d2181160609e3bd43364b605bc98a.png)

## 模式优点

* 简化了对象之间的交互。(将复杂的交互封装到了中介者中)
* 将各同事解耦。
* 减少子类生成。
* 可以简化各同事类的设计和实现。(面向中介者编程)

## 模式缺点

在具体中介者类中包含了同事之间的交互细节，可能会导致具体中介者类非常复杂，使得系统难以维护。

## 适用环境

* 系统中对象之间存在复杂的引用关系，产生的相互依赖关系结构混乱且难以理解。
* 一个对象由于引用了其他很多对象并且直接和这些对象通信，导致难以复用该对象。
* 想通过一个中间类来封装多个类中的行为，而又不想生成太多的子类。可以通过引入中介者类来实现，在中介者中定义对象。
* 交互的公共行为，如果需要改变行为则可以增加新的中介者类。(过了文字 图片大小)

## 模式应用

MVC架构中控制器 Controller 作为一种中介者，它负责控制视图对象View和模型对象Model之间的交互。如在Struts中，Action就可以作为JSP页面与业务对象之间的中介者。

## 模式拓展

### 中介者模式与迪米特法则

在中介者模式中，通过创造出一个中介者对象，将系统中有关的对象所引用的其他对象数目减少到最少，使得一个对象与其同事之间的相互作用被这个对象与中介者对象之间的相互作用所取代。因此，中介者模式就是迪米特法则的一个典型应用。

### 中介者模式与GUI开发

中介者模式可以方便地应用于图形界面(GUI)开发中，在比较复杂的界面中可能存在多个界面组件之间的交互关系。 对于这些复杂的交互关系，有时候我们可以引入一个中介者类，将这些交互的组件作为具体的同事类，将它们之间的引用和控制关系交由中介者负责，在一定程度上简化系统的交互，这也是中介者模式的常见应用之一。

## 总结

* 中介者模式用一个中介对象来封装一系列的对象交互，中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。中介者模式又称为调停者模式，它是一种对象行为型模式。
* 中介者模式包含四个角色：抽象中介者用于定义一个接口，该接口用于与各同事对象之间的通信；具体中介者是抽象中介者的子类，通过协调各个同事对象来实现协作行为，了解并维护它的各个同事对象的引用；抽象同事类定义各同事的公有方法；具体同事类是抽象同事类的子类，每一个同事对象都引用一个中介者对象；每一个同事对象在需要和其他同事对象通信时，先与中介者通信，通过中介者来间接完成与其他同事类的通信；在具体同事类中实现了在抽象同事类中定义的方法。
* 通过引入中介者对象，可以将系统的网状结构变成以中介者为中心的星形结构，中介者承担了中转作用和协调作用。中介者类是中介者模式的核心，它对整个系统进行控制和协调，简化了对象之间的交互，还可以对对象间的交互进行进一步的控制。
* 中介者模式的主要优点在于简化了对象之间的交互，将各同事解耦，还可以减少子类生成，对于复杂的对象之间的交互，通过引入中介者，可以简化各同事类的设计和实现；中介者模式主要缺点在于具体中介者类中包含了同事之间的交互细节，可能会导致具体中介者类非常复杂，使得系统难以维护。
* 中介者模式适用情况包括：系统中对象之间存在复杂的引用关系，产生的相互依赖关系结构混乱且难以理解；一个对象由于引用了其他很多对象并且直接和这些对象通信，导致难以复用该对象；想通过一个中间类来封装多个类中的行为，而又不想生成太多的子类。
