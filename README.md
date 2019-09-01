# SpringFramework
basic concepts of Spring framework.

# Dependency Injection (DI)
The technology that Spring is most identified with is the Dependency Injection (DI) flavor of Inversion of Control. The Inversion of Control (IoC) is a general concept, and it can be expressed in many different ways. Dependency Injection is merely one concrete example of Inversion of Control.

When writing a complex Java application, application classes should be as independent as possible of other Java classes to increase the possibility to reuse these classes and to test them independently of other classes while unit testing. Dependency Injection helps in gluing these classes together and at the same time keeping them independent.

What is dependency injection exactly? Let's look at these two words separately. Here the dependency part translates into an association between two classes. For example, class A is dependent of class B. Now, let's look at the second part, injection. All this means is, class B will get injected into class A by the IoC.

Dependency injection can happen in the way of passing parameters to the constructor or by post-construction using setter methods. As Dependency Injection is the heart of Spring Framework, we will explain this concept in a separate chapter with relevant example.

# Aspect Oriented Programming (AOP)
One of the key components of Spring is the Aspect Oriented Programming (AOP) framework. The functions that span multiple points of an application are called cross-cutting concerns and these cross-cutting concerns are conceptually separate from the application's business logic. There are various common good examples of aspects including logging, declarative transactions, security, caching, etc.

The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. DI helps you decouple your application objects from each other, while AOP helps you decouple cross-cutting concerns from the objects that they affect.

The AOP module of Spring Framework provides an aspect-oriented programming implementation allowing you to define method-interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated. 

# Inversion of Control Container
The Spring container is at the core of the Spring Framework. 
The container will do the following task:- 
  1. Create the objects, 
  2. Wire them together, 
  3. Configure them, and 
  4. Manage their complete life cycle from creation till destruction

The Spring container uses DI to manage the components that make up an application. These objects are called Spring Beans.
The container get instructions on what objects to be instantiate, configure and assembled by reading the configuration metadata provided. 

The configuration metadata can be in any form provided below:
  1. XML based
  2. Java Annotations
  3. Java Codes

The Spring IoC container makes use of Java POJO classes and configuration metadata to produce a fully configured and executable system or application.
  
                                                                             Java Pojo Clasees
                                                                                   |
                                                                                   |
                                                                                   |
                                                                                   \/
                        Meta Data(XML,Java Annotation, Java codes)--------> The Spring Container
                                                                                   |
                                                                                   |   <--- Final Result
                                                                                   |
                                                                                   \/
                                                                            Ready to use Application



Spring provides the following two distinct types of containers.
  1. Spring BeanFactory Container
  2. Spring ApplicationContext container

# Spring BeanFactory Container
This is the simplest container providing the basic support for DI and is defined by the org.springframework.beans.factory.BeanFactory interface. 
The BeanFactory and related interfaces, such as BeanFactoryAware, InitializingBean, DisposableBean, are still present in Spring for the purpose of backward compatibility with a large number of third-party frameworks that integrate with Spring.

# Spring ApplicationContext Container
This container adds more enterprise-specific functionality such as the ability to resolve textual messages from a properties file and the ability to publish application events to interested event listeners. This container is defined by the org.springframework.context.ApplicationContext interface.

The ApplicationContext container includes all functionality of the BeanFactorycontainer, so it is generally recommended over BeanFactory. BeanFactory can still be used for lightweight applications like mobile devices or applet-based applications where data volume and speed is significant.


# Spring - Bean Definition
The objects that are form the backbone of your application and managed by the spring IOC container are called as Beans.
A beans is an object that is instantiate, assembled and otherwise managed by IOC container.
These beans are created using configuration metadata that you supply to the spring IOC container. 

Bean definition contains the information called configuration metadata, which is needed for the container to know the following −
  1. How to create a bean
  2. Bean's lifecycle details
  3. Bean's dependencies

All the above configuration metadata translates into a set of the following properties that make up each bean definition.
1. class
  This attribute is mandatory and specifies the bean class to be used to create the bean.

2. name
  This attribute specifies the bean identifier uniquely. In XMLbased configuration metadata, you use the id and/or name attributes to specify the bean identifier(s).

3. scope
  This attribute specifies the scope of the objects created from a particular bean definition and it will be discussed in bean scopes chapter.

4. constructor-arg
  This is used to inject the dependencies and will be discussed in subsequent chapters.

5. properties
  This is used to inject the dependencies and will be discussed in subsequent chapters.

6. autowiring mode
  This is used to inject the dependencies and will be discussed in subsequent chapters.

7. lazy-initialization mode
  A lazy-initialized bean tells the IoC container to create a bean instance when it is first requested, rather than at the startup.

8. initialization method
  A callback to be called just after all necessary properties on the bean have been set by the container. It will be discussed in bean life cycle chapter.

9. destruction method
  A callback to be used when the container containing the bean is destroyed. It will be discussed in bean life cycle chapter.
                                            

# Spring - Bean Scopes

When defining a <bean> you have the option of declaring a scope for that bean. For example, to force Spring to produce a new bean instance each time one is needed, you should declare the bean's scope attribute to be prototype. Similarly, if you want Spring to return the same bean instance each time one is needed, you should declare the bean's scope attribute to be singleton.

The Spring Framework supports the following five scopes, three of which are available only if you use a web-aware ApplicationContext.

  1. singleton
  - This scopes the bean definition to a single instance per Spring IoC container (default).
  2. prototype
  - This scopes a single bean definition to have any number of object instances.
  3. request
  - This scopes a bean definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext.
  4. session
  - This scopes a bean definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.
  5. global-session
  - This scopes a bean definition to a global HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.


# Spring - Bean Life Cycle

The life cycle of a Spring bean is easy to understand. When a bean is instantiated, it may be required to perform some initialization to get it into a usable state. Similarly, when the bean is no longer required and is removed from the container, some cleanup may be required.

Though, there are lists of the activities that take place behind the scene between the time of bean Instantiation and its destruction.

To define setup and teardown for a bean, we simply declare the <bean> with initmethod and/or destroy-method parameters. The init-method attribute specifies a method that is to be called on the bean immediately upon instantiation. Similarly, destroymethod specifies a method that is called just before a bean is removed from the container.
  
# Initialization callbacks
The org.springframework.beans.factory.InitializingBean interface specifies a single method −

```
void afterPropertiesSet() throws Exception;  

Thus, you can simply implement the above interface and initialization work can be done inside afterPropertiesSet() method as follows −

public class ExampleBean implements InitializingBean {
   public void afterPropertiesSet() {
      // do some initialization work
   }
}
```

In the case of XML-based configuration metadata, you can use the init-method attribute to specify the name of the method that has a void no-argument signature. For example −

```
<bean id = "exampleBean" class = "examples.ExampleBean" init-method = "init"/>
Following is the class definition −

public class ExampleBean {
   public void init() {
      // do some initialization work
   }
}
```

# Destruction callbacks
The org.springframework.beans.factory.DisposableBean interface specifies a single method −

```
void destroy() throws Exception;
Thus, you can simply implement the above interface and finalization work can be done inside destroy() method as follows −

public class ExampleBean implements DisposableBean {
   public void destroy() {
      // do some destruction work
   }
}
```

In the case of XML-based configuration metadata, you can use the destroy-method attribute to specify the name of the method that has a void no-argument signature. For example −
```
<bean id = "exampleBean" class = "examples.ExampleBean" destroy-method = "destroy"/>
Following is the class definition −

public class ExampleBean {
   public void destroy() {
      // do some destruction work
   }
}
```
It is recommended that you do not use the InitializingBean or DisposableBean callbacks, because XML configuration gives much flexibility in terms of naming your method.

Example below

```
import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainApp {
   public static void main(String[] args) {
      AbstractApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");

      HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
      obj.getMessage();
      context.registerShutdownHook();
   }
}

(Beans.xml)
<?xml version = "1.0" encoding = "UTF-8"?>

<beans xmlns = "http://www.springframework.org/schema/beans"
   xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation = "http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <bean id = "helloWorld" class = "HelloWorld" init-method = "init" 
      destroy-method = "destroy">
      <property name = "message" value = "Hello World!"/>
   </bean>

</beans>

public class HelloWorld {
   private String message;

   public void setMessage(String message){
      this.message = message;
   }
   public void getMessage(){
      System.out.println("Your Message : " + message);
   }
   public void init(){
      System.out.println("Bean is going through init.");
   }
   public void destroy() {
      System.out.println("Bean will destroy now.");
   }
}

```

# Spring - Bean Definition Inheritance
