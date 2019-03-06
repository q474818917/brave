# brave-sample

关于zipkin的插件支持的示例在[这里](https://github.com/openzipkin/sleuth-webmvc-example),通过分支切换查看
```$xslt
spring-cloud-sleuth-core:默认传递的依赖，没有的则需要手动添加依赖
    brave-instumentation-spring-web
    brave-instumentation-spring-rabbit
    brave-instumentation-kafka-clients
    brave-instumentation-httpclient
    brave-instumentation-httpasyncclient
    brave-instumentation-spring-webmvc
    brave-instumentation-jms
```

+ dubbo：如果不加插件dubbo-rpc，则只有client端显示trace日志，trace无法到达server端

+ springmvc:
```$xslt
相关两个类：TraceWebClientAutoConfiguration(TracingClientHttpRequestInterceptor)，TraceWebMvcConfigurer(SpanCustomizingAsyncHandlerInterceptor)

因为包含的spring-cloud-cleuth-core中有TraceAutoConfiguration，对应着TracingConfiguration，所以不需要加入TracingConfiguration。

另外实现trace是SpanCustomizingAsyncHandlerInterceptor，在brave-instrumentation-spring-webmvc包中,由TraceWebMvcConfigurer这个加入
```

+ spring cloud：
```$xslt
spring-cloud-starter-sleuth是记录trace日志的，spring-cloud-starter-zipkin是上报zipkin
spring-cloud-starter-zipkin：包含spring-cloud-starter-sleuth 和 spring-cloud-starter-zipkin

日志记录：[testSleuthApp,2a4efa92083577f4,1235a5df007e63e4,false]:2a4efa92083577f4是traceId， 1235a5df007e63e4 是spanId
```

# spring中的一些类：
+ WebMvcConfigurer：spring boot提供，web的很多配置都可以写里面。例如：TraceWebMvcConfigurer中增加了一个拦截器
+ @Configuration：代替xml配置

