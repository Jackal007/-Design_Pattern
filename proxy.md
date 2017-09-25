### Proxy  Pattern 代理模式

一个类代表另一个类的功能。属于**结构型模式**

在代理模式中，我们创建具有现有对象的对象，以便向外界提供功能接口。

---

#### 意图

一个客户不想或者不能够直接引用一个对象，而代理对象可以在客户端和目标对象之间起到中介的作用。

#### 适用性

* ##### 主要解决：

  在直接访问对象时带来的问题，比如说：要访问的对象在远程的机器上。在面向对象系统中，有些对象由于某些原因（比如对象创建开销很大，或者某些操作需要安全控制，或者需要进程外的访问），直接访问会给使用者或者系统结构带来很多麻烦，我们可以在访问此对象时加上一个对此对象的访问层。

* ##### 何时使用：

  想在访问一个类时做一些控制。

* ##### 如何解决：

  增加中间层。

#### 参与者

* ##### 抽象对象角色：

  声明了目标对象和代理对象的共同接口，这样一来在任何可以使用目标对象的地方都可以使用代理对象。
* ##### 目标对象角色：

  定义了代理对象所代表的目标对象。
* ##### 代理对象角色：

  代理对象内部含有目标对象的引用，从而可以在任何时候操作目标对象；代理对象提供一个与目标对象相同的接口，以便可以在任何时候替代目标对象。代理对象通常在客户端调用传递给目标对象之前或之后，执行某个操作，而不是单纯地将调用传递给目标对象。

#### 效果

* ##### 优点：

  * 职责清晰。 
  * 高扩展性。 
  * 智能化。 
* ##### 缺点：

  * 由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。
  * 实现代理模式需要额外的工作，有些代理模式的实现非常复杂。 
* ##### 注意事项：

  * 和适配器模式的区别：适配器模式主要改变所考虑对象的接口，而代理模式不能改变所代理类的接口。 
  * 和装饰器模式的区别：装饰器模式为了增强功能，而代理模式是为了加以控制。

#### 实现

我们将创建一个 Image 接口和实现了 Image 接口的实体类。ProxyImage 是一个代理类，减少 RealImage 对象加载的内存占用。  
ProxyPatternDemo，我们的演示类使用 ProxyImage 来获取要加载的 Image 对象，并按照需求进行显示。

![](/assets/xsddsd.png)

```java
抽象对象角色

public abstract class AbstractObject {
    //操作
    public abstract void operation();
}
　　目标对象角色

public class RealObject extends AbstractObject {
    @Override
    public void operation() {
        //一些操作
        System.out.println("一些操作");
    }
}

　　代理对象角色


public class ProxyObject extends AbstractObject{
    RealObject realObject = new RealObject();
    @Override
    public void operation() {
        //调用目标对象之前可以做相关操作
        System.out.println("before");        
        realObject.operation();        
        //调用目标对象之后可以做相关操作
        System.out.println("after");
    }
}

　　客户端


public class Client {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        AbstractObject obj = new ProxyObject();
        obj.operation();
    }

}
```



