Spring 通过读取 XML 或 Java 注解中的信息来获取哪些对象需要实例化。

Spring 提供 2 种不同类型的 IoC 容器，即 BeanFactory 和 ApplicationContext 容器。

## 1. BeanFactory 容器

BeanFactory 是最简单的容器，由 org.springframework.beans.factory.BeanFactory 接口定义，采用懒加载（lazy-load），所以容器启动比较快。BeanFactory 提供了容器最基本的功能。

为了能够兼容 Spring 集成的第三方框架（如 BeanFactoryAware、InitializingBean、DisposableBean），所以目前仍然保留了该接口。

简单来说，BeanFactory 就是一个管理 Bean 的工厂，它主要负责初始化各种 Bean，并调用它们的生命周期方法。

BeanFactory 接口有多个实现类，最常见的是 org.springframework.beans.factory.xml.XmlBeanFactory。使用 BeanFactory 需要创建 XmlBeanFactory 类的实例，通过 XmlBeanFactory 类的构造函数来传递 Resource 对象。如下所示。

```java
Resource resource = new ClassPathResource("applicationContext.xml"); BeanFactory factory = new XmlBeanFactory(resource);  
```

## 2. ApplicationContext 容器

ApplicationContext 继承了 BeanFactory 接口，由 org.springframework.context.ApplicationContext 接口定义，对象在启动容器时加载。ApplicationContext 在 BeanFactory 的基础上增加了很多企业级功能，例如 AOP、国际化、事件支持等。

ApplicationContext 接口有两个常用的实现类，具体如下。

#### 1）ClassPathXmlApplicationContext

该类从类路径 ClassPath 中寻找指定的 XML 配置文件，并完成 ApplicationContext 的实例化工作，具体如下所示。

```java
ApplicationContext applicationContext = new ClassPathXmlApplicationContext(String configLocation);
```

在上述代码中，configLocation 参数用于指定 Spring 配置文件的名称和位置，如 Beans.xml。

#### 2）FileSystemXmlApplicationContext

该类从指定的文件系统路径中寻找指定的 XML 配置文件，并完成 ApplicationContext 的实例化工作，具体如下所示。

```java
ApplicationContext applicationContext = new FileSystemXmlApplicationContext(String configLocation);
```

它与 ClassPathXmlApplicationContext 的区别是：在读取 Spring 的配置文件时，FileSystemXmlApplicationContext 不会从类路径中读取配置文件，而是通过参数指定配置文件的位置。即 FileSystemXmlApplicationContext 可以获取类路径之外的资源，如“F:/workspaces/Beans.xml”。

通常在 Java 项目中，会采用 ClassPathXmlApplicationContext 类实例化 ApplicationContext 容器的方式，而在 Web 项目中，ApplicationContext 容器的实例化工作会交由 Web 服务器完成。Web 服务器实例化 ApplicationContext 容器通常使用基于 ContextLoaderListener 实现的方式，它只需要在 web.xml 中添加如下代码：

```xml
<!--指定Spring配置文件的位置，有多个配置文件时，以逗号分隔-->
<context-param>    
    <param-name>contextConfigLocation</param-name> 
    <!--spring将加载spring目录下的applicationContext.xml文件-->   
    <param-value>classpath:spring/applicationContext.xml</param-value></context-param>
<!--指定以ContextLoaderListener方式启动Spring容器-->
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener    
    </listener-class>
</listener>
```

需要注意的是，BeanFactory 和 ApplicationContext 都是通过 XML 配置文件加载 Bean 的。

二者的主要区别在于，如果 Bean 的某一个属性没有注入，使用 BeanFacotry 加载后，第一次调用 getBean() 方法时会抛出异常，而 ApplicationContext 则会在初始化时自检，这样有利于检查所依赖的属性是否注入。