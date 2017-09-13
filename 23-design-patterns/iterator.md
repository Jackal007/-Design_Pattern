### Template Pattern 迭代器模式

Iterator、迭代器、游标（Cursor）**属于行为模式** 关于对象的为容器而生

#### 意图

提供一种方法顺序访问一个聚合对象中各个元素，而又不暴露该对象的内部表示

动机

	一个聚合对象（EG：List），应该提供一种方法来让别人可以访问它的元素而又不暴露它的内部结构。

	迭代器模式可以帮助我们解决这个问题，这个模式的关键思想是：将对列表的访问和遍历从列表对象中分离出来并放入一个迭代器对象中。迭代器定义了一个访问该列表元素的接口。

	for \(int i=0;i&lt;arr.length;i++\){System.out.println\(arr\[i\]\)}

		在设计Pattern时，变量i的功能抽象化，结果就称为：

    Iterator Pattern

#### 适用性

1、访问一个聚合对象的内容而无须暴露它的内部表示。

2、需要为聚合对象提供多种遍历方式。 

3、为遍历不同的聚合结构提供一个统一的接口。

#### 参与者

##### 

#### 效果

##### 优点： 

	1、它支持以不同的方式遍历一个聚合对象。

	2、迭代器简化了聚合类。 

	3、在同一个聚合上可以有多个遍历。 

	4、在迭代器模式中，增加新的聚合类和迭代器类都很方便，无须修改原有代码。

##### 缺点：

	由于迭代器模式将存储数据和遍历数据的职责分离，增加新的聚合类需要对应增加新的迭代器类，类的个数成对增加，这在一定程度上增加了系统的复杂性。

#### 实现

我们将创建一个叙述导航方法的 Iterator 接口和一个返回迭代器的 Container 接口。实现了 Container 接口的实体类将负责实现 Iterator 接口。

IteratorPatternDemo，我们的演示类使用实体类 NamesRepository 来打印 NamesRepository 中存储为集合的 Names。

![](/assets/iterator.png)

步骤 1

创建接口。

Iterator.java

public interface Iterator {

   public boolean hasNext\(\);

   public Object next\(\);

}

Container.java

public interface Container {

   public Iterator getIterator\(\);

}

步骤 2

创建实现了 Container 接口的实体类。该类有实现了 Iterator 接口的内部类 NameIterator。

NameRepository.java

public class NameRepository implements Container {

   public String names\[\] = {"Robert" , "John" ,"Julie" , "Lora"};

@Override

   public Iterator getIterator\(\) {

      return new NameIterator\(\);

   }

private class NameIterator implements Iterator {

int index;

@Override

      public boolean hasNext\(\) {

         if\(index &lt; names.length\){

            return true;

         }

         return false;

      }

@Override

      public Object next\(\) {

         if\(this.hasNext\(\)\){

            return names\[index++\];

         }

         return null;

      }		

   }

}

步骤 3

使用 NameRepository 来获取迭代器，并打印名字。

IteratorPatternDemo.java

public class IteratorPatternDemo {

	

   public static void main\(String\[\] args\) {

      NameRepository namesRepository = new NameRepository\(\);

for\(Iterator iter = namesRepository.getIterator\(\); iter.hasNext\(\);\){

         String name = \(String\)iter.next\(\);

         System.out.println\("Name : " + name\);

      } 	

   }

}

步骤 4

验证输出。

Name : Robert

Name : John

Name : Julie

Name : Lora



来自 &lt;http://www.runoob.com/design-pattern/iterator-pattern.html&gt; 



