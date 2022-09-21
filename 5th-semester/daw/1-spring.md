# [Spring Framework](https://spring.io/)

> *The Spring Framework is an application framework and inversion of control container for the Java platform. The framework's core features can be used by any Java application, but there are extensions for building web applications on top of the Java EE platform.*

## Spring Context

* **Container of inversion of control and dependency injection**
* System that allows us to **manage the composition and life cycle of objects and their dependencies, dynamically**;
* *The context is the Spring component responsible for instantiating and managing instances, such as controller instances.*

### Object creation and dependency injection

* Creation of the application graph of objects;
* Instantiation of the objects and their dependencies, passing the dependencies to the objects.

### Inversion of Control - IoC

**The dependent object receives and uses the dependencies, but it does not create them.**

<p align="center">
    <img src="./docs/dependencies.png" alt="Inversion of Control" align="center"/>
</p>

* **Constructor injection**: dependency injection through the constructor;
* **Wiring**: establish the dependencies between objects;

---

### Examples

Steps:

1. Creation of the context;
2. Add the bean definitions to the context;
3. Refresh the context, to take in consideration the new bean definitions;
4. Use the context to get the beans.

**Bean**: *A bean is an object that is created and managed by the context.*

#### 1st Example

Considering the following classes and dependencies (*dependent -> dependency*):

ComponentC -> ComponentB ->  ComponentA

```kotlin
 // Create the context
val context = AnnotationConfigApplicationContext()

// Add the bean definitions
context.register(
    ComponentA::class.java,
    ComponentB::class.java,
    ComponentC::class.java
)

// Refresh the context
context.refresh()

// Get the beans (example: ComponentB)
val componentB = context.getBean<ComponentB>()
```

* If the ComponentA was not registered, the context would not be able to create the ComponentB, throwing an exception;
* If the ComponentB was not registered, the context would not be able to create it, throwing an exception.

#### 2nd Example

You can also add the bean definitions given a package, using the `scan` method. In this case, the context will search for the classes annotated with `@Component` and register them:

```kotlin
// Create the context
val context = AnnotationConfigApplicationContext()

// Add the bean definitions
context.scan("package.name")
```

**Note**: You can also use the context with components initialized with **lists of dependencies**. This can be useful, for example, when creating a router, where you can have a list of controllers and inject them into the router.


#### 3rd Example

If a component registered in the context is not initialized by a constructor, but with a static method, you can use the `@Bean` annotation to register it.

For example, a HttpClient is initialized with the `newBuilder` method, so we create a function that returns a HttpClient and annotate it with `@Bean`:

```kotlin
class BeanConfig {
    @Bean
    fun httpClient(cookieHandler: CookieHandler): HttpClient = HttpClient
        .newBuilder()
        .cookieHandler(cookieHandler)
        .build()
}

// Create the context
val context = AnnotationConfigApplicationContext()

// Add the bean definitions
context.register(BeanConfig::class.java)
```

---

### Summary (in Portuguese)

* Estereótipo: papel que instâncias de classes desempenham no sistema;
  * Contentores de funcionalidade (e.g. handlers, controllers, routers, etc);
  * Contentores de informação estruturada (e.g. classes);

* Relação Dependente -> Dependência
  * IoC: o dependente não cria as dependências;
  * DI: o dependente recebe e usa as dependências;
* Composição do grafo de instâncias:
  * Manual;
  * Contentor de Injeção de Dependências (IoC Container) -> Spring Context;
* Código é independente da existência do contexto.

<p align="center">
    <img src="./docs/context.png" alt="Context" align="center"/>
</p>

---
---

## [Spring MVC](https://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/html/mvc.html)

> Spring MVC is a library/framework for handling HTTP requests, providing higher level features on top of the [Java Servlet API](https://javaee.github.io/servlet-spec/).

* Based on the [Model-View-Controller](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (MVC) pattern;
* Usage of an underlying servlet server, such as [Jetty](https://www.eclipse.org/jetty/), [Tomcat](https://tomcat.apache.org/), etc;
* ...

#### [Servlet](https://docs.oracle.com/javaee/6/tutorial/doc/bnafe.html)

> A servlet is a Java programming language class that is used to extend the capabilities of servers that host applications accessed by means of a request-response programming model.

TODO: Add more information about servlets and Spring MVC.