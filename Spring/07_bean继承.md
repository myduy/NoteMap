Bean 定义可以包含很多配置信息，包括构造函数参数、属性值和容器的一些具体信息，如初始化方法、销毁方法等。子 Bean 可以继承父 Bean 的配置数据，根据需要，子 Bean 可以重写值或添加其它值。

需要注意的是，Spring Bean 定义的继承与 Java 中的继承无关。您可以将父 Bean 的定义作为一个模板，其它子 Bean 从父 Bean 中继承所需的配置。

在配置文件中通过 parent 属性来指定继承的父 Bean。

## 示例

下面使用 Eclipse IDE 演示 Bean 继承，步骤如下：

1. 创建 SpringDemo 项目，并在 src 目录下创建 net.biancheng 包。
2. 添加相应的 jar 包，可以参考《[第一个Spring程序](http://c.biancheng.net/spring/first-spring.html)》一节。
3. 在 net.biancheng 包下创建 HelloWorld、HelloChina 和 MainApp 类。
4. 在 src 目录下创建 Spring 配置文件 Beans.xml。
5. 运行 SpringDemo 项目。


HelloWorld 类代码如下。

```java
public class HelloWorld {
    private String message1;
    private String message2;
    public void setMessage1(String message) {
        this.message1 = message;
    }
    public void setMessage2(String message) {
        this.message2 = message;
    }
    public void getMessage1() {
        System.out.println("World Message1 : " + message1);
    }
    public void getMessage2() {
        System.out.println("World Message2 : " + message2);
    }
}
```

HelloChina 类代码如下。

```java
public class HelloChina {
    private String message1;
    private String message2;
    private String message3;
    public void setMessage1(String message) {
        this.message1 = message;
    }
    public void setMessage2(String message) {
        this.message2 = message;
    }
    public void setMessage3(String message) {
        this.message3 = message;
    }
    public void getMessage1() {
        System.out.println("China Message1 : " + message1);
    }
    public void getMessage2() {
        System.out.println("China Message2 : " + message2);
    }
    public void getMessage3() {
        System.out.println("China Message3 : " + message3);
    }
}
```

在配置文件中，分别为 HelloWorld 中的 message1 和 message2 赋值。使用 parent 属性将 HelloChain 定义为 HelloWorld 的子类，并为 HelloChain 中的 message1 和 message3 赋值。Beans.xml 文件代码如下。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="helloWorld" class="net.biancheng.HelloWorld">
        <property name="message1" value="Hello World！" />
        <property name="message2" value="Hello World2！" />
    </bean>
   
    <bean id="helloChina" class="net.biancheng.HelloChina"
        parent="helloWorld">
        <property name="message1" value="Hello China！" />
        <property name="message3" value="Hello China3！" />
    </bean>
</beans>
```

MainApp 类代码如下。

```java

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class MainApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
        HelloWorld objA = (HelloWorld) context.getBean("helloWorld");
        objA.getMessage1();
        objA.getMessage2();
        HelloChina objB = (HelloChina) context.getBean("helloChina");
        objB.getMessage1();
        objB.getMessage2();
        objB.getMessage3();
    }
}
```

运行结果如下。

World Message1 : Hello World！
World Message2 : Hello World2！
China Message1 : Hello China！
China Message2 : Hello World2！
China Message3 : Hello China3！

由结果可以看出，我们在创建 helloChina 时并没有给 message2 赋值，但是由于 Bean 的继承，将值传递给了 message2。

## Bean定义模板

您可以创建一个 Bean 定义模板，该模板只能被继承，不能被实例化。创建 Bean 定义模板时，不用指定 class 属性，而是指定 abstarct="true" 将该 Bean 定义为抽象 Bean，如下所示。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="beanTeamplate" abstract="true">
        <property name="message1" value="Hello World!" />
        <property name="message2" value="Hello World2!" />
        <property name="message3" value="Hello World3!" />
    </bean>
    <bean id="helloChina" class="net.biancheng.HelloChina"
        parent="beanTeamplate">
        <property name="message1" value="Hello China!" />
        <property name="message3" value="Hello China!" />
    </bean>
</beans>
```