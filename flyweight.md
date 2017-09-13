### Template Pattern 模板模式

#### 

Name 	主要用于减少创建对象的数量，以减少内存占用和提高性能。

	属于结构型模式

	它提供了减少对象数量从而改善应用所需的对象结构的方式。

	享元模式尝试重用现有的同类对象，如果未找到匹配的对象，则创建新对象。

意图	运用共享技术有效地支持大量细粒度的对象。

适用性	主要解决：

	        在有大量对象时，有可能会造成内存溢出，我们把其中共同的部分抽象出来，如果有相同的业务请求，直接返回在内存中已有的对象，避免重新创建。

	何时使用： 

	        1、系统中有大量对象。 

	        2、这些对象消耗大量内存。 

	        3、这些对象的状态大部分可以外部化。 

	        4、这些对象可以按照内蕴状态分为很多组，当把外蕴对象从对象中剔除出来时，每一组对象都可以用一个对象来代替。 

	        5、系统不依赖于这些对象身份，这些对象是不可分辨的。 

	如何解决：

	        用唯一标识码判断，如果在内存中有，则返回这个唯一标识码所标识的对象。

参与者	

效果	优点：

	        大大减少对象的创建，降低系统的内存，使效率提高。

	缺点：

	        提高了系统的复杂度，需要分离出外部状态和内部状态，而且外部状态具有固有化的性质，不应该随着内部状态的变化而变化，否则会造成系统的混乱。

	使用场景： 

	        1、系统有大量相似对象。 

	        2、需要缓冲池的场景。

	注意事项： 

	        1、注意划分外部状态和内部状态，否则可能会引起线程安全问题。 

	        2、这些类必须有一个工厂对象加以控制。

实现	单纯享元模式

	在单纯的享元模式中，所有的享元对象都是可以共享的。

	

	单纯享元模式所涉及到的角色如下：

	●抽象享元\(Flyweight\)角色 ：给出一个抽象接口，以规定出所有具体享元角色需要实现的方法。

	●具体享元\(ConcreteFlyweight\)角色：实现抽象享元角色所规定出的接口。如果有内蕴状态的话，必须负责为内蕴状态提供存储空间。

	●享元工厂\(FlyweightFactory\)角色 ：本角色负责创建和管理享元角色。本角色必须保证享元对象可以被系统适当地共享。当一个客户端对象调用一个享元对象的时候，享元工厂角色会检查系统中是否已经有一个符合要求的享元对象。如果已经有了，享元工厂角色就应当提供这个已有的享元对象；如果系统中没有一个适当的享元对象的话，享元工厂角色就应当创建一个合适的享元对象。

	源代码

	抽象享元角色类

	public interface Flyweight {    //一个示意性方法，参数state是外蕴状态    public void operation\(String state\);}

	具体享元角色类ConcreteFlyweight有一个内蕴状态，在本例中一个Character类型的intrinsicState属性代表，它的值应当在享元对象被创建时赋予。所有的内蕴状态在对象创建之后，就不会再改变了。

	如果一个享元对象有外蕴状态的话，所有的外部状态都必须存储在客户端，在使用享元对象时，再由客户端传入享元对象。这里只有一个外蕴状态，operation\(\)方法的参数state就是由外部传入的外蕴状态。

	

	public class ConcreteFlyweight implements Flyweight {    private Character intrinsicState = null;    /\*\*     \* 构造函数，内蕴状态作为参数传入     \* @param state     \*/    public ConcreteFlyweight\(Character state\){        this.intrinsicState = state;    }            /\*\*     \* 外蕴状态作为参数传入方法中，改变方法的行为，     \* 但是并不改变对象的内蕴状态。     \*/    @Override    public void operation\(String state\) {        // TODO Auto-generated method stub        System.out.println\("Intrinsic State = " + this.intrinsicState\);        System.out.println\("Extrinsic State = " + state\);    }

	}

	

	享元工厂角色类，必须指出的是，客户端不可以直接将具体享元类实例化，而必须通过一个工厂对象，利用一个factory\(\)方法得到享元对象。一般而言，享元工厂对象在整个系统中只有一个，因此也可以使用单例模式。

	当客户端需要单纯享元对象的时候，需要调用享元工厂的factory\(\)方法，并传入所需的单纯享元对象的内蕴状态，由工厂方法产生所需要的享元对象。

	

	public class FlyweightFactory {    private Map&lt;Character,Flyweight&gt; files = new HashMap&lt;Character,Flyweight&gt;\(\);        public Flyweight factory\(Character state\){        //先从缓存中查找对象        Flyweight fly = files.get\(state\);        if\(fly == null\){            //如果对象不存在则创建一个新的Flyweight对象            fly = new ConcreteFlyweight\(state\);            //把这个新的Flyweight对象添加到缓存中            files.put\(state, fly\);        }        return fly;    }}

	

	客户端类

	

	public class Client {

	public static void main\(String\[\] args\) {        // TODO Auto-generated method stub        FlyweightFactory factory = new FlyweightFactory\(\);        Flyweight fly = factory.factory\(new Character\('a'\)\);        fly.operation\("First Call"\);                fly = factory.factory\(new Character\('b'\)\);        fly.operation\("Second Call"\);                fly = factory.factory\(new Character\('a'\)\);        fly.operation\("Third Call"\);    }

	}

	

	虽然客户端申请了三个享元对象，但是实际创建的享元对象只有两个，这就是共享的含义。运行结果如下：

	

	 

	复合享元模式

	在单纯享元模式中，所有的享元对象都是单纯享元对象，也就是说都是可以直接共享的。还有一种较为复杂的情况，将一些单纯享元使用合成模式加以复合，形成复合享元对象。这样的复合享元对象本身不能共享，但是它们可以分解成单纯享元对象，而后者则可以共享。

	

	复合享元角色所涉及到的角色如下：

	●抽象享元\(Flyweight\)角色 ：给出一个抽象接口，以规定出所有具体享元角色需要实现的方法。

	●具体享元\(ConcreteFlyweight\)角色：实现抽象享元角色所规定出的接口。如果有内蕴状态的话，必须负责为内蕴状态提供存储空间。

	●　  复合享元\(ConcreteCompositeFlyweight\)角色 ：复合享元角色所代表的对象是不可以共享的，但是一个复合享元对象可以分解成为多个本身是单纯享元对象的组合。复合享元角色又称作不可共享的享元对象。

	●　  享元工厂\(FlyweightFactory\)角色 ：本角 色负责创建和管理享元角色。本角色必须保证享元对象可以被系统适当地共享。当一个客户端对象调用一个享元对象的时候，享元工厂角色会检查系统中是否已经有 一个符合要求的享元对象。如果已经有了，享元工厂角色就应当提供这个已有的享元对象；如果系统中没有一个适当的享元对象的话，享元工厂角色就应当创建一个 合适的享元对象。

	源代码

	抽象享元角色类

	public interface Flyweight {    //一个示意性方法，参数state是外蕴状态    public void operation\(String state\);}

	具体享元角色类

	

	public class ConcreteFlyweight implements Flyweight {    private Character intrinsicState = null;    /\*\*     \* 构造函数，内蕴状态作为参数传入     \* @param state     \*/    public ConcreteFlyweight\(Character state\){        this.intrinsicState = state;    }            /\*\*     \* 外蕴状态作为参数传入方法中，改变方法的行为，     \* 但是并不改变对象的内蕴状态。     \*/    @Override    public void operation\(String state\) {        // TODO Auto-generated method stub        System.out.println\("Intrinsic State = " + this.intrinsicState\);        System.out.println\("Extrinsic State = " + state\);    }

	}

	

	复合享元对象是由单纯享元对象通过复合而成的，因此它提供了add\(\)这样的聚集管理方法。由于一个复合享元对象具有不同的聚集元素，这些聚集元素在复合享元对象被创建之后加入，这本身就意味着复合享元对象的状态是会改变的，因此复合享元对象是不能共享的。

	复合享元角色实现了抽象享元角色所规定的接口，也就是operation\(\)方法，这个方法有一个参数，代表复合享元对象的外蕴状态。一个复合享元对象的所有单纯享元对象元素的外蕴状态都是与复合享元对象的外蕴状态相等的；而一个复合享元对象所含有的单纯享元对象的内蕴状态一般是不相等的，不然就没有使用价值了。

	

	public class ConcreteCompositeFlyweight implements Flyweight {        private Map&lt;Character,Flyweight&gt; files = new HashMap&lt;Character,Flyweight&gt;\(\);    /\*\*     \* 增加一个新的单纯享元对象到聚集中     \*/    public void add\(Character key , Flyweight fly\){        files.put\(key,fly\);    }    /\*\*     \* 外蕴状态作为参数传入到方法中     \*/    @Override    public void operation\(String state\) {        Flyweight fly = null;        for\(Object o : files.keySet\(\)\){            fly = files.get\(o\);            fly.operation\(state\);        }            }

	}

	

	享元工厂角色提供两种不同的方法，一种用于提供单纯享元对象，另一种用于提供复合享元对象。

	

	public class FlyweightFactory {    private Map&lt;Character,Flyweight&gt; files = new HashMap&lt;Character,Flyweight&gt;\(\);    /\*\*     \* 复合享元工厂方法     \*/    public Flyweight factory\(List&lt;Character&gt; compositeState\){        ConcreteCompositeFlyweight compositeFly = new ConcreteCompositeFlyweight\(\);                for\(Character state : compositeState\){            compositeFly.add\(state,this.factory\(state\)\);        }                return compositeFly;    }    /\*\*     \* 单纯享元工厂方法     \*/    public Flyweight factory\(Character state\){        //先从缓存中查找对象        Flyweight fly = files.get\(state\);        if\(fly == null\){            //如果对象不存在则创建一个新的Flyweight对象            fly = new ConcreteFlyweight\(state\);            //把这个新的Flyweight对象添加到缓存中            files.put\(state, fly\);        }        return fly;    }}

	

	客户端角色

	

	public class Client {

	public static void main\(String\[\] args\) {        List&lt;Character&gt; compositeState = new ArrayList&lt;Character&gt;\(\);        compositeState.add\('a'\);        compositeState.add\('b'\);        compositeState.add\('c'\);        compositeState.add\('a'\);        compositeState.add\('b'\);                FlyweightFactory flyFactory = new FlyweightFactory\(\);        Flyweight compositeFly1 = flyFactory.factory\(compositeState\);        Flyweight compositeFly2 = flyFactory.factory\(compositeState\);        compositeFly1.operation\("Composite Call"\);                System.out.println\("---------------------------------"\);                System.out.println\("复合享元模式是否可以共享对象：" + \(compositeFly1 == compositeFly2\)\);                Character state = 'a';        Flyweight fly1 = flyFactory.factory\(state\);        Flyweight fly2 = flyFactory.factory\(state\);        System.out.println\("单纯享元模式是否可以共享对象：" + \(fly1 == fly2\)\);    }}

	

	 

	运行结果如下：

	

	从运行结果可以看出，一个复合享元对象的所有单纯享元对象元素的外蕴状态都是与复合享元对象的外蕴状态相等的。即外运状态都等于Composite Call。

	

	来自 &lt;http://www.cnblogs.com/java-my-life/archive/2012/04/26/2468499.html&gt; 

	





