### Adapter Pattern适配器模式

是作为两个不兼容的接口之间的桥梁。

属于结构型模式，它结合了两个独立接口的功能。

这种模式涉及到一个单一的类，该类负责加入独立的或不兼容的接口功能。

比如，读卡器是作为内存卡和笔记本之间的适配器。您将内存卡插入读卡器，再将读卡器插入笔记本，这样就可以通过笔记本来读取内存卡。

---

#### 意图

使得客户端和服务端的修改可以独立。

将一个类的接口转换成客户希望的另外一个接口。适配器模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。

#### 用途

Adapter：将一个类的接口转换成客户希望的另外一个接口。

Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作

#### 适用性

你想使用一个已经存在的类，而它的接口不符合你的要

#### 参与者

###### 目标接口（Target）：

```
客户端所期待的接口（原本使用的）。目标可以是具体的或抽象的类，也可以是接口。
```

###### 需要适配的类（Adaptee）：

```
需要适配的类或适配者类（服务端）。
```

###### 适配器（Adapter）：

通过包装一个需要适配的对象，把原接口转换成目标接口。

#### 效果

###### 优点：

```
1、可以让任何两个没有关联的类一起运行。 

2、提高了类的复用。 

3、增加了类的透明度。 

4、灵活性好。
```

###### 缺点：

```
1.过多地使用适配器，会让系统非常零乱，不易整体进行把握。比如，明明看到调用的是 A 接口，其实内部被适配成了 B 接口的实现，一个系统如果太多出现这种情况，无异于一场灾难。因此如果不是很有必要，可以不使用适配器，而是直接对系统进行重构。 

2.由于 JAVA 至多继承一个类，所以至多只能适配一个适配者类，而且目标类必须是抽象类。
```

###### 注意事项：

```
适配器不是在详细设计时添加的，而是解决正在服役的项目的问题。
```

#### 实现

![](/assets/adapter.png)

```
/// 定义客户端期待的接口

/// &lt;/summary&gt;

public class Target

{

    /// &lt;summary&gt;

    /// 使用virtual修饰以便子类可以重写

    /// &lt;/summary&gt;

    public virtual void Request\(\)

    {

        Console.WriteLine\("This is a common request"\);

    }

}



/// 定义需要适配的类

/// &lt;/summary&gt;

public class Adaptee

{

    public void SpecificRequest\(\)

    {

        Console.WriteLine\("This is a special request."\);

    }

}



/// 定义适配器

/// &lt;/summary&gt;

public class Adapter:Target

{

    // 建立一个私有的Adeptee对象

    private Adaptee adaptee = new Adaptee\(\);

    /// 通过重写，表面上调用Request\(\)方法，变成了实际调用SpecificRequest\(\)

    /// &lt;/summary&gt;

    public override void Request\(\)

    {

        adaptee.SpecificRequest\(\);

    }

}
```

客户端代码

```
class Program

{

    static void Main\(string\[\] args\)

    {

        // 对客户端来说，调用的就是Target的Request\(\)

        Target target = new Adapter\(\);

        target.Request\(\);
        Console.Read();
            }
```

```

}
```

来自 &lt;[http://www.cnblogs.com/wangjq/archive/2012/07/09/2582485.html&gt;](http://www.cnblogs.com/wangjq/archive/2012/07/09/2582485.html&gt);

