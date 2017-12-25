# RESTful简介

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1513569886193&di=440df2fa7fa242622ea55a56eb712d3b&imgtype=0&src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farchive%2F5c6fb9b743563ca92a9d76b37249c4b415397826.jpg)

大家好,这篇文章在这里简单的给大家做一个RESTful的简单普及,由于本人也没有过深的追入,所以在这里给大家简短说一说,希望本文能对各位简单理解REST有所帮助。


### RESTful是什么?

**RESTful(Representational State Transfer)** 
一种软件架构风格、设计风格，而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。


### 概述

REST（英文：Representational State Transfer，简称REST）描述了一个架构样式的网络系统，比如 web 应用程序。它首次出现在 2000 年 Roy Fielding 的博士论文中，他是 HTTP 规范的主要编写者之一。在目前主流的三种Web服务交互方案中，REST相比于SOAP（Simple Object Access protocol，简单对象访问协议）以及XML-RPC更加简单明了，无论是对URL的处理还是对Payload的编码，REST都倾向于用更加简单轻量的方法设计和实现。值得注意的是REST并没有一个明确的标准，而更像是一种设计的风格。

![概述图](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=b4a242e032d12f2eda08a6322eabbe07/0eb30f2442a7d93307dbc744a94bd11373f00191.jpg)


### RESTful的好处有哪些?

1. 充分利用 HTTP 协议本身语义。
2. 透明性，暴露资源存在。
3. 无状态，这点非常重要。在调用一个接口（访问、操作资源）的时候，可以不用考虑上下文，不用考虑当前状态，极大的降低了复杂度
4. HTTP 本身提供了丰富的内容协商手段，无论是缓存，还是资源修改的乐观并发控制，都可以以业务无关的中间件来实现

### 表现概念:
* 资源（Resources） REST是"表现层状态转化"，其实它省略了主语。"表现层"其实指的是"资源"的"表现层"。  
那么什么是资源呢？就是我们平常上网访问的一张图片、一个文档、一个视频等。这些资源我们通过URI来定位，也就是一个URI表示一个资源。

* 表现层（Representation）

	资源是做一个具体的实体信息，他可以有多种的展现方式。而把实体展现出来就是表现层，例如一个txt文本信息，他可以输出成html、json、xml等格式，一个图片他可以jpg、png等方式展现，这个就是表现层的意思。

	URI确定一个资源，但是如何确定它的具体表现形式呢？应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述。

* 状态转化（State Transfer）

	访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，肯定涉及到数据和状态的变化。而HTTP协议是无状态的，那么这些状态肯定保存在服务器端，所以如果客户端想要通知服务器端改变数据和状态的变化，肯定要通过某种方式来通知它。

	客户端能通知服务器端的手段，只能是HTTP协议。具体来说，就是HTTP协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。

### 举个例子

要让一个资源可以被识别，需要有个唯一标识，在Web中这个唯一标识就是URI(Uniform Resource Identifier)。 URI既可以看成是资源的地址，也可以看成是资源的名称。如果某些信息没有使用URI来表示，那它就不能算是一个资源， 只能算是资源的一些信息而已。URI的设计应该遵循可寻址性原则，具有自描述性，需要在形式上给人以直觉上的关联。这里以github网站为例，给出一些还算不错的URI：

	https://github.com/git
	https://github.com/git/git
	https://github.com/git/git/blob/master/block-sha1/sha1.h
	https://github.com/git/git/commit/e3af72cdafab5993d18fae056f87e1d675913d08
	https://github.com/git/git/pulls
	https://github.com/git/git/pulls?state=closed
	https://github.com/git/git/compare/master…next

* 使用_或-来让URI可读性更好
* 使用/来表示资源的层级关系
* 使用?用来过滤资源
* ,或;可以用来表示同级资源的关系   (有时候我们需要表示同级资源的关系时，可以使用,或;来进行分割。例如哪天github可以比较某个文件在随意两次提交记录之间的差异，或许可以使用/git/git /block-sha1/sha1.h/compare/e3af72cdafab5993d18fae056f87e1d675913d08;bd63e61bdf38e872d5215c07b264dcc16e4febca作为URI。 不过，现在github是使用…来做这个事情的，例如/git/git/compare/master…next。)

REST是一种架构风格，汲取了WWW的成功经验：无状态，以资源为中心，充分利用HTTP协议和URI协议，提供统一的接口定义，使得它作为一种设计Web服务的方法而变得流行。在某种意义上，通过强调URI和HTTP等早期Internet标准，REST是对大型应用程序服务器时代之前的Web方式的回归。目前Go对于REST的支持还是很简单的，通过实现自定义的路由规则，我们就可以为不同的method实现不同的handle，这样就实现了REST的架构。


### 总结:

REST 描述了一个架构样式的互联系统（如 Web 应用程序）。REST 约束条件作为一个整体应用时，将生成一个简单、可扩展、有效、安全、可靠的架构。由于它简便、轻量级以及通过 HTTP 直接传输数据的特性，RESTful Web 服务成为基于 SOAP 服务的一个最有前途的替代方案。用于 web 服务和动态 Web 应用程序的多层架构可以实现可重用性、简单性、可扩展性和组件可响应性的清晰分离。开发人员可以轻松使用 Ajax 和 RESTful Web 服务一起创建丰富的界面。
	
[如有更好的建议提议,可以发到我的邮箱diosamolee2014@gmail.com](#)
