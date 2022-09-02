# 一、Spring与SpringBoot

## 1、Spring能做什么

### 1.1、Spring的能力
![](image/SpringBoot2/image-20220822174911.png)

### 1.2、Spring的生态
https://spring.io/projects/spring-boot

覆盖了：
- web开发
- 数据访问
- 安全控制
- 分布式
- 消息服务
- 移动开发
- 批处理
- ......

### 1.3、Spring5重大升级

#### 1.3.1、响应式编程
![](image/SpringBoot2/image-20220822175050.png)

#### 1.3.2、内部源码设计
基于Java8的一些新特性，如：接口默认实现。重新设计源码架构。


## 2、为什么用SpringBoot
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".

能快速创建出生产级别的Spring应用

### 2.1、SpringBoot优点
- Create stand-alone Spring applications
  - 创建独立Spring应用
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
  - 内嵌web服务器
- Provide opinionated 'starter' dependencies to simplify your build configuration
  - 自动starter依赖，简化构建配置
- Automatically configure Spring and 3rd party libraries whenever possible
  - 自动配置Spring以及第三方功能
- Provide production-ready features such as metrics, health checks, and externalized configuration
  - 提供生产级别的监控、健康检查及外部化配置
- Absolutely no code generation and no requirement for XML configuration
  - 无代码生成、无需编写XML

> SpringBoot是整合Spring技术栈的一站式框架
> SpringBoot是简化Spring技术栈的快速开发脚手架

### 2.2、SpringBoot缺点
- 人称版本帝，迭代快，需要时刻关注变化
- 封装太深，内部原理复杂，不容易精通


## 3、时代背景

### 3.1、微服务
James Lewis and Martin Fowler (2014)  提出微服务完整概念。https://martinfowler.com/microservices/

> In short, the microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There is a bare minimum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.-- James Lewis and Martin Fowler (2014)

- 微服务是一种架构风格
- 一个应用拆分为一组小型服务
- 每个服务运行在自己的进程内，也就是可独立部署和升级
- 服务之间使用轻量级HTTP交互
- 服务围绕业务功能拆分
- 可以由全自动部署机制独立部署
- 去中心化，服务自治。服务可以使用不同的语言、不同的存储技术

### 3.2、分布式
![](image/SpringBoot2/image-20220822175131.png)

#### 分布式的困难
- 远程调用
- 服务发现
- 负载均衡
- 服务容错
- 配置管理
- 服务监控
- 链路追踪
- 日志管理
- 任务调度
- ......

#### 分布式的解决
- SpringBoot + SpringCloud

![](image/SpringBoot2/image-20220822175207.png)

### 3.3、云原生
原生应用如何上云。 Cloud Native

#### 上云的困难
- 服务自愈
- 弹性伸缩
- 服务隔离
- 自动化部署
- 灰度发布
- 流量治理
- ......

#### 上云的解决
![](image/SpringBoot2/image-20220822175457.png)


## 4、如何学习SpringBoot

### 4.1、官网文档架构
![](image/SpringBoot2/image-20220822175549.png)
![](image/SpringBoot2/image-20220822175556.png)

[查看版本新特性](https://github.com/spring-projects/spring-boot/wiki#release-notes)
[官网文档](https://spring.io/projects/spring-boot#learn)

![](image/SpringBoot2/image-20220822175708.png)



# 二、SpringBoot2入门

## 1、系统要求
- Java 8 & 兼容java14 .【17】
- Maven 3.3+【3.8】
- idea 2019.1.2【vscode1.70】

### 1.1、maven设置
```xml
<mirrors>
    <mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>https://maven.aliyun.com/repository/central</url>
    </mirror>
</mirrors>
<profiles>
    <profile>
        <id>jdk-1.8</id>
        <activation>
            <activeByDefault>true</activeByDefault>
            <jdk>1.8</jdk>
        </activation>
        <properties>
            <maven.compiler.source>1.8</maven.compiler.source>
            <maven.compiler.target>1.8</maven.compiler.target>
            <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
        </properties>
    </profile>
</profiles>
```


## 2、HelloWorld
需求：浏览发送/hello请求，响应 Hello，Spring Boot 2

### 2.1、创建maven工程
### 2.2、引入依赖
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.3.4.RELEASE</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

### 2.3、创建主程序
```java
/**
 * 主程序类
 * 
 * @SpringBootApplication：这是一个SpringBoot应用
 */
@SpringBootApplication
public class MainApplication {

    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class, args);
    }
}
```

### 2.4、编写业务
```java
@RestController // @RestController = @Controller + @ResponseBody
public class HelloController {

    @RequestMapping("/hello")
    public String handle01() {
        return "Hello, Spring Boot 2!";
    }

}
```

### 2.5、测试
直接运行main方法

### 2.6、简化配置
application.properties
```properties
server.port=8888
```

### 2.7、简化部署
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

把项目打成jar包，直接在目标服务器执行即可。

注意点：
- 取消掉cmd的快速编辑模式



# 三、了解自动配置原理

## 1、SpringBoot特点

### 1.1、依赖管理
父项目做依赖管理
```xml
<!-- 依赖管理 -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.3.4.RELEASE</version>
</parent>

<!-- 他的父项目 -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.4.RELEASE</version>
</parent>

<!-- 几乎声明了所有开发中常用的依赖的版本号,自动版本仲裁机制 -->
```

开发导入starter场景启动器
1. 见到很多 `spring-boot-starter-*` ：*就某种场景
2. 只要引入starter，这个场景的所有常规需要的依赖我们都自动引入
3. [SpringBoot所有支持的场景](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter)
4. 见到的 *-spring-boot-starter：第三方为我们提供的简化开发的场景启动器。
5. 所有场景启动器最底层的依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
    <version>2.3.4.RELEASE</version>
    <scope>compile</scope>
</dependency>
```

无需关注版本号，自动版本仲裁
1. 引入依赖默认都可以不写版本
2. 引入非版本仲裁的jar，要写版本号。

可以修改默认版本号
```xml
<!-- 1、查看spring-boot-dependencies里面规定当前依赖的版本 用的 key。 -->
<!-- 2、在当前项目里面重写配置 -->
<properties>
    <mysql.version>5.1.43</mysql.version>
</properties>
```

### 1.2、自动配置
- 自动配好Tomcat
  - 引入Tomcat依赖。
  - 配置Tomcat

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <version>2.3.4.RELEASE</version>
    <scope>compile</scope>
</dependency>
```

- 自动配好SpringMVC
  - 引入SpringMVC全套组件
  - 自动配好SpringMVC常用组件（功能）
- 自动配好Web常见功能，如：字符编码问题
  - SpringBoot帮我们配置好了所有web开发的常见场景
- 默认的包结构
  - 主程序所在包及其下面的所有子包里面的组件都会被默认扫描进来
  - 无需以前的包扫描配置
  - 想要改变扫描路径：`@SpringBootApplication(scanBasePackages="com.atguigu")`
    - 或者@ComponentScan 指定扫描路径

```java
@SpringBootApplication
// 等同于
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.atguigu.boot")
```

- 各种配置拥有默认值
  - 默认配置最终都是映射到某个类上，如：MultipartProperties
  - 配置文件的值最终会绑定每个类上，这个类会在容器中创建对象
- 按需加载所有自动配置项
  - 非常多的starter
  - 引入了哪些场景这个场景的自动配置才会开启
  - SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 依赖中
- ......


## 2、容器功能

### 2.1、组件添加

#### 1、@Configuration
- 基本使用
- Full模式与Lite模式
  - 示例
  - 最佳实战
    - 配置 类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断
    - 配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式

```java
// ==========@Configuration使用示例==========
/**
 * 1、配置类里面使用@Bean标注在方法上给容器注册组件，默认也是单实例的
 * 2、配置类本身也是组件
 * 3、proxyBeanMethods：代理bean的方法【默认true】
 *   Full(proxyBeanMethods = true)、【保证每个@Bean方法被调用多少次返回的组件都是单实例的】
 *   Lite(proxyBeanMethods = false)【每个@Bean方法被调用多少次返回的组件都是新创建的】
 * 组件依赖必须使用Full模式默认。其他默认使用Lite模式
 *
 */
@Configuration // 告诉SpringBoot这是一个配置类 == 配置文件
public class MyConfig {

    /**
     * Full：外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的单实例对象
     * 给容器中添加组件。
     * 方法名：组件的id。
     * 返回类型：组件类型。
     * @return 组件在容器中的实例
     */
    @Bean
    public User user01() {
        User zhangsan = new User("zhangsan", 18);
        // user组件依赖了Pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }

    @Bean("tom")
    public Pet tomcatPet() {
        return new Pet("tomcat");
    }
}
```

```java
// ==========@Configuration测试代码如下==========
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.atguigu.boot")
public class MainApplication {

    public static void main(String[] args) {
        // 1、返回我们IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

        // 2、查看容器里面的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }

        // 3、从容器中获取组件
        Pet tom01 = run.getBean("tom", Pet.class);
        Pet tom02 = run.getBean("tom", Pet.class);
        System.out.println("组件：" + (tom01 == tom02));

        // 4、com.atguigu.boot.config.MyConfig$$EnhancerBySpringCGLIB$$51f1e1ca@1654a892
        MyConfig bean = run.getBean(MyConfig.class);
        System.out.println(bean);

        // 如果@Configuration(proxyBeanMethods = true)代理对象调用方法。
        // SpringBoot总会检查这个组件是否在容器中有。
        // 保持组件单实例
        User user = bean.user01();
        User user1 = bean.user01();
        System.out.println(user == user1);

        User user01 = run.getBean("user01", User.class);
        Pet tom = run.getBean("tom", Pet.class);
        System.out.println("用户的宠物：" + (user01.getPet() == tom));

    }
}
```

#### 2、@Bean、@Component、@Controller、@Service、@Repository
#### 3、@ComponentScan、@Import
```java
/**
 * 4、@Import({User.class, DBHelper.class})
 * 给容器中自动创建出这两个类型的组件、默认组件的名字就是全类名
 */
@Import({ User.class, DBHelper.class })
@Configuration(proxyBeanMethods = false) // 告诉SpringBoot这是一个配置类 == 配置文件
public class MyConfig {
}
```

主程序类中的测试：
```java
//5、获取组件
String[] beanNamesForType = run.getBeanNamesForType(User.class);
System.out.println("======");
for (String s : beanNamesForType) {
    System.out.println(s);
}
//
DBHelper bean1 = run.getBean(DBHelper.class);
System.out.println(bean1);
```

[@Import 高级用法](https://www.bilibili.com/video/BV1gW411W7wy?p=8)

#### 4、@Conditional
条件装配：满足Conditional指定的条件，则进行组件注入

![](image/SpringBoot2/image-20220823083935.png)

```java
// ==========测试条件装配==========
@Configuration(proxyBeanMethods = false)
@ConditionalOnMissingBean(name = "tom")
public class MyConfig {

    @Bean
    // @ConditionalOnBean(name = "tom")
    public User user01() {
        User zhangsan = new User("zhangsan", 18);
        // user组件依赖了Pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }

    @Bean("tom22")
    public Pet tomcatPet() {
        return new Pet("tomcat");
    }

}
```

```java
public static void main(String[] args) {
    // 1、返回我们IOC容器
    ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);

    // 2、查看容器里面的组件
    String[] names = run.getBeanDefinitionNames();
    for (String name : names) {
        System.out.println(name);
    }

    boolean tom = run.containsBean("tom");
    System.out.println("容器中Tom组件：" + tom);

    boolean user01 = run.containsBean("user01");
    System.out.println("容器中user01组件：" + user01);

    boolean tom22 = run.containsBean("tom22");
    System.out.println("容器中tom22组件：" + tom22);

}
```

### 2.2、原生配置文件引入

#### 1、@ImportResource
```xml
<!-- ==========beans.xml========== -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="haha" class="com.atguigu.boot.bean.User">
        <property name="name" value="zhangsan"></property>
        <property name="age" value="18"></property>
    </bean>

    <bean id="hehe" class="com.atguigu.boot.bean.Pet">
        <property name="name" value="tomcat"></property>
    </bean>
</beans>
```

```java
@ImportResource("classpath:beans.xml")
public class MyConfig {}
```

```java
// ==========测试==========
boolean haha = run.containsBean("haha");
boolean hehe = run.containsBean("hehe");
System.out.println("haha：" + haha); //true
System.out.println("hehe：" + hehe); //true
```

### 2.3、配置绑定
如何使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用；

```java
public class getProperties {
    public static void main(String[] args) throws FileNotFoundException, IOException {
        Properties pps = new Properties();
        pps.load(new FileInputStream("a.properties"));
        Enumeration enum1 = pps.propertyNames();// 得到配置文件的名字
        while (enum1.hasMoreElements()) {
            String strKey = (String) enum1.nextElement();
            String strValue = pps.getProperty(strKey);
            System.out.println(strKey + "=" + strValue);
            // 封装到JavaBean。
        }
    }
}
```

#### 1、@ConfigurationProperties
application.properties
```properties
mycar.brand=YD
mycar.price=100000
```

#### 2、@EnableConfigurationProperties + @ConfigurationProperties
EnableConfigurationProperties两个作用：
1. 把这个Car这个组件自动注册到容器中【第三方的类】
2. 开启Car配置绑定功能

```java
@EnableConfigurationProperties(Car.class)
public class MyConfig {
}
```

```java
@ConfigurationProperties(prefix = "mycar")
public class Car {

    private String brand;
    private Integer price;

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public Integer getPrice() {
        return price;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }

    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }
}
```

#### 3、@Component + @ConfigurationProperties
如果是我们自己写的类，可以直接使用Component系注解将类加入IOC容器
```java
@Component //只有在容器中的组件，才会拥有SpringBoot提供的强大功能
@ConfigurationProperties(prefix = "mycar")
public class Car {
}
```


## 3、自动配置原理入门

### 3.1、引导加载自动配置类
```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
        @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
}
```

#### 1、@SpringBootConfiguration
@Configuration。代表当前是一个配置类

#### 2、@ComponentScan
指定扫描哪些，Spring注解；

#### 3、@EnableAutoConfiguration
```java
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
}
```

##### 1、@AutoConfigurationPackage
自动配置包？指定了默认的包规则

```java
@Import(AutoConfigurationPackages.Registrar.class) // 给容器中导入一个组件
public @interface AutoConfigurationPackage {
}

// 利用Registrar给容器中导入一系列组件
// 将指定的一个包下的所有组件导入进来？MainApplication 所在包下。
```

AutoConfigurationPackages.Registrar：
```java
static class Registrar implements ImportBeanDefinitionRegistrar, DeterminableImports {

    @Override
    public void registerBeanDefinitions(AnnotationMetadata metadata, BeanDefinitionRegistry registry) {
        register(registry, new PackageImports(metadata).getPackageNames().toArray(new String[0]));
        // 计算得；new PackageImports(metadata).getPackageNames()的值为com.atguigu.boot
    }

    @Override
    public Set<Object> determineImports(AnnotationMetadata metadata) {
        return Collections.singleton(new PackageImports(metadata));
    }

}
```

##### 2、@Import(AutoConfigurationImportSelector.class)
1. AutoConfigurationImportSelector: `public String[] selectImports(AnnotationMetadata annotationMetadata)`
   1. 利用 `AutoConfigurationEntry autoConfigurationEntry = getAutoConfigurationEntry(annotationMetadata);` 给容器中批量导入一些组件
2. AutoConfigurationImportSelector: `protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata)`
   1. 调用 `List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes)` 获取到所有需要导入到容器中的配置类
3. AutoConfigurationImportSelector: `protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes)`
   1. 调用 `List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(), getBeanClassLoader());`
4. SpringFactoriesLoader: `public static List<String> loadFactoryNames(Class<?> factoryType, @Nullable ClassLoader classLoader)`
   1. 利用工厂加载 `loadSpringFactories(classLoader).getOrDefault(factoryTypeName, Collections.emptyList());`得到所有的组件
5. SpringFactoriesLoader: `private static Map<String, List<String>> loadSpringFactories(@Nullable ClassLoader classLoader)`
   1. `classLoader.getResources(FACTORIES_RESOURCE_LOCATION)`
   2. `FACTORIES_RESOURCE_LOCATION = "META-INF/spring.factories";`
   3. 从META-INF/spring.factories位置来加载一个文件。
      - 默认扫描我们当前系统里面所有META-INF/spring.factories位置的文件
      - spring-boot-autoconfigure-2.3.4.RELEASE.jar包里面也有META-INF/spring.factories

![](image/SpringBoot2/image-20220823085930.png)

文件里面写死了spring-boot一启动就要给容器中加载的所有配置类（略）

### 3.2、按需开启自动配置项
虽然我们127个场景的所有自动配置启动的时候默认全部加载。XxxAutoConfiguration

按照条件装配规则（@Conditional），最终会按需配置。

### 3.3、修改默认配置
```java
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)
@Configuration(proxyBeanMethods = false)
@ConditionalOnWebApplication(type = Type.SERVLET)
@ConditionalOnClass(DispatcherServlet.class)
@AutoConfigureAfter(ServletWebServerFactoryAutoConfiguration.class)
public class DispatcherServletAutoConfiguration {

    /*
     * The bean name for a DispatcherServlet that will be mapped to the root URL "/"
     */
    public static final String DEFAULT_DISPATCHER_SERVLET_BEAN_NAME = "dispatcherServlet";

    /*
     * The bean name for a ServletRegistrationBean for the DispatcherServlet "/"
     */
    public static final String DEFAULT_DISPATCHER_SERVLET_REGISTRATION_BEAN_NAME = "dispatcherServletRegistration";

    @Configuration(proxyBeanMethods = false)
    @Conditional(DefaultDispatcherServletCondition.class)
    @ConditionalOnClass(ServletRegistration.class)
    @EnableConfigurationProperties(WebMvcProperties.class)
    protected static class DispatcherServletConfiguration {

        @Bean(name = DEFAULT_DISPATCHER_SERVLET_BEAN_NAME)
        public DispatcherServlet dispatcherServlet(WebMvcProperties webMvcProperties) {
            DispatcherServlet dispatcherServlet = new DispatcherServlet();
            dispatcherServlet.setDispatchOptionsRequest(webMvcProperties.isDispatchOptionsRequest());
            dispatcherServlet.setDispatchTraceRequest(webMvcProperties.isDispatchTraceRequest());
            dispatcherServlet.setThrowExceptionIfNoHandlerFound(webMvcProperties.isThrowExceptionIfNoHandlerFound());
            dispatcherServlet.setPublishEvents(webMvcProperties.isPublishRequestHandledEvents());
            dispatcherServlet.setEnableLoggingRequestDetails(webMvcProperties.isLogRequestDetails());
            return dispatcherServlet;
        }

        @Bean
        @ConditionalOnBean(MultipartResolver.class) // 容器中有这个类型组件
        @ConditionalOnMissingBean(name = DispatcherServlet.MULTIPART_RESOLVER_BEAN_NAME) // 容器中没有这个名字 multipartResolver 的组件
        public MultipartResolver multipartResolver(MultipartResolver resolver) {
            // 给@Bean标注的方法传入了对象参数，这个参数的值就会从容器中找。
            // SpringMVC multipartResolver。防止有些用户配置的文件上传解析器不符合规范
            // Detect if the user has created a MultipartResolver but named it incorrectly
            return resolver;
        }
        // 给容器中加入了文件上传解析器；
    }
```

SpringBoot默认会在底层配好所有的组件。但是如果用户自己配置了以用户的优先
```java
// org.springframework.boot.autoconfigure.web.servlet.HttpEncodingAutoConfiguration
@Bean
@ConditionalOnMissingBean // 如果用户自己配置了以用户的优先
public CharacterEncodingFilter characterEncodingFilter() {
    CharacterEncodingFilter filter = new OrderedCharacterEncodingFilter();
    filter.setEncoding(this.properties.getCharset().name());
    filter.setForceRequestEncoding(this.properties.shouldForce(Encoding.Type.REQUEST));
    filter.setForceResponseEncoding(this.properties.shouldForce(Encoding.Type.RESPONSE));
    return filter;
}
```

总结：
- SpringBoot先加载所有的自动配置类 XxxAutoConfiguration
- 每个自动配置类按照条件进行生效，默认都会绑定配置文件指定的值。
  - 自动配置类的配置从XxxProperties里面拿。
  - XxxProperties和配置文件进行了绑定
- 生效的配置类就会给容器中装配很多组件
- 只要容器中有这些组件，相当于这些功能就有了
- 定制化配置
  - 用户直接自己@Bean替换底层的组件
  - 用户去看这个组件是获取的配置文件什么值就去修改。【常用】

XxxAutoConfiguration -> 组件 -> XxxProperties里面拿值 -> application.properties

### 3.4、最佳实践
- [引入场景依赖](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter)
- 查看自动配置了哪些【可不看】
  - 自己分析，引入场景对应的自动配置一般都生效了
  - 配置文件中debug=true开启自动配置报告。Negative（不生效）、Positive（生效）
- 是否需要修改
  - [参照文档修改配置项](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
    - 自己分析，XxxProperties绑定了配置文件的哪些。
  - 自定义加入或者替换组件
    - @Bean、@Component...
  - 自定义器 XxxCustomizer
  - ......


## 4、开发小技巧

### 4.1、Lombok
简化JavaBean开发
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>

<!-- idea中搜索安装lombok插件 -->
```

```java
// ==========简化JavaBean开发==========
@Data // = @Getter + @Setter + @RequiredArgsConstructor(@NoArgsConstructor + @AllArgsConstructor) + @ToString + @EqualsAndHashCode
public class User {

    private String name;
    private Integer age;

    private Pet pet;

    public User(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

}
```

```java
// ==========简化日志开发==========
@Slf4j
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(@RequestParam("name") String name) {

        log.info("请求进来了....");

        return "Hello, Spring Boot 2!" + "你好：" + name;
    }
}
```

### 4.2、dev-tools
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

项目或者页面修改以后：<kbd>Ctrl</kbd>+<kbd>F9</kbd>；

> 注：这里的 <kbd>Ctrl</kbd>+<kbd>F9</kbd> 是idea中的 build project 的快捷键，所谓的更新其实只是restart。如果想要实现reload，那么需要付费功能JRebel。

### 4.3、Spring Initailizr（项目初始化向导）

#### 0、选择我们需要的开发场景
![](image/SpringBoot2/image-20220823090532.png)

#### 1、自动依赖引入
![](image/SpringBoot2/image-20220823090558.png)

#### 2、自动创建项目结构
![](image/SpringBoot2/image-20220823090631.png)

#### 3、自动编写好主配置类
![](image/SpringBoot2/image-20220823090635.png)



# 四、配置文件

## 1、文件类型

### 1.1、properties
同以前的properties用法

### 1.2、yaml

#### 1.2.1、简介
YAML 是 "YAML Ain't Markup Language"（YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种标记语言）。 

非常适合用来做以数据为中心的配置文件

#### 1.2.2、基本语法
- key: value；kv之间有空格
- 大小写敏感
- 使用缩进表示层级关系
- 缩进不允许使用tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- '#'表示注释
- 字符串无需加引号，如果要加：
  - ''（单引号）：原样输出
  - ""（双引号）：转义字符转义，例：`\n` -> 换行

#### 1.2.3、数据类型
- 字面量：单个的、不可再分的值。date、boolean、string、number、null
- 对象：键值对的集合。map、hash、set、object 
- 数组：一组按次序排列的值。array、list、queue

```yaml
k: v

# 行内写法：
k: {k1:v1,k2:v2,k3:v3}
# 或
k: 
  k1: v1
  k2: v2
  k3: v3

# 行内写法：
k: [v1,v2,v3]
#或者
k:
  - v1
  - v2
  - v3
```

#### 1.2.4、示例
```java
@Data
public class Person {

    private String userName;
    private Boolean boss;
    private Date birth;
    private Integer age;
    private Pet pet;
    private String[] interests;
    private List<String> animal;
    private Map<String, Object> score;
    private Set<Double> salarys;
    private Map<String, List<Pet>> allPets;
}

@Data
public class Pet {
    private String name;
    private Double weight;
}
```

```yaml
# yaml表示以上对象
person:
  userName: zhangsan
  boss: false
  birth: 2019/12/12 20:12:33
  age: 18
  pet: 
    name: tomcat
    weight: 23.4
  interests: [篮球,游泳]
  animal: 
    - jerry
    - mario
  score:
    english: 
      first: 30
      second: 40
      third: 50
    math: [131,140,148]
    chinese: {first: 128,second: 136}
  salarys: [3999,4999.98,5999.99]
  allPets:
    sick:
      - {name: tom}
      - name: jerry
        weight: 47
    health: [{name: mario,weight: 47}]
```


## 2、配置提示
自定义的类和配置文件绑定一般没有提示。

加入配置处理器，这样我们自己的类在配置时就会有提示：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

打包排除配置处理器，配置处理器在程序运行时没什么用，排除减小jar包大小：
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <excludes>
                    <exclude>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-configuration-processor</artifactId>
                    </exclude>
                </excludes>
            </configuration>
        </plugin>
    </plugins>
</build>
```



# 五、Web开发

## 1、SpringMVC自动配置概览
Spring Boot provides auto-configuration for Spring MVC that works well with most applications.(大多场景我们都无需自定义配置)

The auto-configuration adds the following features on top of Spring’s defaults:
- Inclusion of ContentNegotiatingViewResolver and BeanNameViewResolver beans.
  - 内容协商视图解析器和BeanName视图解析器
- Support for serving static resources, including support for WebJars (covered later in this document)).
  - 静态资源（包括webjars）
- Automatic registration of Converter, GenericConverter, and Formatter beans.
  - 自动注册 Converter，GenericConverter，Formatter 
- Support for HttpMessageConverters (covered later in this document).
  - 支持 HttpMessageConverters （后来我们配合内容协商理解原理）
- Automatic registration of MessageCodesResolver (covered later in this document).
  - 自动注册 MessageCodesResolver （国际化用）
- Static index.html support.
  - 静态index.html 页支持
- Custom Favicon support (covered later in this document).
  - 自定义 Favicon  
- Automatic use of a ConfigurableWebBindingInitializer bean (covered later in this document).
  - 自动使用 ConfigurableWebBindingInitializer ，（DataBinder负责将请求数据绑定到JavaBean上）

> If you want to keep those Spring Boot MVC customizations and make more MVC customizations (interceptors, formatters, view controllers, and other features), you can add your own @Configuration class of type WebMvcConfigurer but without @EnableWebMvc.
> 不用@EnableWebMvc注解。使用 @Configuration + WebMvcConfigurer 自定义规则

> If you want to provide custom instances of RequestMappingHandlerMapping, RequestMappingHandlerAdapter, or ExceptionHandlerExceptionResolver, and still keep the Spring Boot MVC customizations, you can declare a bean of type WebMvcRegistrations and use it to provide custom instances of those components.
> 声明 WebMvcRegistrations 改变默认底层组件

> If you want to take complete control of Spring MVC, you can add your own @Configuration annotated with @EnableWebMvc, or alternatively add your own @Configuration-annotated DelegatingWebMvcConfiguration as described in the Javadoc of @EnableWebMvc.
> 使用 @EnableWebMvc+@Configuration+DelegatingWebMvcConfiguration 全面接管SpringMVC


## 2、简单功能分析

### 2.1、静态资源访问

#### 1、静态资源目录
只要静态资源放在类路径下：called `/static` (or `/public` or `/resources` or `/META-INF/resources`
访问：当前项目根路径/ + 静态资源名

原理：静态映射 `/**`。
请求进来，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器。静态资源也找不到则响应404页面

改变默认的静态资源路径，一般不做改变。
```yaml
spring:
  resources:
    static-locations: [classpath:/haha/]
```

#### 2、静态资源访问前缀
默认无前缀，常设置一个前缀用于拦截请求。
```yaml
spring:
  mvc:
    static-path-pattern: /res/**
```

当前项目 + static-path-pattern + 静态资源名 = 静态资源文件夹下找

#### 3、webjar
自动映射：`/webjars/**`
https://www.webjars.org/

```xml
<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>jquery</artifactId>
    <version>3.5.1</version>
</dependency>
```

访问地址：http://localhost:8080/webjars/jquery/3.5.1/jquery.js 后面地址要按照依赖里面的包路径

### 2.2、欢迎页支持
- 静态资源路径下 index.html
  - 可以配置静态资源路径
  - 但是不可以配置静态资源的访问前缀。否则导致 index.html 不能被默认访问

```yaml
spring:
#  mvc:
#    static-path-pattern: /res/**  这个会导致welcome page功能失效

  resources:
    static-locations: [classpath:/haha/]
```

controller能处理/index

### 2.3、自定义 Favicon
favicon.ico 放在静态资源目录下即可。
```yaml
spring:
#  mvc:
#    static-path-pattern: /res/**  这个会导致 Favicon 功能失效
```

### 2.4、静态资源配置原理
- SpringBoot启动默认加载 XxxAutoConfiguration 类（自动配置类）
- SpringMVC功能的自动配置类 WebMvcAutoConfiguration，生效

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnWebApplication(type = Type.SERVLET)
@ConditionalOnClass({ Servlet.class, DispatcherServlet.class, WebMvcConfigurer.class })
@ConditionalOnMissingBean(WebMvcConfigurationSupport.class)
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE + 10)
@AutoConfigureAfter({ DispatcherServletAutoConfiguration.class, TaskExecutionAutoConfiguration.class,
        ValidationAutoConfiguration.class })
public class WebMvcAutoConfiguration {
}
```

- 给容器中配了什么。

```java
@Configuration(proxyBeanMethods = false)
@Import(EnableWebMvcConfiguration.class)
@EnableConfigurationProperties({ WebMvcProperties.class, ResourceProperties.class })
@Order(0)
public static class WebMvcAutoConfigurationAdapter implements WebMvcConfigurer {
}
```

- 配置文件的相关属性和xxx进行了绑定。
  - WebMvcProperties -> spring.mvc
  - ResourceProperties -> spring.resources

##### 1、配置类只有一个有参构造器
```java
// 有参构造器所有参数的值都会从容器中确定
// ResourceProperties resourceProperties：获取和spring.resources绑定的所有的值的对象
// WebMvcProperties mvcProperties：获取和spring.mvc绑定的所有的值的对象
// ListableBeanFactory beanFactory：Spring的beanFactory
// HttpMessageConverters：找到所有的HttpMessageConverters
// ResourceHandlerRegistrationCustomizer：找到 #资源处理器的自定义器#。
// DispatcherServletPath
// ServletRegistrationBean：给应用注册Servlet、Filter...
public WebMvcAutoConfigurationAdapter(ResourceProperties resourceProperties, WebMvcProperties mvcProperties,
        ListableBeanFactory beanFactory, ObjectProvider<HttpMessageConverters> messageConvertersProvider,
        ObjectProvider<ResourceHandlerRegistrationCustomizer> resourceHandlerRegistrationCustomizerProvider,
        ObjectProvider<DispatcherServletPath> dispatcherServletPath,
        ObjectProvider<ServletRegistrationBean<?>> servletRegistrations) {
    this.resourceProperties = resourceProperties;
    this.mvcProperties = mvcProperties;
    this.beanFactory = beanFactory;
    this.messageConvertersProvider = messageConvertersProvider;
    this.resourceHandlerRegistrationCustomizer = resourceHandlerRegistrationCustomizerProvider.getIfAvailable();
    this.dispatcherServletPath = dispatcherServletPath;
    this.servletRegistrations = servletRegistrations;
}
```

##### 2、资源处理的默认规则
```java
@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
        return;
    }
    Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
    CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
    // webjars的规则
    if (!registry.hasMappingForPattern("/webjars/**")) {
        customizeResourceHandlerRegistration(registry.addResourceHandler("/webjars/**")
                .addResourceLocations("classpath:/META-INF/resources/webjars/")
                .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
    }

    // 静态资源
    String staticPathPattern = this.mvcProperties.getStaticPathPattern();
    if (!registry.hasMappingForPattern(staticPathPattern)) {
        customizeResourceHandlerRegistration(registry.addResourceHandler(staticPathPattern)
                .addResourceLocations(getResourceLocations(this.resourceProperties.getStaticLocations()))
                .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
    }
}
```

```yaml
spring:
  resources:
    add-mappings: false #禁用所有静态资源规则
```

```java
@ConfigurationProperties(prefix = "spring.resources", ignoreUnknownFields = false)
public class ResourceProperties {

    private static final String[] CLASSPATH_RESOURCE_LOCATIONS = { "classpath:/META-INF/resources/",
            "classpath:/resources/", "classpath:/static/", "classpath:/public/"
    };

    /**
     * Locations of static resources. Defaults to classpath:[/META-INF/resources/,
     * /resources/, /static/, /public/].
     */
    private String[] staticLocations = CLASSPATH_RESOURCE_LOCATIONS;
```

##### 3、欢迎页的处理规则
HandlerMapping：处理器映射。保存了每一个Handler能处理哪些请求。
```java
@Bean
public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext,
        FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
    WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(
            new TemplateAvailabilityProviders(applicationContext), applicationContext, getWelcomePage(),
            this.mvcProperties.getStaticPathPattern());
    welcomePageHandlerMapping.setInterceptors(getInterceptors(mvcConversionService, mvcResourceUrlProvider));
    welcomePageHandlerMapping.setCorsConfigurations(getCorsConfigurations());
    return welcomePageHandlerMapping;
}
```

```java
WelcomePageHandlerMapping(TemplateAvailabilityProviders templateAvailabilityProviders,
        ApplicationContext applicationContext, Optional<Resource> welcomePage, String staticPathPattern) {
    if (welcomePage.isPresent() && "/**".equals(staticPathPattern)) {
        // 要用欢迎页功能，必须是/**
        logger.info("Adding welcome page: " + welcomePage.get());
        setRootViewName("forward:index.html");
    } else if (welcomeTemplateExists(templateAvailabilityProviders, applicationContext)) {
        // 调用Controller /index
        logger.info("Adding welcome page template: index");
        setRootViewName("index");
    }
}
```

##### 4、favicon
浏览器会请求：项目/favicon.ico


## 3、请求参数处理

### 0、请求映射
- @xxxMapping；
- Rest风格支持（使用HTTP请求方式动词来表示对资源的操作）
  - 以前：
    - /getUser：获取用户
    - /deleteUser：删除用户
    - /editUser：修改用户
    - /saveUser：保存用户
  - 现在 /user：
    - GET-获取用户
    - DELETE-删除用户
    - PUT-修改用户
    - POST-保存用户
  - 核心Filter；HiddenHttpMethodFilter
    - 用法：表单method=post，隐藏域 _method=put
    - SpringBoot中手动开启
  - 扩展：如何把_method 这个名字换成我们自己喜欢的。

#### 1、rest使用与原理
```java
@RequestMapping(value = "/user", method = RequestMethod.GET)
public String getUser() {
    return "GET-张三";
}

@RequestMapping(value = "/user", method = RequestMethod.POST)
public String saveUser() {
    return "POST-张三";
}

@RequestMapping(value = "/user", method = RequestMethod.PUT)
public String putUser() {
    return "PUT-张三";
}

@RequestMapping(value = "/user", method = RequestMethod.DELETE)
public String deleteUser() {
    return "DELETE-张三";
}
```

```yaml
spring:
  mvc:
    hiddenmethod:
      filter:
        enabled: true   #开启页面表单的Rest功能
```

```java
@Bean
@ConditionalOnMissingBean(HiddenHttpMethodFilter.class)
@ConditionalOnProperty(prefix = "spring.mvc.hiddenmethod.filter", name = "enabled", matchIfMissing = false)
public OrderedHiddenHttpMethodFilter hiddenHttpMethodFilter() {
    return new OrderedHiddenHttpMethodFilter();
}
```

测试：
```html
<form action="/user" method="get">
    <input value="REST-GET 提交" type="submit" />
</form>
<form action="/user" method="post">
    <input value="REST-POST 提交" type="submit" />
</form>
<form action="/user" method="post">
    <input name="_method" type="hidden" value="delete" />
    <input name="_m" type="hidden" value="delete" />
    <input value="REST-DELETE 提交" type="submit" />
</form>
<form action="/user" method="post">
    <input name="_method" type="hidden" value="PUT" />
    <input value="REST-PUT 提交" type="submit" />
</form>
```

Rest原理（表单提交要使用REST的时候）
- 表单提交会带上_method=PUT
- 请求过来被HiddenHttpMethodFilter拦截
  - 请求是否正常，并且是POST
    - 获取到_method的值。
    - 兼容以下请求；PUT.DELETE.PATCH
    - 原生request（post），包装模式requesWrapper重写了getMethod方法，返回的是传入的值。
    - 过滤器链放行的时候用wrapper。以后的方法调用getMethod是调用requesWrapper的。

Rest使用客户端工具，
- 如PostMan直接发送Put、delete等方式请求，无需Filter。

```java
// 自定义filter，以下在配置类中编写
@Bean
public HiddenHttpMethodFilter hiddenHttpMethodFilter() {
    HiddenHttpMethodFilter methodFilter = new HiddenHttpMethodFilter();
    methodFilter.setMethodParam("_m");
    return methodFilter;
}
```

#### 2、请求映射原理
![](image/SpringBoot2/image-20220823152235.png)

SpringMVC功能分析都从 org.springframework.web.servlet.DispatcherServlet -> doDispatch()

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    boolean multipartRequestParsed = false;

    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);

    try {
        ModelAndView mv = null;
        Exception dispatchException = null;

        try {
            processedRequest = checkMultipart(request);
            multipartRequestParsed = (processedRequest != request);

            // 找到当前请求使用哪个Handler（Controller的方法）处理
            mappedHandler = getHandler(processedRequest);
```

HandlerMapping：处理器映射。/xxx -> xxxx
![](image/SpringBoot2/image-20220823152510.png)

RequestMappingHandlerMapping：保存了所有 @RequestMapping 和 handler 的映射规则。

![](image/SpringBoot2/image-20220823152554.png)

所有的请求映射都在HandlerMapping中。
- SpringBoot自动配置欢迎页的 WelcomePageHandlerMapping 。访问 /能访问到index.html；
- SpringBoot自动配置了默认的 RequestMappingHandlerMapping
- 请求进来，挨个尝试所有的HandlerMapping看是否有请求信息。
  - 如果有就找到这个请求对应的handler
  - 如果没有就是下一个 HandlerMapping
- 我们需要一些自定义的映射处理，我们也可以自己给容器中放HandlerMapping。自定义 HandlerMapping

```java
protected HandlerExecutionChain getHandler(HttpServletRequest request) throws Exception {
    if (this.handlerMappings != null) {
        for (HandlerMapping mapping : this.handlerMappings) {
            HandlerExecutionChain handler = mapping.getHandler(request);
            if (handler != null) {
                return handler;
            }
        }
    }
    return null;
}
```

### 1、普通参数与基本注解

#### 1.1、注解：
- @PathVariable：路径变量（rest风格）
  - 指定注解的value属性：获取该变量的值（自动类型转换）
  - 不指定：获取一个map（键值均为String类型），包含所有变量。
- @RequestHeader：获取请求头
  - 指定注解的value属性：获取该变量的值
  - 不指定：获取请求头所有参数，支持如下参数类型：`Map<String, String>`, `MultiValueMap<String, String>`, `HttpHeaders`
- @RequestParam：
  - 指定注解的value属性：获取该变量的值
    - 变量是单值：获取该变量的值（自动类型转换）
    - 变量有多个值：
      - 使用数组或集合接收，各个项即各个值；
      - 使用String接收，`,`分割的多个值。
  - 不指定：获取所有请求参数，支持如下参数类型：`Map<String, String>`, `MultiValueMap<String, String>`
- @CookieValue：获取value属性指定的Cookie
  - String接收：获取指定的Cookie值
  - Cookie接收：获取指定的Cookie对象
- @RequestBody：获取POST请求的表单数据
  - String接收：`k1=v1&k2=v2`

```java
@RestController
public class ParameterTestController {

    // car/2/owner/zhangsan
    @GetMapping("/car/{id}/owner/{username}")
    public Map<String, Object> getCar(@PathVariable("id") Integer id,
                                      @PathVariable("username") String name,
                                      @PathVariable Map<String, String> pv,
                                      @RequestHeader("User-Agent") String userAgent,
                                      @RequestHeader Map<String, String> header,
                                      @RequestParam("age") Integer age,
                                      @RequestParam("inters") List<String> inters,
                                      @RequestParam Map<String, String> params,
                                      @CookieValue("_ga") String _ga,
                                      @CookieValue("_ga") Cookie cookie) {

        Map<String, Object> map = new HashMap<>();

        // map.put("id",id);
        // map.put("name",name);
        // map.put("pv",pv);
        // map.put("userAgent",userAgent);
        // map.put("headers",header);
        map.put("age", age);
        map.put("inters", inters);
        map.put("params", params);
        map.put("_ga", _ga);
        System.out.println(cookie.getName() + "===>" + cookie.getValue());
        return map;
    }

    @PostMapping("/save")
    public Map postMethod(@RequestBody String content) {
        Map<String, Object> map = new HashMap<>();
        map.put("content", content);
        return map;
    }

}
```

##### @RequestAttribute（获取request域属性）
```java
@Controller
public class RequestController {

    @GetMapping("/goto")
    public String goToPage(HttpServletRequest request) {

        request.setAttribute("msg", "成功了...");
        request.setAttribute("code", 200);
        return "forward:/success"; // 转发到 /success请求
    }

    @ResponseBody
    @GetMapping("/success")
    public Map success(@RequestAttribute(value = "msg", required = false) String msg,
            @RequestAttribute(value = "code", required = false) Integer code,
            HttpServletRequest request) {
        Object msg1 = request.getAttribute("msg");

        Map<String, Object> map = new HashMap<>();
        Object hello = request.getAttribute("hello");
        Object world = request.getAttribute("world");
        Object message = request.getAttribute("message");

        map.put("reqMethod_msg", msg1);
        map.put("annotation_msg", msg);
        map.put("hello", hello);
        map.put("world", world);
        map.put("message", message);

        return map;
    }
}
```

##### @MatrixVariable（矩阵变量）
- queryString 查询字符串 `@RequestParam`：/cars/{path}?xxx=xxx&aaa=ccc
- 矩阵变量 `@MatrixVariable`：/cars/sell;low=34;brand=byd,audi,yd
- 应用场景：页面开发，cookie禁用了，session里面的内容怎么使用；
  - session.set(a,b) -> jsessionid -> cookie -> 每次发请求携带。
  - url重写：/abc;jsesssionid=xxx 把cookie的值使用矩阵变量的方式进行传递.

---
- 矩阵变量需要在SpringBoot中手动开启
- 根据RFC3986的规范，矩阵变量应当绑定在路径变量中！
- 若是有多个矩阵变量，应当使用英文符号;进行分隔。
- 若是一个矩阵变量有多个值，应当使用英文符号,进行分隔，或之命名多个重复的key即可。

开启矩阵变量：
```java
//1、WebMvcConfigurer定制化SpringMVC的功能
@Bean
public WebMvcConfigurer webMvcConfigurer(){
    return new WebMvcConfigurer() { //WebMvcConfigurer是一个接口，里面都是默认方法
        @Override
        public void configurePathMatch(PathMatchConfigurer configurer) {
            UrlPathHelper urlPathHelper = new UrlPathHelper();
            // 不移除；后面的内容。矩阵变量功能就可以生效
            urlPathHelper.setRemoveSemicolonContent(false);
            configurer.setUrlPathHelper(urlPathHelper);
        }
    };
}
// 也可以直接让配置类实现该接口
```

测试：
```html
<a href="/cars/sell;low=34;brand=byd,audi,yd">@MatrixVariable（矩阵变量）</a>
<a href="/cars/sell;low=34;brand=byd;brand=audi;brand=yd">@MatrixVariable（矩阵变量）</a>
<a href="/boss/1;age=20/2;age=10">@MatrixVariable（矩阵变量）/boss/{bossId}/{empId}</a>
```

```java
// 1、语法：请求路径：/cars/sell;low=34;brand=byd,audi,yd
// 2、SpringBoot默认是禁用了矩阵变量的功能
//   手动开启：原理。对于路径的处理。UrlPathHelper进行解析。
//     removeSemicolonContent（移除分号内容）支持矩阵变量的
// 3、矩阵变量必须有url路径变量才能被解析
@GetMapping("/cars/{path}")
public Map carsSell(@MatrixVariable("low") Integer low,
                    @MatrixVariable("brand") List<String> brand,
                    @PathVariable("path") String path) {
    Map<String, Object> map = new HashMap<>();

    map.put("low", low);
    map.put("brand", brand);
    map.put("path", path);
    return map;
}

// /boss/1;age=20/2;age=10
@GetMapping("/boss/{bossId}/{empId}")
public Map boss(@MatrixVariable(value = "age", pathVar = "bossId") Integer bossAge,
                @MatrixVariable(value = "age", pathVar = "empId") Integer empAge) {
    Map<String, Object> map = new HashMap<>();

    map.put("bossAge", bossAge);
    map.put("empAge", empAge);
    return map;
}
```

#### 1.2、Servlet API：
WebRequest、ServletRequest、MultipartRequest、 HttpSession、javax.servlet.http.PushBuilder、Principal、InputStream、Reader、HttpMethod、Locale、TimeZone、ZoneId

```java
// 位置：ServletRequestMethodArgumentResolver
@Override
public boolean supportsParameter(MethodParameter parameter) {
    Class<?> paramType = parameter.getParameterType();
    return (WebRequest.class.isAssignableFrom(paramType) ||
            ServletRequest.class.isAssignableFrom(paramType) ||
            MultipartRequest.class.isAssignableFrom(paramType) ||
            HttpSession.class.isAssignableFrom(paramType) ||
            (pushBuilder != null && pushBuilder.isAssignableFrom(paramType)) ||
            Principal.class.isAssignableFrom(paramType) ||
            InputStream.class.isAssignableFrom(paramType) ||
            Reader.class.isAssignableFrom(paramType) ||
            HttpMethod.class == paramType ||
            Locale.class == paramType ||
            TimeZone.class == paramType ||
            ZoneId.class == paramType);
}
```

#### 1.3、复杂参数：
Map、Model（map、model里面的数据会被放在request的请求域 request.setAttribute）
Errors/BindingResult、RedirectAttributes（重定向携带数据）
ServletResponse（response）、SessionStatus、UriComponentsBuilder、ServletUriComponentsBuilder

`Map<String,Object> map`, `Model model`, `HttpServletRequest request` 都是可以给request域中放数据，`request.getAttribute();`

测试：
```java
@GetMapping("/params")
public String testParam(Map<String, Object> map,
                        Model model,
                        HttpServletRequest request,
                        HttpServletResponse response) {
    map.put("hello", "world666");
    model.addAttribute("world", "hello666");
    request.setAttribute("message", "HelloWorld");

    Cookie cookie = new Cookie("c1", "v1");
    response.addCookie(cookie);
    return "forward:/success";
}
```

Map、Model类型的参数，会返回 mavContainer.getModel(); -> BindingAwareModelMap 是 Model 也是 Map
mavContainer.getModel(); 获取到值的

![](image/SpringBoot2/image-20220823153313.png)
![](image/SpringBoot2/image-20220823153318.png)
![](image/SpringBoot2/image-20220823153323.png)

#### 1.4、自定义对象参数：
可以自动类型转换与格式化，可以级联封装。

```java
/**
 * 姓名： <input name="userName"/> <br/>
 * 年龄： <input name="age"/> <br/>
 * 生日： <input name="birth"/> <br/>
 * 宠物姓名：<input name="pet.name"/><br/>
 * 宠物年龄：<input name="pet.age"/>
 */
@Data
public class Person {

    private String userName;
    private Integer age;
    private Date birth;
    private Pet pet;

}

@Data
public class Pet {

    private String name;
    private String age;

}

// result
```

### 2、POJO封装过程
ServletModelAttributeMethodProcessor
【见：5.3、自定义类型参数 封装POJO】

### 3、参数处理原理
- HandlerMapping中找到能处理请求的Handler `Controller.method()`
- 为当前 Handler 找一个适配器 HandlerAdapter；RequestMappingHandlerAdapter
- 适配器执行目标方法并确定方法参数的每一个值

#### 1、HandlerAdapter
![](image/SpringBoot2/image-20220823153603.png)

0 - 支持方法上标注@RequestMapping 
1 - 支持函数式编程的
xxxxxx

#### 2、执行目标方法
```java
// 位置：DispatcherServlet -> doDispatch（被doService调用）
// Actually invoke the handler.
mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
```

```java
// 位置：RequestMappingHandlerAdapter -> handleInternal
mav = invokeHandlerMethod(request, response, handlerMethod); // 执行目标方法
```

```java
// 位置：RequestMappingHandlerAdapter -> invokeHandlerMethod
if (this.argumentResolvers != null) {
    invocableMethod.setHandlerMethodArgumentResolvers(this.argumentResolvers);
}
if (this.returnValueHandlers != null) {
    invocableMethod.setHandlerMethodReturnValueHandlers(this.returnValueHandlers);
}
// ...
invocableMethod.invokeAndHandle(webRequest, mavContainer);
```

```java
// 位置：ServletInvocableHandlerMethod -> invokeAndHandle
Object returnValue = invokeForRequest(webRequest, mavContainer, providedArgs);
```

```java
// 位置：InvocableHandlerMethod -> invokeForRequest
// 获取方法的参数值【见：5、如何确定目标方法每一个参数的值】
Object[] args = getMethodArgumentValues(request, mavContainer, providedArgs);
if (logger.isTraceEnabled()) {
    logger.trace("Arguments: " + Arrays.toString(args));
}
// 反射调用处理器方法
return doInvoke(args);
```

#### 3、参数解析器-HandlerMethodArgumentResolver
确定将要执行的目标方法的每一个参数的值是什么;
SpringMVC目标方法能写多少种参数类型。取决于参数解析器。

![](image/SpringBoot2/image-20220823153734.png)
![](image/SpringBoot2/image-20220823153743.png)

- 当前解析器是否支持解析这种参数
- 支持就调用 resolveArgument

#### 4、返回值处理器
![](image/SpringBoot2/image-20220823153841.png)

#### 5、如何确定目标方法每一个参数的值
```java
// 位置：InvocableHandlerMethod
protected Object[] getMethodArgumentValues(NativeWebRequest request, @Nullable ModelAndViewContainer mavContainer,
        Object... providedArgs) throws Exception {

    // 获取处理器方法的每个参数的详细信息
    MethodParameter[] parameters = getMethodParameters();
    if (ObjectUtils.isEmpty(parameters)) {
        return EMPTY_ARGS;  // Object[0]
    }

    Object[] args = new Object[parameters.length];
    for (int i = 0; i < parameters.length; i++) {
        MethodParameter parameter = parameters[i];
        parameter.initParameterNameDiscovery(this.parameterNameDiscoverer);
        args[i] = findProvidedArgument(parameter, providedArgs);
        if (args[i] != null) {
            continue;
        }
        if (!this.resolvers.supportsParameter(parameter)) { // -> 5、1
            throw new IllegalStateException(formatArgumentError(parameter, "No suitable resolver"));
        }
        try {
            args[i] = this.resolvers.resolveArgument(parameter, mavContainer, request, this.dataBinderFactory); // -> 5、2
        } catch (Exception ex) {
            // Leave stack trace for later, exception may actually be resolved and
            // handled...
            if (logger.isDebugEnabled()) {
                String exMsg = ex.getMessage();
                if (exMsg != null && !exMsg.contains(parameter.getExecutable().toGenericString())) {
                    logger.debug(formatArgumentError(parameter, exMsg));
                }
            }
            throw ex;
        }
    }
    return args;
}
```

##### 5.1、挨个判断所有参数解析器那个支持解析这个参数
```java
// 位置：HandlerMethodArgumentResolverComposite
@Override
public boolean supportsParameter(MethodParameter parameter) {
    return getArgumentResolver(parameter) != null;
}

@Nullable
private HandlerMethodArgumentResolver getArgumentResolver(MethodParameter parameter) {
    HandlerMethodArgumentResolver result = this.argumentResolverCache.get(parameter);
    if (result == null) {
        for (HandlerMethodArgumentResolver resolver : this.argumentResolvers) {
            if (resolver.supportsParameter(parameter)) {
                result = resolver;
                this.argumentResolverCache.put(parameter, result);
                break;
            }
        }
    }
    return result;
}
```

##### 5.2、解析这个参数的值
调用各自 HandlerMethodArgumentResolver 的 resolveArgument 方法即可

```java
// 位置：HandlerMethodArgumentResolverComposite
@Override
@Nullable
public Object resolveArgument(MethodParameter parameter, @Nullable ModelAndViewContainer mavContainer,
        NativeWebRequest webRequest, @Nullable WebDataBinderFactory binderFactory) throws Exception {

    HandlerMethodArgumentResolver resolver = getArgumentResolver(parameter);
    if (resolver == null) {
        throw new IllegalArgumentException("Unsupported parameter type [" +
                parameter.getParameterType().getName() + "]. supportsParameter should be called first.");
    }
    return resolver.resolveArgument(parameter, mavContainer, webRequest, binderFactory);
}
```

##### 5.3、自定义类型参数 封装POJO
```java
// 位置：ModelAttributeMethodProcessor
@Override
public boolean supportsParameter(MethodParameter parameter) {
    return (parameter.hasParameterAnnotation(ModelAttribute.class) ||
            (this.annotationNotRequired && !BeanUtils.isSimpleProperty(parameter.getParameterType())));
}
```

```java
// 位置：BeanUtils
public static boolean isSimpleProperty(Class<?> type) {
    Assert.notNull(type, "'type' must not be null");
    return isSimpleValueType(type) || (type.isArray() && isSimpleValueType(type.getComponentType()));
}

public static boolean isSimpleValueType(Class<?> type) {
    return (Void.class != type && void.class != type &&
            (ClassUtils.isPrimitiveOrWrapper(type) ||
            Enum.class.isAssignableFrom(type) ||
            CharSequence.class.isAssignableFrom(type) ||
            Number.class.isAssignableFrom(type) ||
            Date.class.isAssignableFrom(type) ||
            Temporal.class.isAssignableFrom(type) ||
            URI.class == type ||
            URL.class == type ||
            Locale.class == type ||
            Class.class == type));
}
```

```java
@Override
@Nullable
public final Object resolveArgument(MethodParameter parameter, @Nullable ModelAndViewContainer mavContainer,
        NativeWebRequest webRequest, @Nullable WebDataBinderFactory binderFactory) throws Exception {

    Assert.state(mavContainer != null, "ModelAttributeMethodProcessor requires ModelAndViewContainer");
    Assert.state(binderFactory != null, "ModelAttributeMethodProcessor requires WebDataBinderFactory");

    String name = ModelFactory.getNameForParameter(parameter);
    ModelAttribute ann = parameter.getParameterAnnotation(ModelAttribute.class);
    if (ann != null) {
        mavContainer.setBinding(name, ann.binding());
    }

    Object attribute = null;
    BindingResult bindingResult = null;

    if (mavContainer.containsAttribute(name)) {
        attribute = mavContainer.getModel().get(name);
    } else {
        // Create attribute instance
        try {
            // 创建属性实例（属性未赋值）
            attribute = createAttribute(name, parameter, binderFactory, webRequest);
        } catch (BindException ex) {
            if (isBindExceptionRequired(parameter)) {
                // No BindingResult parameter -> fail with BindException
                throw ex;
            }
            // Otherwise, expose null/empty value and associated BindingResult
            if (parameter.getParameterType() == Optional.class) {
                attribute = Optional.empty();
            }
            bindingResult = ex.getBindingResult();
        }
    }

    if (bindingResult == null) {
        // Bean property binding and validation;
        // skipped in case of binding failure on construction.
        // WebDataBinder：web数据绑定器，可以将请求参数的值绑定到指定的JavaBean里面
        WebDataBinder binder = binderFactory.createBinder(webRequest, attribute, name);
        if (binder.getTarget() != null) {
            if (!mavContainer.isBindingDisabled(name)) {
                // 将请求参数的值绑定到指定的JavaBean里面
                bindRequestParameters(binder, webRequest);
            }
            validateIfApplicable(binder, parameter);
            if (binder.getBindingResult().hasErrors() && isBindExceptionRequired(binder, parameter)) {
                throw new BindException(binder.getBindingResult());
            }
        }
        // Value type adaptation, also covering java.util.Optional
        if (!parameter.getParameterType().isInstance(attribute)) {
            attribute = binder.convertIfNecessary(binder.getTarget(), parameter.getParameterType(), parameter);
        }
        bindingResult = binder.getBindingResult();
    }

    // Add resolved attribute and BindingResult at the end of the model
    Map<String, Object> bindingResultModel = bindingResult.getModel();
    mavContainer.removeAttributes(bindingResultModel);
    mavContainer.addAllAttributes(bindingResultModel);

    return attribute;
}
```

WebDataBinder 利用它里面的 Converters 将请求数据转成指定的数据类型。再次封装到JavaBean中
![](image/SpringBoot2/image-20220823154247.png)
![](image/SpringBoot2/image-20220823154254.png)

GenericConversionService：在设置每一个值的时候，找它里面的所有converter那个可以将这个数据类型（request带来参数的字符串）转换到指定的类型

未来我们可以给WebDataBinder里面放自己的Converter；
```java
@FunctionalInterface
public interface Converter<S, T> {
    @Nullable
    T convert(S source);
}
```

自定义 Converter
```java
// WebMvcConfigurer定制化SpringMVC的功能
@Bean
public WebMvcConfigurer webMvcConfigurer() {
    return new WebMvcConfigurer() {
        @Override
        public void configurePathMatch(PathMatchConfigurer configurer) {
            UrlPathHelper urlPathHelper = new UrlPathHelper();
            // 不移除；后面的内容。矩阵变量功能就可以生效
            urlPathHelper.setRemoveSemicolonContent(false);
            configurer.setUrlPathHelper(urlPathHelper);
        }

        @Override
        public void addFormatters(FormatterRegistry registry) {
            registry.addConverter(new Converter<String, Pet>() {

                @Override
                public Pet convert(String source) {
                    // 啊猫,3
                    if (!StringUtils.isEmpty(source)) {
                        Pet pet = new Pet();
                        String[] split = source.split(",");
                        pet.setName(split[0]);
                        pet.setAge(Integer.parseInt(split[1]));
                        return pet;
                    }
                    return null;
                }
            });
        }
    };
}
```

#### 6、目标方法执行完成
将所有的数据都放在 ModelAndViewContainer；包含要去的页面地址View。还包含Model数据。

![](image/SpringBoot2/image-20220823154436.png)

#### 7、处理派发结果
```java
// 位置：DispatcherServlet -> doDispatch
processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
```

```java
// 位置：DispatcherServlet -> processDispatchResult
render(mv, request, response);
```

```java
// 位置：DispatcherServlet -> render
view.render(mv.getModelInternal(), request, response);
```

```java
// 位置：AbstractView
@Override
public void render(@Nullable Map<String, ?> model, HttpServletRequest request,
        HttpServletResponse response) throws Exception {

    if (logger.isDebugEnabled()) {
        logger.debug("View " + formatViewName() +
                ", model " + (model != null ? model : Collections.emptyMap()) +
                (this.staticAttributes.isEmpty() ? "" : ", static attributes " + this.staticAttributes));
    }

    Map<String, Object> mergedModel = createMergedOutputModel(model, request, response);
    prepareResponse(request, response);
    renderMergedOutputModel(mergedModel, getRequestToExpose(request), response);
}
```

```java
// 位置：InternalResourceView
@Override
protected void renderMergedOutputModel(
        Map<String, Object> model, HttpServletRequest request, HttpServletResponse response) throws Exception {

    // Expose the model object as request attributes.
    // 暴露模型作为请求域属性
    exposeModelAsRequestAttributes(model, request);

    // Expose helpers as request attributes, if any.
    exposeHelpers(request);

    // Determine the path for the request dispatcher.
    String dispatcherPath = prepareForRendering(request, response);

    // Obtain a RequestDispatcher for the target resource (typically a JSP).
    RequestDispatcher rd = getRequestDispatcher(request, dispatcherPath);
    if (rd == null) {
        throw new ServletException("Could not get RequestDispatcher for [" + getUrl() +
                "]: Check that the corresponding file exists within your web application archive!");
    }

    // If already included or response already committed, perform include, else
    // forward.
    if (useInclude(request, response)) {
        response.setContentType(getContentType());
        if (logger.isDebugEnabled()) {
            logger.debug("Including [" + getUrl() + "]");
        }
        rd.include(request, response);
    }

    else {
        // Note: The forwarded resource is supposed to determine the content type
        // itself.
        if (logger.isDebugEnabled()) {
            logger.debug("Forwarding to [" + getUrl() + "]");
        }
        rd.forward(request, response);
    }
}
```

```java
protected void exposeModelAsRequestAttributes(Map<String, Object> model,
        HttpServletRequest request) throws Exception {

    // model中的所有数据遍历挨个放在请求域中
    model.forEach((name, value) -> {
        if (value != null) {
            request.setAttribute(name, value);
        } else {
            request.removeAttribute(name);
        }
    });
}
```


## 4、数据响应与内容协商

### 1、响应JSON

#### 1.1、jackson.jar+@ResponseBody
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<!-- web场景自动引入了json场景 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-json</artifactId>
    <version>2.3.4.RELEASE</version>
    <scope>compile</scope>
</dependency>
```

![](image/SpringBoot2/image-20220823154808.png)

给前端自动返回json数据；

##### 1、返回值解析器
![](image/SpringBoot2/image-20220823154815.png)

```java
// 位置：ServletInvocableHandlerMethod -> invokeAndHandle
try {
    this.returnValueHandlers.handleReturnValue(
            returnValue, getReturnValueType(returnValue), mavContainer, webRequest);
}
```

```java
// 位置：HandlerMethodReturnValueHandlerComposite
@Override
public void handleReturnValue(@Nullable Object returnValue, MethodParameter returnType,
        ModelAndViewContainer mavContainer, NativeWebRequest webRequest) throws Exception {

    HandlerMethodReturnValueHandler handler = selectHandler(returnValue, returnType);
    if (handler == null) {
        throw new IllegalArgumentException("Unknown return value type: " + returnType.getParameterType().getName());
    }
    handler.handleReturnValue(returnValue, returnType, mavContainer, webRequest);
}
```

```java
// 位置：RequestResponseBodyMethodProcessor
@Override
public void handleReturnValue(@Nullable Object returnValue, MethodParameter returnType,
        ModelAndViewContainer mavContainer, NativeWebRequest webRequest)
        throws IOException, HttpMediaTypeNotAcceptableException, HttpMessageNotWritableException {

    mavContainer.setRequestHandled(true);
    ServletServerHttpRequest inputMessage = createInputMessage(webRequest);
    ServletServerHttpResponse outputMessage = createOutputMessage(webRequest);

    // Try even with null return value. ResponseBodyAdvice could get involved.
    // 使用消息转换器进行写出操作
    writeWithMessageConverters(returnValue, returnType, inputMessage, outputMessage);
}
```

##### 2、返回值解析器原理
![](image/SpringBoot2/image-20220823155142.png)

1. 返回值处理器判断是否支持这种类型返回值 supportsReturnType
2. 返回值处理器调用 handleReturnValue 进行处理
3. RequestResponseBodyMethodProcessor 可以处理返回值标了 @ResponseBody 注解的。
  1. 利用 MessageConverters 进行处理，将数据写为json
    1. 内容协商（浏览器默认会以请求头的方式告诉服务器他能接受什么样的内容类型）
    2. 服务器最终根据自己自身的能力，决定服务器能生产出什么样内容类型的数据，
    3. SpringMVC会挨个遍历所有容器底层的 HttpMessageConverter ，看谁能处理？
      1. 得到MappingJackson2HttpMessageConverter可以将对象写为json
      2. 利用MappingJackson2HttpMessageConverter将对象转为json再写出去。

![](image/SpringBoot2/image-20220823160912.png)

#### 1.2、SpringMVC到底支持哪些返回值
```java
ModelAndView
Model
View
ResponseEntity
ResponseBodyEmitter
StreamingResponseBody
HttpEntity
HttpHeaders
Callable
DeferredResult
ListenableFuture
CompletionStage
WebAsyncTask
// 有 @ModelAttribute 且为对象类型的
// @ResponseBody 注解 -> RequestResponseBodyMethodProcessor；
```

#### 1.3、HTTPMessageConverter原理

##### 1、MessageConverter规范
![](image/SpringBoot2/image-20220823161002.png)

HttpMessageConverter: 看是否支持将 此 Class类型的对象，转为MediaType类型的数据。
例子：Person对象转为JSON。或者 JSON转为Person

##### 2、默认的MessageConverter
![](image/SpringBoot2/image-20220823161023.png)

0 - byte[]
1 - String
2 - String
3 - Resource
4 - ResourceRegion
5 - DOMSource、SAXSource、StAXSource、StreamSource、Source
6 - MultiValueMap
7 - true
8 - true
9 - 支持注解方式xml处理的。

最终 MappingJackson2HttpMessageConverter 把对象转为JSON（利用底层的jackson的objectMapper转换的）
![](image/SpringBoot2/image-20220823161051.png)

### 2、内容协商
根据客户端接收能力不同，返回不同媒体类型的数据。

#### 1、引入xml依赖
```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

#### 2、postman分别测试返回json和xml
只需要改变请求头中Accept字段。Http协议中规定的，告诉服务器本客户端可以接收的数据类型。

![](image/SpringBoot2/image-20220823161205.png)

#### 3、开启浏览器参数方式内容协商功能
为了方便内容协商，开启基于请求参数的内容协商功能。
```yaml
spring:
  contentnegotiation:
    favor-parameter: true  #开启请求参数内容协商模式
```

发请求：
- http://localhost:8080/test/person?format=json
- http://localhost:8080/test/person?format=xml

![](image/SpringBoot2/image-20220823161258.png)

确定客户端接收什么样的内容类型；
1、Parameter策略优先确定是要返回json数据（获取请求头中的format的值）

![](image/SpringBoot2/image-20220823161324.png)

2、最终进行内容协商返回给客户端json即可。

#### 4、内容协商原理
1. 判断当前响应头中是否已经有确定的媒体类型。MediaType
2. 获取客户端（PostMan、浏览器）支持接收的内容类型。（获取客户端Accept请求头字段）【application/xml】
   - contentNegotiationManager 内容协商管理器 默认使用基于请求头的策略
   - ![](image/SpringBoot2/image-20220823161419.png)
   - HeaderContentNegotiationStrategy 确定客户端可以接收的内容类型 
   - ![](image/SpringBoot2/image-20220823161427.png)
3. 遍历循环所有当前系统的 MessageConverter，看谁支持操作这个对象（Person）
4. 找到支持操作Person的converter，把converter支持的媒体类型统计出来。
5. 客户端需要【application/xml】。服务端能力【10种、json、xml】
    ![](image/SpringBoot2/image-20220823161431.png)
6. 进行内容协商的最佳匹配媒体类型
7. 用 支持 将对象转为 最佳匹配媒体类型 的converter。调用它进行转化 。

![](image/SpringBoot2/image-20220823161555.png)

导入了jackson处理xml的包，xml的converter就会自动进来
```java
// 位置：WebMvcConfigurationSupport
static {
    ClassLoader classLoader = WebMvcConfigurationSupport.class.getClassLoader();
    romePresent = ClassUtils.isPresent("com.rometools.rome.feed.WireFeed", classLoader);
    jaxb2Present = ClassUtils.isPresent("javax.xml.bind.Binder", classLoader);
    jackson2Present = ClassUtils.isPresent("com.fasterxml.jackson.databind.ObjectMapper", classLoader) &&
            ClassUtils.isPresent("com.fasterxml.jackson.core.JsonGenerator", classLoader);
    jackson2XmlPresent = ClassUtils.isPresent("com.fasterxml.jackson.dataformat.xml.XmlMapper", classLoader); // xml的converter
    jackson2SmilePresent = ClassUtils.isPresent("com.fasterxml.jackson.dataformat.smile.SmileFactory", classLoader);
    jackson2CborPresent = ClassUtils.isPresent("com.fasterxml.jackson.dataformat.cbor.CBORFactory", classLoader);
    gsonPresent = ClassUtils.isPresent("com.google.gson.Gson", classLoader);
    jsonbPresent = ClassUtils.isPresent("javax.json.bind.Jsonb", classLoader);
}
```

```java
// 位置：WebMvcConfigurationSupport -> addDefaultHttpMessageConverters
if (jackson2XmlPresent) {
    Jackson2ObjectMapperBuilder builder = Jackson2ObjectMapperBuilder.xml();
    if (this.applicationContext != null) {
        builder.applicationContext(this.applicationContext);
    }
    messageConverters.add(new MappingJackson2XmlHttpMessageConverter(builder.build()));
}
```

#### 5、自定义 MessageConverter
实现多协议数据兼容。json、xml、x-guigu

0、@ResponseBody 响应数据出去 调用 RequestResponseBodyMethodProcessor 处理
1、Processor 处理方法返回值。通过 MessageConverter 处理
2、所有 MessageConverter 合起来可以支持各种媒体类型数据的操作（读、写）
3、内容协商找到最终的 messageConverter；

SpringMVC的什么功能。一个入口给容器中添加一个 WebMvcConfigurer
```java
@Bean
public WebMvcConfigurer webMvcConfigurer(){
    return new WebMvcConfigurer() {

        @Override
        public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {

        }
    }
}
```

```java
public class GuiguMessageConverter implements HttpMessageConverter<Person> {

    @Override
    public boolean canRead(Class<?> clazz, MediaType mediaType) {
        return false;
    }

    @Override
    public boolean canWrite(Class<?> clazz, MediaType mediaType) {
        return Person.class.isAssignableFrom(clazz);
    }

    // 服务器要统计所有MessageConverter都能写出哪些内容类型
    @Override
    public List<MediaType> getSupportedMediaTypes() {
        return MediaType.parseMediaTypes("application/x-guigu");
    }

    @Override
    public Person read(Class<? extends Person> clazz, HttpInputMessage inputMessage)
            throws IOException, HttpMessageNotReadableException {
        return null;
    }

    @Override
    public void write(Person person, MediaType contentType, HttpOutputMessage outputMessage)
            throws IOException, HttpMessageNotWritableException {
        // 自定义协议数据的写出
        String data = person.getUserName() + ";" + person.getAge() + ";" + person.getBirth();
        OutputStream body = outputMessage.getBody();
        body.write(data.getBytes());
    }
}
```

![](image/SpringBoot2/image-20220823161758.png)

```java
@Bean
public WebMvcConfigurer webMvcConfigurer() {
    return new WebMvcConfigurer() {

        @Override
        public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
            Map<String, MediaType> mediaTypes = new HashMap<>();
            mediaTypes.put("json", MediaType.APPLICATION_JSON);
            mediaTypes.put("xml", MediaType.APPLICATION_XML);
            mediaTypes.put("gg", MediaType.parseMediaType("application/x-guigu"));
            // 指定支持解析哪些参数对应的哪些媒体类型
            ParameterContentNegotiationStrategy parameterStrategy = new ParameterContentNegotiationStrategy(
                    mediaTypes);
            configurer.strategies(Arrays.asList(parameterStrategy));
        }
```

![](image/SpringBoot2/image-20220823161814.png)

有可能我们添加的自定义的功能会覆盖默认很多功能，导致一些默认的功能失效。
大家考虑，上述功能除了我们完全自定义外？SpringBoot有没有为我们提供基于配置文件的快速修改媒体类型功能？怎么配置呢？【提示：参照SpringBoot官方文档web开发内容协商章节】

```java
@Override
public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
    Map<String, MediaType> mediaTypes = new HashMap<>();
    mediaTypes.put("json", MediaType.APPLICATION_JSON);
    mediaTypes.put("xml", MediaType.APPLICATION_XML);
    mediaTypes.put("gg", MediaType.parseMediaType("application/x-guigu"));
    // 指定支持解析哪些参数对应的哪些媒体类型
    ParameterContentNegotiationStrategy parameterStrategy = new ParameterContentNegotiationStrategy(
            mediaTypes);
    // parameterStrategy.setParameterName("ff"); // format
    HeaderContentNegotiationStrategy headeStrategy = new HeaderContentNegotiationStrategy();
    configurer.strategies(Arrays.asList(parameterStrategy, headeStrategy));
}
```


## 5、视图解析与模板引擎
视图解析：SpringBoot默认不支持 JSP，需要引入第三方模板引擎技术实现页面渲染。

### 1、视图解析

#### 1、视图解析原理流程
1. 目标方法处理的过程中，所有数据都会被放在 ModelAndViewContainer 里面。包括
   1. 数据
   2. 视图地址
   3. 控制器方法的参数（从请求参数中确定的）
2. 任何目标方法执行完成以后都会返回 ModelAndView（数据和视图地址）。

```java
// 位置：DispatcherServlet -> doDispatch
processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException); // 处理派发结果（页面改如何响应）
```

```java
// 位置：DispatcherServlet -> processDispatchResult
// Did the handler return a view to render?
if (mv != null && !mv.wasCleared()) {
    render(mv, request, response); // 进行页面渲染逻辑
    if (errorView) {
        WebUtils.clearErrorRequestAttributes(request);
    }
}
```

```java
// 位置：DispatcherServlet -> render
// 根据方法的String返回值得到 View 对象，方法内遍历所有的视图解析器尝试根据当前返回值得到View对象
view = resolveViewName(viewName, mv.getModelInternal(), locale, request);
```

![](image/SpringBoot2/image-20220823162054.png)

ContentNegotiationViewResolver 里面包含了上面所有的视图解析器，内部还是利用上面所有视图解析器得到视图对象。

![](image/SpringBoot2/image-20220823162100.png)

![](image/SpringBoot2/image-20220823162039.png)
![](image/SpringBoot2/image-20220823162048.png)

```java
// 位置：DispatcherServlet -> render
view.render(mv.getModelInternal(), request, response); // 视图对象调用自定义的render进行页面渲染工作
```

视图解析：
- 返回值以 `forward:` 开始：【转发】
  - new InternalResourceView(forwardUrl);
  - request.getRequestDispatcher(path).forward(request, response);
- 返回值以 `redirect:` 开始：【重定向】
  - new RedirectView();
  - 获取目标url地址
  - response.sendRedirect(encodedURL);
- 返回值是普通字符串：
  - new ThymeleafView();

### 2、模板引擎-Thymeleaf

#### 1、thymeleaf简介
Thymeleaf is a modern server-side Java template engine for both web and standalone environments, capable of processing HTML, XML, JavaScript, CSS and even plain text.

现代化、服务端Java模板引擎

#### 2、基本语法

##### 1、表达式
| 表达式名字 | 语法   | 用途                               |
| ---------- | ------ | ---------------------------------- |
| 变量取值   | ${...} | 获取请求域、session域、对象等值    |
| 选择变量   | *{...} | 获取上下文对象值                   |
| 消息       | #{...} | 获取国际化等值                     |
| 链接       | @{...} | 生成链接                           |
| 片段表达式 | ~{...} | jsp:include 作用，引入公共页面片段 |

##### 2、字面量
文本值: 'one text' , 'Another one!' , ...
数字: 0 , 34 , 3.0 , 12.3 , ...
布尔值: true , false
空值: null
变量: one , two , ...
变量不能有空格

##### 3、文本操作
字符串拼接: +
变量替换: |The name is ${name}| 

##### 4、数学运算
运算符: + , - , * , / , %

##### 5、布尔运算
运算符: and , or
一元运算: ! , not 

##### 6、比较运算
比较: > , < , >= , <= ( gt , lt , ge , le )
等式: == , != ( eq , ne ) 

##### 7、条件运算
If-then: (if) ? (then)
If-then-else: (if) ? (then) : (else)
Default: (value) ?: (defaultvalue) 

##### 8、特殊操作
无操作: _

#### 3、设置属性值-th:attr
设置单个值
```html
<form action="subscribe.html" th:attr="action=@{/subscribe}">
    <fieldset>
        <input type="text" name="email" />
        <input type="submit" value="Subscribe!" th:attr="value=#{subscribe.submit}" />
    </fieldset>
</form>
```

设置多个值
```html
<img src="../../images/gtvglogo.png" th:attr="src=@{/images/gtvglogo.png},title=#{logo},alt=#{logo}" />
```

以上两个的代替写法 th:xxxx
```html
<input type="submit" value="Subscribe!" th:value="#{subscribe.submit}" />
<form action="subscribe.html" th:action="@{/subscribe}">
```

[所有h5兼容的标签写法](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#setting-value-to-specific-attributes)

#### 4、迭代
```html
<tr th:each="prod : ${prods}">
    <td th:text="${prod.name}">Onions</td>
    <td th:text="${prod.price}">2.41</td>
    <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

```html
<tr th:each="prod,iterStat : ${prods}" th:class="${iterStat.odd}? 'odd'">
    <td th:text="${prod.name}">Onions</td>
    <td th:text="${prod.price}">2.41</td>
    <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

#### 5、条件运算
```html
<a href="comments.html"
   th:href="@{/product/comments(prodId=${prod.id})}"
   th:if="${not #lists.isEmpty(prod.comments)}">view</a>
```

```html
<div th:switch="${user.role}">
    <p th:case="'admin'">User is an administrator</p>
    <p th:case="#{roles.manager}">User is a manager</p>
    <p th:case="*">User is some other thing</p>
</div>
```

#### 6、属性优先级
![](image/SpringBoot2/image-20220823162945.png)

### 3、thymeleaf使用

##### 1、引入Starter
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

##### 2、自动配置好了thymeleaf
```java
@Configuration(proxyBeanMethods = false)
@EnableConfigurationProperties(ThymeleafProperties.class)
@ConditionalOnClass({ TemplateMode.class, SpringTemplateEngine.class })
@AutoConfigureAfter({ WebMvcAutoConfiguration.class, WebFluxAutoConfiguration.class })
public class ThymeleafAutoConfiguration {
```

自动配好的策略
1. 所有thymeleaf的配置值都在 ThymeleafProperties
2. 配置好了 SpringTemplateEngine 
3. 配好了 ThymeleafViewResolver 
4. 我们只需要直接开发页面

```java
@ConfigurationProperties(prefix = "spring.thymeleaf")
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING = StandardCharsets.UTF_8;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
```

##### 3、页面开发
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
        <meta charset="UTF-8">
            <title>Title</title>
    </head>
    <body>
        <h1 th:text="${msg}">哈哈</h1>
        <h2>
            <a href="www.atguigu.com" th:href="${link}">去百度</a>
            <br />
            <a href="www.atguigu.com" th:href="@{link}">去百度2</a>
        </h2>
    </body>
</html>
```

### 4、构建后台管理系统

#### 1、项目创建
thymeleaf、web-starter、devtools、lombok

#### 2、静态资源处理
自动配置好，我们只需要把所有静态资源放到 static 文件夹下

#### 3、路径构建
th:action="@{/login}"

#### 4、模板抽取
th:insert/replace/include

[官方文档](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#template-layout)

#### 5、页面跳转
```java
@PostMapping("/login")
public String main(User user, HttpSession session, Model model) {

    if (StringUtils.hasLength(user.getUserName()) && "123456".equals(user.getPassword())) {
        // 把登陆成功的用户保存起来
        session.setAttribute("loginUser", user);
        // 登录成功重定向到main.html; 重定向防止表单重复提交
        return "redirect:/main.html";
    } else {
        model.addAttribute("msg", "账号密码错误");
        // 回到登录页面
        return "login";
    }

}
```

#### 6、数据渲染
```java
@GetMapping("/dynamic_table")
public String dynamic_table(Model model) {
    // 表格内容的遍历
    List<User> users = Arrays.asList(new User("zhangsan", "123456"),
            new User("lisi", "123444"),
            new User("haha", "aaaaa"),
            new User("hehe ", "aaddd"));
    model.addAttribute("users", users);

    return "table/dynamic_table";
}
```

```html
<table class="display table table-bordered" id="hidden-table-info">
    <thead>
        <tr>
            <th>#</th>
            <th>用户名</th>
            <th>密码</th>
        </tr>
    </thead>
    <tbody>
        <tr class="gradeX" th:each="user,stats:${users}">
            <td th:text="${stats.count}">Trident</td>
            <td th:text="${user.userName}">Internet</td>
            <td>[[${user.password}]]</td>
        </tr>
    </tbody>
</table>
```


## 6、拦截器

### 1、HandlerInterceptor 接口
```java
/**
 * 登录检查
 * 1、配置好拦截器要拦截哪些请求
 * 2、把这些配置放在容器中
 */
@Slf4j
public class LoginInterceptor implements HandlerInterceptor {

    // 目标方法执行之前
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
            throws Exception {

        String requestURI = request.getRequestURI();
        log.info("preHandle拦截的请求路径是{}", requestURI);

        // 登录检查逻辑
        HttpSession session = request.getSession();
        Object loginUser = session.getAttribute("loginUser");

        // 登录了
        if (loginUser != null) {
            return true;// 放行
        }

        // 未登录：拦截，跳转到登录页
        request.setAttribute("msg", "请先登录");
        // re.sendRedirect("/");
        request.getRequestDispatcher("/").forward(request, response);
        return false;
    }

    // 目标方法执行完成以后
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
            ModelAndView modelAndView) throws Exception {
        log.info("postHandle执行{}", modelAndView);
    }

    // 页面渲染以后
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
            throws Exception {
        log.info("afterCompletion执行异常{}", ex);
    }
}
```

### 2、配置拦截器
```java
/**
 * 1、编写一个拦截器实现HandlerInterceptor接口（见：1、HandlerInterceptor 接口）
 * 2、拦截器注册到容器中（实现WebMvcConfigurer的addInterceptors）
 * 3、指定拦截规则【如果是拦截所有，静态资源也会被拦截】
 */
@Configuration
public class AdminWebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor())
                .addPathPatterns("/**") // 所有请求都被拦截包括静态资源
                .excludePathPatterns("/", "/login", "/css/**", "/fonts/**", "/images/**", "/js/**"); // 放行的请求
    }
}
```

### 3、拦截器原理
根据当前请求，找到HandlerExecutionChain【可以处理请求的handler以及handler的所有 拦截器】
![](image/SpringBoot2/image-20220823164239.png)
```java
// 位置：DispatcherServlet -> doDispatch
// Determine handler for the current request.
mappedHandler = getHandler(processedRequest);
// ...
if (!mappedHandler.applyPreHandle(processedRequest, response)) {
    return;
}
// Actually invoke the handler.
mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
// ...
mappedHandler.applyPostHandle(processedRequest, response, mv);
// ...
processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
```

```java
// 位置：DispatcherServlet -> processDispatchResult
if (mappedHandler != null) {
    // Exception (if any) is already handled..
    mappedHandler.triggerAfterCompletion(request, response, null);
}
```

```java
// 位置：HandlerExecutionChain
boolean applyPreHandle(HttpServletRequest request, HttpServletResponse response) throws Exception {
    for (int i = 0; i < this.interceptorList.size(); i++) {
        // 先顺序执行所有拦截器的 preHandle 方法
        HandlerInterceptor interceptor = this.interceptorList.get(i);
        if (!interceptor.preHandle(request, response, this.handler)) {
            // 如果当前拦截器返回为false。
            // 直接倒序执行所有已经执行了的拦截器的 afterCompletion
            triggerAfterCompletion(request, response, null);
            // 如果任何一个拦截器返回false，直接跳出不执行目标方法。
            return false;
        }
        // 如果当前拦截器prehandler返回为true。则执行下一个拦截器的preHandle
        this.interceptorIndex = i;
    }
    // 所有拦截器都返回True，执行目标方法。
    return true;
}

void applyPostHandle(HttpServletRequest request, HttpServletResponse response, @Nullable ModelAndView mv)
        throws Exception {

    for (int i = this.interceptorList.size() - 1; i >= 0; i--) {
        // 倒序执行所有拦截器的postHandle方法。
        HandlerInterceptor interceptor = this.interceptorList.get(i);
        interceptor.postHandle(request, response, this.handler, mv);
    }
}

void triggerAfterCompletion(HttpServletRequest request, HttpServletResponse response, @Nullable Exception ex) {
    // 前面的步骤有任何异常都会直接倒序触发 afterCompletion
    // 页面成功渲染完成以后，也会倒序触发 afterCompletion
    for (int i = this.interceptorIndex; i >= 0; i--) {
        HandlerInterceptor interceptor = this.interceptorList.get(i);
        try {
            interceptor.afterCompletion(request, response, this.handler, ex);
        }
        catch (Throwable ex2) {
            logger.error("HandlerInterceptor.afterCompletion threw exception", ex2);
        }
    }
}
```

![](image/SpringBoot2/image-20220823164246.png)


## 7、文件上传

### 1、页面表单
```html
<form th:action="@{/upload}" method="post" enctype="multipart/form-data">
    <div>
        <label>邮箱</label>
        <input type="email" name="email" placeholder="Enter email">
    </div>
    <div>
        <label>名字</label>
        <input type="text" name="username" placeholder="Password">
    </div>
    <div>
        <label>头像</label>
        <input type="file" name="headerImg">
    </div>
    <div>
        <label>生活照</label>
        <input type="file" name="photos" multiple>
    </div>
    <button type="submit">提交</button>
</form>
```

### 2、文件上传代码
```java
// MultipartFile 自动封装上传过来的文件
@PostMapping("/upload")
public String upload(@RequestParam("email") String email,
                     @RequestParam("username") String username,
                     @RequestPart("headerImg") MultipartFile headerImg,
                     @RequestPart("photos") MultipartFile[] photos) throws IOException {

    log.info("上传的信息：email={}，username={}，headerImg={}，photos={}",
            email, username, headerImg.getSize(), photos.length);

    if (!headerImg.isEmpty()) {
        // 保存到文件服务器，OSS服务器
        String originalFilename = headerImg.getOriginalFilename();
        headerImg.transferTo(new File("H:\\cache\\" + originalFilename));
    }

    if (photos.length > 0) {
        for (MultipartFile photo : photos) {
            if (!photo.isEmpty()) {
                String originalFilename = photo.getOriginalFilename();
                photo.transferTo(new File("H:\\cache\\" + originalFilename));
            }
        }
    }

    return "main";
}
```

### 3、自动配置原理
文件上传自动配置类 -> MultipartAutoConfiguration -> MultipartProperties
- 自动配置好了 StandardServletMultipartResolver 【文件上传解析器】

### 4、文件上传原理步骤
```java
// 位置：DispatcherServlet -> doDispatch
processedRequest = checkMultipart(request);
```

```java
// 位置：DispatcherServlet
protected HttpServletRequest checkMultipart(HttpServletRequest request) throws MultipartException {
    // 使用文件上传解析器判断并封装文件上传请求
    // 判断（isMultipart）：StringUtils.startsWithIgnoreCase(request.getContentType(), "multipart/")
    if (this.multipartResolver != null && this.multipartResolver.isMultipart(request)) {
        if (WebUtils.getNativeRequest(request, MultipartHttpServletRequest.class) != null) {
            if (request.getDispatcherType().equals(DispatcherType.REQUEST)) {
                logger.trace("Request already resolved to MultipartHttpServletRequest, e.g. by MultipartFilter");
            }
        }
        else if (hasMultipartException(request)) {
            logger.debug("Multipart resolution previously failed for current request - " +
                    "skipping re-resolution for undisturbed error rendering");
        }
        else {
            try {
                // 参数解析器来解析请求中的文件内容封装成MultipartFile，返回值类型：MultipartHttpServletRequest
                return this.multipartResolver.resolveMultipart(request);
            }
```

```java
// 位置：DispatcherServlet -> doDispatch
mv = ha.handle(processedRequest, response, mappedHandler.getHandler());
// 位置：AbstractHandlerMethodAdapter -> handle
return handleInternal(request, response, (HandlerMethod) handler);
// 位置：RequestMappingHandlerAdapter -> handleInternal
mav = invokeHandlerMethod(request, response, handlerMethod);
```

![](image/SpringBoot2/image-20220823164509.png)

```java
// 位置：RequestMappingHandlerAdapter -> invokeHandlerMethod
invocableMethod.invokeAndHandle(webRequest, mavContainer);
// 位置：ServletInvocableHandlerMethod -> invokeAndHandle
Object returnValue = invokeForRequest(webRequest, mavContainer, providedArgs);
// 位置：InvocableHandlerMethod -> invokeForRequest
Object[] args = getMethodArgumentValues(request, mavContainer, providedArgs);
// 位置：InvocableHandlerMethod -> getMethodArgumentValues
args[i] = this.resolvers.resolveArgument(parameter, mavContainer, request, this.dataBinderFactory);
// 位置：HandlerMethodArgumentResolverComposite -> resolveArgument
return resolver.resolveArgument(parameter, mavContainer, webRequest, binderFactory);
// 位置：RequestPartMethodArgumentResolver -> resolveArgument
Object mpArg = MultipartResolutionDelegate.resolveMultipartArgument(name, parameter, servletRequest);
// 位置：MultipartResolutionDelegate -> resolveMultipartArgument
List<MultipartFile> files = multipartRequest.getFiles(name);
// 位置：AbstractMultipartHttpServletRequest -> getFiles
List<MultipartFile> multipartFiles = getMultipartFiles().get(name);
```

getMultipartFiles中提前将request中文件信息封装为一个Map；`MultiValueMap<String, MultipartFile>`

`MultipartFile::transferTo` 使用FileCopyUtils：实现文件流的拷贝


## 8、异常处理

### 1、错误处理

##### 1、默认规则
- 默认情况下，Spring Boot提供 `/error` 处理所有错误的映射
- 对于机器客户端，它将生成JSON响应，其中包含错误，HTTP状态和异常消息的详细信息。
    ![](image/SpringBoot2/image-20220823164720.png)
- 对于浏览器客户端，响应一个“whitelabel”错误视图，以HTML格式呈现相同的数据
    ![](image/SpringBoot2/image-20220823164816.png)

- 要对其进行自定义，添加View解析为error
- 要完全替换默认行为，可以实现 ErrorController 并注册该类型的Bean定义，或添加ErrorAttributes类型的组件以使用现有机制但替换其内容。
- error/下的4xx，5xx页面会被自动解析；
    ![](image/SpringBoot2/image-20220823164853.png)

##### 2、定制错误处理逻辑
自定义错误页
- error/404.html、error/5xx.html；
- 有精确的错误状态码页面就匹配精确，没有就找 4xx.html；如果都没有就触发白页

@ControllerAdvice + @ExceptionHandler处理全局异常；底层支持：ExceptionHandlerExceptionResolver
```java
@Slf4j
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler({ ArithmeticException.class, NullPointerException.class }) // 处理异常
    public String handleArithException(Exception e) {

        log.error("异常是：{}", e);
        return "login"; // 视图地址
    }
}
```

@ResponseStatus + 自定义异常；底层支持：ResponseStatusExceptionResolver
```java
@ResponseStatus(value = HttpStatus.FORBIDDEN, reason = "用户数量太多")
public class UserTooManyException extends RuntimeException {

    public UserTooManyException() {}

    public UserTooManyException(String message) { super(message); }
}
```
- 把responsestatus注解的信息底层调用 `response.sendError(statusCode, resolvedReason);`
- tomcat发送 /error 请求，进入 /error 处理逻辑

Spring底层的异常（如参数类型转换异常）；底层支持：DefaultHandlerExceptionResolver（处理框架底层的异常）
- response.sendError(HttpServletResponse.SC_BAD_REQUEST, ex.getMessage()); 
- ![](image/SpringBoot2/image-20220823165049.png)

自定义实现 HandlerExceptionResolver 处理异常；可以作为默认的全局异常处理规则
```java
@Order(value = Ordered.HIGHEST_PRECEDENCE) // 优先级，数字越小优先级越高
@Component
public class CustomerHandlerExceptionResolver implements HandlerExceptionResolver {
    @Override
    public ModelAndView resolveException(HttpServletRequest request,
                                        HttpServletResponse response,
                                        Object handler, Exception ex) {

        try {
            response.sendError(511, "我喜欢的错误");
        } catch (IOException e) {
            e.printStackTrace();
        }
        return new ModelAndView();
    }
}
```
- ![](image/SpringBoot2/image-20220823165058.png)

ErrorViewResolver 实现自定义处理异常（一般不使用这种方式自定义）
- `response.sendError()`：/error 请求就会转给 controller
- 你的异常没有任何人能处理：tomcat底层response.sendError，error请求就会转给controller
- basicErrorController 要去的页面地址是 ErrorViewResolver；

##### 3、异常处理自动配置原理
ErrorMvcAutoConfiguration 自动配置异常处理规则：server、spring.mvc

容器中的组件：【类型 id】
- DefaultErrorAttributes errorAttributes：定义错误页面中可以包含哪些数据。
    ```java
    @Order(Ordered.HIGHEST_PRECEDENCE)
    public class DefaultErrorAttributes implements ErrorAttributes, HandlerExceptionResolver, Ordered {
    ```
    - ![](image/SpringBoot2/image-20220823165245.png)
    - ![](image/SpringBoot2/image-20220823165252.png)
- BasicErrorController basicErrorController（json+白页 适配响应）
    ```java
    @Controller
    @RequestMapping("${server.error.path:${error.path:/error}}")
    // 默认处理 /error 路径的请求
    public class BasicErrorController extends AbstractErrorController {
    ```
    - 页面响应：new ModelAndView("error", model);
    - 写出去json  ![](image/SpringBoot2/image-20220823165305.png)
    - 错误页  ![](image/SpringBoot2/image-20220823165312.png)
- WhitelabelErrorViewConfiguration whitelabelErrorViewConfiguration
  - View error：响应默认错误页（StaticView::render中默认是一个白页HTML）
  - BeanNameViewResolver beanNameViewResolver（视图解析器）：按照返回的视图名作为组件的id去容器中找View对象。
- DefaultErrorViewResolverConfiguration（过时）
  - DefaultErrorViewResolver conventionErrorViewResolver
    - 如果发生错误，会以HTTP的状态码 作为视图页地址（viewName），找到真正的页面

```java
// 位置：DefaultErrorViewResolver
static {
    Map<Series, String> views = new EnumMap<>(Series.class);
    views.put(Series.CLIENT_ERROR, "4xx");
    views.put(Series.SERVER_ERROR, "5xx");
    SERIES_VIEWS = Collections.unmodifiableMap(views);
}
@Override
public ModelAndView resolveErrorView(HttpServletRequest request, HttpStatus status, Map<String, Object> model) {
    ModelAndView modelAndView = resolve(String.valueOf(status.value()), model);
    if (modelAndView == null && SERIES_VIEWS.containsKey(status.series())) {
        modelAndView = resolve(SERIES_VIEWS.get(status.series()), model);
    }
    return modelAndView;
}

private ModelAndView resolve(String viewName, Map<String, Object> model) {
    String errorViewName = "error/" + viewName;
    TemplateAvailabilityProvider provider = this.templateAvailabilityProviders.getProvider(errorViewName,
            this.applicationContext);
    if (provider != null) {
        return new ModelAndView(errorViewName, model);
    }
    return resolveResource(errorViewName, model);
}
```

##### 4、异常处理步骤流程
1、执行目标方法，目标方法运行期间有任何异常都会被catch、而且标志当前请求结束；并且用 dispatchException 封装异常
```java
// 位置：DispatcherServlet -> doDispatch
catch (Exception ex) {
    dispatchException = ex;
}
catch (Throwable err) {
    // As of 4.3, we're processing Errors thrown from handler methods as well,
    // making them available for @ExceptionHandler methods and other scenarios.
    dispatchException = new NestedServletException("Handler dispatch failed", err);
}
```

2、进入视图解析流程（页面渲染） 
```java
// 位置：DispatcherServlet -> doDispatch
processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
```

3、处理handler发生的异常，处理完成返回ModelAndView
```java
// 位置：DispatcherServlet -> processDispatchResult
mv = processHandlerException(request, response, handler, exception);
```

```java
// 位置：DispatcherServlet -> processHandlerException
ModelAndView exMv = null;
if (this.handlerExceptionResolvers != null) {
    // 遍历 handlerExceptionResolvers【见：5、系统默认的异常解析器】，处理当前异常直到exMv != null
    for (HandlerExceptionResolver resolver : this.handlerExceptionResolvers) {
        exMv = resolver.resolveException(request, response, handler, ex);
        if (exMv != null) {
            break;
        }
    }
}
// ...
throw ex; // 默认没有任何处理器能处理异常，所以异常会被抛出
```

如果异常没有被处理，最终底层就会发送 /error 请求，会被底层的 BasicErrorController 处理
```java
// 位置：BasicErrorController -> errorHtml
ModelAndView modelAndView = resolveErrorView(request, response, status, model); // 解析错误视图
```

```java
// 位置：AbstractErrorController -> resolveErrorView
// 遍历所有的 ErrorViewResolver 【见：6、系统默认的错误视图解析器】，解析错误视图。
for (ErrorViewResolver resolver : this.errorViewResolvers) {
    ModelAndView modelAndView = resolver.resolveErrorView(request, status, model);
    if (modelAndView != null) {
        return modelAndView;
    }
}
return null;
```

##### 5、系统默认的异常解析器
![](image/SpringBoot2/image-20220823165416.png)

![](image/SpringBoot2/image-20220823165423.png)

```java
// 位置：DefaultErrorAttributes -> resolveException
storeErrorAttributes(request, ex); // 把异常信息保存到request域：request.setAttribute(ERROR_ATTRIBUTE, ex);
return null;
```

```java
// 位置：HandlerExceptionResolverComposite -> resolveException
if (this.resolvers != null) {
    for (HandlerExceptionResolver handlerExceptionResolver : this.resolvers) {
        // ExceptionHandlerExceptionResolver -> @ExceptionHandler
        // ResponseStatusExceptionResolver -> @ResponseStatus
        // DefaultHandlerExceptionResolver -> ...
        ModelAndView mav = handlerExceptionResolver.resolveException(request, response, handler, ex);
        if (mav != null) {
            return mav;
        }
    }
}
return null;
```

##### 6、系统默认的错误视图解析器
![](image/SpringBoot2/image-20220823165436.png)

```java
// 位置：DefaultErrorViewResolver
@Override
public ModelAndView resolveErrorView(HttpServletRequest request, HttpStatus status, Map<String, Object> model) {
    ModelAndView modelAndView = resolve(String.valueOf(status.value()), model);
    if (modelAndView == null && SERIES_VIEWS.containsKey(status.series())) {
        modelAndView = resolve(SERIES_VIEWS.get(status.series()), model);
    }
    return modelAndView;
}
private ModelAndView resolve(String viewName, Map<String, Object> model) {
    String errorViewName = "error/" + viewName; // 把响应状态码作为错误页的地址
    TemplateAvailabilityProvider provider = this.templateAvailabilityProviders.getProvider(errorViewName,
            this.applicationContext);
    if (provider != null) {
        return new ModelAndView(errorViewName, model);
    }
    return resolveResource(errorViewName, model);
}
private ModelAndView resolveResource(String viewName, Map<String, Object> model) {
    for (String location : this.resources.getStaticLocations()) {
        try {
            Resource resource = this.applicationContext.getResource(location);
            resource = resource.createRelative(viewName + ".html");
            if (resource.exists()) {
                return new ModelAndView(new HtmlResourceView(resource), model);
            }
        }
        catch (Exception ex) {
        }
    }
    return null;
}
```

模板引擎最终响应这个逻辑视图：error/500


## 9、Web原生组件注入（Servlet、Filter、Listener）

### 1、使用Servlet API（推荐）
```java
// ServletComponentScan注解开启原生Servlet组件扫描，该注解标注在SpringBoot的启动类上
// basePackages默认值为SpringBoot的启动类所在包及其子包
@ServletComponentScan(basePackages = "com.atguigu.admin")
```

```java
@WebServlet(urlPatterns = "/my") // 效果：直接响应，没有经过Spring的拦截器。
public class MyServlet extends HttpServlet {
```
```java
@WebFilter(urlPatterns = { "/css/*", "/images/*" }) // 原生Servlet中所有：/*，SpringMVC中：/**
public class MyFilter implements Filter {
```
```java
@WebListener
public class MySwervletContextListener implements ServletContextListener {
```

扩展：DispatchServlet 如何注册进来
- 容器中自动配置了 DispatcherServlet 属性绑定到 WebMvcProperties；对应的配置文件配置项是 spring.mvc。
- 通过 `ServletRegistrationBean<DispatcherServlet>` 把 DispatcherServlet 配置进来。
- 默认映射的是 / 路径。

![](image/SpringBoot2/image-20220823165623.png)

Tomcat-Servlet：
多个Servlet都能处理到同一层路径，精确优选原则
- DispatcherServlet: /
- MyServlet: /my

### 2、使用RegistrationBean
`ServletRegistrationBean`, `FilterRegistrationBean`, and `ServletListenerRegistrationBean`

```java
@Configuration
public class MyRegistConfig {

    @Bean
    public ServletRegistrationBean myServlet() {
        MyServlet myServlet = new MyServlet();
        return new ServletRegistrationBean(myServlet, "/my", "/my02");
    }

    @Bean
    public FilterRegistrationBean myFilter() {
        MyFilter myFilter = new MyFilter();
        // return new FilterRegistrationBean(myFilter,myServlet());
        FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean(myFilter);
        filterRegistrationBean.setUrlPatterns(Arrays.asList("/my", "/css/*"));
        return filterRegistrationBean;
    }

    @Bean
    public ServletListenerRegistrationBean myListener() {
        MySwervletContextListener mySwervletContextListener = new MySwervletContextListener();
        return new ServletListenerRegistrationBean(mySwervletContextListener);
    }
}
```


## 10、嵌入式Servlet容器

### 1、切换嵌入式Servlet容器
- 默认支持的webServer
  - Tomcat, Jetty, or Undertow
  - ServletWebServerApplicationContext 容器启动寻找 ServletWebServerFactory 并引导创建服务器
- 切换服务器

![](image/SpringBoot2/image-20220823165809.png)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

#### 原理
- SpringBoot应用启动发现当前是Web应用。web场景包-导入tomcat
- web应用会创建一个web版的ioc容器 ServletWebServerApplicationContext 
- ServletWebServerApplicationContext 启动的时候寻找 ServletWebServerFactory（Servlet 的web服务器工厂 -> Servlet 的web服务器）  
- SpringBoot底层默认有很多的 WebServer 工厂：TomcatServletWebServerFactory, JettyServletWebServerFactory, or UndertowServletWebServerFactory
- 底层直接会有一个自动配置类：ServletWebServerFactoryAutoConfiguration
- ServletWebServerFactoryAutoConfiguration导入了ServletWebServerFactoryConfiguration（配置类）
- ServletWebServerFactoryConfiguration 配置类 根据动态判断系统中到底导入了那个Web服务器的包。（默认是web-starter导入tomcat包），容器中就有 TomcatServletWebServerFactory
- TomcatServletWebServerFactory 创建出Tomcat服务器并启动；TomcatWebServer 的构造器拥有初始化方法 -> initialize -> this.tomcat.start();
- 内嵌服务器，就是手动把启动服务器的代码调用（tomcat核心jar包存在）

### 2、定制Servlet容器
- 修改配置文件 server.xxx（推荐）
- 直接自定义 ConfigurableServletWebServerFactory 
- 实现 `WebServerFactoryCustomizer<ConfigurableServletWebServerFactory>`
  - 把配置文件的值和ServletWebServerFactory 进行绑定

XxxCustomizer：定制化器，可以改变Xxx的默认规则

```java
import org.springframework.boot.web.server.WebServerFactoryCustomizer;
import org.springframework.boot.web.servlet.server.ConfigurableServletWebServerFactory;
import org.springframework.stereotype.Component;

@Component
public class CustomizationBean implements WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> {

    @Override
    public void customize(ConfigurableServletWebServerFactory server) {
        server.setPort(9000);
    }

}
```


## 11、定制化原理

### 1、定制化的常见方式
- 修改配置文件（推荐）
- XxxCustomizer
- 编写自定义的配置类 XxxConfiguration + @Bean替换、增加容器中默认组件。如视图解析器 
- Web应用：编写一个配置类实现 WebMvcConfigurer 即可定制化web功能 + @Bean给容器中再扩展一些组件
    ```java
    @Configuration
    public class AdminWebConfig implements WebMvcConfigurer
    ```

#### 全面接管SpringMVC
@EnableWebMvc + WebMvcConfigurer + @Bean：所有规则全部自己重新配置；实现定制和扩展功能

原理
1. WebMvcAutoConfiguration：默认的SpringMVC的自动配置功能类。静态资源、欢迎页...
2. 一旦使用 @EnableWebMvc 。会 @Import(DelegatingWebMvcConfiguration.class)
3. DelegatingWebMvcConfiguration 的作用，只保证SpringMVC最基本的使用
   - 把所有系统中的 WebMvcConfigurer 拿过来。所有功能的定制都是这些 WebMvcConfigurer 合起来一起生效
   - 自动配置了一些非常底层的组件。RequestMappingHandlerMapping、这些组件依赖的组件都是从容器中获取
    ```java
    public class DelegatingWebMvcConfiguration extends WebMvcConfigurationSupport
    ```
4. WebMvcAutoConfiguration 里面的配置要能生效必须 @ConditionalOnMissingBean(WebMvcConfigurationSupport.class)
5. @EnableWebMvc 导致了 WebMvcAutoConfiguration 没有生效。

### 2、原理分析套路
场景starter -> XxxAutoConfiguration -> 导入xxx组件 -> 绑定XxxProperties -> 绑定配置文件项



# 六、数据访问

## 1、SQL

### 1、数据源的自动配置-HikariDataSource

#### 1、导入JDBC场景
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jdbc</artifactId>
</dependency>
```

![](image/SpringBoot2/image-20220823173340.png)

数据库驱动？
为什么导入JDBC场景，官方不导入驱动？官方不知道我们接下要操作什么数据库。
数据库版本和驱动版本对应

```xml
<!-- 默认版本： -->
<mysql.version>8.0.22</mysql.version>

<!-- 想要修改版本 -->
<!-- 1、直接依赖引入具体版本（maven的就近依赖原则） -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.49</version>
</dependency>
<!-- 2、重新声明版本（maven的属性的就近优先原则） -->
<properties>
    <mysql.version>5.1.49</mysql.version>
</properties>
```

#### 2、分析自动配置

##### 1、自动配置的类
- DataSourceAutoConfiguration：数据源的自动配置
  - 修改数据源相关的配置：spring.datasource
  - 数据库连接池的配置，是自己容器中没有DataSource才自动配置的
  - 底层配置好的连接池是：HikariDataSource

```java
@Configuration(proxyBeanMethods = false)
@Conditional(PooledDataSourceCondition.class)
@ConditionalOnMissingBean({ DataSource.class, XADataSource.class })
@Import({ DataSourceConfiguration.Hikari.class, DataSourceConfiguration.Tomcat.class,
        DataSourceConfiguration.Dbcp2.class, DataSourceConfiguration.OracleUcp.class,
        DataSourceConfiguration.Generic.class, DataSourceJmxConfiguration.class })
protected static class PooledDataSourceConfiguration {
```

- DataSourceTransactionManagerAutoConfiguration：事务管理器的自动配置
- JdbcTemplateAutoConfiguration：JdbcTemplate的自动配置，可以来对数据库进行crud
  - 修改 `spring.jdbc` 前缀的配置项以修改JdbcTemplate
  - @Bean @Primary JdbcTemplate：容器中有这个组件
- JndiDataSourceAutoConfiguration：jndi的自动配置
- XADataSourceAutoConfiguration：分布式事务相关的

#### 3、修改配置项
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db_account
    username: root
    password: 123456
    driver-class-name: com.mysql.jdbc.Driver
```

#### 4、测试
```java
@Slf4j
@SpringBootTest
class Boot05WebAdminApplicationTests {

    @Autowired
    JdbcTemplate jdbcTemplate;

    @Test
    void contextLoads() {

        Long aLong = jdbcTemplate.queryForObject("select count(*) from account_tbl", Long.class);
        log.info("记录总数：{}", aLong);
    }

}
```

### 2、使用Druid数据源

#### 1、druid官方github地址
https://github.com/alibaba/druid

整合第三方技术的两种方式
- 自定义
- 找starter

#### 2、自定义方式

##### 1、创建数据源
```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.17</version>
</dependency>
```

```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
    <property name="maxActive" value="20" />
    <property name="initialSize" value="1" />
    <property name="maxWait" value="60000" />
    <property name="minIdle" value="1" />
    <property name="timeBetweenEvictionRunsMillis" value="60000" />
    <property name="minEvictableIdleTimeMillis" value="300000" />
    <property name="testWhileIdle" value="true" />
    <property name="testOnBorrow" value="false" />
    <property name="testOnReturn" value="false" />
    <property name="poolPreparedStatements" value="true" />
    <property name="maxOpenPreparedStatements" value="20" />
```

```java
@ConfigurationProperties("spring.datasource")
@Bean
public DataSource dataSource() throws SQLException {
    DruidDataSource druidDataSource = new DruidDataSource();
    return druidDataSource;
}
```

##### 2、StatViewServlet
StatViewServlet的用途包括：
- 提供监控信息展示的html页面
- 提供监控信息的JSON API

```xml
<servlet>
    <servlet-name>DruidStatView</servlet-name>
    <servlet-class>com.alibaba.druid.support.http.StatViewServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>DruidStatView</servlet-name>
    <url-pattern>/druid/*</url-pattern>
</servlet-mapping>
```

```java
// 配置 druid的监控页功能
@Bean
public ServletRegistrationBean statViewServlet() {
    StatViewServlet statViewServlet = new StatViewServlet();
    ServletRegistrationBean<StatViewServlet> registrationBean = new ServletRegistrationBean<>(statViewServlet,
            "/druid/*");

    registrationBean.addInitParameter("loginUsername", "admin");
    registrationBean.addInitParameter("loginPassword", "123456");

    return registrationBean;
}
```

##### 3、StatFilter
用于统计监控信息；如SQL监控、URI监控

需要给数据源中配置如下属性；可以允许多个filter，多个用，分割；如：
```xml
<property name="filters" value="stat,slf4j" />
```

```java
druidDataSource.setFilters("stat,wall");
```

系统中所有filter：
| 别名          | Filter类名                                              |
| ------------- | ------------------------------------------------------- |
| default       | com.alibaba.druid.filter.stat.StatFilter                |
| stat          | com.alibaba.druid.filter.stat.StatFilter                |
| mergeStat     | com.alibaba.druid.filter.stat.MergeStatFilter           |
| encoding      | com.alibaba.druid.filter.encoding.EncodingConvertFilter |
| log4j         | com.alibaba.druid.filter.logging.Log4jFilter            |
| log4j2        | com.alibaba.druid.filter.logging.Log4j2Filter           |
| slf4j         | com.alibaba.druid.filter.logging.Slf4jLogFilter         |
| commonlogging | com.alibaba.druid.filter.logging.CommonsLogFilter       |

慢SQL记录配置
```xml
<bean id="stat-filter" class="com.alibaba.druid.filter.stat.StatFilter">
    <property name="slowSqlMillis" value="10000" />
    <property name="logSlowSql" value="true" />
</bean>
<!-- 使用 slowSqlMillis 定义慢SQL的时长 -->
```

```java
// WebStatFilter 用于采集web-jdbc关联监控的数据。
@Bean
public FilterRegistrationBean webStatFilter() {
    WebStatFilter webStatFilter = new WebStatFilter();

    FilterRegistrationBean<WebStatFilter> filterRegistrationBean = new FilterRegistrationBean<>(webStatFilter);
    filterRegistrationBean.setUrlPatterns(Arrays.asList("/*"));
    filterRegistrationBean.addInitParameter("exclusions", "*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*");

    return filterRegistrationBean;
}
```

#### 3、使用官方starter方式

##### 1、引入druid-starter
```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.17</version>
</dependency>
```

##### 2、分析自动配置
```java
@Configuration
@ConditionalOnClass(DruidDataSource.class)
@AutoConfigureBefore(DataSourceAutoConfiguration.class)
@EnableConfigurationProperties({DruidStatProperties.class, DataSourceProperties.class}) // spring.datasource.druid, spring.datasource
@Import({DruidSpringAopConfiguration.class,       // 监控SpringBean: spring.datasource.druid.aop-patterns
         DruidStatViewServletConfiguration.class, // 监控页: spring.datasource.druid.stat-view-servlet
         DruidWebStatFilterConfiguration.class,   // Web监控: spring.datasource.druid.web-stat-filter
         DruidFilterConfiguration.class})         // Druid自己Filter
public class DruidDataSourceAutoConfigure {

    private static final Logger LOGGER = LoggerFactory.getLogger(DruidDataSourceAutoConfigure.class);

    @Bean(initMethod = "init")
    @ConditionalOnMissingBean
    public DataSource dataSource() {
        LOGGER.info("Init DruidDataSource");
        return new DruidDataSourceWrapper();
    }
}
```

DruidFilter
- spring.datasource.druid.filter.stat
- spring.datasource.druid.filter.config
- spring.datasource.druid.filter.encoding
- spring.datasource.druid.filter.slf4j
- spring.datasource.druid.filter.log4j
- spring.datasource.druid.filter.log4j2
- spring.datasource.druid.filter.commons-log
- spring.datasource.druid.filter.wall

##### 3、配置示例
```yaml
spring:
  datasource:
    druid:
      aop-patterns: com.atguigu.admin.* # 监控SpringBean
      filters: stat,wall                # 底层开启功能，stat（sql监控），wall（防火墙）

      stat-view-servlet:                # 配置监控页功能
        enabled: true
        login-username: admin
        login-password: admin
        resetEnable: false

      web-stat-filter:                  # 监控web
        enabled: true
        urlPattern: /*
        exclusions: '*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*'

      filter:
        stat:                           # 对上面filters里面的stat的详细配置
          slow-sql-millis: 1000
          logSlowSql: true
          enabled: true
        wall:
          enabled: true
          config:
            drop-table-allow: false
```

[SpringBoot配置示例](https://github.com/alibaba/druid/tree/master/druid-spring-boot-starter)

[配置项列表](https://github.com/alibaba/druid/wiki/DruidDataSource%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7%E5%88%97%E8%A1%A8)

### 3、整合MyBatis操作
https://github.com/mybatis

starter
- SpringBoot官方的Starter: spring-boot-starter-*
- 第三方的: *-spring-boot-starter

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.4</version>
</dependency>
```

![](image/SpringBoot2/image-20220823174122.png)

#### 1、配置模式
- 全局配置文件
- SqlSessionFactory：自动配置好了
- SqlSession：自动配置了 SqlSessionTemplate 组合了 SqlSession
- @Import(AutoConfiguredMapperScannerRegistrar.class)
- Mapper：只要我们写的操作MyBatis的接口标注了 @Mapper 注解就会被自动扫描进来

```java
@org.springframework.context.annotation.Configuration
@ConditionalOnClass({ SqlSessionFactory.class, SqlSessionFactoryBean.class })
@ConditionalOnSingleCandidate(DataSource.class)
@EnableConfigurationProperties(MybatisProperties.class) // MybatisProperties -> mybatis
@AutoConfigureAfter({ DataSourceAutoConfiguration.class, MybatisLanguageDriverAutoConfiguration.class })
public class MybatisAutoConfiguration implements InitializingBean {
```

修改配置文件中 mybatis 前缀的配置项：
```yaml
# 配置mybatis规则
mybatis:
  config-location: classpath:mybatis/mybatis-config.xml  #全局配置文件位置
  mapper-locations: classpath:mybatis/mapper/*.xml  #sql映射文件位置
```

```xml
<!-- Mapper接口 -> 绑定xml -->
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.atguigu.admin.mapper.AccountMapper">
    <!-- public Account getAcct(Long id); -->
    <select id="getAcct" resultType="com.atguigu.admin.bean.Account">
        select * from account_tbl where id=#{id}
    </select>
</mapper>
```

```yaml
# 配置mybatis规则
mybatis:
# config-location: classpath:mybatis/mybatis-config.xml
  mapper-locations: classpath:mybatis/mapper/*.xml
  configuration:
    map-underscore-to-camel-case: true

# 配置mybatis.configuration下面的所有，就是相当于改mybatis全局配置文件中的值
# 可以不写全局配置文件，所有全局配置文件的配置都放在configuration配置项中即可
# config-location和configuration只能配置一个
```

- 导入mybatis官方starter
- 编写mapper接口，标注 @Mapper 注解
- 编写sql映射文件并绑定mapper接口
- 在application.yaml中指定Mapper配置文件的位置，以及指定全局配置文件的信息
  - 建议：配置在mybatis.configuration

#### 2、注解模式
```java
@Mapper
public interface CityMapper {

    @Select("select * from city where id=#{id}")
    public City getById(Long id);

    @Insert("insert into city(`name`,`state`,`country`) values(#{name},#{state},#{country})")
    @Options(useGeneratedKeys = true,keyProperty = "id")
    public void insert(City city);

}
```

#### 3、混合模式
最佳实战：
- 引入mybatis-starter
- 配置application.yaml中，指定mapper-location位置即可
- 编写Mapper接口并标注@Mapper注解
  - 简化：`@MapperScan("com.atguigu.admin.mapper")`
  - 其他的接口就可以不用标注@Mapper注解
- 简单方法直接注解方式
- 复杂方法编写mapper.xml进行绑定映射

### 4、整合 MyBatis-Plus 完成CRUD

#### 1、什么是MyBatis-Plus
MyBatis-Plus（简称 MP）是一个 MyBatis 的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。
[MyBatis-Plus官网](https://baomidou.com/)
建议安装 MybatisX 插件

#### 2、整合MyBatis-Plus
```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.1</version>
</dependency>
```

自动配置
- MybatisPlusAutoConfiguration 配置类 -> MybatisPlusProperties 配置项绑定 -> mybatis-plus 配置文件前缀
- SqlSessionFactory【默认：容器中的数据源】
- mapperLocations【默认：`classpath*:/mapper/**/*.xml`】
  - 任意包的类路径下的所有mapper文件夹下任意路径下的所有xml都是sql映射文件。
  - 建议以后sql映射文件，放在 mapper 下
- 容器中也自动配置好了 SqlSessionTemplate
- @Mapper 标注的接口也会被自动扫描
  - 建议直接 `@MapperScan("com.atguigu.admin.mapper")` 批量扫描就行


优点：
- 只需要我们的Mapper继承 BaseMapper 就可以拥有crud能力

几个注解
- @TableName("user_tbl") 表名
- @TableField(exist = false)  当前属性表中不存在

#### 3、CRUD功能
```java
@GetMapping("/user/delete/{id}")
public String deleteUser(@PathVariable("id") Long id,
        @RequestParam(value = "pn", defaultValue = "1") Integer pn,
        RedirectAttributes ra) {

    userService.removeById(id);

    ra.addAttribute("pn", pn);
    return "redirect:/dynamic_table";
}

@GetMapping("/dynamic_table")
public String dynamic_table(@RequestParam(value = "pn", defaultValue = "1") Integer pn, Model model) {

    // 构造分页参数
    Page<User> page = new Page<>(pn, 2);
    // 调用page进行分页
    Page<User> userPage = userService.page(page, null);

    model.addAttribute("users", userPage);
    return "table/dynamic_table";
}
```

```java
public interface UserService extends IService<User> { }
```

```java
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService { }
```


## 2、NoSQL
Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。
它支持多种类型的数据结构，如 字符串（strings）， 散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets） 与范围查询， bitmaps， hyperloglogs 和 地理空间（geospatial） 索引半径查询。
Redis 内置了 复制（replication），LUA脚本（Lua scripting）， LRU驱动事件（LRU eviction），事务（transactions） 和不同级别的 磁盘持久化（persistence）， 并通过 Redis哨兵（Sentinel）和自动 分区（Cluster）提供高可用性（high availability）。

### 1、Redis自动配置
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

![](image/SpringBoot2/image-20220823174732.png)

自动配置：
- RedisAutoConfiguration 自动配置类 -> RedisProperties 属性类 -> spring.redis.xxx 配置文件前缀
- 连接工厂是准备好的。LettuceConnectionConfiguration、JedisConnectionConfiguration
- 自动注入了 `RedisTemplate<Object, Object>`，K, V
- 自动注入了 `StringRedisTemplate`，KV都是字符串
- 我们使用 StringRedisTemplate、RedisTemplate 即可操作redis

redis环境搭建
1. 阿里云按量付费redis、经典网络
2. 申请redis的公网连接地址
3. 修改白名单允许0.0.0.0/0 访问

### 2、RedisTemplate与Lettuce
```java
@Test
void testRedis() {
    ValueOperations<String, String> operations = redisTemplate.opsForValue();

    operations.set("hello", "world");

    String hello = operations.get("hello");
    System.out.println(hello);
}
```

> TIPS:
> Filter、Interceptor 几乎拥有相同的功能？
> * Filter是Servlet定义的原生组件。好处，脱离Spring应用也能使用
> * Interceptor是Spring定义的接口。可以使用Spring的自动装配等功能

### 3、切换至jedis
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<!--导入jedis-->
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

```yaml
spring:
  redis:
    host: r-bp1nc7reqesxisgxpipd.redis.rds.aliyuncs.com
    port: 6379
    password: lfy:Lfy123456

    client-type: jedis
    jedis:
      pool:
        max-active: 10
```



# 七、单元测试

## 1、JUnit5 的变化
Spring Boot 2.2.0 版本开始引入 JUnit 5 作为单元测试默认库

作为最新版本的JUnit框架，JUnit5与之前版本的Junit框架有很大的不同。由三个不同子项目的几个不同模块组成。

> JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage

JUnit Platform: Junit Platform是在JVM上启动测试框架的基础，不仅支持Junit自制的测试引擎，其他测试引擎也都可以接入。

JUnit Jupiter: JUnit Jupiter提供了JUnit5的新的编程模型，是JUnit5新特性的核心。内部 包含了一个测试引擎，用于在Junit Platform上运行。

JUnit Vintage: 由于JUint已经发展多年，为了照顾老的项目，JUnit Vintage提供了兼容JUnit4.x,Junit3.x的测试引擎。

![](image/SpringBoot2/afeae670-6be9-11e9-8b0d-d3a853e66b8e-20220823175419.png)

注意：
- SpringBoot 2.4 以上版本移除了默认对 Vintage 的依赖。如果需要兼容junit4需要自行引入（不能使用junit4的功能 @Test）
- JUnit 5’s Vintage Engine Removed from spring-boot-starter-test,如果需要继续兼容junit4需要自行引入vintage

```xml
<dependency>
    <groupId>org.junit.vintage</groupId>
    <artifactId>junit-vintage-engine</artifactId>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>org.hamcrest</groupId>
            <artifactId>hamcrest-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

### 使用JUnit
![](image/SpringBoot2/image-20220823175456.png)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

现在版本：
```java
@SpringBootTest
class Boot05WebAdminApplicationTests {
    @Test
    void contextLoads() {}
}
```

以前：
@SpringBootTest + @RunWith(SpringTest.class)

SpringBoot整合Junit以后。
- 编写测试方法：@Test标注（注意需要使用junit5版本的注解）
- Junit类具有Spring的功能，@Autowired、比如 @Transactional 标注测试方法，测试完成后自动回滚


## 2、JUnit5常用注解
[文档](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations)

JUnit5的注解与JUnit4的注解有所变化
- @Test :表示方法是测试方法。但是与JUnit4的@Test不同，他的职责非常单一不能声明任何属性，拓展的测试将会由Jupiter提供额外测试
- @ParameterizedTest :表示方法是参数化测试，下方会有详细介绍
- @RepeatedTest :表示方法可重复执行，下方会有详细介绍
- @DisplayName :为测试类或者测试方法设置展示名称
- @BeforeEach :表示在每个单元测试之前执行
- @AfterEach :表示在每个单元测试之后执行
- @BeforeAll :表示在所有单元测试之前执行
- @AfterAll :表示在所有单元测试之后执行
- @Tag :表示单元测试类别，类似于JUnit4中的@Categories
- @Disabled :表示测试类或测试方法不执行，类似于JUnit4中的@Ignore
- @Timeout :表示测试方法运行如果超过了指定时间将会返回错误
- @ExtendWith :为测试类或测试方法提供扩展类引用，类似于JUnit4中的RunWith

```java
import org.junit.jupiter.api.Test; //注意这里使用的是jupiter的Test注解！！

public class TestDemo {

    @Test
    @DisplayName("第一次测试")
    public void firstTest() {
        System.out.println("hello world");
    }
```


## 3、断言（assertions）
断言（assertions）是测试方法中的核心部分，用来对测试需要满足的条件进行验证。
这些断言方法都是 org.junit.jupiter.api.Assertions 的静态方法。
JUnit 5 内置的断言可以分成如下几个类别：
检查业务逻辑返回的数据是否合理。
所有的测试运行结束以后，会有一个详细的测试报告；

### 1、简单断言
用来对单个值进行简单的验证。如：
| 方法            | 说明                                 |
| --------------- | ------------------------------------ |
| assertEquals    | 判断两个对象或两个原始类型是否相等   |
| assertNotEquals | 判断两个对象或两个原始类型是否不相等 |
| assertSame      | 判断两个对象引用是否指向同一个对象   |
| assertNotSame   | 判断两个对象引用是否指向不同的对象   |
| assertTrue      | 判断给定的布尔值是否为 true          |
| assertFalse     | 判断给定的布尔值是否为 false         |
| assertNull      | 判断给定的对象引用是否为 null        |
| assertNotNull   | 判断给定的对象引用是否不为 null      |

```java
@Test
@DisplayName("simple assertion")
public void simple() {
    assertEquals(3, 1 + 2, "simple math");
    assertNotEquals(3, 1 + 1);

    assertNotSame(new Object(), new Object());
    Object obj = new Object();
    assertSame(obj, obj);

    assertFalse(1 > 2);
    assertTrue(1 < 2);

    assertNull(null);
    assertNotNull(new Object());
}
```

### 2、数组断言
通过 assertArrayEquals 方法来判断两个对象或原始类型的数组是否相等
```java
@Test
@DisplayName("array assertion")
public void array() {
    assertArrayEquals(new int[] { 1, 2 }, new int[] { 1, 2 });
}
```

### 3、组合断言
assertAll 方法接受多个 org.junit.jupiter.api.Executable 函数式接口的实例作为要验证的断言，可以通过 lambda 表达式很容易的提供这些断言
```java
@Test
@DisplayName("assert all")
public void all() {
    assertAll("Math",
            () -> assertEquals(2, 1 + 1),
            () -> assertTrue(1 > 0));
}
```

### 4、异常断言
在JUnit4时期，想要测试方法的异常情况时，需要用@Rule注解的ExpectedException变量还是比较麻烦的。而JUnit5提供了一种新的断言方式Assertions.assertThrows() ,配合函数式编程就可以进行使用。
```java
@Test
@DisplayName("异常测试")
public void exceptionTest() {
    ArithmeticException exception = Assertions.assertThrows(
            // 扔出断言异常
            ArithmeticException.class, () -> System.out.println(1 % 0));

}
```

### 5、超时断言
Junit5还提供了Assertions.assertTimeout() 为测试方法设置了超时时间
```java
@Test
@DisplayName("超时测试")
public void timeoutTest() {
    // 如果测试方法时间超过1s将会异常
    Assertions.assertTimeout(Duration.ofMillis(1000), () -> Thread.sleep(500));
}
```

### 6、快速失败
通过 fail 方法直接使得测试失败
```java
@Test
@DisplayName("fail")
public void shouldFail() {
    fail("This should fail");
}
```


## 4、前置条件（assumptions）
JUnit 5 中的前置条件（assumptions【假设】）类似于断言，不同之处在于不满足的断言会使得测试方法失败，而不满足的前置条件只会使得测试方法的执行终止。
前置条件可以看成是测试方法执行的前提，当该前提不满足时，就没有继续执行的必要。
```java
@DisplayName("前置条件")
public class AssumptionsTest {
    private final String environment = "DEV";

    @Test
    @DisplayName("simple")
    public void simpleAssume() {
        assumeTrue(Objects.equals(this.environment, "DEV"));
        assumeFalse(() -> Objects.equals(this.environment, "PROD"));
    }

    @Test
    @DisplayName("assume then do")
    public void assumeThenDo() {
        assumingThat(
                Objects.equals(this.environment, "DEV"),
                () -> System.out.println("In DEV"));
    }
}
```

assumeTrue 和 assumFalse 确保给定的条件为 true 或 false，不满足条件会使得测试执行终止。assumingThat 的参数是表示条件的布尔值和对应的 Executable 接口的实现对象。只有条件满足时，Executable 对象才会被执行；当条件不满足时，测试执行并不会终止。


## 5、嵌套测试
JUnit 5 可以通过 Java 中的内部类和@Nested 注解实现嵌套测试，从而可以更好的把相关的测试方法组织在一起。
在内部类中可以使用 @BeforeEach 和 @AfterEach 注解，而且嵌套的层次没有限制。
```java
@DisplayName("A stack")
class TestingAStackDemo {

    Stack<Object> stack;

    @Test
    @DisplayName("is instantiated with new Stack()")
    void isInstantiatedWithNew() {
        new Stack<>();
    }

    @Nested
    @DisplayName("when new")
    class WhenNew {

        @BeforeEach
        void createNewStack() {
            stack = new Stack<>();
        }

        @Test
        @DisplayName("is empty")
        void isEmpty() {
            assertTrue(stack.isEmpty());
        }

        @Test
        @DisplayName("throws EmptyStackException when popped")
        void throwsExceptionWhenPopped() {
            assertThrows(EmptyStackException.class, stack::pop);
        }

        @Test
        @DisplayName("throws EmptyStackException when peeked")
        void throwsExceptionWhenPeeked() {
            assertThrows(EmptyStackException.class, stack::peek);
        }

        @Nested
        @DisplayName("after pushing an element")
        class AfterPushing {

            String anElement = "an element";

            @BeforeEach
            void pushAnElement() {
                stack.push(anElement);
            }

            @Test
            @DisplayName("it is no longer empty")
            void isNotEmpty() {
                assertFalse(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when popped and is empty")
            void returnElementWhenPopped() {
                assertEquals(anElement, stack.pop());
                assertTrue(stack.isEmpty());
            }

            @Test
            @DisplayName("returns the element when peeked but remains not empty")
            void returnElementWhenPeeked() {
                assertEquals(anElement, stack.peek());
                assertFalse(stack.isEmpty());
            }
        }
    }
}
```


## 6、参数化测试
参数化测试是JUnit5很重要的一个新特性，它使得用不同的参数多次运行测试成为了可能，也为我们的单元测试带来许多便利。

利用@ValueSource等注解，指定入参，我们将可以使用不同的参数进行多次单元测试，而不需要每新增一个参数就新增一个单元测试，省去了很多冗余代码。

@ValueSource: 为参数化测试指定入参来源，支持八大基础类以及String类型,Class类型
@NullSource: 表示为参数化测试提供一个null的入参
@EnumSource: 表示为参数化测试提供一个枚举入参
@CsvFileSource：表示读取指定CSV文件内容作为参数化测试入参
@MethodSource：表示读取指定方法的返回值作为参数化测试入参(注意方法返回需要是一个流)

> 当然如果参数化测试仅仅只能做到指定普通的入参还达不到让我觉得惊艳的地步。
> 让我真正感到他的强大之处的地方在于他可以支持外部的各类入参。
> 如:CSV,YML,JSON 文件甚至方法的返回值也可以作为入参。
> 只需要去实现ArgumentsProvider接口，任何外部文件都可以作为它的入参。

```java
@ParameterizedTest
@ValueSource(strings = { "one", "two", "three" })
@DisplayName("参数化测试1")
public void parameterizedTest1(String string) {
    System.out.println(string);
    Assertions.assertTrue(StringUtils.isNotBlank(string));
}

@ParameterizedTest
@MethodSource("method") // 指定方法名
@DisplayName("方法来源参数")
public void testWithExplicitLocalMethodSource(String name) {
    System.out.println(name);
    Assertions.assertNotNull(name);
}

static Stream<String> method() {
    return Stream.of("apple", "banana");
}
```


## 7、迁移指南
在进行迁移的时候需要注意如下的变化：
- 注解在 org.junit.jupiter.api 包中，断言在 org.junit.jupiter.api.Assertions 类中，前置条件在 org.junit.jupiter.api.Assumptions 类中。
- 把@Before 和@After 替换成@BeforeEach 和@AfterEach。
- 把@BeforeClass 和@AfterClass 替换成@BeforeAll 和@AfterAll。
- 把@Ignore 替换成@Disabled。
- 把@Category 替换成@Tag。
- 把@RunWith、@Rule 和@ClassRule 替换成@ExtendWith。



# 八、指标监控

## 1、SpringBoot Actuator

### 1、简介
未来每一个微服务在云上部署以后，我们都需要对其进行监控、追踪、审计、控制等。SpringBoot就抽取了Actuator场景，使得我们每个微服务快速引用即可获得生产级别的应用监控、审计等功能。
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

![](image/SpringBoot2/image-20220823181253.png)

### 2、1.x与2.x的不同
![](image/SpringBoot2/image-20220823181359.png)

### 3、如何使用
- 引入场景
- 访问 http://localhost:8080/actuator/**
- 暴露所有监控信息为HTTP

```yaml
management:
  endpoints:
    enabled-by-default: true  #暴露所有端点信息
    web:
      exposure:
        include: '*'  #以web方式暴露
```

- 测试：http://localhost:8080/actuator/endpointName/detailPath
  - http://localhost:8080/actuator/beans
  - http://localhost:8080/actuator/configprops
  - http://localhost:8080/actuator/metrics
    - http://localhost:8080/actuator/metrics/jvm.gc.pause
    

### 4、可视化
https://github.com/codecentric/spring-boot-admin

#### 1、服务端
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>de.codecentric</groupId>
        <artifactId>spring-boot-admin-starter-server</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

主程序类加上注解：@EnableAdminServer

记得修改端口号：server.port

#### 2、客户端
```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.3.1</version>
</dependency>
```

spring.boot.admin.client.url=http://localhost:8888（这里要和服务器设置的server.port保持一致）
spring.boot.admin.client.url.instance.prefer-ip=true（使用ip注册，默认以主机名注册）
spring.application.name（给应用取个名字）


## 2、Actuator Endpoint

### 1、最常使用的端点
| ID               | 描述                                                                                                       |
| ---------------- | ---------------------------------------------------------------------------------------------------------- |
| auditevents      | 暴露当前应用程序的审核事件信息。需要一个AuditEventRepository组件。                                         |
| beans            | 显示应用程序中所有Spring Bean的完整列表。                                                                  |
| caches           | 暴露可用的缓存。                                                                                           |
| conditions       | 显示自动配置的所有条件信息，包括匹配或不匹配的原因。                                                       |
| configprops      | 显示所有@ConfigurationProperties。                                                                         |
| env              | 暴露Spring的属性ConfigurableEnvironment                                                                    |
| flyway           | 显示已应用的所有Flyway数据库迁移。<br/>需要一个或多个Flyway组件。                                          |
| health           | 显示应用程序运行状况信息。                                                                                 |
| httptrace        | 显示HTTP跟踪信息（默认情况下，最近100个HTTP请求-响应）。需要一个HttpTraceRepository组件。                  |
| info             | 显示应用程序信息。                                                                                         |
| integrationgraph | 显示Spring integrationgraph 。需要依赖spring-integration-core。                                            |
| loggers          | 显示和修改应用程序中日志的配置。                                                                           |
| liquibase        | 显示已应用的所有Liquibase数据库迁移。需要一个或多个Liquibase组件。                                         |
| metrics          | 显示当前应用程序的“指标”信息。                                                                             |
| mappings         | 显示所有@RequestMapping路径列表。                                                                          |
| scheduledtasks   | 显示应用程序中的计划任务。                                                                                 |
| sessions         | 允许从Spring Session支持的会话存储中检索和删除用户会话。需要使用Spring Session的基于Servlet的Web应用程序。 |
| shutdown         | 使应用程序正常关闭。默认禁用。                                                                             |
| startup          | 显示由ApplicationStartup收集的启动步骤数据。需要使用SpringApplication进行配置BufferingApplicationStartup。 |
| threaddump       | 执行线程转储。                                                                                             |

如果您的应用程序是Web应用程序（Spring MVC，Spring WebFlux或Jersey），则可以使用以下附加端点：
| ID         | 描述                                                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| heapdump   | 返回hprof堆转储文件。                                                                                                     |
| jolokia    | 通过HTTP暴露JMX bean（需要引入Jolokia，不适用于WebFlux）。需要引入依赖jolokia-core。                                      |
| logfile    | 返回日志文件的内容（如果已设置logging.file.name或logging.file.path属性）。支持使用HTTPRange标头来检索部分日志文件的内容。 |
| prometheus | 以Prometheus服务器可以抓取的格式公开指标。需要依赖micrometer-registry-prometheus。                                        |

最常用的Endpoint
- Health：监控状况
- Metrics：运行时指标
- Loggers：日志记录

### 2、Health Endpoint
健康检查端点，我们一般用于在云平台，平台会定时的检查应用的健康状况，我们就需要Health Endpoint可以为平台返回当前应用的一系列组件健康状况的集合。
重要的几点：
- health endpoint返回的结果，应该是一系列健康检查后的一个汇总报告
- 很多的健康检查默认已经自动配置好了，比如：数据库、redis等
- 可以很容易的添加自定义的健康检查机制

![](image/SpringBoot2/image-20220823181648.png)

### 3、Metrics Endpoint
提供详细的、层级的、空间指标信息，这些信息可以被pull（主动推送）或者push（被动获取）方式得到；
- 通过Metrics对接多种监控系统
- 简化核心Metrics开发
- 添加自定义Metrics或者扩展已有Metrics

![](image/SpringBoot2/image-20220823181710.png)

### 4、管理Endpoints

#### 1、开启与禁用Endpoints
- 默认所有的Endpoint除过shutdown都是开启的。
- 需要开启或者禁用某个Endpoint。配置模式为 `management.endpoint.<endpointName>.enabled = true`

```yaml
management:
  endpoint:
    beans:
      enabled: true
```

- 或者禁用所有的Endpoint然后手动开启指定的Endpoint

```yaml
management:
  endpoints:
    enabled-by-default: false
  endpoint:
    beans:
      enabled: true
    health:
      enabled: true
```

#### 2、暴露Endpoints
支持的暴露方式
- HTTP：默认只暴露health和info Endpoint
- JMX：默认暴露所有Endpoint（jconsole）
- 除过health和info，剩下的Endpoint都应该进行保护访问。
  - 如果引入SpringSecurity，则会默认配置安全访问规则

| ID               | JMX | Web |
| ---------------- | --- | --- |
| auditevents      | Yes | No  |
| beans            | Yes | No  |
| caches           | Yes | No  |
| conditions       | Yes | No  |
| configprops      | Yes | No  |
| env              | Yes | No  |
| flyway           | Yes | No  |
| health           | Yes | Yes |
| heapdump         | N/A | No  |
| httptrace        | Yes | No  |
| info             | Yes | Yes |
| integrationgraph | Yes | No  |
| jolokia          | N/A | No  |
| logfile          | N/A | No  |
| loggers          | Yes | No  |
| liquibase        | Yes | No  |
| metrics          | Yes | No  |
| mappings         | Yes | No  |
| prometheus       | N/A | No  |
| scheduledtasks   | Yes | No  |
| sessions         | Yes | No  |
| shutdown         | Yes | No  |
| startup          | Yes | No  |
| threaddump       | Yes | No  |


## 3、定制 Endpoint

### 1、定制 Health 信息
```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MyHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        int errorCode = check(); // perform some specific health check
        if (errorCode != 0) {
            return Health.down().withDetail("Error Code", errorCode).build();
        }
        return Health.up().build();

    }

}
```

```java
// 构建Health
Health build = Health.down()
        .withDetail("msg", "error service")
        .withDetail("code", "500")
        .withException(new RuntimeException())
        .build();
```

```yaml
management:
  health:
    enabled: true
    show-details: always #总是显示详细信息。可显示每个模块的状态信息
```

```java
@Component
public class MyComHealthIndicator extends AbstractHealthIndicator {

    /**
     * 真实的检查方法
     * 
     * @param builder
     * @throws Exception
     */
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        // mongodb。 获取连接进行测试
        Map<String, Object> map = new HashMap<>();
        // 检查完成
        if (1 == 2) {
            // builder.up(); //健康
            builder.status(Status.UP);
            map.put("count", 1);
            map.put("ms", 100);
        } else {
            // builder.down();
            builder.status(Status.OUT_OF_SERVICE);
            map.put("err", "连接超时");
            map.put("ms", 3000);
        }

        builder.withDetail("code", 100)
                .withDetails(map);

    }
}
```

### 2、定制info信息
常用两种方式

#### 1、编写配置文件
```yaml
info:
  appName: boot-admin
  version: 2.0.1
  mavenProjectName: @project.artifactId@  #使用@@可以获取maven的pom文件值
  mavenProjectVersion: @project.version@
```

#### 2、编写InfoContributor
```java
import java.util.Collections;

import org.springframework.boot.actuate.info.Info;
import org.springframework.boot.actuate.info.InfoContributor;
import org.springframework.stereotype.Component;

@Component
public class ExampleInfoContributor implements InfoContributor {

    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("example",
                Collections.singletonMap("key", "value"));
    }

}
```

http://localhost:8080/actuator/info 会输出以上方式返回的所有info信息

### 3、定制Metrics信息

#### 1、SpringBoot支持自动适配的Metrics
- JVM metrics, report utilization of:
  - Various memory and buffer pools
  - Statistics related to garbage collection
  - Threads utilization
  - Number of classes loaded/unloaded
- CPU metrics
- File descriptor metrics
- Kafka consumer and producer metrics
- Log4j2 metrics: record the number of events logged to Log4j2 at each level
- Logback metrics: record the number of events logged to Logback at each level
- Uptime metrics: report a gauge for uptime and a fixed gauge representing the application’s absolute start time
- Tomcat metrics (server.tomcat.mbeanregistry.enabled must be set to true for all Tomcat metrics to be registered)
- Spring Integration metrics

#### 2、增加定制Metrics
```java
class MyService {
    Counter counter;

    public MyService(MeterRegistry meterRegistry) {
        counter = meterRegistry.counter("myservice.method.running.counter");
    }

    public void hello() {
        counter.increment();
    }
}
```

```java
// 也可以使用下面的方式
@Bean
MeterBinder queueSize(Queue queue) {
    return (registry) -> Gauge.builder("queueSize", queue::size).register(registry);
}
```

### 4、定制Endpoint
```java
@Component
@Endpoint(id = "container")
public class DockerEndpoint {

    @ReadOperation
    public Map getDockerInfo() {
        return Collections.singletonMap("info", "docker started...");
    }

    @WriteOperation
    private void restartDocker() {
        System.out.println("docker restarted....");
    }

}
```

场景：开发ReadinessEndpoint来管理程序是否就绪，或者LivenessEndpoint来管理程序是否存活；

当然，这个也可以直接使用 https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-kubernetes-probes



# 九、原理解析

## 1、Profile功能
为了方便多环境适配，springboot简化了profile功能。

### 1、application-profile功能
- 默认配置文件 `application.yaml`：任何时候都会加载
- 环境配置文件 `application-{env}.yaml`
  - 默认配置与环境配置同时生效
  - 同名配置项，profile配置优先
- 激活指定环境
  - 配置文件激活：`spring.profiles.active=env`
  - 命令行激活：`java -jar xxx.jar --spring.profiles.active=env`
    - 修改配置文件的任意值，命令行优先 `java -jar xxx.jar --person.name=haha`

### 2、@Profile条件装配功能
```java
@Configuration(proxyBeanMethods = false)
@Profile("env")
public class ProductionConfiguration {
    // @Bean
}
```

### 3、profile分组
spring.profiles.group.production[0]=proddb
spring.profiles.group.production[1]=prodmq

使用：`--spring.profiles.active=production` 激活


## 2、外部化配置
https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config

1. Default properties (specified by setting SpringApplication.setDefaultProperties).
2. @PropertySource annotations on your @Configuration classes. Please note that such property sources are not added to the Environment until the application context is being refreshed. This is too late to configure certain properties such as logging.* and spring.main.* which are read before refresh begins.
3. Config data (such as application.properties files).【见：配置文件查找位置】
4. A RandomValuePropertySource that has properties only in random.*.
5. OS environment variables.
6. Java System properties (System.getProperties()).
7. JNDI attributes from java:comp/env.
8. ServletContext init parameters.
9. ServletConfig init parameters.
10. Properties from SPRING_APPLICATION_JSON (inline JSON embedded in an environment variable or system property).
11. Command line arguments.
12. properties attribute on your tests. Available on @SpringBootTest and the test annotations for testing a particular slice of your application.
13. @TestPropertySource annotations on your tests.
14. Devtools global settings properties in the $HOME/.config/spring-boot directory when devtools is active.

以上配置方式，后面的可以覆盖前面的同名配置项

### 1、外部配置源
常用：Java属性文件、YAML文件、环境变量、命令行参数；
`@Value("${属性名}")`

### 2、配置文件查找位置
1. classpath 根路径
2. classpath 根路径下的config目录
3. jar包所在目录
4. jar包所在目录的config目录
5. `/config`目录的直接子目录

同样，后面的可以覆盖前面的同名配置项

### 3、配置文件加载：
- 当前jar包内部的 `application.properties` 和 `application.yml`
- 当前jar包内部的 `application-{profile}.properties` 和 `application-{profile}.yml`
- 引用的外部jar包的 `application.properties` 和 `application.yml`
- 引用的外部jar包的 `application-{profile}.properties` 和 `application-{profile}.yml`


## 3、自定义starter

### 1、starter启动原理
- starter-pom引入 autoconfigure 包

![1661253403524](image/SpringBoot2/1661253403524.png)

- autoconfigure 包中配置使用 META-INF/spring.factories 中 EnableAutoConfiguration 的值，使得项目启动加载指定的自动配置类
- 编写自动配置类 XxxAutoConfiguration -> XxxProperties
  - @Configuration
  - @Conditional
  - @EnableConfigurationProperties
  - @Bean
  - ......

引入starter -> XxxAutoConfiguration -> 容器中放入组件 -> 绑定XxxProperties -> 配置项

### 2、自定义starter
atguigu-hello-spring-boot-starter（启动器）
atguigu-hello-spring-boot-starter-autoconfigure（自动配置包）


## 4、SpringBoot原理
Spring原理【Spring注解】、SpringMVC原理、自动配置原理、SpringBoot原理

### 1、SpringBoot启动过程
```java
SpringApplication.run(Boot09HelloTestApplication.class, args);
// ->
new SpringApplication(primarySources).run(args);
```

#### 创建 SpringApplication
```java
@SuppressWarnings({ "unchecked", "rawtypes" })
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
    this.resourceLoader = resourceLoader; // 保存一些信息
    Assert.notNull(primarySources, "PrimarySources must not be null");
    this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
    this.webApplicationType = WebApplicationType.deduceFromClasspath(); // 判定当前应用的类型：SERVLET
    // 初始启动引导器：List<Bootstrapper> bootstrappers;
    // getSpringFactoriesInstances(type)：去spring.factories找type
    this.bootstrappers = new ArrayList<>(getSpringFactoriesInstances(Bootstrapper.class));
    // 初始化器：List<ApplicationContextInitializer<?>> initializers;
    setInitializers((Collection) getSpringFactoriesInstances(ApplicationContextInitializer.class));
    // 应用监听器：List<ApplicationListener<?>> listeners;
    setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
    this.mainApplicationClass = deduceMainApplicationClass();
}
```

#### 运行 SpringApplication（SpringApplication::run）
```java
public ConfigurableApplicationContext run(String... args) {
    StopWatch stopWatch = new StopWatch();
    // 记录应用的启动时间
    stopWatch.start();
    // 创建引导上下文（Context环境）->
    DefaultBootstrapContext bootstrapContext = createBootstrapContext();
    ConfigurableApplicationContext context = null;
    // 让当前应用进入headless模式：java.awt.headless
    configureHeadlessProperty();
    // 获取所有 RunListener（运行监听器）【为了方便所有Listener进行事件感知】
    SpringApplicationRunListeners listeners = getRunListeners(args);
    // 遍历 SpringApplicationRunListener 调用 starting 方法，通知所有感兴趣系统正在启动过程的人，项目正在 starting
    listeners.starting(bootstrapContext, this.mainApplicationClass);
    try {
        // 保存命令行参数：ApplicationArguments
        ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
        // 准备环境->
        ConfigurableEnvironment environment = prepareEnvironment(listeners, bootstrapContext, applicationArguments);
        configureIgnoreBeanInfo(environment);
        Banner printedBanner = printBanner(environment);
        // ★创建IOC容器->
        context = createApplicationContext();
        context.setApplicationStartup(this.applicationStartup);
        // 准备ApplicationContext IOC容器的基本信息->
        prepareContext(bootstrapContext, context, environment, listeners, applicationArguments, printedBanner);
        // 刷新IOC容器（Spring核心）：创建容器中的所有组件
        refreshContext(context);
        // 容器刷新完成后
        afterRefresh(context, applicationArguments);
        stopWatch.stop();
        if (this.logStartupInfo) {
            new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
        }
        // 遍历监听器调用 started 方法：通知所有的监听器 started
        listeners.started(context);
        // 调用所有runners->
        callRunners(context, applicationArguments);
    }
    catch (Throwable ex) {
        // 如果以上有异常：listeners.failed(context, exception);
        handleRunFailure(context, ex, listeners);
        throw new IllegalStateException(ex);
    }

    try {
        // 遍历监听器调用 running 方法：通知所有的监听器 running
        listeners.running(context);
    }
    catch (Throwable ex) {
        // running如果有问题：listeners.failed(context, exception);
        handleRunFailure(context, ex, null);
        throw new IllegalStateException(ex);
    }
    return context;
}
```

```java
private DefaultBootstrapContext createBootstrapContext() {
    // 获取到所有之前的 bootstrappers
    DefaultBootstrapContext bootstrapContext = new DefaultBootstrapContext();
    // 依次执行 intitialize() 来完成对引导启动器上下文环境设置
    this.bootstrappers.forEach((initializer) -> initializer.intitialize(bootstrapContext));
    return bootstrapContext;
}
```

```java
private ConfigurableEnvironment prepareEnvironment(SpringApplicationRunListeners listeners,
        DefaultBootstrapContext bootstrapContext, ApplicationArguments applicationArguments) {
    // Create and configure the environment
    // 返回或者创建基础环境信息对象->
    ConfigurableEnvironment environment = getOrCreateEnvironment();
    // 读取所有的配置源的配置属性值，配置环境信息对象
    configureEnvironment(environment, applicationArguments.getSourceArgs());
    // 绑定环境信息
    ConfigurationPropertySources.attach(environment);
    // 监听器调用 environmentPrepared() 通知所有的监听器当前环境准备完成
    listeners.environmentPrepared(bootstrapContext, environment);
    DefaultPropertiesPropertySource.moveToEnd(environment);
    configureAdditionalProfiles(environment);
    bindToSpringApplication(environment);
    if (!this.isCustomEnvironment) {
        environment = new EnvironmentConverter(getClassLoader()).convertEnvironmentIfNecessary(environment,
                deduceEnvironmentClass());
    }
    ConfigurationPropertySources.attach(environment);
    return environment;
}

private ConfigurableEnvironment getOrCreateEnvironment() {
    if (this.environment != null) {
        return this.environment;
    }
    switch (this.webApplicationType) {
    case SERVLET:
        return new StandardServletEnvironment();
    case REACTIVE:
        return new StandardReactiveWebEnvironment();
    default:
        return new StandardEnvironment();
    }
}
```

```java
protected ConfigurableApplicationContext createApplicationContext() {
    return this.applicationContextFactory.create(this.webApplicationType);
}

// 位置：ApplicationContextFactory
ApplicationContextFactory DEFAULT = (webApplicationType) -> {
    try {
        // 根据项目类型（Servlet）创建容器
        switch (webApplicationType) {
        case SERVLET: // 示例
            return new AnnotationConfigServletWebServerApplicationContext();
        case REACTIVE:
            return new AnnotationConfigReactiveWebServerApplicationContext();
        default:
            return new AnnotationConfigApplicationContext();
        }
    }
    catch (Exception ex) {
        throw new IllegalStateException("Unable create a default ApplicationContext instance, "
                + "you may need a custom ApplicationContextFactory", ex);
    }
};
```

```java
private void prepareContext(DefaultBootstrapContext bootstrapContext, ConfigurableApplicationContext context,
        ConfigurableEnvironment environment, SpringApplicationRunListeners listeners,
        ApplicationArguments applicationArguments, Banner printedBanner) {
    context.setEnvironment(environment); // 保存环境信息
    postProcessApplicationContext(context); // IOC容器的后置处理流程
    applyInitializers(context); // 应用初始化器->
    // 所有的监听器调用 contextPrepared，通知所有的监听器 contextPrepared
    listeners.contextPrepared(context);
    bootstrapContext.close(context);
    if (this.logStartupInfo) {
        logStartupInfo(context.getParent() == null);
        logStartupProfileInfo(context);
    }
    // Add boot specific singleton beans
    ConfigurableListableBeanFactory beanFactory = context.getBeanFactory();
    beanFactory.registerSingleton("springApplicationArguments", applicationArguments);
    if (printedBanner != null) {
        beanFactory.registerSingleton("springBootBanner", printedBanner);
    }
    if (beanFactory instanceof DefaultListableBeanFactory) {
        ((DefaultListableBeanFactory) beanFactory)
                .setAllowBeanDefinitionOverriding(this.allowBeanDefinitionOverriding);
    }
    if (this.lazyInitialization) {
        context.addBeanFactoryPostProcessor(new LazyInitializationBeanFactoryPostProcessor());
    }
    // Load the sources
    Set<Object> sources = getAllSources();
    Assert.notEmpty(sources, "Sources must not be empty");
    load(context, sources.toArray(new Object[0]));
    // 所有的监听器调用 contextLoaded，通知所有的监听器 contextLoaded
    listeners.contextLoaded(context);
}

@SuppressWarnings({ "rawtypes", "unchecked" })
protected void applyInitializers(ConfigurableApplicationContext context) {
    // 遍历所有的初始化器调用初始化方法，来对IOC容器进行初始化扩展功能
    for (ApplicationContextInitializer initializer : getInitializers()) {
        Class<?> requiredType = GenericTypeResolver.resolveTypeArgument(initializer.getClass(),
                ApplicationContextInitializer.class);
        Assert.isInstanceOf(requiredType, context, "Unable to call initializer.");
        initializer.initialize(context);
    }
}
```

```java
private void callRunners(ApplicationContext context, ApplicationArguments args) {
    List<Object> runners = new ArrayList<>();
    // 获取容器中的 ApplicationRunner、CommandLineRunner
    runners.addAll(context.getBeansOfType(ApplicationRunner.class).values());
    runners.addAll(context.getBeansOfType(CommandLineRunner.class).values());
    // 合并所有runner并且按照@Order进行排序
    AnnotationAwareOrderComparator.sort(runners);
    // 遍历所有的runner，调用 run 方法
    for (Object runner : new LinkedHashSet<>(runners)) {
        if (runner instanceof ApplicationRunner) {
            callRunner((ApplicationRunner) runner, args);
        }
        if (runner instanceof CommandLineRunner) {
            callRunner((CommandLineRunner) runner, args);
        }
    }
}
```
![](image/SpringBoot2/image-20220823191918.png)
![](image/SpringBoot2/image-20220823191922.png)
![](image/SpringBoot2/image-20220823191926.png)

### 2、Application Events and Listeners
https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-application-events-and-listeners

自定义的以下实现：需要配置在 `META-INF/spring.factories`
```java
@FunctionalInterface
public interface ApplicationContextInitializer<C extends ConfigurableApplicationContext> {

	/**
	 * Initialize the given application context.
	 * @param applicationContext the application to configure
	 */
	void initialize(C applicationContext);

}
```

```java
@FunctionalInterface
public interface ApplicationListener<E extends ApplicationEvent> extends EventListener {

	/**
	 * Handle an application event.
	 * @param event the event to respond to
	 */
	void onApplicationEvent(E event);


	/**
	 * Create a new {@code ApplicationListener} for the given payload consumer.
	 * @param consumer the event payload consumer
	 * @param <T> the type of the event payload
	 * @return a corresponding {@code ApplicationListener} instance
	 * @since 5.3
	 * @see PayloadApplicationEvent
	 */
	static <T> ApplicationListener<PayloadApplicationEvent<T>> forPayload(Consumer<T> consumer) {
		return event -> consumer.accept(event.getPayload());
	}

}
```

```java
public interface SpringApplicationRunListener {

	/**
	 * Called immediately when the run method has first started. Can be used for very
	 * early initialization.
	 * @param bootstrapContext the bootstrap context
	 */
	default void starting(ConfigurableBootstrapContext bootstrapContext) {
		starting();
	}

	/**
	 * Called immediately when the run method has first started. Can be used for very
	 * early initialization.
	 * @deprecated since 2.4.0 in favor of {@link #starting(ConfigurableBootstrapContext)}
	 */
	@Deprecated
	default void starting() {
	}

	/**
	 * Called once the environment has been prepared, but before the
	 * {@link ApplicationContext} has been created.
	 * @param bootstrapContext the bootstrap context
	 * @param environment the environment
	 */
	default void environmentPrepared(ConfigurableBootstrapContext bootstrapContext,
			ConfigurableEnvironment environment) {
		environmentPrepared(environment);
	}

	/**
	 * Called once the environment has been prepared, but before the
	 * {@link ApplicationContext} has been created.
	 * @param environment the environment
	 * @deprecated since 2.4.0 in favor of
	 * {@link #environmentPrepared(ConfigurableBootstrapContext, ConfigurableEnvironment)}
	 */
	@Deprecated
	default void environmentPrepared(ConfigurableEnvironment environment) {
	}

	/**
	 * Called once the {@link ApplicationContext} has been created and prepared, but
	 * before sources have been loaded.
	 * @param context the application context
	 */
	default void contextPrepared(ConfigurableApplicationContext context) {
	}

	/**
	 * Called once the application context has been loaded but before it has been
	 * refreshed.
	 * @param context the application context
	 */
	default void contextLoaded(ConfigurableApplicationContext context) {
	}

	/**
	 * The context has been refreshed and the application has started but
	 * {@link CommandLineRunner CommandLineRunners} and {@link ApplicationRunner
	 * ApplicationRunners} have not been called.
	 * @param context the application context.
	 * @since 2.0.0
	 */
	default void started(ConfigurableApplicationContext context) {
	}

	/**
	 * Called immediately before the run method finishes, when the application context has
	 * been refreshed and all {@link CommandLineRunner CommandLineRunners} and
	 * {@link ApplicationRunner ApplicationRunners} have been called.
	 * @param context the application context.
	 * @since 2.0.0
	 */
	default void running(ConfigurableApplicationContext context) {
	}

	/**
	 * Called when a failure occurs when running the application.
	 * @param context the application context or {@code null} if a failure occurred before
	 * the context was created
	 * @param exception the failure
	 * @since 2.0.0
	 */
	default void failed(ConfigurableApplicationContext context, Throwable exception) {
	}

}
```

### 3、ApplicationRunner 与 CommandLineRunner
自定义的以下实现：需要加入IOC容器（使用@Component注解即可）
```java
@FunctionalInterface
public interface ApplicationRunner {

    /**
     * Callback used to run the bean.
     * 
     * @param args incoming application arguments
     * @throws Exception on error
     */
    void run(ApplicationArguments args) throws Exception;

}
```

```java
@FunctionalInterface
public interface CommandLineRunner {

    /**
     * Callback used to run the bean.
     * 
     * @param args incoming main method arguments
     * @throws Exception on error
     */
    void run(String... args) throws Exception;

}
```
