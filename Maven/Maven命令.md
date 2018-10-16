# 一.Maven常用命令

### 1.创建Maven的普通java项目

mvn archetype:create -DgroupId=com.yida.framework -DartifactId=helloworld

### 2.创建Maven的Web项目

mvn archetype:create 
-DgroupId=packageName    
-DartifactId=webappName 
-DarchetypeArtifactId=maven-archetype-webapp  

  mvn archetype:create -DgroupId=struts2  -DartifactId=blogSystem -DarchetypeArtifactId=maven-archetype-webapp  

### 3.编译源代码： mvn compile 

第一次执行会下载各种插件、依赖包

### 4.编译测试代码：mvn test-compile    

### 5.运行测试：mvn test   

### 6.产生site：mvn site   

### 7.打包：mvn package   

  生成target目录，编译、测试代码，生成测试报告，生成jar/war文件 

### 8.在本地Repository中安装jar：mvn install 

​    maven的install可以将项目本身编译并打包到本地仓库，这样其他项目引用本项目的jar包时不用去私服上下载jar包，直  接从本地就可以拿到刚刚编译打包好的项目的jar包，很灵活，避免每次都需要重新往私服发布jar包的痛苦；

![](D:\笔记\Maven\picture\20170802110727085 .jpg)

### 9.清除产生的项目：mvn clean   

​    清除target文件

### 10生成eclipse项目：mvn eclipse:eclipse 清除mvn eclipse:clean 

### 11.生成idea项目：mvn idea:idea 

### 12组合使用goal命令，如只打包不测试：mvn -Dtest package   

### 13.编译测试的内容：mvn test-compile 

### 14.只打jar包: mvn jar:jar 

### 15.只测试而不编译，也不测试编译：mvn test -skipping compile -skipping test-compile 

( -skipping 的灵活运用，当然也可以用于其他组合命令) 

### 16.清除eclipse的一些系统设置:mvn eclipse:clean 

# 二.容易混淆的概念

## 1.package

完成了项目编译、单元测试、打包功能，但没有把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库和远程maven私服仓库

## 2.install

命令完成了项目编译、单元测试、打包功能，同时把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库，但没有布署到远程maven私服仓库

## 3.deploy

命令完成了项目编译、单元测试、打包功能，同时把打好的可执行jar包（war包或其它形式的包）布署到本地maven仓库和远程maven私服仓库

ps： 

一般使用情况是这样，首先通过cvs或svn下载代码到本机，然后执行mvn eclipse:eclipse生成ecllipse项目文件，然后导入到eclipse就行了；修改代码后执行mvn compile或mvn test检验，也可以下载eclipse的maven插件(一般的Eclipse有没有集成)。 

mvn -version/-v 显示版本信息 
mvn archetype:generate        创建mvn项目 
mvn archetype:create -DgroupId=com.oreilly -DartifactId=my-app   创建mvn项目 

mvn jetty:run            运行项目于jetty上, 
mvn site                    生成项目相关信息的网站 
mvn -Dwtpversion=1.0 eclipse:eclipse        生成Wtp插件的Web项目 
mvn -Dwtpversion=1.0 eclipse:clean        清除Eclipse项目的配置信息(Web项目) 
mvn eclipse:eclipse                将项目转化为Eclipse项目 

在应用程序用使用多个存储库 

```xml
<repositories>    
    <repository>      
        <id>Ibiblio</id>      
        <name>Ibiblio</name>      
        <url>http://www.ibiblio.org/maven/</url>    
    </repository>    
    <repository>      
        <id>PlanetMirror</id>      
        <name>Planet Mirror</name>      
        <url>http://public.planetmirror.com/pub/maven/</url>    
    </repository> 
</repositories> 
```




mvn deploy:deploy-file -DgroupId=com -DartifactId=client -Dversion=0.1.0 -Dpackaging=jar -Dfile=d:\client-0.1.0.jar -DrepositoryId=maven-repository-inner -Durl=ftp://xxxxxxx/opt/maven/repository/ 


发布第三方Jar到本地库中： 

mvn install:install-file -DgroupId=com -DartifactId=client -Dversion=0.1.0 -Dpackaging=jar -Dfile=d:\client-0.1.0.jar 


-DdownloadSources=true 

-DdownloadJavadocs=true 

mvn -e            显示详细错误 信息. 

mvn validate        验证工程是否正确，所有需要的资源是否可用。 
mvn test-compile    编译项目测试代码。 。 
mvn integration-test     在集成测试可以运行的环境中处理和发布包。 
mvn verify        运行任何检查，验证包是否有效且达到质量标准。     
mvn generate-sources    产生应用需要的任何额外的源代码，如xdoclet。 

常用命令： 
mvn -v 显示版本 
mvn help:describe -Dplugin=help 使用 help 插件的 describe 目标来输出 Maven Help 插件的信息。 
mvn help:describe -Dplugin=help -Dfull 使用Help 插件输出完整的带有参数的目标列 
mvn help:describe -Dplugin=compiler -Dmojo=compile -Dfull 获取单个目标的信息,设置 mojo 参数和 plugin 参数。此命令列出了Compiler 插件的compile 目标的所有信息 
mvn help:describe -Dplugin=exec -Dfull 列出所有 Maven Exec 插件可用的目标 
mvn help:effective-pom 看这个“有效的 (effective)”POM，它暴露了 Maven的默认设置 

mvn archetype:create -DgroupId=org.sonatype.mavenbook.ch03 -DartifactId=simple -DpackageName=org.sonatype.mavenbook 创建Maven的普通java项目，在命令行使用Maven Archetype 插件 
mvn exec:java -Dexec.mainClass=org.sonatype.mavenbook.weather.Main Exec 插件让我们能够在不往 classpath 载入适当的依赖的情况下，运行这个程序 
mvn dependency:resolve 打印出已解决依赖的列表 
mvn dependency:tree 打印整个依赖树 

mvn install -X 想要查看完整的依赖踪迹，包含那些因为冲突或者其它原因而被拒绝引入的构件，打开 Maven 的调试标记运行 
mvn install -Dmaven.test.skip=true 给任何目标添加maven.test.skip 属性就能跳过测试 
mvn install assembly:assembly 构建装配Maven Assembly 插件是一个用来创建你应用程序特有分发包的插件 

mvn jetty:run 调用 Jetty 插件的 Run 目标在 Jetty Servlet 容器中启动 web 应用 
mvn compile 编译你的项目 
mvn clean install 删除再编译 

mvn hibernate3:hbm2ddl 使用 Hibernate3 插件构造数据库 

序号 快捷键 功能 
1 mvn artchetype:generate 使用交互式的方法建立工程，代替artchetype：create 
2 mvn compile 编译工程 
3 mvn clean 清理生成的文件， 一般与package install 等命令一起使用 
4 mvn test 测试src/main/test下的文件 
5 mvn package 将整个工程打包 
6 mvn install 将工程打包并部署到本地库中 
7 mvn help:effective-pom 实际的pom文件，显示所有的默认配置 
8 mvn help:effective-settings 运行时使用setting文件 
9 mvn eclipse:eclipse 生成eclipse工程文件 
10 mvn help:describe 显示某个插件（目标）的功能 
11 mvn jetty:run 启动jetty容器，可以在测试时代替tomcat 
12 mvn tomcat:run 启动tomcat容器 
13 mvnDebug tomcat:run 可以在eclipse中设置断点进行调试 
14 mvn dependency:analyze 查看工程所依赖的插件，进行pom优化时可以用到 
15 mvn dependency:sources 自动寻找并下载jar包的源码 
16 mvn dependency:resolved 查看已经解决的依赖 
17 mvn dependency:tree 查看依赖树，可以分析出间接依赖关系 
18 mvn exec:java 运行指定的应用 
19 mvn assembly:assembly 生成一个单独的可运行的jar包 



# 三.maven构建web project

##  1.方法一（快捷键）

  mvn archetype:create -DgroupId={groupId} -DartifactId={artifactId} -DarchetypeArtien-archetype-webapp -Dversion=1.0
   mvn eclipse:eclipse -Dwtpversion=2.0 
   说明：archetypeArtifactId（项目骨架的类型） 

* maven-archetype-archetype 
* maven-archetype-j2ee-simple 
* maven-archetype-mojo 
* maven-archetype-portlet 
* maven-archetype-profiles (currently under development) 
* maven-archetype-quickstart 
* maven-archetype-simple (currently under development) 
* maven-archetype-site 
* maven-archetype-site-simple 
* maven-archetype-webapp 

## 2.方法二（Eclipse）

还有一个方法，就是在pom中加入 

```xml
   <build>   
        <plugins>   
            <plugin>   
                <groupId>org.apache.maven.plugins</groupId>   
                <artifactId>maven-eclipse-plugin</artifactId> 
           <configuration>   
                    <wtpversion>2.0</wtpversion>   
                    <additionalProjectnatures>   
<projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>   
                    </additionalProjectnatures>   
                </configuration>  
            </plugin> 
        </plugins>   
    </build> 
```



然后执行mvn eclipse:eclipse,同样的效果 
最后mvn install发布下，就可以了。 不过注意是发布成war而不是jar

## 3.方法三(通过模板 )

mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes  -DgroupId=cn.everlook.myweb -DartifactId=myweb 

# 四.Maven的生命周期(clean -compile -site)

## 1.clean

​      包含三个步骤pre-clean执行一些需要在clean之前完成的工作,clean：移除所有上一次构建生成的文件,post-clean执  行一些需要在clean之后立刻完成的工作。

## 2.compile:

​              validate
​             generate-sources
​             process-sources
​             generate-resources
​              process-resources复制并处理源文件，至目标目录，准备打包。
​             compile编译项目的源代码。
​             process-classes
​             generate-test-sources
​             process-test-sources
​             generate-test-resources
​              process-test-resources复制并处理源文件，至目标测试目录
​              test-compile编译测试源代码
​              process-test-classes
​              test使用合适的单元测试框架运行测试。这些测试代码不会被打包或部署。
​              prepare-package
​              package接受编译好的代码，打包成可发布的格式，如JAR
​              pre-intergration-test
​              intergration-test
​              post-intergration-test
​              verify
​              install将包安装到本地仓库，以让其他项目依赖。
​              deploy将最终的包复制到远程仓库，以让其他开发人员与项目共享。
​              site

## 3.maven的配置中的<scope></scope>详解

   (1)scope的默认值是compile，指的是编译时依赖，即编译时就会将依赖包下载到maven仓库中(缺省值，适用于所有阶段，会随着项目一起发布)
   (2)test：只有在测试的时候会依赖这个包，即打包的时候不会将配置为test的junit包加进去。(只在测试时使用，用于编译和运行测试代码。不会随项目发布)
​        test项的包只对test源文件下的类起作用，如果将junit的代码放到src下，而junit配置为test将会出现找不到junit包的错误。
   (3)provided，类似compile，期望JDK、容器或使用者会提供这个依赖。如servlet.jar。
   (4)runtime，只在运行时使用，如JDBC驱动，适用运行和测试阶段。
   (5)system，类似provided，需要显式提供包含依赖的jar，Maven不会在Repository中查找它。



maven中的隐藏名称：
${basedir}:项目根目录
${project.build.directory}:构建目录，缺省为target
${project.build.outputDirectory}:构建过程输出目录，缺省为target/classess
${project.build.finalName}产出物名称，缺省为${project.artifactId}-${project.version}
${project.packaging}打包类型，缺省为jar
${project.xxx}当前pom文件的任意节点内容，例如：想得到groupId可以${project.groupId},得到项目版本号可以使用${project.version}