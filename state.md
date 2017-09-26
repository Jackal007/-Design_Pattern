### State Pattern 状态模式

类的行为是基于它的状态改变的。属于**行为型模式**。

---

#### 意图

允许对象在内部状态发生改变时行为改变，对象看起来好像修改了它的类。

对象的行为依赖于它的状态（属性），并且可以根据它的状态改变而改变它的相关行为。

#### 适用性

何时使用：代码中包含大量与对象状态有关的条件语句。

#### 参与者

* ###### 环境\(Context\)角色，也称上下文：

  定义客户端所感兴趣的接口，并且保留一个具体状态类的实例。这个具体状态类的实例给出此环境对象的现有状态。

* ###### 抽象状态\(State\)角色：

  定义一个接口，用以封装环境（Context）对象的一个特定的状态所对应的行为。

* ###### 具体状态\(ConcreteState\)角色：

  每一个具体状态类都实现了环境（Context）的一个状态所对应的行为。

#### 效果

* ###### 优点：

  1. 封装了转换规则。 
  2. 枚举可能的状态，在枚举状态之前需要确定状态种类。 
  3. 将所有与某个状态有关的行为放到一个类中，并且可以方便地增加新的状态，只需要改变对象状态即可改变对象的行为。 
  4. 允许状态转换逻辑与状态对象合成一体，而不是某一个巨大的条件语句块。 
  5. 可以让多个环境对象共享一个状态对象，从而减少系统中对象的个数。
* ###### 缺点：

  1. 状态模式的使用必然会增加系统类和对象的个数。 
  2. 状态模式的结构与实现都较为复杂，如果使用不当将导致程序结构和代码的混乱。 
  3. 状态模式对"开闭原则"的支持并不太好，对于可以切换状态的状态模式，增加新的状态类需要修改那些负责状态转换的源代码，否则无法切换到新增状态，而且修改某个状态类的行为也需修改对应类的源代码。

#### 使用场景：

1. 行为随状态改变而改变的场景。 
2. 条件、分支语句的代替者。

* ###### 注意事项：

  在行为受状态约束的时候使用状态模式，而且状态不超过 5 个。

#### 实现

![](/assets/stTE.png)

```java
环境角色类

public class Context {
    //持有一个State类型的对象实例
    private State state;

    public void setState(State state) {
        this.state = state;
    }
    /**
     * 用户感兴趣的接口方法
     */
    public void request(String sampleParameter) {
        //转调state来处理
        state.handle(sampleParameter);
    }
}

　　抽象状态类


public interface State {
    /**
     * 状态对应的处理
     */
    public void handle(String sampleParameter);
}

　　具体状态类

public class ConcreteStateA implements State {

    @Override
    public void handle(String sampleParameter) {
        
        System.out.println("ConcreteStateA handle ：" + sampleParameter);
    }

}

public class ConcreteStateB implements State {

    @Override
    public void handle(String sampleParameter) {
        
        System.out.println("ConcreteStateB handle ：" + sampleParameter);
    }

}

　　客户端类

public class Client {

    public static void main(String[] args){
        //创建状态
        State state = new ConcreteStateB();
        //创建环境
        Context context = new Context();
        //将状态设置到环境中
        context.setState(state);
        //请求
        context.request("test");
    }
}
```



