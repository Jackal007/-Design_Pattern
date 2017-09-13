### Template Pattern 模板模式

#### 

Name 	桥接（Bridge）是用于把抽象化与实现化解耦，使得二者可以独立变化。

	属于结构型模式。

	设想如果要绘制矩形、圆形、椭圆、正方形，我们至少需要4个形状类，但是如果绘制的图形需要具有不同的颜色，如红色、绿色、蓝色等，此时至少有如下两种设计方案：

	• 第一种设计方案是为每一种形状都提供一套各种颜色的版本。

	• 第二种设计方案是根据实际需要对形状和颜色进行组合

	对于有两个变化维度（即两个变化的原因）的系统，采用方案二来进行设计系统中类的个数更少，且系统扩展更为方便。设计方案二即是桥接模式的应用。桥接模式将继承关系转换为关联关系，从而降低了类与类之间的耦合，减少了代码编写量。

	来自 &lt;http://design-patterns.readthedocs.io/zh\_CN/latest/structural\_patterns/bridge.html&gt; 

意图	将抽象部分与实现部分分离，使它们都可以独立的变化。

适用性	在有多种可能会变化的情况下，用继承会造成类爆炸问题，扩展起来不灵活。

	实现系统可能有多个角度分类，每一种角度都可能变化。

	对于两个独立变化的维度，使用桥接模式再适合不过了。

参与者	

效果	优点： 

	        1、抽象和实现的分离。 

	        2、优秀的扩展能力。 

	        3、实现细节对客户透明。

	缺点：

	        桥接模式的引入会增加系统的理解与设计难度，由于聚合关联关系建立在抽象层，要求开发者针对抽象进行设计与编程。

实现	

	![](/assets/nnimport.png)

	

	abstract class AbstractRoad{      AbstractCar aCar;      void run\(\){};  }  abstract class AbstractCar{      void run\(\){};  }  

	class Street extends AbstractRoad{      @Override      void run\(\) {            super.run\(\);          aCar.run\(\);          System.out.println\("在市区街道行驶"\);      }  }  class SpeedWay extends AbstractRoad{      @Override      void run\(\) {          super.run\(\);          aCar.run\(\);          System.out.println\("在高速公路行驶"\);      }  }  class Car extends AbstractCar{      @Override      void run\(\) {          super.run\(\);          System.out.print\("小汽车"\);      }  }  class Bus extends AbstractCar{      @Override      void run\(\) {          super.run\(\);          System.out.print\("公交车"\);      }  }  

	public static void main\(String\[\] args\){  

	    AbstractRoad speedWay = new SpeedWay\(\);      speedWay.aCar = new Car\(\);      speedWay.run\(\);  

	    AbstractRoad street = new Street\(\);      street.aCar = new Bus\(\);      street.run\(\);  }  

	

	来自 &lt;https://cnbin.github.io/blog/2015/12/11/javashe-ji-mo-shi-chu-tan-zhi-qiao-jie-mo-shi/&gt; 





