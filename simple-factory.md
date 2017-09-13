### Simple FactoryPattern 工厂模式

简单工厂模式（Simple Factory Pattern）根本就不算是一种设计模式。

又叫静态工厂方法模式（Static FactoryMethod Pattern）。

属于创建型模式，它提供了一种创建对象的最佳方式。

#### 意图

在工厂模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象。

#### 适用性

我们明确地计划不同条件下创建不同实例时。

使用场景：

```
1、日志记录器：记录可能记录到本地硬盘、系统事件、远程服务器等，用户可以选择记录日志到什么地方。 

2、数据库访问，当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时。 

   3、设计一个连接服务器的框架，需要三个协议，"POP3"、"IMAP"、"HTTP"，可以把这三个作为产品类，共同实现一个接口。
```

#### 参与者

![](/assets/factory.png)

#### 效果

##### 优点：

```
1、一个调用者想创建一个对象，只要知道其名称就可以了。 

2、扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。 

3、屏蔽产品的具体实现，调用者只关心产品的接口。
```

##### 缺点：

每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。这并不是什么好事。

#### 实现

就拿登录功能来说，假如应用系统需要支持多种登录方式如：口令认证、域认证（口令认证通常是去数据库中验证用户，而域认证则是需要到微软的域中验证用户）。那么自然的做法就是建立一个各种登录方式都适用的接口，如下图所示：

![](/assets/factory2.png)

//登录验证

public boolean verify\(String name , String password\);

}

public class DomainLogin implements Login {

@Override

public boolean verify\(String name, String password\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

return true;

}

}

public class PasswordLogin implements Login {

@Override

public boolean verify\(String name, String password\) {

// TODO Auto-generated method stub

/\*\*

\* 业务逻辑

\*/

return true;

}

}

我们还需要一个工厂类LoginManager，根据调用者不同的要求，创建出不同的登录对象并返回。而如果碰到不合法的要求，会返回一个Runtime异常。

public class LoginManager {

public static Login factory\(String type\){

if\(type.equals\("password"\)\){

return new PasswordLogin\(\);

}else if\(type.equals\("passcode"\)\){

return new DomainLogin\(\);

}else{

/\*\*

\* 这里抛出一个自定义异常会更恰当

\*/

throw new RuntimeException\("没有找到登录类型"\);

}

}

}

测试类：

public class Test {

public static void main\(String\[\] args\) {

// TODO Auto-generated method stub

String loginType = "password";

String name = "name";

String password = "password";

Login login = LoginManager.factory\(loginType\);

boolean bool = login.verify\(name, password\);

if \(bool\) {

/\*\*

\* 业务逻辑

\*/

} else {

/\*\*

\* 业务逻辑

\*/

}

}

}

来自 &lt;[http://www.cnblogs.com/java-my-life/archive/2012/03/22/2412308.html&gt](http://www.cnblogs.com/java-my-life/archive/2012/03/22/2412308.html&gt);

