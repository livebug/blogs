---
title : 'Dapr 学习路线整理'
date : 2024-02-24T22:23:49+08:00
toc: true
tags: ['dapr']
categories: ['技术博客']
---

这篇文章为了整理dapr从接触到试错的一步步探索。

### 一、简单了解

Dapr 是一种可移植、事件驱动的运行时，使任何开发人员都可以轻松构建在云和边缘运行的弹性、无状态和有状态应用程序，并支持多种语言和开发框架。

![dapr 介绍图](https://docs.dapr.io/images/overview.png)

#### 1. 具体实现就是把API包装成构建块，dapr提供组件服务这些构建块，构建块就是最小单元，也提供切面支持

Dapr 将构建微服务应用程序的最佳实践编入**开放、独立的 API（称为构建块）**中。 

Dapr 的构建模块：
+ 使您能够使用您选择的语言和框架构建可移植应用程序。
+ 是完全独立的
+ 对您的应用程序中使用的数量没有限制

Dapr 与平台无关，这意味着您可以运行您的应用程序，在（1）本地、（2）在任何 Kubernetes 集群上、（3）在虚拟机或物理机上、（4）在 Dapr 集成的其他托管环境中。

Dapr 提供分布式系统构建块，供您以标准方式构建微服务应用程序并部署到任何环境。
这些构建块 API 中的每一个都是独立的，这意味着您可以在应用程序中使用任意数量的它们。

dapr提供的 分布式系统构建块 ：
<table ><thead ><tr ><th >Building Block<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >积木</font></font></font></th><th >Description<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >描述</font></font></font></th></tr></thead><tbody ><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/service-invocation/service-invocation-overview/" ><strong >Service-to-service invocation<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >服务到服务的调用</font></font></font></strong></a></td><td >Resilient service-to-service invocation enables method calls, including retries, on remote services, wherever they are located in the supported hosting environment.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >弹性服务到服务调用支持对远程服务进行方法调用（包括重试），无论它们位于受支持的托管环境中的任何位置。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/state-management/state-management-overview/" ><strong >State management<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >状态管理</font></font></font></strong></a></td><td >With state management for storing and querying key/value pairs, long-running, highly available, stateful services can be easily written alongside stateless services in your application. The state store is pluggable and examples include AWS DynamoDB, Azure Cosmos&nbsp;DB, Azure SQL Server, GCP Firebase, PostgreSQL or Redis, among others.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >通过用于存储和查询键/值对的状态管理，可以在应用程序中轻松地与无状态服务一起编写长期运行、高度可用的有状态服务。状态存储是可插入的，示例包括 AWS DynamoDB、Azure Cosmos DB、Azure SQL Server、GCP Firebase、PostgreSQL 或 Redis 等。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/pubsub/pubsub-overview/" ><strong >Publish and subscribe<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >发布和订阅</font></font></font></strong></a></td><td >Publishing events and subscribing to topics between services enables event-driven architectures to simplify horizontal scalability and make them resilient to failure. Dapr provides at-least-once message delivery guarantee, message TTL, consumer groups and other advance features.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >在服务之间发布事件和订阅主题使事件驱动的架构能够简化水平可扩展性并使其能够适应故障。 Dapr 提供至少一次消息传递保证、消息 TTL、消费者组和其他高级功能。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/bindings/bindings-overview/" ><strong >Resource bindings<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >资源绑定</font></font></font></strong></a></td><td >Resource bindings with triggers builds further on event-driven architectures for scale and resiliency by receiving and sending events to and from any external source such as databases, queues, file systems, etc.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >具有触发器的资源绑定进一步构建在事件驱动架构的基础上，通过从任何外部源（例如数据库、队列、文件系统等）接收和发送事件来实现规模和弹性。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/actors/actors-overview/" ><strong >Actors<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >演员</font></font></font></strong></a></td><td >A pattern for stateful and stateless objects that makes concurrency simple, with method and state encapsulation. Dapr provides many capabilities in its actor runtime, including concurrency, state, and life-cycle management for actor activation/deactivation, and timers and reminders to wake up actors.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >有状态和无状态对象的模式，通过方法和状态封装使并发变得简单。 Dapr 在其 Actor 运行时提供了许多功能，包括并发、状态和 Actor 激活/停用的生命周期管理，以及唤醒 Actor 的计时器和提醒。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/secrets/secrets-overview/" ><strong >Secrets<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >密钥</font></font></font></strong></a></td><td >The secrets management API integrates with public cloud and local secret stores to retrieve the secrets for use in application code.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >机密管理 API 与公共云和本地机密存储集成，以检索机密以在应用程序代码中使用。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/configuration/configuration-api-overview/" ><strong >Configuration<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >配置</font></font></font></strong></a></td><td >The configuration API enables you to retrieve and subscribe to application configuration items from configuration stores.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >配置 API 使您能够从配置存储中检索和订阅应用程序配置项。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/distributed-lock/distributed-lock-api-overview/" ><strong >Distributed lock<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >分布式锁</font></font></font></strong></a></td><td >The distributed lock API enables your application to acquire a lock for any resource that gives it exclusive access until either the lock is released by the application, or a lease timeout occurs.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >分布式锁 API 使您的应用程序能够获取任何为其提供独占访问权限的资源的锁，直到应用程序释放该锁或发生租用超时。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/workflow/workflow-overview/" ><strong >Workflows<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >工作流程</font></font></font></strong></a></td><td >The workflow API can be combined with other Dapr building blocks to define long running, persistent processes or data flows that span multiple microservices using Dapr workflows or workflow components.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >工作流 API 可以与其他 Dapr 构建块结合使用，使用 Dapr 工作流或工作流组件定义跨多个微服务的长期运行、持久的流程或数据流。</font></font></font></td></tr><tr ><td ><a href="https://docs.dapr.io/developing-applications/building-blocks/cryptography/cryptography-overview/" ><strong >Cryptography<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><font class="notranslate" >&nbsp;</font><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-inline-wrapper-theme-dashed immersive-translate-target-translation-inline-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >密码学</font></font></font></strong></a></td><td >The cryptography API provides an abstraction layer on top of security infrastructure such as key vaults. It contains APIs that allow you to perform cryptographic operations, such as encrypting and decrypting messages, without exposing keys to your applications.<font class="notranslate immersive-translate-target-wrapper" lang="zh-CN" ><br><font class="notranslate immersive-translate-target-translation-theme-dashed immersive-translate-target-translation-block-wrapper-theme-dashed immersive-translate-target-translation-block-wrapper" ><font class="notranslate immersive-translate-target-inner immersive-translate-target-translation-theme-dashed-inner" >加密 API 在密钥库等安全基础设施之上提供了一个抽象层。它包含允许您执行加密操作（例如加密和解密消息）的 API，而无需向应用程序暴露密钥。</font></font></font></td></tr></tbody>
</table>

另外提供 AOP 切面API用于服务所有构建块

+ **Resiliency 弹性**	 Dapr 提供通过弹性规范定义和应用容错弹性策略的功能。支持的规范定义了弹性模式的策略，例如超时、重试/回退和断路器
+ **Observability 可观察性**	 Dapr 发出指标、日志和跟踪来调试和监控 Dapr 和用户应用程序。 Dapr 支持分布式跟踪，可以使用 W3C 跟踪上下文标准和开放遥测发送到不同的监控工具，轻松诊断和服务生产中的服务间调用。
+ **Security 安全**	 Dapr 支持使用 Dapr 控制平面 Sentry 服务对 Dapr 实例之间的通信进行传输加密。您可以引入自己的证书，或者让 Dapr 自动创建并保留自签名根证书和颁发者证书。

#### 2. 针对这些构建块，dapr的操作方式就是给每个构建块搭一个 sidecar, sidecar 包括 HTTP 和 gRPC API 

Dapr 将其 HTTP 和 gRPC API 作为 sidecar 架构公开，既可以作为容器，也可以作为进程，不需要应用程序代码包含任何 Dapr 运行时代码。这使得与其他运行时的 Dapr 集成变得容易，并提供应用程序逻辑的分离以提高可支持性。

#### 3.托管环境包括 本地和集群两个

+ 自托管本地开发  
在自托管模式下，Dapr 作为单独的 sidecar 进程运行，您的服务代码可以通过 HTTP 或 gRPC 调用该进程。每个正在运行的服务都有一个 Dapr 运行时进程（或 sidecar），配置为使用状态存储、发布/订阅、绑定组件和其他构建块。
+ k8s  
生产时候，我还不太熟悉，后面再写

#### 4. 开发语言
不限制开发语言和框架

### 二、构建块 build
构建块是一种 HTTP 或 gRPC API，可以从您的代码调用并使用一个或多个 Dapr 组件。 Dapr 由一组 API 构建块组成，具有添加新构建块的可扩展性。

*dapr提供了许多服务构建块的组件，已经默认好了API Endpoint，所以在自己开发的应用程序中通过相应的Endpoint调用*

### 三、Components 组件，其实就是基础服务
可以根据dapr提供的标准，开发自己的可插拔组件

![](https://docs.dapr.io/images/concepts-components.png)

可用的组件类型:
+ State stores 状态库
+ Name resolution 名称解析
+ Pub/sub brokers 发布/订阅经纪人
+ Bindings 绑定
+ Secret stores 密钥库
+ Configuration stores 配置存储
+ Locks 分布式锁
+ Workflows 工作流程
+ Cryptography 加解密工具
+ Middleware 中间件  
Dapr 允许将自定义中间件插入 HTTP 请求处理管道。在将请求路由到用户代码或将响应返回到客户端之前，中间件可以对 HTTP 请求执行其他操作（例如身份验证、加密和消息转换）。中间件组件与服务调用构建块一起使用。

### 四、配置等
更改 Dapr 应用程序 sidecar 的行为或在 Dapr 控制平面系统服务上进行全局更改。

后续还有很多术语和概念，主要也是将怎么使用dapr的组件更好的服务构建块

小结： 概念第一篇通读下，留下印象即可

### 五、实现基础操作