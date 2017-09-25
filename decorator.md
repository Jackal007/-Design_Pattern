### Decorator Pattern 装饰器模式

又名包装\(Wrapper\)模式

允许向一个现有的对象添加新的功能，同时又不改变其结构。

属于**结构型模式**，它是作为现有的类的一个包装。

---

#### 意图

动态地给一个对象添加一些额外的职责。就增加功能来说，装饰器模式相比生成子类更为灵活。

这种模式创建了一个装饰类，用来包装原有的类，并在保持类方法签名完整性的前提下，提供了额外的功能。

#### 适用性

一般的，我们为了扩展一个类经常使用继承方式实现，由于继承为类引入静态特征，并且随着扩展功能的增多，子类会很膨胀。

在不想增加很多子类的情况下扩展类。

#### 参与者

* ##### 抽象构件\(Component\)角色：

  给出一个抽象接口，以规范准备接收附加责任的对象。

* ##### 具体构件\(ConcreteComponent\)角色：

  定义一个将要接收附加责任的类。

* ##### 装饰\(Decorator\)角色

  持有一个构件\(Component\)对象的实例，并定义一个与抽象构件接口一致的接口。

* ##### 具体装饰\(ConcreteDecorator\)角色：

  负责给构件对象“贴上”附加的责任。

#### 效果

* ##### 优点：

  装饰类和被装饰类可以独立发展，不会相互耦合，装饰模式是继承的一个替代模式，装饰模式可以动态扩展一个实现类的功能。

* ##### 缺点：

  多层装饰比较复杂。

* ##### 使用场景：

  1. 扩展一个类的功能。 
  2. 动态增加功能，动态撤销。
* ##### 注意事项：

  可代替继承。

#### 实现

我们将创建一个 Shape 接口和实现了 Shape 接口的实体类。然后我们创建一个实现了 Shape 接口的抽象装饰类 ShapeDecorator，并把 Shape 对象作为它的实例变量。

RedShapeDecorator 是实现了 ShapeDecorator 的实体类.

DecoratorPatternDemo，我们的演示类使用 RedShapeDecorator 来装饰 Shape 对象。

![](/assets/sdsdimport.png)

```java
抽象构件角色

public interface Component {
    
    public void sampleOperation();
    
}

　　具体构件角色


public class ConcreteComponent implements Component {

    @Override
    public void sampleOperation() {
        // 写相关的业务代码
    }

}

　　装饰角色


public class Decorator implements Component{
    private Component component;    //这里体现与代理模式得区别
    
    public Decorator(Component component){
        this.component = component;
    }

    @Override
    public void sampleOperation() {
        // 委派给构件
        component.sampleOperation();
    }
    
}
具体装饰角色


public class ConcreteDecoratorA extends Decorator {

    public ConcreteDecoratorA(Component component) {
        super(component);
    }
    
    @Override
    public void sampleOperation() {
　　　　　super.sampleOperation();
        // 写相关的业务代码
    }
}

public class ConcreteDecoratorB extends Decorator {

    public ConcreteDecoratorB(Component component) {
        super(component);
    }
    
    @Override
    public void sampleOperation() {
　　　　  super.sampleOperation();
        // 写相关的业务代码
    }
}
```



