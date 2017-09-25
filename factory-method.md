### Factory method 工厂方法模式

**类的创建模式**，又叫做虚拟构造子\(Virtual Constructor\)模式或者多态性工厂（Polymorphic Factory）模式。

---

意图   

 定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。

```
主要解决接口选择的问题。
```

适用性

参与者    抽象工厂（ExportFactory）：

```
        担任这个角色的是工厂方法模式的核心，任何在模式中创建对象的工厂类必须实现这个接口。在实际的系统中，这个角色也常常使用抽象类实现。



具体工厂（ExportHtmlFactory、ExportPdfFactory）：

        担任这个角色的是实现了抽象工厂接口的具体JAVA类。具体工厂角色含有与业务密切相关的逻辑，并且受到使用者的调用以创建导出类（如：ExportStandardHtmlFile）。



抽象导出（ExportFile）角色：

        工厂方法模式所创建的对象的超类，也就是所有导出类的共同父类或共同拥有的接口。在实际的系统中，这个角色也常常使用抽象类实现。



具体导出（ExportStandardHtmlFile等）：

        这个角色实现了抽象导出（ExportFile）角色所声明的接口，工厂方法模式所创建的每一个对象都是某个具体导出角色的实例。
```

效果

实现    相信很多人都做过导入导出功能，就拿导出功能来说。有这么一个需求：XX系统需要支持对数据库中的员工薪资进行导出，并且支持多种格式如：HTML、CSV、PDF等，每种格式导出的结构有所不同，比如：财务跟其他人对导出薪资的HTML格式要求可能会不一样，因为财务可能需要特定的格式方便核算或其他用途。

```
如果使用简单工厂模式，则工厂类必定过于臃肿。因为简单工厂模式只有一个工厂类，它需要处理所有的创建的逻辑。假如以上需求暂时只支持3种导出的格式以及2种导出的结构，那工厂类则需要6个if else来创建6种不同的类型。如果日后需求不断增加，则后果不堪设想。

这时候就需要工厂方法模式来处理以上需求。在工厂方法模式中，核心的工厂类不再负责所有的对象的创建，而是将具体创建的工作交给子类去做。这个核心类则摇身一变，成为了一个抽象工厂角色，仅负责给出具体工厂子类必须实现的接口，而不接触哪一个类应当被实例化这种细节。

这种进一步抽象化的结果，使这种工厂方法模式可以用来允许系统在不修改具体工厂角色的情况下引进新的产品，这一特点无疑使得工厂方法模式具有超过简单工厂模式的优越性。下面就针对以上需求设计UML图：
```

![](/assets/qqimport.png)

```
源代码

首先是抽象工厂角色源代码。它声明了一个工厂方法，要求所有的具体工厂角色都实现这个工厂方法。参数type表示导出的格式是哪一种结构，如：导出HTML格式有两种结构，一种是标准结构，一种是财务需要的结构。

public interface ExportFactory {

public ExportFile factory\(String type\);

}

具体工厂角色类源代码：



public class ExportHtmlFactory implements ExportFactory{



@Override

public ExportFile factory\(String type\) {

// TODO Auto-generated method stub

if\("standard".equals\(type\)\){



return new ExportStandardHtmlFile\(\);



}else if\("financial".equals\(type\)\){



return new ExportFinancialHtmlFile\(\);



}else{

throw new RuntimeException\("没有找到对象"\);

}

}



}







public class ExportPdfFactory implements ExportFactory {



@Override

public ExportFile factory\(String type\) {

// TODO Auto-generated method stub

if\("standard".equals\(type\)\){



return new ExportStandardPdfFile\(\);



}else if\("financial".equals\(type\)\){



return new ExportFinancialPdfFile\(\);



}else{

throw new RuntimeException\("没有找到对象"\);

}

}



}



抽象导出角色类源代码：

public interface ExportFile {

public boolean export\(String data\);

}

具体导出角色类源代码，通常情况下这个类会有复杂的业务逻辑。



public class ExportFinancialHtmlFile implements ExportFile{



@Override

public boolean export\(String data\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

System.out.println\("导出财务版HTML文件"\);

return true;

}



}







public class ExportFinancialPdfFile implements ExportFile{



@Override

public boolean export\(String data\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

System.out.println\("导出财务版PDF文件"\);

return true;

}



}







public class ExportStandardHtmlFile implements ExportFile{



@Override

public boolean export\(String data\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

System.out.println\("导出标准HTML文件"\);

return true;

}



}







public class ExportStandardPdfFile implements ExportFile {



@Override

public boolean export\(String data\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

System.out.println\("导出标准PDF文件"\);

return true;

}



}



客户端角色类源代码：



public class Test {



/\*\*

\* @param args

\*/

public static void main\(String\[\] args\) {

// TODO Auto-generated method stub

String data = "";

ExportFactory exportFactory = new ExportHtmlFactory\(\);

ExportFile ef = exportFactory.factory\("financial"\);

ef.export\(data\);

}



}





来自 &lt;http://www.cnblogs.com/java-my-life/archive/2012/03/25/2416227.html&gt; 
```



