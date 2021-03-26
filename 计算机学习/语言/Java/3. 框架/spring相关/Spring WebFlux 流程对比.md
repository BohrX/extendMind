https://www.jianshu.com/p/0ac921cf829e
笔记是学习了小马哥在慕课网的课程的《Spring Boot 2.0深度实践之核心技术篇》的内容结合自己的需要和理解做的笔记。

前言
在了解了WebFlux核心组件之后，我们就该了解相应的请求流程了，在之前就写过几篇关于 SpringMvc 请求的流程笔记，如果之前有过了解的并且自己debugger 过的小伙伴，相信了解 WebFlux 的执行流程会很快。

我们知道WebFlux支持两种请求模式

注解驱动
函数式端点
接下来我们会重点讲一下函数式端点请求的具体流程，注解驱动由于跟SpringMVC很像，所以大家只要看一下流程图，基本就可以了解了。

注解驱动组件请求处理流程
流程图
下面我们先来看一下具体流程图

![](../../../../.local/static/2020/9/3/webFluxl流程.webp)
我们可以对比SpringMVC的请求流程图对比来看


我们可以看到，处理流程基本一样，有以下主要的点不同

处理核心

WebFlux--DispatcherHandler
SpringMvc--DispatcherServlet
返回值处理器

WebFlux--HandlerResultHandler
SpringMvc--HandlerMethodReturnValueHandler
内容协商配置器

WebFlux--RequestedContentTypeResolverBuilder
SpringMvc--ContentNegotiationConfigurer
还有很多就不一一例举了，想知道核心组件对比结果的同学，可以看下图。注意很多图上的组件名称相同，但是包的位置是不同的，所以大家要注意区分，不要弄混了。

Web MVC VS. WebFlux 核心组件对比
p17.png
函数式端点请求处理流程
流程图
按照惯例，上流程图

p15.png
通过上图，我们可以看到，这个处理跟之前的注解驱动请求大有不同，但是请求的流程是万变不离其宗，只是组件有所变化。

作者：NealLemon
链接：https://www.jianshu.com/p/0ac921cf829e
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。