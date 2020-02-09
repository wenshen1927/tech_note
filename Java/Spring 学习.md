#Spring 学习

主要记录Spring框架的学习过程。

## 1、 Spring 简介

### 1.1 Spring 历史

诞生于2002年，成型与2003年，作者Rod Johnson。

目前已经到Spring 5.x 版本，支持 JDK8-11 及JavaEE8。

###1.2 Spring 的发展

主要关注 SpringBoot/SpringFramework/SpringCloud 这三个东西。

SpringFramework：

- 用于构建企业级应用的轻量级一站式解决方案
- 设计理念
  - 力争让选择无处不在
  - 保持向后兼容
  - 专注API设计
  - 追求严苛的代码质量

SpringBoot：

- 快
- 开箱即用
- 不用生成代码，没有XML配置
- 提供了很多非功能性的特性：比如监控，安全等都为程序员考虑了很多。可以更多的focus逻辑问题而不是这些问题。

SpringCloud：

- 简化分布式系统的开发
  - 配置管理
  - 服务注册与发现
  - 熔断
  - 服务追踪
  - ...

### 1.3 Spring5.X 技术趋势

ReleaseNote:

![image-20190511194929429](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190511194929429.png)

- 应该努力追上语言的变化，学习Java 8，Kotin获得了很多支持，说明这门语言还是有优势的，可以关注一下
- 异步的模型可能会慢慢流行，但是需要时间，我们可以开始关注这个技术
- 对一些工具的支持的改变，我们应该需要选择一些活跃的框架，而不是不再维护的框架，考虑使用人群，维护的活跃度等

SpringBoot和SpringCloud是必然趋势：

- 开箱即用(希望把非功能性的问题抽取出来，不做综合的考虑)
- 与生态圈的深度整合
- 注重运维
- Cloud Native的大方向
- 最佳时间不嫌多，固化到系统实现中才是王道
- …...

### 1.4 Hello Spring 

start.spring.io 可以帮助我们快速初始配置spring工程  (Get !)

记：第一次运行，出现了点问题，每次启动的时候无法打开==SpringBoot内置的Tomcat==.最后在pom文件中去掉了Actuator的依赖才解决，不知道是为什么，我猜是版本不兼容。

## 2、Spring 数据库

