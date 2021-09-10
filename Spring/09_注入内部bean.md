Java 中在类内部定义的类称为内部类，同理在 Bean 中定义的 Bean 称为内部 Bean。注入内部 Bean 使用 <property> 和 <constructor-arg> 中的 <bean> 标签。如下所示。

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="outerBean" class="...">
        <property name="target">
            <!-- 定义内部Bean -->
            <bean class="..." />
        </property>
    </bean>
</beans>
```

内部 Bean 的定义不需要指定 id 和 name 。如果指定了，容器也不会将其作为区分 Bean 的标识符，反而会无视内部 Bean 的 scope 属性。所以内部 Bean 总是匿名的，而且总是随着外部 Bean 创建。

> 在实际开发中很少注入内部 Bean，因为开发者无法将内部的 Bean 注入外部 Bean 以外的其它 Bean。

## 示例

下面使用 Eclipse IDE 演示如何注入内部 Bean，步骤如下：

1. 创建 SpringDemo 项目，并在 src 目录下创建 net.biancheng 包。
2. 添加相应的 jar 包，可以参考《[第一个Spring程序](http://c.biancheng.net/spring/first-spring.html)》一节。
3. 在 net.biancheng 包下创建 Person、Man 和 MainApp 类。
4. 在 src 目录下创建 Spring 配置文件 Beans.xml。
5. 运行 SpringDemo 项目。


Person 类代码如下。

```java

public class Person {
    private Man man;
    public Man getMan() {
        return man;
    }
    public void setMan(Man man) {
        System.out.println("在setMan方法内");
        this.man = man;
    }
    public void man() {
        man.show();
    }
}
```

Man 类代码如下。

```java
public class Man {
    private String name;
    private int age;
    public Man() {
        System.out.println("在man的构造函数内");
    }
    public Man(String name, int age) {
        System.out.println("在man的有参构造函数内");
        this.name = name;
        this.age = age;
    }
    public void show() {
        System.out.println("名称：" + name + "\n年龄：" + age);
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
```

Beans.xml 配置文件如下。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="person" class="net.biancheng.Person">
        <property name="man">
            <bean class="net.biancheng.Man">
                <property name="name" value="bianchengbang" />
                <property name="age" value="12" />
            </bean>
        </property>
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
        Person person = (Person) context.getBean("person");
        person.man();
    }
}
```

运行结果如下。

在man的有参构造函数内
在Person的构造函数内
名称：bianchengbang
年龄：12