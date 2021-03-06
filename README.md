# 2017 IT Race with Dubbo Startup

基于 `[spring-boot-starter-dubbo](https://github.com/teaey/spring-boot-starter-dubbo)` 准备的 Dubbo 开发框架。

## 初始化 IDE 配置
``` shell
$ mvn eclipse:eclipse  # or
$ mvn idea:idea
```

## 调试和运行
工程采用了Spring Boot 搭建。使运行这个工程变得非常简单。
``` shell
$ cd itrace_startup
$ mvn spring-boot:run
```

## 工程打包
Spring Boot 工程集成了快速打包工程的方式。
``` shell
$ cd itrace_startup
$ mvn package
```
打包完成后生成 `./tartget/itrace_startup-0.0.1-SNAPSHOT.jar` 文件。

## 部署和运行
搭建web 工程，一般需要web容器来运行（tomcat、jetty等）。采用Spring Boot 方式，工程里面自动集成了内嵌的 web 容器，因此不需要先部署tomcat、weblogic等来运行服务。
``` shell
$ java -jar itrace_startup-0.0.1-SNAPSHOT.jar
```

## 执行读取和写入文件
文件读写和分析，参考代码：`Section01Bootstrap.java`。

文件读取是从 `classpath` 读取的，相关代码如下：
``` java
InputStream in = Section01Bootstrap.class.getClassLoader().getResourceAsStream("service.txt");
BufferedReader br = new BufferedReader(new InputStreamReader(in));
String line;
while ((line = br.readLine()) != null) {
    ...
}
```

执行工程打包后，需要在运行时将文件的路径加入到 classpath 上：
``` shell
$ java -jar -cp=.:./files/* itrace_startup-0.0.1-SNAPSHOT.jar
```

## 集成 JPA
`spring-boot-starter-data-jpa` 是非常轻量级的 ORM 框架。

只要创建实体（`Cust`、`CustGroup`）、创建接口（`CustRepository`、`CustGroupRepository`）即可完成对数据库表到对象的 ORM 访问。

具体参考：`CustController` -> `CustRepository` -> `Cust`。

### 启动时报错
需要在 `application.properties` 文件指定的数据库实例上创建 `itrace_startup` 数据库。

### 参考材料
- [Spring Boot中使用Spring-data-jpa让数据访问更简单、更优雅](http://www.jianshu.com/p/38d27b633d9c)
- [spring-boot/spring-boot-samples/spring-boot-sample-data-jpa - GitHub](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-data-jpa)

## to-do
- [X] 实现选拔赛题目一
- [X] 实现选拔赛题目二
- [X] 集成文件读取和写入（从 classpth）
- [X] 集成简单的web/http 功能
- [X] 集成轻量级的ORM 框架（JPA）
- [ ] 集成 Dubbo