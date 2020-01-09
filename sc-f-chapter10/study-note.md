## demo操作

1.进入 eureka-server，执行下面的命令：

    mvn clean
    mvn package
    
2.启动 eureka-server 服务

    java -jar target/eureka-server-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer1
    java -jar target/eureka-server-0.0.1-SNAPSHOT.jar --spring.profiles.active=peer2
    
3.创建可执行的 service-hi jar，进入 service-hi 目录后，执行命令：

    mvn clean
    mvn package
    
4.启动 server-hi 服务

    java -jar target/service-hi-0.0.1-SNAPSHOT.jar
    
5. client只向8761注册，但是你打开8769，你也会发现，8769也有 client的注册信息。