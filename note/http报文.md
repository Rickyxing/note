## http报文

### 一、什么是报文

报文，是网络中交换和传输的数据单元，即站点一次性要发送的数据块。报文包含了将要发送的完整的数据信息，其长短很不一致，长度不限且可变。

HTTP报文是由一行一行简单的字符串组成的。HTTP报文都是纯文本，不是二进制代码，所以人们可以很方便地对其进行读写。如果说HTTP是因特网的信使，那么HTTP报文就是它用来搬东西的包裹了。

### 二、报文的流动

报文会流入源端服务器，工作完成之后，会流会用户的Agent代理。

HTTP报文会像河水一样流动，不管是请求报文还是响应报文，所有报文都会向下游流动。所有报文的发送者都在接受者的上游。如下图所示，对请求报文来说，代理1位于代理3的上游，但对响应报文来说，它就位于代理3的下游。

![img](https://gitee.com/angelzou927/picgourl/raw/master/20210319151447.jpeg)

### 三、报文的组成部分

HTTP报文是简单的格式化文本。如下图所示。每条报文都包含一条来自客户端的请求或者一条来自服务器的响应。它们由三部分组成：对报文进行描述的**起始行**、包含属性的**首部块**以及可选的、包含数据的**主体部分**。

![img](https://gitee.com/angelzou927/picgourl/raw/master/20210319151507.jpeg)


所有的HTTP报文都可以分为两类：**请求报文**和**响应报文**。请求报文会向Web服务器请求一个动作。响应报文会将请求的结果返回给客户端。请求报文和响应报文的基本报文结构相同。

#### 1、报文的语法

请求报文的格式：

    <method> <request-URL> <version>  
    <headers>  
    
    <entity-body> 


响应报文的格式

~~~https
<method> <status> <reason-phrase>  
<headers>  

<entity-body> 
~~~


下面是对报文格式各部分的解释：

##### method(方法)

客户端希望服务器对资源执行的动作。是一个单独的词，如：GET、HEAD、POST。

##### request-URL(请求URL)

命名了所请求资源，或者URL路径组件的完整URL。

##### version(版本)

报文所使用的HTTP版本，其格式：HTTP/<major>.<minor>

其中major(主要版本号)和minor(次要版本号)都是整数。

##### status(状态码)

由三位数字组成，描述了请求过程中所发生的情况。

##### reason-phrase(原因短语)

上面数字状态码的可读版本包含行终止序列之前的所有文本。

##### headers(首部)

可以有零个或多个首部，每个首部都包含一个名字，后面跟着一个冒号(:)，然后是一个可选的空格，接着是一个值，最后是一个CRLF。首部是由一个空行(CRLF)结束的，表示了首部列表的结束和实体主体部分的开始，

##### entity-body(实体的主体部分)

包含一个由任意数据组成的数据块。并不是所有的报文都包含实体的主体部分。有时，报文只是以一个CRLF结束。



#### 2、请求报文

下图给出了请求报文的一般格式。

![image-20210319151848839](https://gitee.com/angelzou927/picgourl/raw/master/20210319151850.png)


方法。请求的起始行以方法作为开始，方法用来告知服务器要做些什么。
       HTTP规范中定义了一组常用的请求方法。

![img](https://gitee.com/angelzou927/picgourl/raw/master/20210319151906.jpeg)

注：并不是所有服务器都实现了上面列出的7种方法。而且，由于HTTP设计得易于扩展，所以除了这些方法以外，其他服务器可能还会是实现一些自己的请求方法，称为扩展方法。

看PPT13-15

#### 3、响应报文 （ppt16）

● 状态码

       由三位数字组成，第一位数字表示响应的类型，常用的状态码有五大类如下所示：

　　1xx：表示服务器已接收了客户端请求，客户端可继续发送请求;

　　2xx：表示服务器已成功接收到请求并进行处理;

　　3xx：表示服务器要求客户端重定向;

　　4xx：表示客户端的请求有非法内容;

　　5xx：表示服务器未能正常处理客户端的请求而出现意外错误;

　　状态码描述文本有如下取值：

　　200 OK：表示客户端请求成功;

　　400 Bad Request：表示客户端请求有语法错误，不能被服务器所理解;

　　401 Unauthonzed：表示请求未经授权，该状态代码必须与 WWW-Authenticate 报头域一起使用;

　　403 Forbidden：表示服务器收到请求，但是拒绝提供服务，通常会在响应正文中给出不提供服务的原因;

　　404 Not Found：请求的资源不存在，例如，输入了错误的URL;

　　500 Internal Server Error：表示服务器发生不可预期的错误，导致无法完成客户端的请求;

　　503 Service Unavailable：表示服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常;


#### 请求报文首部

请求头部由关键字/值对组成，每行一对，关键字和值用英文冒号“:”分隔。请求头部通知服务器有关于客户端请求的信息，典型的请求头有：

**User-Agent：**产生请求的浏览器类型。

**Accept：**客户端可识别的内容类型列表。

**connection：**连接方式(close 或 keepalive);
**Cookie：**存储于客户端扩展字段，向同一域名的服务端发送属于该域的cookie;
**Host：**请求的主机名，允许多个域名同处一个IP地址，即虚拟主机。

**Accept：**浏览器可接受的MIME类型。
**Accept-Charset：**浏览器可接受的字符集。

**Accept-Encoding：**浏览器能够进行解码的数据编码方式，比如gzip。Servlet能够向支持gzip的浏览器返回经gzip编码的HTML页面。许多情形下这可以减少5到10倍的下载时间。

**Accept-Language：**浏览器所希望的语言种类，当服务器能够提供一种以上的语言版本时要用到。

**Authorization：**授权信息，通常出现在对服务器发送的WWW-Authenticate头的应答中。

**Connection：**表示是否需要持久连接。如果Servlet看到这里的值为“Keep- Alive”，或者看到请求使用的是HTTP 1.1（HTTP 1.1默认进行持久连接），它就可以利用持久连接的优点，当页面包含多个元素时（例如Applet，图片），显著地减少下载所需要的时间。要实现这一点，Servlet需要在应答中发送一个Content-Length头，最简单的实现方法是：先把内容写入 ByteArrayOutputStream，然后在正式写出内容之前计算它的大小。

**Content-Length：**表示请求消息正文的长度。

**Cookie：**这是最重要的请求头信息之一

**From：**请求发送者的email地址，由一些特殊的Web客户程序使用，浏览器不会用到它。

**Host：**初始URL中的主机和端口。

**If-Modified-Since：**只有当所请求的内容在指定的日期之后又经过修改才返回它，否则返回304“Not Modified”应答。

**Pragma：**指定“no-cache”值表示服务器必须返回一个刷新后的文档，即使它是代理服务器而且已经有了页面的本地拷贝。

**Referer：**包含一个URL，用户从该URL代表的页面出发访问当前请求的页面。

**User-Agent：**浏览器类型，如果Servlet返回的内容与浏览器类型有关则该值非常有用。

**UA-Pixels，UA-Color，UA-OS，UA-CPU：**由某些版本的IE浏览器所发送的非标准的请求头，表示屏幕大小、颜色深度、操作系统和CPU类型。



实体的主体部分
HTTP要传输的内容。



#### 响应头部

**Allow** 服务器支持哪些请求方法（如GET、POST等）。

**Content-Encoding** 文档的编码（Encode）方法。只有在解码之后才可以得到Content-Type头指定的内容类型。利用gzip压缩文档能够显著地减少HTML文档的下载时间。Java的GZIPOutputStream可以很方便地进行gzip压缩，但只有Unix上的Netscape和Windows上的IE 4、IE 5才支持它。因此，Servlet应该通过查看Accept-Encoding头（即request.getHeader("Accept- Encoding")）检查浏览器是否支持gzip，为支持gzip的浏览器返回经gzip压缩的HTML页面，为其他浏览器返回普通页面。

 **Content-Length** 表示内容长度。只有当浏览器使用持久HTTP连接时才需要这个数据。如果你想要利用持久连接的优势，可以把输出文档写入 ByteArrayOutputStram，完成后查看其大小，然后把该值放入Content-Length头，最后通过 byteArrayStream.writeTo(response.getOutputStream()发送内容。

**Content- Type** 表示后面的文档属于什么MIME类型。Servlet默认为text/plain，但通常需要显式地指定为text/html。由于经常要设置 Content-Type，因此HttpServletResponse提供了一个专用的方法setContentTyep。

**Date** 当前的GMT时间。你可以用setDateHeader来设置这个头以避免转换时间格式的麻烦。

**Expires** 应该在什么时候认为文档已经过期，从而不再缓存它？

**Last-Modified** 文档的最后改动时间。客户可以通过If-Modified-Since请求头提供一个日期，该请求将被视为一个条件GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304（Not Modified）状态。Last-Modified也可用setDateHeader方法来设置。

**Location** 表示客户应当到哪里去提取文档。Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法，该方法同时设置状态代码为302。

**Refresh** 表示浏览器应该在多少时间之后刷新文档，以秒计。除了刷新当前文档之外，你还可以通过setHeader("Refresh", "5; URL=http://host/path")让浏览器读取指定的页面。注意这种功能通常是通过设置HTML页面HEAD区的<META HTTP-EQUIV="Refresh" CONTENT="5;URL=http://host/path">实现，这是因为，自动刷新或重定向对于那些不能使用CGI或Servlet的 HTML编写者十分重要。但是，对于Servlet来说，直接设置Refresh头更加方便。注意Refresh的意义是“N秒之后刷新本页面或访问指定页面”，而不是“每隔N秒刷新本页面或访问指定页面”。因此，连续刷新要求每次都发送一个Refresh头，而发送204状态代码则可以阻止浏览器继续刷新，不管是使用Refresh头还是<META HTTP-EQUIV="Refresh" ...>。注意Refresh头不属于HTTP 1.1正式规范的一部分，而是一个扩展，但Netscape和IE都支持它。

**Server** 服务器名字。Servlet一般不设置这个值，而是由Web服务器自己设置。

Set-Cookie 设置和页面关联的Cookie。Servlet不应使用response.setHeader("Set-Cookie", ...)，而是应使用HttpServletResponse提供的专用方法addCookie。参见下文有关Cookie设置的讨论。

**WWW-Authenticate** 客户应该在Authorization头中提供什么类型的授权信息？在包含401（Unauthorized）状态行的应答中这个头是必需的。例如，response.setHeader("WWW-Authenticate", "BASIC realm=\"executives\"")。注意Servlet一般不进行这方面的处理，而是让Web服务器的专门机制来控制受密码保护页面的访问（例如.htaccess）。