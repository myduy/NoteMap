在传统的 Java 应用中，Bean 的生命周期很简单，使用关键字 new 实例化 Bean，当不需要该 Bean 时，由 Java 自动进行垃圾回收。

Spring 中 Bean 的生命周期较复杂，可以表示为：Bean 的定义 -> Bean 的初始化 -> Bean 的使用 -> Bean 的销毁。

Spring 根据 Bean 的作用域来选择管理方式。对于 singleton 作用域的 Bean，Spring 能够精确地知道该 Bean 何时被创建，何时初始化完成，以及何时被销毁；而对于 prototype 作用域的 Bean，Spring 只负责创建，当容器创建了 Bean 的实例后，Bean 的实例就交给客户端代码管理，Spring 容器将不再跟踪其生命周期。

## Spring Bean生命周期执行流程

Spring 容器在确保一个 Bean 能够使用之前，会进行很多工作。Spring 容器中 Bean 的生命周期流程如下图所示。



![Bean的生命周期](F:\笔记\Spring\png\05_01.png)
图 1 Bean 的生命周期

Bean 生命周期的整个执行过程描述如下。

1. Spring 启动，查找并加载需要被 Spring 管理的 Bean，并实例化 Bean。
2. 利用依赖注入完成 Bean 中所有属性值的配置注入。
3. 如果 Bean 实现了 BeanNameAware 接口，则 Spring 调用 Bean 的 setBeanName() 方法传入当前 Bean 的 id 值。
4. 如果 Bean 实现了 BeanFactoryAware 接口，则 Spring 调用 setBeanFactory() 方法传入当前工厂实例的引用。
5. 如果 Bean 实现了 ApplicationContextAware 接口，则 Spring 调用 setApplicationContext() 方法传入当前 ApplicationContext 实例的引用。
6. 如果 Bean 实现了 [BeanPostProcessor](http://c.biancheng.net/spring/bean-post-processor.html) 接口，则 Spring 调用该接口的预初始化方法 postProcessBeforeInitialzation() 对 Bean 进行加工操作，此处非常重要，Spring 的 AOP 就是利用它实现的。
7. 如果 Bean 实现了 InitializingBean 接口，则 Spring 将调用 afterPropertiesSet() 方法。
8. 如果在配置文件中通过 init-method 属性指定了初始化方法，则调用该初始化方法。
9. 如果 [BeanPostProcessor ](http://c.biancheng.net/spring/bean-post-processor.html)和 Bean 关联，则 Spring 将调用该接口的初始化方法 postProcessAfterInitialization()。此时，Bean 已经可以被应用系统使用了。
10. 如果在 <bean> 中指定了该 Bean 的作用域为 singleton，则将该 Bean 放入 Spring IoC 的缓存池中，触发 Spring 对该 Bean 的生命周期管理；如果在 <bean> 中指定了该 Bean 的作用域为 prototype，则将该 Bean 交给调用者，调用者管理该 Bean 的生命周期，Spring 不再管理该 Bean。
11. 如果 Bean 实现了 DisposableBean 接口，则 Spring 会调用 destory() 方法销毁 Bean；如果在配置文件中通过 destory-method 属性指定了 Bean 的销毁方法，则 Spring 将调用该方法对 Bean 进行销毁。


Spring 为 Bean 提供了细致全面的生命周期过程，实现特定的接口或设置 <bean> 的属性都可以对 Bean 的生命周期过程产生影响。建议不要过多的使用 Bean 实现接口，因为这样会导致代码的耦合性过高。

了解 Spring 生命周期的意义就在于，可以利用 Bean 在其存活期间的指定时刻完成一些相关操作。一般情况下，会在 Bean 被初始化后和被销毁前执行一些相关操作。

Spring 官方提供了 3 种方法实现初始化回调和销毁回调：

1. 实现 InitializingBean 和 DisposableBean 接口；
2. 在 XML 中配置 init-method 和 destory-method；
3. 使用 @PostConstruct 和 @PreDestory 注解。


在一个 Bean 中有多种生命周期回调方法时，优先级为：注解 > 接口 > XML。

> 不建议使用接口和注解，这会让 pojo 类和 Spring 框架紧耦合。

## 初始化回调

#### 1. 使用接口

org.springframework.beans.factory.InitializingBean 接口提供了以下方法：

```java
void afterPropertiesSet() throws Exception;
```

您可以实现以上接口，在 afterPropertiesSet 方法内指定 Bean 初始化后需要执行的操作。

```java
<bean id="..." class="..." />
public class User implements InitializingBean {
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("调用接口：InitializingBean，方法：afterPropertiesSet，无参数");
    }
}
```

#### 2. 配置XML

可以通过 init-method 属性指定 Bean 初始化后执行的方法。

```java
<bean id="..." class="..." init-method="init"/>
public class User {
    public void init() {
        System.out.println("调用init-method指定的初始化方法:init" );
    }
}
```

#### 3. 使用注解

使用 @PostConstruct 注解标明该方法为 Bean 初始化后的方法。

```java
public class ExampleBean {
    @PostConstruct
    public void init() {
        System.out.println("@PostConstruct注解指定的初始化方法:init" );
    }
}
```

## 销毁回调

#### 1. 使用接口

org.springframework.beans.factory.DisposableBean 接口提供了以下方法：

```java
void destroy() throws Exception;
```

您可以实现以上接口，在 destroy 方法内指定 Bean 初始化后需要执行的操作。

```java
<bean id="..." class="..." />
public class User implements InitializingBean {
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("调用接口：InitializingBean，方法：afterPropertiesSet，无参数");
    }
}
```

#### 2. 配置XML

可以通过 destroy-method 属性指定 Bean 销毁后执行的方法。

```java
<bean id="..." class="..." destroy-method="destroy"/>
public class User {
    public void destroy() {
        System.out.println("调用destroy-method指定的销毁方法:destroy" );
    }
}
```



#### 3. 使用注解

使用 @PreDestory 注解标明该方法为 Bean 销毁前执行的方法。

```java
public class ExampleBean {
    @PreDestory 
    public void destroy() {
        System.out.println("@PreDestory注解指定的初始化方法:destroy" );
    }
}
```

## 示例

下面使用 Eclipse IDE 演示如何通过配置 XML 的方式实现初始化回调和销毁回调，步骤如下：

1. 创建 SpringDemo 项目，并在 src 目录下创建 net.biancheng 包。
2. 添加相应的 jar 包，可以参考《[第一个Spring程序](http://c.biancheng.net/spring/eclipse-example.html)》一节。
3. 在 net.biancheng 包下创建 HelloWorld 和 MainApp 类。
4. 在 src 目录下创建 Spring 配置文件 Beans.xml。
5. 运行 SpringDemo 项目。


HelloWorld 类代码如下。

```java

public class HelloWorld {
    private String message;
    public void setMessage(String message) {
        this.message = message;
    }
    public void getMessage() {
        System.out.println("message : " + message);
    }
    public void init() {
        System.out.println("Bean正在进行初始化");
    }
    public void destroy() {
        System.out.println("Bean将要被销毁");
    }
}
```


MainApp 类代码如下，该类中我们使用 AbstractApplicationContext 类的 registerShutdownHook() 方法，来确保正常关机并调用相关的 destroy() 方法。

```java
import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class MainApp {
    public static void main(String[] args) {
        AbstractApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
        HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
        obj.getMessage();
        context.registerShutdownHook();
    
```

Beans.xml 配置文件代码如下。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="helloWorld" class="net.biancheng.HelloWorld"
        init-method="init" destroy-method="destroy">
        <property name="message" value="Hello World！" />
    </bean>
</beans>
```


运行结果如下。

Bean正在进行初始化
message : Hello World！
Bean将要被销毁

## 默认的初始化和销毁方法

如果多个 Bean 需要使用相同的初始化或者销毁方法，不用为每个 bean 声明初始化和销毁方法，可以使用 default-init-method 和 default-destroy-method 属性，如下所示。

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd"
    default-init-method="init"
    default-destroy-method="destroy">
    <bean id="..." class="...">
        ...
    </bean>
</beans>
```