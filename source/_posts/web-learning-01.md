---
layout:     post
title:      "网页状态码记录"
date:       2018-11-07 22:30:00
categories: Web Security
tags:   [๑Web, ๑Security]
---


## HTTP状态码
---

- 五个不同的类别:
　　1. `1XX`临时/信息响应
　　2. `2XX`成功
　　3. `3XX`重定向
　　4. `4XX`客户端/请求错误
　　5. `5XX`服务器错误
> 五个类别的响应状态代码的第一个数字是唯一代表。

### 4XX 服务器外部错误

#### 400
- 400 无法解析此请求。说明正在搜索的网页可能已经删除、更名或暂时不可用。

#### 401.X
- 401.1 未经授权：访问由于凭据无效被拒绝。说明没有权限查看该目录或网页。
- 401.2 未经授权: 访问由于服务器配置倾向使用替代身份验证方法而被拒绝。
`由于服务器配置问题而导致登陆失败，由于服务器端脚本未能正确发送 WWW 身份验证头文件字段。如果要通过 Active Server Pages 脚本完成此项任务，可以使用"Response"对象的"AddHeader"方法来要求客户端用特定身份验证方法访问资源。`

- 401.3 未经授权：访问由于 ACL 对所请求资源的设置被拒绝。
- 401.4 未经授权：Web 服务器上安装的筛选器授权失败。
`如果Web 服务器安装了筛选器程序以检查连接到服务器的用户。该筛选器程序能够禁止通过连接到服务器的身份验证来访问资源。`

- 401.5 未经授权：ISAPI/CGI 应用程序授权失败。
`由于 ISAPI/CGI 应用程序导致授权失败。如果所要访问的 Web 服务器地址上安装了 ISAPI 或 CGI 程序用于在继续执行之前检验用户证书。该程序能够禁止通过连接到服务器的身份验证证书来访问资源。`

- 401.7 未经授权：由于 Web 服务器上的 URL 授权策略而拒绝访问。

#### 403.X
- 403 禁止访问：访问被拒绝。
- 403.1 禁止访问：执行访问被拒绝。
`由于"执行"访问被禁止而造成的，若试图从目录中执行 CGI、ISAPI 或其他可执行程序，但该目录不允许执行程序时便会出现此种错误。`

- 403.2 禁止访问：读取访问被拒绝。
`导致此错误是由于没有可用的默认网页并且没有对目录启用目录浏览，或者要显示的 HTML 网页所驻留的目录仅标记为"可执行"或"脚本"权限。`
- 403.3 禁止访问：写入访问被拒绝。
`当试图将文件上载到目录或在目录中修改文件，但该目录不允许"写"访问时就会出现此种错误。`

- 403.4 禁止访问：需要使用 SSL 查看该资源。
`由于要求SSL而造成的，您必须在要查看的网页的地址中使用"https"。`

- 403.5 禁止访问：需要使用 SSL 128 查看该资源。
`由于要求使用 128 位加密算法的 Web 浏览器而造成的，如果您的浏览器不支持128位加密算法就会出现这个错误，您可以连接微软网站进行浏览器升级。`

- 403.6 禁止访问：客户端的 IP 地址被拒绝。
`如果服务器中有不能访问该站点的 IP 地址列表，并且您使用的 IP 地址在该列表中时您就会返回这条错误信息。`

- 403.7 禁止访问：需要 SSL 客户端证书。
- 403.8 禁止访问：客户端的 DNS 名称被拒绝。
`由于禁止站点访问而造成的，若服务器中有不能访问该站点的 DNS 名称列表，而您使用的 DNS 名称在列表中时就会返回此种信息。请注意区别403.6与403.8错误。`

- 403.9 禁止访问：太多客户端试图连接到 Web 服务器。
`由于连接的用户过多而造成的，由于Web 服务器很忙，因通讯量过多而无法处理请求时便会返回这条错误。`

- 403.10 禁止访问：Web 服务器配置为拒绝执行访问。
`由于无效配置而导致的错误，当您试图从目录中执行 CGI、ISAPI 或其他可执行程序，但该目录不允许执行程序时便会返回这条错误。`

- 403.11 禁止访问：密码已更改。
- 403.12 禁止访问：服务器证书映射器拒绝了客户端证书访问。
`由于映射器拒绝访问而造成的。若要查看的网页要求使用有效的客户证书，而您的客户证书映射没有权限访问该 Web 站点时就会返回映射器拒绝访问的错误。`

- 403.13 禁止访问：客户端证书已在 Web 服务器上吊销。
`由于需要查看的网页要求使用有效的客户证书而使用的客户证书已经被吊销，或者无法确定证书是否已吊销造成的。`

- 403.14 禁止访问：在 Web 服务器上已拒绝目录列表。
- 403.15 禁止访问：Web 服务器已超过客户端访问许可证限制。
- 403.16 禁止访问：客户端证书格式错误或未被 Web 服务器信任。
- 403.17 禁止访问：客户端证书已经到期或者尚未生效。
- 403.18 禁止访问：无法在当前应用程序池中执行请求的 URL。
- 403.19 禁止访问：无法在该应用程序池中为客户端执行 CGI。
- 403.20 禁止访问：Passport 登录失败。

#### 404.X
- 404 找不到文件或目录。
`由于无法找到文件而造成的，通常是由于正在搜索的网页可能已经删除、更名或暂时不可用。`

- 404.1 文件或目录未找到：网站无法在所请求的端口访问。
`表明所访问 Web 站点的 IP 地址不接受对端口（请求的来源端口）的请求。404.1 错误只会出现在具有多个 IP 地址的计算机上。如果在特定 IP 地址/端口组合上收到客户端请求，而且没有将 IP 地址配置为在该特定的端口上侦听，则 IIS 返回 404.1 HTTP 错误。例如，如果一台计算机有两个 IP 地址，而只将其中一个 IP 地址配置为在端口 80 上侦听，则另一个 IP 地址从端口 80 收到的任何请求都将导致 IIS 返回 404.1 错误。只应在此服务级别设置该错误，因为只有当服务器上使用多个 IP 地址时才会将它返回给客户端。`

- 404.2 文件或目录无法找到：锁定策略禁止该请求。
- 404.3 文件或目录无法找到：MIME 映射策略禁止该请求。

#### else
- 405 用于访问该页的 HTTP 动作未被许可。
`由于资源被禁止而导致的网页地址不正确，因此要寻找的网页无法显示。`

- 406 客户端浏览器不接受所请求页面的 MIME 类型。`由于浏览器无法打开正在寻找的资源而导致的错误。`

- 407 Web 服务器需要初始的代理验证。
- 410 要寻找的网页已被永久删除而导致的，这意味着资源永远无法使用。
- 412 客户端设置的前提条件在 Web 服务器上评估时失败。
`412错误是由于要查看的网页设置有先决条件，因此该请求无法完成。一般是网页中有一个或多个请求标题字段中具有先决条件，这些字段经服务器测试后被认为是"FALSE"。客户端为当前资源的 meta 信息（头文件字段数据）设置了先决条件，以便防止请求的方法被用于指定资源外的其他资源。`

- 414 请求 URL 太大，因此在 Web 服务器上不接受该 URL。
`一般的可能性有： 1）客户端错误地将 POST 请求转换为带有长查询信息的 GET 请求。 2）或者是客户端遇到重定向问题（例如，重定向 URL 的前缀指向自身的后缀）。 3）服务器遭到客户端的攻击，该客户端试图利用那些使用定长缓冲来读取或控制请求 URI 的服务器上的安全漏洞。`

### 5XX 服务器内部错误
- 500 服务器内部错误。
- 500.11 服务器错误：Web 服务器上的应用程序正在关闭。
- 500.12 服务器错误：Web 服务器上的应用程序正在重新启动。
- 500.13 服务器错误：Web 服务器太忙。
- 500.14 服务器错误：服务器上的无效应用程序配置。
- 500.15 服务器错误：不允许直接请求 GLOBAL.ASA。
- 500.16 服务器错误：UNC 授权凭据不正确。
- 500.17 服务器错误：URL 授权存储无法找到。
- 500.18 服务器错误：URL 授权存储无法打开。
- 500.19 服务器错误：该文件的数据在配置数据库中配置不正确。
- 500.20 服务器错误：URL 授权域无法找到。
- 500-100.asp 内部服务器错误：ASP 错误。
- 501 标题值指定的配置没有执行。

- 502 Web 服务器作为网关或代理服务器时收到无效的响应。
`由于网关错误而造成的，当作为网关或代理的服务器与上层内容服务器联络时，收到无效的响应时就会出现502错误。`

- 参考 [https://blog.csdn.net/aaa_aa000/article/details/46997991](https://blog.csdn.net/aaa_aa000/article/details/46997991)

- 参考[https://www.jianshu.com/p/d50bcc605a13](https://www.jianshu.com/p/d50bcc605a13)