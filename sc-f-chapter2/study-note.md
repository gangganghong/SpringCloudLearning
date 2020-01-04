## demo操作

1.访问 http://localhost:8764/hello?name=cg 并刷新，
浏览器会出现下面的结果

    hi cg ,i am from port:8763
    hi cg ,i am from port:8762
    hi cg ,i am from port:8765
    
2.运行时 Run Dashboard 如下：

1-1.png

3.服务名称大小写不敏感，下面二者都行

    public String hiService(String name) {
    return restTemplate.getForObject("http://sERVICE-HI/hi?name="+name,String.class);
    }
    
    public String hiService(String name) {
        return restTemplate.getForObject("http://SERVICE-HI/hi?name="+name,String.class);
    }
    
4.新建服务后，需要重启 ServiceRibbonApplication

5.idea 修改 应用 端口后，创建多个实例，见图：

1-2.png
1-3.png
