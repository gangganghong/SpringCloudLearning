## demo操作

1.启动 Mac 电脑上的 rabbitmq

    #rabbitmq
    docker run -d --name myrabbit -p 15672:15672 -p 5672:5672 rabbitmq:latest
    #rabbitmq 的 web管理系统
    docker run -d --hostname localhost --name myrabbit-ad -p 8080:15672 rabbitmq:3-management
    
web管理系统访问地址：http://127.0.0.1:8080/

默认账号和密码都是 guest

2.本 demo 的理解

去代码仓库将foo的值改为“foo version 4”，即改变配置文件foo的值。如果是传统的做法，需要重启服务，才能达到配置文件的更新。此时，我们只需要
发送post请求：http://localhost:8881/actuator/bus-refresh。