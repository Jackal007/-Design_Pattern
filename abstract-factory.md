### Abstract Factory Pattern 抽象工厂模式

工厂创建一种产品，抽象工厂创建的是一组产品，是一个产品系列。这里要注意的是“系列”的意思，也就是说，抽象工厂创建出的一组产品是成套的。

> 当你发现，有一个接口可以有多种实现的时候，可以考虑使用工厂方法来创建实例。
>
> 当你返现，有一组接口可以有多种实现方案的时候，可以考虑使用抽象工厂创建实例组。

抽象工厂模式（Abstract Factory Pattern）是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。

属于**创建型模式**，它提供了一种创建对象的最佳方式。

在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。

#### 意图

* 把各种抽象零件组合起来称为抽象产品
* 所谓“抽象的”是指“不考虑具体实现，只注意接口API”
* 提供一个创建一系列相关或相互依赖对象的接口，而无需指定他们具体的类。
* 客户仅与抽象类定义的接口交互，而不使用特定的具体类的接口

#### 适用性

1. 一个系统不应当依赖于产品类实例如何被创建、组合和表达的细节，这对于所有形态的工厂模式都是重要的。
2. 这个系统的产品有多于一个的产品族，而系统只消费其中某一族的产品。
3. 同属于同一个产品族的产品是在一起使用的，这一约束必须在系统的设计中体现出来。（比如：Intel主板必须使用Intel CPU、Intel芯片组）
4. 系统提供一个产品类的库，所有的产品以同样的接口出现，从而使客户端不依赖于实现。

#### 参与者

* AbstractFactory：声明一个创建抽象产品对象的操作接口。
* ConcreteFactory：实现创建具体产品对象的操作。
* AbstractProduct：为一类产品对象声明一个接口。
* ConcreteProduct：定义一个将被相应的具体工厂创建的产品对象；实现AbstractProduct的接口。
* Client：仅使用由AbstractFactory和AbstractProduct类声明的接口

#### 效果

* ##### 优点：

  当一个产品族中的多个对象被设计成一起工作时，它能保证客户端始终只使用同一个产品族中的对象。

* ##### 缺点：

  产品族扩展非常困难，要增加一个系列的某一产品，既要在抽象的 Creator 里加代码，又要在具体的里面加代码。

注意事项：产品族难扩展，产品等级易扩展。

#### 实现

每一个模式都是针对一定问题的解决方案。抽象工厂模式与工厂方法模式的最大区别就在于，工厂方法模式针对的是一个产品等级结构；而抽象工厂模式则需要面对多个产品等级结构。

在学习抽象工厂具体实例之前，应该明白两个重要的概念：产品族和产品等级。

所谓产品族，是指位于不同产品等级结构中，功能相关联的产品组成的家族。比如AMD的主板、芯片组、CPU组成一个家族，Intel的主板、芯片组、CPU组成一个家族。而这两个家族都来自于三个产品等级：主板、芯片组、CPU。一个等级结构是由相同的结构的产品组成，示意图如下：

![](/assets/import.png)

```
显然，每一个产品族中含有产品的数目，与产品等级结构的数目是相等的。产品的等级结构与产品族将产品按照不同方向划分，形成一个二维的坐标系。横轴表示产品的等级结构，纵轴表示产品族，上图共有两个产品族，分布于三个不同的产品等级结构中。只要指明一个产品所处的产品族以及它所属的等级结构，就可以唯一的确定这个产品。

上面所给出的三个不同的等级结构具有平行的结构。因此，如果采用工厂方法模式，就势必要使用三个独立的工厂等级结构来对付这三个产品等级结构。由于这三个产品等级结构的相似性，会导致三个平行的工厂等级结构。随着产品等级结构的数目的增加，工厂方法模式所给出的工厂等级结构的数目也会随之增加。如下图：
```

![](/assets/imsport.png)

```
那么，是否可以使用同一个工厂等级结构来对付这些相同或者极为相似的产品等级结构呢？当然可以的，而且这就是抽象工厂模式的好处。同一个工厂等级结构负责三个不同产品等级结构中的产品对象的创建。
```

![](/assets/imwport.png)

```
可以看出，一个工厂等级结构可以创建出分属于不同产品等级结构的一个产品族中的所有对象。显然，这时候抽象工厂模式比简单工厂模式、工厂方法模式更有效率。对应于每一个产品族都有一个具体工厂。而每一个具体工厂负责创建属于同一个产品族，但是分属于不同等级结构的产品。

抽象工厂模式结构

抽象工厂模式是对象的创建模式，它是工厂方法模式的进一步推广。

假设一个子系统需要一些产品对象，而这些产品又属于一个以上的产品等级结构。那么为了将消费这些产品对象的责任和创建这些产品对象的责任分割开来，可以引进抽象工厂模式。这样的话，消费产品的一方不需要直接参与产品的创建工作，而只需要向一个公用的工厂接口请求所需要的产品。

通过使用抽象工厂模式，可以处理具有相同（或者相似）等级结构中的多个产品族中的产品对象的创建问题。如下图所示：
```

![](/assets/wimport.png)

由于这两个产品族的等级结构相同，因此使用同一个工厂族也可以处理这两个产品族的创建问题，这就是抽象工厂模式。

根据产品角色的结构图，就不难给出工厂角色的结构设计图。

![](/assets/whimport.png)

可以看出，每一个工厂角色都有两个工厂方法，分别负责创建分属不同产品等级结构的产品对象。

![](/assets/aaimport.png)

```java
public interface AbstractFactory {
    /**
     * 创建CPU对象
     * @return CPU对象
     */
    public Cpu createCpu();
    /**
     * 创建主板对象
     * @return 主板对象
     */
    public Mainboard createMainboard();
}

public class IntelFactory implements AbstractFactory {

    @Override
    public Cpu createCpu() {
        // TODO Auto-generated method stub
        return new IntelCpu(755);
    }

    @Override
    public Mainboard createMainboard() {
        // TODO Auto-generated method stub
        return new IntelMainboard(755);
    }

}
 
public class AmdFactory implements AbstractFactory {

    @Override
    public Cpu createCpu() {
        // TODO Auto-generated method stub
        return new IntelCpu(938);
    }

    @Override
    public Mainboard createMainboard() {
        // TODO Auto-generated method stub
        return new IntelMainboard(938);
    }

}

　　装机工程师类跟前面的实现相比，主要的变化是：从客户端不再传入选择CPU和主板的参数，而是直接传入客户已经选择好的产品对象。这样就避免了单独去选择CPU和主板所带来的兼容性问题，客户要选就是一套，就是一个系列。


public class ComputerEngineer {
    /**
     * 定义组装机需要的CPU
     */
    private Cpu cpu = null;
    /**
     * 定义组装机需要的主板
     */
    private Mainboard mainboard = null;
    public void makeComputer(AbstractFactory af){
        /**
         * 组装机器的基本步骤
         */
        //1:首先准备好装机所需要的配件
        prepareHardwares(af);
        //2:组装机器
        //3:测试机器
        //4：交付客户
    }
    private void prepareHardwares(AbstractFactory af){
        //这里要去准备CPU和主板的具体实现，为了示例简单，这里只准备这两个
        //可是，装机工程师并不知道如何去创建，怎么办呢？
        
        //直接找相应的工厂获取
        this.cpu = af.createCpu();
        this.mainboard = af.createMainboard();
        
        //测试配件是否好用
        this.cpu.calculate();
        this.mainboard.installCPU();
    }
}

客户端代码：

public class Client {
    public static void main(String[]args){
        //创建装机工程师对象
        ComputerEngineer cf = new ComputerEngineer();
        //客户选择并创建需要使用的产品对象
        AbstractFactory af = new IntelFactory();
        //告诉装机工程师自己选择的产品，让装机工程师组装电脑
        cf.makeComputer(af);
    }
}
```

* ###### 简单工厂：

  工厂类直接实现，一个产品抽象类，一个工厂类可以产生多种产品
* ###### 工厂方法：

  一个抽象工厂类，一个产品抽象类，一个工厂类产生一种产品

* ###### 抽象工厂：

  一个抽象工厂类，多个产品抽象类。一个工厂类可以产生一系列产品族的产品



