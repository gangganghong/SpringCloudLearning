## 问题

1.config-server 报错

Caused by: java.lang.IllegalStateException: You need to configure a uri for the git repository

原因是，application.properties 配置文件未生效，即未被使用。
根据IDEA的提示也能看出，配置文件未被使用。

在target的classes中也没有发现application.properties，而其他正常的项目target的对应文件夹都有配置文件。

解决方法，把 pom.xml 中的

    <groupId>com.forezp</groupId>
        <artifactId>config-server</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    
修改为

    <groupId>com.forezp</groupId>
        <artifactId>config-server</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>
    
2.增加了 ribbon module ，启动时，出现问题

To enable URLs as dynamic configuration sources, define System property archaius.configurationSource.additionalUrls or make config.properties available on classpath

解决

将正确的demo中的pom.xml复制了一份，问题解决。后续再对比二者的差异。

3.这时发现，在读取配置文件不再写ip地址，而是服务名，这时如果配置服务部署多份，通过负载均衡，从而高可用。

不能通过 Ribbon 和 Feign 实现，怎样实现服务的高可用？