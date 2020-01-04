## 问题

1.Caused by: java.lang.IllegalStateException: Failed to introspect Class [org.springframework.cloud.netflix.hystrix.HystrixCircuitBreakerAutoConfiguration] from ClassLoader [sun.misc.Launcher$AppClassLoader@18b4aac2]

除了这个问题，后面还遇到了很多问题，

@HystrixCommand 找不到

spring-cloud-starter-netflix-hystrix 2.0.0.RELEASE 找不到

后来，我改成了 spring-cloud-starter-netflix-hystrix 2.0.1.RELEASE，并且 File>Invalidate Caches/Restart 后解决问题

首先启动 ServiceRibbonApplication 的时候，出现错误 com.sun.jersey.api.client.ClientHandlerException: java.net.ConnectException: Connection refused (Connection refused) ，
但是从后面的运行效果来看，并没有影响。

## deom操作

### Ribbon熔断

1.访问：http://localhost:8764/hi?name=forezp

然后关闭 ServiceHiApplication，若正常，会看到 hi,forezp,sorry,error!

2.在 com.forezp.serviceribbon.service.HelloService 中设置熔断

    @HystrixCommand(fallbackMethod = "hiError")
    public String hiService(String name) {
        return restTemplate.getForObject("http://SERVICE-HI/hi?name="+name,String.class);
    }

    public String hiError(String name) {
        return "hi,"+name+",sorry,error!";
    }

### Feign中使用断路器

1.访问 http://localhost:8765/hi?name=forezp

2.关闭 ServiceHiApplication 后，断路器立即发挥了作用。

重启 ServiceHiApplication 后，并不能访问到 ServiceHiApplication 服务，需要重启 ServiceFeignApplication。

Ribbon也是如此。

有不需要重启的组件吗？