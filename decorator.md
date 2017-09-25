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

![](/assets/vvimport.png)

```java
步骤 1
创建一个接口。
Shape.java
public interface Shape {
   void draw();
}
步骤 2
创建实现接口的实体类。
Rectangle.java
public class Rectangle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Rectangle");
   }
}
Circle.java
public class Circle implements Shape {

   @Override
   public void draw() {
      System.out.println("Shape: Circle");
   }
}
步骤 3
创建实现了 Shape 接口的抽象装饰类。
ShapeDecorator.java
public abstract class ShapeDecorator implements Shape {
   protected Shape decoratedShape;

   public ShapeDecorator(Shape decoratedShape){
      this.decoratedShape = decoratedShape;
   }

   public void draw(){
      decoratedShape.draw();
   }    
}
步骤 4
创建扩展了 ShapeDecorator 类的实体装饰类。
RedShapeDecorator.java
public class RedShapeDecorator extends ShapeDecorator {

   public RedShapeDecorator(Shape decoratedShape) {
      super(decoratedShape);        
   }

   @Override
   public void draw() {
      decoratedShape.draw();           
      setRedBorder(decoratedShape);
   }

   private void setRedBorder(Shape decoratedShape){
      System.out.println("Border Color: Red");
   }
}
步骤 5
使用 RedShapeDecorator 来装饰 Shape 对象。
DecoratorPatternDemo.java
public class DecoratorPatternDemo {
   public static void main(String[] args) {

      Shape circle = new Circle();

      Shape redCircle = new RedShapeDecorator(new Circle());

      Shape redRectangle = new RedShapeDecorator(new Rectangle());
      System.out.println("Circle with normal border");
      circle.draw();

      System.out.println("\nCircle of red border");
      redCircle.draw();

      System.out.println("\nRectangle of red border");
      redRectangle.draw();
   }
}
步骤 6
验证输出。
Circle with normal border
Shape: Circle

Circle of red border
Shape: Circle
Border Color: Red

Rectangle of red border
Shape: Rectangle
Border Color: Red
```

```
来自 http://www.runoob.com/design-pattern/decorator-pattern.html;
```



