**状态模式(State Pattern)——处理对象的多种状态及其相互转换**

说明：设计模式系列文章是读`刘伟`所著`《设计模式的艺术之道(软件开发人员内功修炼之道)》`一书的阅读笔记。个人感觉这本书讲的不错，有兴趣推荐读一读。详细内容也可以看看此书作者的博客`https://blog.csdn.net/LoveLion/article/details/17517213`。

## 模式概述

很多事物都具有多种状态，而且在不同状态下会具有不同的行为，这些状态在特定条件下还将发生相互转换。就像水，它可以凝固成冰，也可以受热蒸发后变成水蒸汽，水可以流动，冰可以雕刻，蒸汽可以扩散。

在软件系统中，有些对象也像水一样具有多种状态，这些状态在某些情况下能够相互转换，而且对象在不同的状态下也将具有不同的行为。为了更好地对这些具有多种状态的对象进行设计，可以使用一种被称之为状态模式的设计模式——处理对象的多种状态及其相互转换。

在状态模式中，将对象在每一个状态下的行为和状态转移语句封装在一个个状态类中，通过这些状态类来分散冗长的条件转移语句，让系统具有更好的灵活性和可扩展性。

### 模式定义

状态模式用于解决系统中复杂对象的状态转换以及不同状态下行为的封装问题。当系统中某个对象存在多个状态，这些状态之间可以进行转换，而且对象在不同状态下行为不相同时可以使用状态模式。状态模式将一个对象的状态从该对象中分离出来，封装到专门的状态类中，使得对象状态可以灵活变化，对于客户端而言，无须关心对象状态的转换以及对象所处的当前状态，无论对于何种状态的对象，客户端都可以一致处理。

状态模式定义如下：

> 状态模式(`State Pattern`)：允许一个对象在其内部状态改变时改变它的行为，对象看起来似乎修改了它的类。其别名为状态对象(`Objects for States`)，状态模式是一种对象行为型模式。

### 模式结构图

在状态模式中引入了抽象状态类和具体状态类，它们是状态模式的核心，其结构如下图所示：

![](https://img2020.cnblogs.com/blog/1546632/202112/1546632-20211229165107031-621190878.png)

### 模式伪代码

抽象状态类典型代码如下：

```java
/**
 * 抽象状态
 */
public interface State {

    /**
     * 抽象状态行为1
     */
    void action1();

    /**
     * 抽象状态行为2
     */
    void action2();
}
```

不同的具体状态类可以提供不同的实现，如下：

```java
public class ConcreteState implements State {

    @Override
    public void action1() {
        // 具体实现
    }

    @Override
    public void action2() {
        // 具体实现
    }
}
```

环境类维持一个对抽象状态类的引用，代码大致如下：

```java
public class Context {

    // 抽象状态
    private State state;

    // 该属性值的变化可能会导致对象状态发生变化
    private int value;

    public void setState(State state) {
        this.state = state;
    }

    /**
     * 状态变化
     */
    public void changeState() {
        //判断属性值，根据属性值进行状态转换
        if (value == 0) {
            this.setState(new ConcreteState());
        } else if (value == 1) {
            // this.setState(new ConcreteStateB());
        } else {
            // ...
        }
    }
    
    /**
     * 具体业务逻辑
     */
    public void service() {
        // ...
        // 状态行为1
        this.state.action1();
        // 状态行为2
        this.state.action2();
        // ...
    }
}
```


## 模式应用

待完善。

## 模式总结

状态模式将一个对象在不同状态下的不同行为封装在一个个状态类中，通过设置不同的状态对象可以让环境对象拥有不同的行为，而状态转换的细节对于客户端而言是透明的，方便了客户端的使用。

在实际开发中，状态模式具有较高的使用频率，在工作流和游戏开发中状态模式都得到了广泛的应用，例如公文状态的转换、游戏中角色的升级等。


### 主要优点

状态模式可以避免使用庞大的条件语句来将业务方法和状态转换代码交织在一起。

### 适用场景

- 对象的行为依赖于它的状态（如某些属性值），状态的改变将导致行为的变化。
- 在代码中包含大量与对象状态有关的条件语句，这些条件语句的出现，会导致代码的可维护性和灵活性变差，不能方便地增加和删除状态，并且导致客户类与类库之间的耦合增强。
