# JAVA 基础

## JAVA八大基本类型

byte；short；int；long；char，boolean；float；double
在实际项目中，一般建议使用包装类进行操作。

## JAVA的三大特性

### 继承

> 子类继承父类，子类可以调用父类非私有的方法和属性。java只有单继承。

#### 继承和实现的区别
1. java只支持单继承,可以多实现.
2. 修饰不同,继承使用extends,实现使用inplements
3. 属性不同,接口中只能定义全局变量和无实现的方法,继承可以定义属性方法,常量等.
4. 接口被类实现时,在类中一定实现接口的抽象方法,继承想调用哪个方法就调用哪个方法.
   
### 多态

> 就是根据传入的对象的不同而执行不同的行为方式

#### 多态存在的条件
存在继承，父类引用指向子类对象，子类重写父类方法

>被static,final,private修饰不能使用多态

#### 优点
编译时看左边的父类对象,运行时看右边子类对象
可以拓展父类的功能

### 封装

> 就是把数据和操作数据的方法封装在一起，通过使用操作数据的方法来操作数据。
> 优点： 提高安全性和可维护性，降低耦合度，可以不关注内部细节。

## 构造方法和一般方法的区别

构造方法是在创建类时调用,只会调用一次,一般方法可以随时调用,调用多次

## JDK和JRE的区别

> JRE是java运行时环境,他是运行Java应用程序必须的程序包,它包含了JVM,java核心类库,以及其他支持java程序运行的基础组件.
> JDK是java程序开发包,不仅包含JRE还包含编译,调试java程序所需的全套工具,例如java编译器javac,java文档生成器javadoc,打包工具jar,以及源代码调试器jdb等.
> 简单来说就是JDK包含JRE.


## JAVA 运行时异常有哪些

- 类找不到异常ClassNotException: 指定的类找不到,类名或路径加载错误,一般通过类名字符串加载时出现
- 数组下标越界异常IndexOutOfBoundsException
- 类型转换异常ClassCastException:强转错误
- 字符串转换数字异常NumberFormatException
- 空指针异常NullPointerException
- 算数异常ArithmeticException:1/0
- sql异常SQLException

## 抽象类和接口的区别
> 抽象类描述的是事物的本质:是一个什么东西.是用来被继承的.接口描述的是功能:有什么用,是用来被实现的.
- 接口是:interface,抽象类是abstrat
- 抽象类有构造器,到那时不能创建对象,目的是为了供子类调用,接口没有构造器.
- 接口的所有方法都是抽象方法,所有属性都是静态常量;抽象类中可以有非抽象的方法和非常量的属性
- 抽象类只能单继承,接口可以多实现
## ==和equals()的区别

- > == : 基本数据类型直接比值,引用类型比较内存地址
- > equals() 方法是Object类的方法,底层和==一样,可以被重写,八大基本类型的包装类和String都重写了该方法和hashCode方法

## 重写equals()方法为什么必须重写hashcode方法

> 因为为了保证是一个对象,如果重写了equals方法,不重写hashcode方法会导致equals相等,hashcode不同的情况.
> 使用hashcode提前校验,可以避免每一次都调用equals方法提高效率

## String StringBuffer和SrtingBuilder
- String 是一个常量类,存在于字符串常量池内,提高内存利用率,在创建字符串时JVM会检查池内是否存在,如果存在返回其引用,不存在实例化一个字符串,存入常量池,然后返回其引用
-  String的一个可变工作类,可以对一个字符串进行多次修改,不会创建新对象
   - StringBuffer : 线程安全,每个方法都加入了同步锁,适合多线程的环境执行.
   - StringBuilder : 线程不安全,适合单线程环境执行.
## Object 常用方法
- eqluas
- hashcode
- clone
- wait
- notify
- notifyall
- finalize
## String 常用方法

- length
- trim
- join
- split
- subString
- indexOf
- lastIndexOf
- concat



## java创建对象的方式

1. 使用new关键字,调用构造器创建
2. 使用newInstance方法,反射调用创建
3. 使用反序列化方法readObject()类必须实现Serializable接口
4. 实现cloneAble接口,使用clone方法,进行拷贝.
