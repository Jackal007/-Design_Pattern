### Template Pattern 模板模式

Name 	又叫发布-订阅\(Publish/Subscribe\)模式、模型-视图\(Model/View\)模式、源-监听器\(Source/Listener\)模式或从属者\(Dependents\)模式。

	属于行为型模式。

意图	观察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个主题对象。这个主题对象在状态上发生变化时，会通知所有观察者对象，使它们能够自动更新自己。

适用性	主要解决：

	        一个对象状态改变给其他对象通知的问题，而且要考虑到易用和低耦合，保证高度的协作。

	何时使用：

	        一个对象（目标对象）的状态发生改变，所有的依赖对象（观察者对象）都将得到通知，进行广播通知。

参与者	如何解决：

	        使用面向对象技术，可以将这种依赖关系弱化。

	        在状态模式中，我们创建表示各种状态的对象和一个行为随着状态对象改变而改变的 context 对象。

效果	优点： 

	        1、观察者和被观察者是抽象耦合的。 

	        2、建立一套触发机制。

	缺点： 

	        1、如果一个被观察者对象有很多的直接和间接的观察者的话，将所有的观察者都通知到会花费很多时间。 

	        2、如果在观察者和观察目标之间有循环依赖的话，观察目标会触发它们之间进行循环调用，可能导致系统崩溃。 

	        3、观察者模式没有相应的机制让观察者知道所观察的目标对象是怎么发生变化的，而仅仅只是知道观察目标发生了变化。

	使用场景： 

	        1、有多个子类共有的方法，且逻辑相同。 

	        2、重要的、复杂的方法，可以考虑作为模板方法。

	注意事项： 

	        1、JAVA 中已经有了对观察者模式的支持类。 

	        2、避免循环引用。 

	        3、如果顺序执行，某一观察者错误会导致系统卡壳，一般采用异步方式。

实现	观察者模式使用三个类 Subject、Observer 和 Client。Subject 对象带有绑定观察者到 Client 对象和从 Client 对象解绑观察者的方法。我们创建 Subject 类、Observer 抽象类和扩展了抽象类 Observer 的实体类。

	ObserverPatternDemo，我们的演示类使用 Subject 和实体类对象来演示观察者模式。

	

	步骤 1

	创建 Subject 类。

	Subject.java

	import java.util.ArrayList;import java.util.List;

	public class Subject {	   private List&lt;Observer&gt; observers       = new ArrayList&lt;Observer&gt;\(\);   private int state;

	public int getState\(\) {      return state;   }

	public void setState\(int state\) {      this.state = state;      notifyAllObservers\(\);   }

	public void attach\(Observer observer\){      observers.add\(observer\);		   }

	public void notifyAllObservers\(\){      for \(Observer observer : observers\) {         observer.update\(\);      }   } 	}

	步骤 2

	创建 Observer 类。

	Observer.java

	public abstract class Observer {   protected Subject subject;   public abstract void update\(\);}

	步骤 3

	创建实体观察者类。

	BinaryObserver.java

	public class BinaryObserver extends Observer{

	public BinaryObserver\(Subject subject\){      this.subject = subject;      this.subject.attach\(this\);   }

	@Override   public void update\(\) {      System.out.println\( "Binary String: "       + Integer.toBinaryString\( subject.getState\(\) \) \);    }}

	OctalObserver.java

	public class OctalObserver extends Observer{

	public OctalObserver\(Subject subject\){      this.subject = subject;      this.subject.attach\(this\);   }

	@Override   public void update\(\) {     System.out.println\( "Octal String: "      + Integer.toOctalString\( subject.getState\(\) \) \);    }}

	HexaObserver.java

	public class HexaObserver extends Observer{

	public HexaObserver\(Subject subject\){      this.subject = subject;      this.subject.attach\(this\);   }

	@Override   public void update\(\) {      System.out.println\( "Hex String: "       + Integer.toHexString\( subject.getState\(\) \).toUpperCase\(\) \);    }}

	步骤 4

	使用 Subject 和实体观察者对象。

	ObserverPatternDemo.java

	public class ObserverPatternDemo {   public static void main\(String\[\] args\) {      Subject subject = new Subject\(\);

	new HexaObserver\(subject\);      new OctalObserver\(subject\);      new BinaryObserver\(subject\);

	System.out.println\("First state change: 15"\);	      subject.setState\(15\);      System.out.println\("Second state change: 10"\);	      subject.setState\(10\);   }}

	步骤 5

	验证输出。

	First state change: 15Hex String: FOctal String: 17Binary String: 1111Second state change: 10Hex String: AOctal String: 12Binary String: 1010

	

	来自 &lt;http://www.runoob.com/design-pattern/observer-pattern.html&gt; 

	

	





