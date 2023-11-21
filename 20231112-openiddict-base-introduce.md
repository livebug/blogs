---
title : 'Openiddict Base Introduce'
date : 2023-11-12T09:07:42+08:00
toc: true
tags: ['openiddict','C#']
categories: ['技术博客']
---

身份认证服务、多租户的实现 

用于学习的目的，必须要从identityServer开始学习


`Authentication` 验证

当应用程序需要知道当前用户的身份时，需要进行身份验证。通常，这些应用程序代表该用户管理数据，并且需要确保该用户只能访问允许他们访问的数据。

最常见的身份验证协议是 `SAML2p`、`WS-Federation` 和 `OpenID Connect` - SAML2p 是最流行且部署最广泛的协议。

`OpenID Connect` 是这三者中最新的一个，但被认为是未来，因为它对于现代应用程序最具潜力。它从一开始就是为移动应用场景而构建的，并且被设计为 API 友好。

`OAuth2` 是一种协议，允许应用程序从安全令牌服务请求访问令牌并使用它们与 API 进行通信。由于身份验证和授权可以集中化，因此这种委派降低了客户端应用程序和 API 的复杂性。

OpenID Connect 和 OAuth 2.0 非常相似 - 事实上 OpenID Connect 是 OAuth 2.0 之上的扩展。身份验证和 API 访问这两个基本安全问题被组合到一个协议中 - 通常与安全令牌服务进行单次往返。

我们相信，OpenID Connect 和 OAuth 2.0 的结合是在可预见的未来保护现代应用程序安全的最佳方法。 Duende IdentityServer 是这两个协议的实现，并经过高度优化，可以解决当今移动、本机和 Web 应用程序的典型安全问题。

Duende IdentityServer 是一个中间件，它将符合规范的 OpenID Connect 和 OAuth 2.0 端点添加到任意 ASP.NET Core 主机。

通常，您构建（或重用）包含登录和注销页面（以及可选的同意页面，具体取决于您的需要）的应用程序，并将 IdentityServer 中间件添加到该应用程序。中间件向应用程序添加必要的协议头，以便客户端可以使用这些标准协议与其进行通信。

Duende IdentityServer 是一个 OpenID Connect 和 OAuth 引擎 - 它实现了 OpenID Connect 和 OAuth 2.0 系列协议。


Client 

Client 分类

1. Machine to Machine Communication 机器对机器通信  
在这种情况下，两台机器相互通信（例如后台进程、批处理作业、服务器守护进程），并且不存在交互式用户。为了授权此通信，您的 IdentityServer 向调用者发出一个令牌。
2. Interactive Applications 互动应用  
这是最常见的客户端场景类型：Web 应用程序、SPA 或具有交互式用户的本机/移动应用程序。此场景通常涉及用于用户交互的浏览器（例如，用于身份验证或同意）。


## IdentityServer 和 JWT身份服务器和 JWT


IdentityServer 和 JSON Web Tokens (JWT) 是两个在身份验证和授权方面经常一起使用的概念，但它们具有不同的角色和功能。

IdentityServer：身份服务器：

角色： IdentityServer 是一个开源的身份验证和授权服务器，旨在为应用程序提供安全的身份验证和授权服务。它实现了 OAuth 2.0 和 OpenID Connect 协议，为客户端应用程序提供了标准化的认证和授权流程。
功能： IdentityServer 充当中央身份验证和授权服务，允许多个客户端应用程序通过它进行身份验证和获取授权。它可以颁发包含用户身份信息和访问令牌的 JWT。

JSON Web Tokens (JWT)：JSON网络令牌（JWT）：

角色： JWT 是一种用于在网络应用之间传递信息的开放标准 (RFC 7519)。它通常被用作在客户端和服务器之间传递有关用户身份和授权的信息。
功能： JWT 是一种轻量级的、自包含的令牌格式，可以在不同系统之间传递信息。在身份验证场景中，JWT 通常包含用户身份信息、权限声明以及其他相关信息。IdentityServer 可以生成包含用户身份信息的 JWT，并将其提供给客户端应用程序。

关联：

IdentityServer 和 JWT 关系： IdentityServer 通常使用 JWT 作为访问令牌 (Access Token) 的一种格式。当客户端应用程序通过身份验证并获得授权时，IdentityServer 可以颁发包含用户身份信息的 JWT 作为访问令牌，客户端可以使用该令牌向受保护的资源发起请求。 

### 几个好用的网站

https://source.dot.net/  源码查看网站

[ASP.NET Core 认证与授权[1]:初识认证](https://www.cnblogs.com/RainingNight/p/introduce-basic-authentication-in-asp-net-core.html#microsoft.aspnetcore.authentication)

