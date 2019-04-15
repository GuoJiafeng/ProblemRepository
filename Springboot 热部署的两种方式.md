原文：https://www.cnblogs.com/a8457013/p/8065489.html             **未进行测试**

# [springboot 热部署的两种方式](https://www.cnblogs.com/a8457013/p/8065489.html)



问题的提出： 在编写代码的时候，你会发现我们只是简单把打印信息改变了，就需要重新部署，如果是这样的编码方式，那么我们估计一天下来就真的是打几个Hello World就下班了。那么如何解决热部署的问题呢？那就是springloaded

运行方法一

使用spring-boot:run                                                                             

**使用方式一**

**在pom.xml文件添加依赖包：**



```
                   <plugin>
                      <groupId>org.springframework.boot</groupId>
                      <artifactId>spring-boot-maven-plugin </artifactId>
                      <dependencies>  
                       <!--springloaded  hot deploy -->  
                       <dependency>  
                           <groupId>org.springframework</groupId>  
                           <artifactId>springloaded</artifactId>  
                           <version>1.2.4.RELEASE</version>
                       </dependency>  
                    </dependencies>  
                    <executions>  
                       <execution>  
                           <goals>  
                               <goal>repackage</goal>  
                           </goals>  
                           <configuration>  
                               <classifier>exec</classifier>  
                           </configuration>  
                       </execution>  
                       </executions>
                </plugin>
```



 

运行方法二

如果使用的run as – java application的话，那么还需要做一些处理。 把spring-loader-1.2.4.RELEASE.jar下载下来，放到项目的lib目录中，然后把IDEA的run参数里VM参数设置为： -javaagent:.\lib\springloaded-1.2.4.RELEASE.jar -noverify 然后启动就可以了，这样在run as的时候，也能进行热部署

springboot + devtools（热部署）

问题的提出： 通过使用springloaded进行热部署，但是些代码修改了，并不会进行热部署。

spring-boot-devtools

1、

spring-boot-devtools 是一个为开发者服务的一个模块，其中最重要的功能就是自动应用代码更改到最新的App上面去。原理是在发现代码有更改之后，重新启动应用，但是速度比手动停止后再启动还要更快，更快指的不是节省出来的手工操作的时间。

2、

其深层原理是使用了两个ClassLoader，一个Classloader加载那些不会改变的类（第三方Jar包），另一个ClassLoader加载会更改的类，称为 restart ClassLoader

3、

这样在有代码更改的时候，原来的restart ClassLoader 被丢弃，重新创建一个restart ClassLoader，由于需要加载的类相比较少，所以实现了较快的重启时间（5秒以内）。

**使用方法二：**

**1、添加依赖包：** 



```
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional><!-- optional=true,依赖不会传递，该项目依赖devtools；之后依赖myboot项目的项目如果想要使用devtools，需要重新引入 -->  
            <scope>true</scope>
</dependency>
```



 

2、**添加spring-boot-maven-plugin：**

 



```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>     <!--fork :  如果没有该项配置，肯呢个devtools不会起作用，即应用不会restart -->
            </configuration>
        </plugin>
    </plugins>
</build>
```



 

 

 

测试方法

修改类-->保存：应用会重启

修改配置文件-->保存：应用会重启

修改页面-->保存：应用会重启，页面会刷新（原理是将spring.thymeleaf.cache设为false）

 

**三、不能使用分析**

 

```
对应的spring-boot版本是否正确，这里使用的是1.4.1版本；
是否加入plugin以及属性<fork>true</fork>
Eclipse Project 是否开启了Build Automatically（我自己就在这里栽了坑，不知道为什么我的工具什么时候关闭了自动编译的功能）。
如果设置SpringApplication.setRegisterShutdownHook(false)，则自动重启将不起作用。
```

 