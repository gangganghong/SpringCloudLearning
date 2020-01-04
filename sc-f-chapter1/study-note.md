## 问题

1.pom.xml 文件中 spring-cloud-starter-netflix-eureka-server:<unknown> not found 

解决：加版本号，如下，

    <!-- https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-server -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        <version>2.1.0.RELEASE</version>
    </dependency>

引申知识点

Maven库

https://mvnrepository.com/search?q=Spring+Cloud+Starter+Netflix+Eureka+Server

上面可以找到要使用的依赖。

## demo操作

1.IDEA会出现Run Dashborad的面板

1-1.png

2.点击面板中的项目，分别进入项目代码，点击启动按钮

1-2.png

3.访问 http://localhost:8761/

emergency! eureka may be incorrectly claiming instances are up when they're not. renewals are lesser than threshold and hence the instances are not being expired just to be safe.

1-3.png

不理解这个知识点，后续再读资料

https://www.cnblogs.com/breath-taking/articles/7940364.html

### 创建一个服务提供者 (eureka client)

1.直接使用idea创建，过程如图 c1/1-8.png --- c1/1-11.png

2.在新建的module中做如下修改

service-cart/pom.xml 增加

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>5.2.2.RELEASE</version>
    </dependency>
    
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
com/forezp/cart/CartApplication.java 增加

    @EnableEurekaClient
    @RestController // 非必须
    
    // 非必须
    @GetMapping(value = "cart")
    public String home(){
        return "I'm cart.";
    }
    
3.服务启动后的效果

1-12.png

## 注释

1./Users/cg/data/code/springboot-study/SpringCloudLearning/sc-f-chapter1/service-hi/src/main/resources/application.yml 

中的 defaultZone 必须是 http://localhost:8761/eureka/，不能是 : http://localhost:8761