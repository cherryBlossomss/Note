# 一.spring Boot 入门

## 1.spring Boot 简介

> 简化spring应用开发的一个框架
>
> 整个spring技术栈的一个大集合
>
> J2EE开发的一站式解决方案

## 2.微服务

微服务:服务架构(服务微化)

一个应用应该是一些小型服务的集合，其通过Http协议的方式进行互通

单体应用：ALL IN ONE

微服务：每一个功能单元都是 可独立替换和独立升级的软件单元

[详细参照微服务文档](https://martinfowler.com/articles/microservices.html#MicroservicesAndSoa)

## 3.spring Boot Hello的编写

一个功能：

浏览器发送hello请求，服务器接受请求并处理，响应Hello World字符串

### 1、创建一个maven工程；（jar）

### 2、导入spring boot相关的依赖

```xml
   <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

### 3、编写一个主程序：启动Spring Boot应用

```xml
/**
 * @Author: cuzz
 * @Date: 2018/9/20 18:06
 * @Description: @SpringBootApplication 来标注一个主程序，说明这是一个SpringBoot应用
 */
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        
        // Spring应用启动起来
        SpringApplication.run(Application.class, args);
    }
}
```

### 4、编写相关的Controller、Service

```java
@Controller
public class HelloController {

    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

### 5、运行主程序测试

直接右键runapplication

## 5、Hello World探究

### 1、POM文件

#### 1、父项目

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.9.RELEASE</version>
</parent>
```

他的父项目:

```xml
 <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.0.5.RELEASE</version>
        <relativePath>../../spring-boot-dependencies</relativePath>
    </parent>
```

这是真正管理Spring Boot应用里面所依赖的版本

Spring Boot的版本仲裁中心；

```xml
  <properties>
        <activemq.version>5.15.6</activemq.version>
        <antlr2.version>2.7.7</antlr2.version>
        <appengine-sdk.version>1.9.64</appengine-sdk.version>
        <artemis.version>2.4.0</artemis.version>
        <aspectj.version>1.8.13</aspectj.version>
        <assertj.version>3.9.1</assertj.version>
        <atomikos.version>4.0.6</atomikos.version>
        <bitronix.version>2.1.4</bitronix.version>
        <build-helper-maven-plugin.version>3.0.0</build-helper-maven-plugin.version>
        <byte-buddy.version>1.7.11</byte-buddy.version>
        <caffeine.version>2.6.2</caffeine.version>
        <cassandra-driver.version>3.4.0</cassandra-driver.version>
        <classmate.version>1.3.4</classmate.version>
        <commons-codec.version>1.11</commons-codec.version>
        <commons-dbcp2.version>2.2.0</commons-dbcp2.version>
        <commons-lang3.version>3.7</commons-lang3.version>
        <commons-pool.version>1.6</commons-pool.version>
        <commons-pool2.version>2.5.0</commons-pool2.version>
        <couchbase-cache-client.version>2.1.0</couchbase-cache-client.version>
        <couchbase-client.version>2.5.9</couchbase-client.version>
        <derby.version>10.14.2.0</derby.version>
        <dom4j.version>1.6.1</dom4j.version>
        <dropwizard-metrics.version>3.2.6</dropwizard-metrics.version>
        <ehcache.version>2.10.5</ehcache.version>
        <ehcache3.version>3.5.2</ehcache3.version>
        <elasticsearch.version>5.6.11</elasticsearch.version>
        <embedded-mongo.version>2.0.3</embedded-mongo.version>
        <exec-maven-plugin.version>1.5.0</exec-maven-plugin.version>
        <flatten-maven-plugin.version>1.0.1</flatten-maven-plugin.version>
        <flyway.version>5.0.7</flyway.version>
        <freemarker.version>2.3.28</freemarker.version>
        <git-commit-id-plugin.version>2.2.5</git-commit-id-plugin.version>
        <glassfish-el.version>3.0.0</glassfish-el.version>
        <groovy.version>2.4.15</groovy.version>
        <gson.version>2.8.5</gson.version>
        <h2.version>1.4.197</h2.version>
        <hamcrest.version>1.3</hamcrest.version>
        <hazelcast.version>3.9.4</hazelcast.version>
        <hazelcast-hibernate5.version>1.2.3</hazelcast-hibernate5.version>
        <hibernate.version>5.2.17.Final</hibernate.version>
        <hibernate-jpa-2.1-api.version>1.0.2.Final</hibernate-jpa-2.1-api.version>
        <hibernate-validator.version>6.0.12.Final</hibernate-validator.version>
        <hikaricp.version>2.7.9</hikaricp.version>
        <hsqldb.version>2.4.1</hsqldb.version>
        <htmlunit.version>2.29</htmlunit.version>
        <httpasyncclient.version>4.1.4</httpasyncclient.version>
        <httpclient.version>4.5.6</httpclient.version>
        <httpcore.version>4.4.10</httpcore.version>
        <infinispan.version>9.1.7.Final</infinispan.version>
        <influxdb-java.version>2.9</influxdb-java.version>
        <jackson.version>2.9.6</jackson.version>
        <janino.version>3.0.9</janino.version>
        <javax-annotation.version>1.3.2</javax-annotation.version>
        <javax-cache.version>1.1.0</javax-cache.version>
        <javax-jaxb.version>2.3.0</javax-jaxb.version>
        <javax-jms.version>2.0.1</javax-jms.version>
        <javax-json.version>1.1.2</javax-json.version>
        <javax-jsonb.version>1.0</javax-jsonb.version>
        <javax-mail.version>1.6.2</javax-mail.version>
        <javax-money.version>1.0.3</javax-money.version>
        <javax-transaction.version>1.2</javax-transaction.version>
        <javax-validation.version>2.0.1.Final</javax-validation.version>
        <jaxen.version>1.1.6</jaxen.version>
        <jaybird.version>3.0.5</jaybird.version>
        <jboss-logging.version>3.3.2.Final</jboss-logging.version>
        <jboss-transaction-spi.version>7.6.0.Final</jboss-transaction-spi.version>
        <jdom2.version>2.0.6</jdom2.version>
        <jedis.version>2.9.0</jedis.version>
        <jersey.version>2.26</jersey.version>
        <jest.version>5.3.4</jest.version>
        <jetty.version>9.4.12.v20180830</jetty.version>
        <jetty-el.version>8.5.33</jetty-el.version>
        <jetty-jsp.version>2.2.0.v201112011158</jetty-jsp.version>
        <jmustache.version>1.14</jmustache.version>
        <jna.version>4.5.2</jna.version>
        <joda-time.version>2.9.9</joda-time.version>
        <johnzon-jsonb.version>1.1.9</johnzon-jsonb.version>
        <jolokia.version>1.5.0</jolokia.version>
        <jooq.version>3.10.8</jooq.version>
        <jsonassert.version>1.5.0</jsonassert.version>
        <json-path.version>2.4.0</json-path.version>
        <jstl.version>1.2</jstl.version>
        <jtds.version>1.3.1</jtds.version>
        <junit.version>4.12</junit.version>
        <junit-jupiter.version>5.1.1</junit-jupiter.version>
        <junit-platform.version>1.1.0</junit-platform.version>
        <kafka.version>1.0.2</kafka.version>
        <kotlin.version>1.2.51</kotlin.version>
        <lettuce.version>5.0.5.RELEASE</lettuce.version>
        <liquibase.version>3.5.5</liquibase.version>
        <log4j2.version>2.10.0</log4j2.version>
        <logback.version>1.2.3</logback.version>
        <lombok.version>1.16.22</lombok.version>
        <mariadb.version>2.2.6</mariadb.version>
        <maven-antrun-plugin.version>1.8</maven-antrun-plugin.version>
        <maven-assembly-plugin.version>3.1.0</maven-assembly-plugin.version>
        <maven-clean-plugin.version>3.0.0</maven-clean-plugin.version>
        <maven-compiler-plugin.version>3.7.0</maven-compiler-plugin.version>
        <maven-dependency-plugin.version>3.0.2</maven-dependency-plugin.version>
        <maven-deploy-plugin.version>2.8.2</maven-deploy-plugin.version>
        <maven-eclipse-plugin.version>2.10</maven-eclipse-plugin.version>
        <maven-enforcer-plugin.version>3.0.0-M2</maven-enforcer-plugin.version>
        <maven-failsafe-plugin.version>2.21.0</maven-failsafe-plugin.version>
        <maven-help-plugin.version>2.2</maven-help-plugin.version>
        <maven-install-plugin.version>2.5.2</maven-install-plugin.version>
        <maven-invoker-plugin.version>3.1.0</maven-invoker-plugin.version>
        <maven-jar-plugin.version>3.0.2</maven-jar-plugin.version>
        <maven-javadoc-plugin.version>3.0.1</maven-javadoc-plugin.version>
        <maven-resources-plugin.version>3.0.2</maven-resources-plugin.version>
        <maven-shade-plugin.version>2.4.3</maven-shade-plugin.version>
        <maven-site-plugin.version>3.6</maven-site-plugin.version>
        <maven-source-plugin.version>3.0.1</maven-source-plugin.version>
        <maven-surefire-plugin.version>2.21.0</maven-surefire-plugin.version>
        <maven-war-plugin.version>3.1.0</maven-war-plugin.version>
        <micrometer.version>1.0.6</micrometer.version>
        <mockito.version>2.15.0</mockito.version>
        <mongodb.version>3.6.4</mongodb.version>
        <mongo-driver-reactivestreams.version>1.7.1</mongo-driver-reactivestreams.version>
        <mssql-jdbc.version>6.2.2.jre8</mssql-jdbc.version>
        <mysql.version>5.1.47</mysql.version>
        <narayana.version>5.8.2.Final</narayana.version>
        <nekohtml.version>1.9.22</nekohtml.version>
        <neo4j-ogm.version>3.1.2</neo4j-ogm.version>
        <netty.version>4.1.29.Final</netty.version>
        <nio-multipart-parser.version>1.1.0</nio-multipart-parser.version>
        <postgresql.version>42.2.5</postgresql.version>
        <quartz.version>2.3.0</quartz.version>
        <querydsl.version>4.1.4</querydsl.version>
        <rabbit-amqp-client.version>5.4.1</rabbit-amqp-client.version>
        <reactive-streams.version>1.0.2</reactive-streams.version>
        <reactor-bom.version>Bismuth-SR11</reactor-bom.version>
        <rest-assured.version>3.0.7</rest-assured.version>
        <rxjava.version>1.3.8</rxjava.version>
        <rxjava2.version>2.1.17</rxjava2.version>
        <rxjava-adapter.version>1.2.1</rxjava-adapter.version>
        <selenium.version>3.9.1</selenium.version>
        <selenium-htmlunit.version>2.29.3</selenium-htmlunit.version>
        <sendgrid.version>4.1.2</sendgrid.version>
        <servlet-api.version>3.1.0</servlet-api.version>
        <simple-json.version>1.1.1</simple-json.version>
        <slf4j.version>1.7.25</slf4j.version>
        <snakeyaml.version>1.19</snakeyaml.version>
        <solr.version>6.6.5</solr.version>
        <spring.version>5.0.9.RELEASE</spring.version>
        <spring-amqp.version>2.0.6.RELEASE</spring-amqp.version>
        <spring-batch.version>4.0.1.RELEASE</spring-batch.version>
        <spring-cloud-connectors.version>2.0.3.RELEASE</spring-cloud-connectors.version>
        <spring-data-releasetrain.version>Kay-SR10</spring-data-releasetrain.version>
        <spring-hateoas.version>0.25.0.RELEASE</spring-hateoas.version>
        <spring-integration.version>5.0.8.RELEASE</spring-integration.version>
        <spring-kafka.version>2.1.10.RELEASE</spring-kafka.version>
        <spring-ldap.version>2.3.2.RELEASE</spring-ldap.version>
        <spring-plugin.version>1.2.0.RELEASE</spring-plugin.version>
        <spring-restdocs.version>2.0.2.RELEASE</spring-restdocs.version>
        <spring-retry.version>1.2.2.RELEASE</spring-retry.version>
        <spring-security.version>5.0.8.RELEASE</spring-security.version>
        <spring-session-bom.version>Apple-SR5</spring-session-bom.version>
        <spring-ws.version>3.0.3.RELEASE</spring-ws.version>
        <sqlite-jdbc.version>3.21.0.1</sqlite-jdbc.version>
        <statsd-client.version>3.1.0</statsd-client.version>
        <sun-mail.version>1.6.2</sun-mail.version>
        <thymeleaf.version>3.0.9.RELEASE</thymeleaf.version>
        <thymeleaf-extras-data-attribute.version>2.0.1</thymeleaf-extras-data-attribute.version>
        <thymeleaf-extras-java8time.version>3.0.1.RELEASE</thymeleaf-extras-java8time.version>
        <thymeleaf-extras-springsecurity4.version>3.0.2.RELEASE</thymeleaf-extras-springsecurity4.version>
        <thymeleaf-layout-dialect.version>2.3.0</thymeleaf-layout-dialect.version>
        <tomcat.version>8.5.34</tomcat.version>
        <unboundid-ldapsdk.version>4.0.7</unboundid-ldapsdk.version>
        <undertow.version>1.4.25.Final</undertow.version>
        <versions-maven-plugin.version>2.3</versions-maven-plugin.version>
        <webjars-hal-browser.version>3325375</webjars-hal-browser.version>
        <webjars-locator-core.version>0.35</webjars-locator-core.version>
        <wsdl4j.version>1.6.3</wsdl4j.version>
        <xml-apis.version>1.4.01</xml-apis.version>
        <xml-maven-plugin.version>1.0.2</xml-maven-plugin.version>
        <xmlunit2.version>2.5.1</xmlunit2.version>
    </properties>
```



以后我们导入依赖默认是不需要写版本；（没有在dependencies里面管理的依赖自然需要声明版本号）

#### 2、启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

spring-boot-starter-==web==

spring-boot-starter：spring-boot场景启动器

![](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1538013865871.png)

spring-boot-starter-web：Starter for building web, including RESTful, applications using Spring MVC. Uses Tomcat as the default embedded container

帮我们导入了web模块正常运行所依赖的组件； 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd" xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <modelVersion>4.0.0</modelVersion>
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starters</artifactId>
    <version>2.0.5.RELEASE</version>
  </parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  <version>2.0.5.RELEASE</version>
  <name>Spring Boot Web Starter</name>
  <description>Starter for building web, including RESTful, applications using Spring
		MVC. Uses Tomcat as the default embedded container</description>
  <url>https://projects.spring.io/spring-boot/#/spring-boot-parent/spring-boot-starters/spring-boot-starter-web</url>
  <organization>
    <name>Pivotal Software, Inc.</name>
    <url>https://spring.io</url>
  </organization>
  <licenses>
    <license>
      <name>Apache License, Version 2.0</name>
      <url>http://www.apache.org/licenses/LICENSE-2.0</url>
    </license>
  </licenses>
  <developers>
    <developer>
      <name>Pivotal</name>
      <email>info@pivotal.io</email>
      <organization>Pivotal Software, Inc.</organization>
      <organizationUrl>http://www.spring.io</organizationUrl>
    </developer>
  </developers>
  <scm>
    <connection>scm:git:git://github.com/spring-projects/spring-boot.git/spring-boot-starters/spring-boot-starter-web</connection>
    <developerConnection>scm:git:ssh://git@github.com/spring-projects/spring-boot.git/spring-boot-starters/spring-boot-starter-web</developerConnection>
    <url>http://github.com/spring-projects/spring-boot/spring-boot-starters/spring-boot-starter-web</url>
  </scm>
  <issueManagement>
    <system>Github</system>
    <url>https://github.com/spring-projects/spring-boot/issues</url>
  </issueManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.0.5.RELEASE</version>
      <scope>compile</scope>
    </dependency>
      <!---支持jason-->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-json</artifactId>
      <version>2.0.5.RELEASE</version>
      <scope>compile</scope>
    </dependency>
      <!--Tomcat-->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.0.5.RELEASE</version>
      <scope>compile</scope>
    </dependency>
      <!--hibernate参数校验
       @NotBlank(message="用户名不能为空")
       private String userName;
      -->
    <dependency>
      <groupId>org.hibernate.validator</groupId>
      <artifactId>hibernate-validator</artifactId>
      <version>6.0.12.Final</version>
      <scope>compile</scope>
    </dependency>
      <!--web-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.0.9.RELEASE</version>
      <scope>compile</scope>
    </dependency>
      <!--webmvc-->
      <!--webmvc主要是对mvc的支持，包括restful协议
      web则对远程调用和远程服务的支持。-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.0.9.RELEASE</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
</project>

```

Spring Boot将所有的功能场景都抽取出来，做成一个个的starters（启动器），只需要在项目里面引入这些starter相关场景的所有依赖都会导入进来，要用什么功能就导入什么场景的启动器 

### 2.主程序类，主入口类

```java
/**
 * @Author: luohuiqi
 * @Date: 2018/9/27 
 * @Description: @SpringBootApplication 来标注一个主程序，说明这是一个SpringBoot应用
 */
@SpringBootApplication
public class Application {

    public static void main(String[] args) {

        // Spring应用启动起来
        SpringApplication.run(Application.class, args);
    }
}
```

@**SpringBootApplication** : Spring Boot应用标注在某个类上说明这个类是SpringBoot的主配置类，SpringBoot就应该运行这个类的main方法来启动SpringBoot应用； 

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
```

* @**SpringBootConfiguration** : Spring Boot的配置类，标注在某个类上，表示这是一个Spring Boot的配置类 

  ​            @**Configuration** : 配置类上来标注这个注解，配置类也是容器中的一个组件==>@Component

* @**EnableAutoConfiguration**：开启自动配置功能

  以前我们需要配置的东西，Spring Boot帮我们自动配置；   @**EnableAutoConfiguration**告诉SpringBoot开启自动配置功能；这样自动配置才能生效；

  ```java
  @AutoConfigurationPackage
  @Import(AutoConfigurationImportSelector.class)
  public @interface EnableAutoConfiguration {
  ```

  * @**AutoConfigurationPackage**：自动配置包

    ```java
    @Import(AutoConfigurationPackages.Registrar.class)
    public @interface AutoConfigurationPackage {
    ```

    ![](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1538015991364.png)

     将主配置类（@SpringBootApplication标注的类）的所在包及下面所有子包里面的所有组件扫描到Spring容器；

    * @Import(AutoConfigurationImportSelector.class) ，给容器中导入组件

       将所有需要导入的组件以全类名的方式返回，这些组件就会被添加到容器中； 会给容器中导入非常多的自动   配置类（xxxAutoConfiguration），就是给容器中导入这个场景需要的所有组件，并配置好这些组件；

      * 有了自动配置类，免去了我们手动编写配置注入功能组件等的工作；

      * 调用了`SpringFactoriesLoader.loadFactoryNames(EnableAutoConfiguration.class,classLoader)`；

      * Spring Boot在启动的时候从类路径下的META-INF/spring.factories中获取EnableAutoConfiguration指定的值，将这些值作为自动配置类导入到容器中，自动配置类就生效，帮我们进行自动配置工作；

        ![](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1538016723154.png)

      * 以前我们需要自己配置的东西，自动配置类都帮我们；

      * J2EE的整体整合解决方案和自动配置都在`spring-boot-autoconfigure-1.5.9.RELEASE.jar`；

# 二.配置文件

## 1.配置文件

* application.properties
* application.yml

配置文件的作用：修改SpringBoot自动配置的默认值；SpringBoot在底层都给我们自动配置好；

标记语言：

​	以前的配置文件；大多都使用的是 **xxx.xml**文件；

​	YAML：**以数据为中心**，比json、xml等更适合做配置文件；

​	YAML：

```yml
server:
  port: 8081
```

​         xml:

       ```xml
<server>
	<port>8081</port>
</server>
       ```

## 2.YMAL语法

###   1.基本语法

 k:(空格)v：表示一对键值对（空格必须有）；

  以**空格**的缩进来控制层级关系；只要是左对齐的一列数据，都是同一个层级的

  属性和值也是大小写敏感；

```yaml
server:
    port: 8081
    path: /hello
```

### 2、值的写法

#### 字面量：普通的值（数字，字符串，布尔）

​	k: v：字面直接来写；

​	字符串默认不用加上单引号或者双引号；

​	""：双引号；不会转义字符串里面的特殊字符；特殊字符会作为本身想表示的意思

​	name: "zhangsan \n lisi"：输出；zhangsan 换行 lisi

​	''：单引号；会转义特殊字符，特殊字符最终只是一个普通的字符串数据

​	name: ‘zhangsan \n lisi’：输出；zhangsan \n lisi

#### 对象、Map（属性和值）（键值对）：

​	k: v：在下一行来写对象的属性和值的关系；注意缩进

​	对象还是k: v的方式

```yml
friends:
	lastName: zhangsan
	age: 20
```

行内写法：

```yml
friends: {lastName: zhangsan, age: 18}
```

#### 数组（List、Set）：

用 - 值表示数组中的一个元素

```yml
pets:
 - cat
 - dog
 - pig
```

行内写法

```yml
pets: [cat, dog, pig]
```

## 3.配置文件注入

配置文件

```yml
person:
    lastName: hello
    age: 18
    boss: false
    birth: 2017/12/12
    maps: {k1: v1, k2: 12}
    lists:
      - lisi
      - zhaoliu
    dog:
      name: 小狗
      age: 12
```















































