在配置文件中，除了可以定义 Bean 的属性值和相互之间的依赖关系，还可以声明 Bean 的作用域。例如，如果每次获取 Bean 时，都需要一个 Bean 实例，那么应该将 Bean 的 scope 属性定义为 prototype，如果 Spring 需要每次都返回一个相同的 Bean 实例，则应将 Bean 的 scope 属性定义为 singleton。

## 作用域的种类

Spring 容器在初始化一个 Bean 实例时，同时会指定该实例的作用域。Spring 5 支持以下 6 种作用域。

#### 1）singleton

默认值，单例模式，表示在 Spring 容器中只有一个 Bean 实例，Bean 以单例的方式存在。

#### 2）prototype

原型模式，表示每次通过 Spring 容器获取 Bean 时，容器都会创建一个 Bean 实例。

#### 3）request

每次 HTTP 请求，容器都会创建一个 Bean 实例。该作用域只在当前 HTTP Request 内有效。

#### 4）session

同一个 HTTP Session 共享一个 Bean 实例，不同的 Session 使用不同的 Bean 实例。该作用域仅在当前 HTTP Session 内有效。

#### 5）application

同一个 Web 应用共享一个 Bean 实例，该作用域在当前 ServletContext 内有效。

类似于 singleton，不同的是，singleton 表示每个 IoC 容器中仅有一个 Bean 实例，而同一个 Web 应用中可能会有多个 IoC 容器，但一个 Web 应用只会有一个 ServletContext，也可以说 application 才是 Web 应用中货真价实的单例模式。

#### 6）websocket

websocket 的作用域是 WebSocket ，即在整个 WebSocket 中有效。

> 注意：Spring 5 版本之前还支持 global Session，该值表示在一个全局的 HTTP Session 中，容器会返回该 Bean 的同一个实例。一般用于 Portlet 应用环境。Spring 5.2.0 版本中已经将该值移除了。

request、session、application、websocket 和 global Session 作用域只能在 Web 环境下使用，如果使用 ClassPathXmlApplicationContext 加载这些作用域中的任意一个的 Bean，就会抛出以下异常。

java.lang.IllegalStateException: No Scope registered for scope name 'xxx'


下面我们详细讲解常用的两个作用域：singleton 和 prototype。

## singleton

singleton 是 Spring 容器默认的作用域。当 Bean 的作用域为 singleton 时，Spring 容器中只会存在一个共享的 Bean 实例。该 Bean 实例将存储在高速缓存中，并且所有对 Bean 的请求，只要 id 与该 Bean 定义相匹配，都会返回该缓存对象。

通常情况下，这种单例模式对于无会话状态的 Bean（如 DAO 层、Service 层）来说，是最理想的选择。

在 Spring 配置文件中，可以使用 <bean> 元素的 scope 属性，将 Bean 的作用域定义成 singleton，其配置方式如下所示：

```xml
<bean id="..." class="..." scope="singleton"/>
```

#### 例 1

下面使用 Eclipse IDE 演示如何将 Bean 的作用域指定为 singleton，步骤如下：

1. 创建 SpringDemo 项目，并在 src 目录下创建 net.biancheng 包。
2. 添加相应的 jar 包，可以参考《[第一个Spring程序](http://c.biancheng.net/spring/first-spring.html)》一节。
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
}
```

MainApp 类如下。

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class MainApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
        HelloWorld objA = (HelloWorld) context.getBean("helloWorld");
        objA.setMessage("对象A");
        objA.getMessage();
        HelloWorld objB = (HelloWorld) context.getBean("helloWorld");
        objB.getMessage();
    }
}
```

Beans.xml 文件内容如下。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"    
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"    
       xsi:schemaLocation="http://www.springframework.org/schema/beans   
                           http://www.springframework.org/schema/beans/spring-beans-3.0.xsd"
       >    
    <bean id="helloWorld" class="xxxxx.HelloWorld" scope="singleton"/>      
</beans>
```

运行结果如下。

message : 对象A
message : 对象A

从运行结果可以看出，两次输出内容相同，这说明 Spring 容器只创建了一个 HelloWorld 类的实例。由于 Spring 容器默认作用域是 singleton，所以如果省略 scope 属性，其输出结果也会是一个实例。

## prototype

对于 prototype 作用域的 Bean，Spring 容器会在每次请求该 Bean 时都创建一个新的 Bean 实例。prototype 作用域适用于需要保持会话状态的 Bean（如 Struts2 的 Action 类）。

在 Spring 配置文件中，可以使用 <bean> 元素的 scope 属性，将 Bean 的作用域定义成 prototype，其配置方式如下所示：

```xml
<bean id="..." class="..." scope="prototype"/>
```

#### 例 2

在例 1 的基础上，修改配置文件 Beans.xml，内容如下。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"    xsi:schemaLocation="http://www.springframework.org/schema/beans   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">    
    <bean id="helloWorld" class="net.biancheng.HelloWorld" scope="prototype"/>      
</beans>
```

运行结果如下。

message : 对象A
message : null

从运行结果可以看出，两次输出的内容并不相同，这说明在 prototype 作用域下，Spring 容器创建了两个不同的 HelloWorld 实例。