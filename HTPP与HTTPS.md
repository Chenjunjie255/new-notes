# 了解 HTTP 协议

## HTTP 是什么

HTTP (HyperText Transfer Protocol, 超文本传输协议) 是一种应用非常广泛的 [应用层](https://so.csdn.net/so/search?q=应用层&spm=1001.2101.3001.7020)协议.

> 所谓 “超文本” 的含义, 就是传输的内容不仅仅是文本(比如 html, css 这个就是文本), 还可以是一些
> 其他的资源, 比如图片, 视频, 音频等[二进制](https://so.csdn.net/so/search?q=二进制&spm=1001.2101.3001.7020)的数据

## 抓包工具的使用

## [抓包](https://so.csdn.net/so/search?q=抓包&spm=1001.2101.3001.7020)工具的使用

- 可以直接在官网下载 [Fiddler官网地址](https://www.telerik.com/download/fiddler)
- 也可以直接进入 [fiddler搜索页](https://www.sogou.com/web?query=fiddler&_asf=www.sogou.com&_ast=&w=01019900&p=40040100&ie=utf8&from=index-nologin&s_from=index&sut=2602&sst0=1650441810212&lkt=0,0,0&sugsuv=1650186416440610&sugtime=1650441810212)

<img src="E:\Typora笔记\图片\image-20220617100123331.png" alt="image-20220617100123331" style="zoom:50%;" />

### Fiddler 基本的设置

① 首先设置 点击 `Tools` -> `Options`

<img src="E:\Typora笔记\图片\image-20220617100155585.png" alt="image-20220617100155585" style="zoom:50%;" />

② 点击 `HTTPS` 将下面能勾选的勾上

<img src="E:\Typora笔记\图片\image-20220617100226461.png" alt="image-20220617100226461" style="zoom: 50%;" />

###  Fillder 的使用

将左边的内容清空,然后再进入一个网站,找到对应的那个

<img src="E:\Typora笔记\图片\image-20220617100258487.png" alt="image-20220617100258487" style="zoom: 50%;" />

按照图片的顺序进行点击,右上就是请求,右下就是响应

<img src="E:\Typora笔记\图片\image-20220617100614966.png" alt="image-20220617100614966" style="zoom:50%;" />

## 观察一个抓包结果

HTTP 请求

<img src="E:\Typora笔记\图片\image-20220617100638712.png" alt="image-20220617100638712" style="zoom:50%;" />



HTTP响应

<img src="E:\Typora笔记\图片\image-20220617100700224.png" alt="image-20220617100700224" style="zoom:50%;" />

# HTTP 协议的报文格式

## 请求报文格式

**首行:** `[方法]` `[URL]` `[版本]`

**Header:** 请求的属性.
**空行**
**Body:** 空行后面的内容为 Body.

## 响应报文格式

**首行:** `[版本号]` `[状态码]` `[状态码的解释]`
**Header**: 请求的属性.
**空行**
**Body:** 空行后面的内容为 Body.

## 报文格式的注意事项

1. 首行的内容之间有一个空格.

<img src="E:\Typora笔记\图片\image-20220617100815270.png" alt="image-20220617100815270" style="zoom:50%;" />

2.请求的属性是使用冒号分割的键值对.
	每组属性之间使用\n分割
	遇到空行表示Header部分结束

3.Body 允许为空.
	如果Body存在,Header中会有一个Content-Length属性来标识Body的长度

4.协议格式总结

<img src="E:\Typora笔记\图片\image-20220617100923011.png" alt="image-20220617100923011" style="zoom:50%;" />

# 认识 URL

## URL 基本格式

<img src="E:\Typora笔记\图片\image-20220617101821829.png" alt="image-20220617101821829" style="zoom:50%;" />

##  分析一个具体的 URL:

```shell
https://dict.youdao.com/result?word=1&lang=en
```

> - https: 协议方案名.
> - user:pass: 登录信息. 目前一般会省略
> - dict.youdao.com: 服务器地址. 此处是一个 “域名”, 域名会通过 DNS 系统解析成一个具体的 IP 地址
> - 端口号: 目前一般会省略. http协议默认使用 80 端口. https协议默认使用 443 端口
> - /result 带层次的文件路径
> - word=1&lang=en: 查询字符串(query string). 本质是一个键值对结构,键值对之间使用&分割,键和值之间使用=分割
> - 片段标识: 此 URL 中省略了片段标识. 片段标识主要用于页面内跳转.

## URL 中的可省略部分

> - 协议名: 可以省略, 省略后 默认为 http://
> - ip 地址 / 域名: 在 HTML 中可以省略(比如 img, link, script, a 标签的 src 或者 href 属性). 省略后表示服务器的 ip / 域名与当前 HTML 所属的 ip / 域名一致.
> - 端口号: 可以省略. 省略后如果是 http 协议, 端口号自动设为 80; 如果是 https 协议, 端口号自动设为 443.
> - 带层次的文件路径: 可以省略. 省略后相当于 / . 有些服务器会在发现 / 路径的时候自动问/index.html
> - 查询字符串: 可以省略
> - 片段标识: 可以省略

## 关于 URL encode 和 URL decode

像` / ? : = &` 等这样的字符, 已经被url当做特殊意义理解了. 因此这些字符不能随意出现

把特殊字符,转换成转义字符 => `URL encode`
把转义字符,还原成原来的字符 => `URL decode`

<img src="E:\Typora笔记\图片\image-20220617102030194.png" alt="image-20220617102030194" style="zoom:50%;" />

<img src="E:\Typora笔记\图片\image-20220617102045498.png" alt="image-20220617102045498" style="zoom:50%;" />



# HTTP 请求(Request)

## HTTP 方法

![image-20220617102415006](E:\Typora笔记\图片\image-20220617102415006.png)

### GET 方法

#### ① 构造 HTTP GET 请求的情况

1. 直接在浏览器中输入 URL
2. HTML 中的 link,img,a,script 标签等
3. form 表单
4. ajax
5. 使用 java代码/其他的库
6. 通过 linux 下的 wget / curl
7. 通过第三方工具,postman 这类工具

#### ② 使用 Fiddler 观察 GET请求

在浏览器中输入`sogou.com`

<img src="E:\Typora笔记\图片\image-20220617102453653.png" alt="image-20220617102453653" style="zoom:50%;" />

**GET 请求的特点**

- 首行的第一部分为 GET
- URL 的 query string 可以为空, 也可以不为空.
- header 部分有若干个键值对结构.
- body 部分为空.(可以不为空)

> 关于 GET 请求的 URL 长度问题
> HTTP 协议由 RFC 2616 标准定义.没有对 URL 的长度有任何的限制

### POST 方法

#### ① 构造 HTTP POST 请求的情况

1. form表单
2. ajax
3. 第三方工具

#### ② 使用 Fiddler 观察 POST 请求

![image-20220617102603429](E:\Typora笔记\图片\image-20220617102603429.png)

**POST 请求的特点**

- 首行的第一部分为 POST
- URL 的 query string 一般为空 (也可以不为空)
- header 部分有若干个键值对结构.
- body 部分一般不为空. body 内的数据格式通过 header 中的 Content-Type 指定. body 的长度由header 中的 Content-Length 指定.

### 面试题: 谈谈 GET 和 POST 的区别

GET 和 POST 之间没有本质的区别

1. 数据位置: GET 把自定义数据放到 query string, POST 把自定义数据放到 body
2. 语义区别: GET 一般用于"获取数据",POST 一般用于提交数据
3. 幂等性: GET 请求一般会设计成"幂等". POST 请求一般不要求设计成"幂等"(如果多次请求得到的结果一样, 就视为请求是幂等的)
4. 可缓存: GET 请求一般会被缓存 POST 请求一般不能被缓存

### 其他相关方法

- PUT 与 POST 相似，只是具有幂等特性，一般用于更新
- DELETE 删除服务器指定资源
- OPTIONS 返回服务器所支持的请求方法
- HEAD 类似于GET，只不过响应体不返回，只返回响应头
- TRACE 回显服务器端收到的请求，测试的时候会用到这个
- CONNECT 预留，暂无使用

这些方法都可以使用ajax来构造.(也可以通过第三方工具).

## 认识请求报头 (header)

header 的整体的格式也是 “键值对” 结构
每个键值对占一行. 键和值之间使用分号分割

### ① Host

> 表示服务器主机的地址和端口

### ② Content-Length

> 表示 body 中的数据长度

### ③ Content-Type

> 表示 body 中的数据格式的类型

#### 1) application/x-www-form-urlencoded

在 form 表单提交的时候会出现的数据格式类型.

![image-20220617151831979](E:\Typora笔记\图片\image-20220617151831979.png)

此时的body的格式

![image-20220617151859218](E:\Typora笔记\图片\image-20220617151859218.png)

#### 2) multipart/form-data:

通常用于提交图片/文件

![image-20220617151920848](E:\Typora笔记\图片\image-20220617151920848.png)

body的格式

![image-20220617151943501](E:\Typora笔记\图片\image-20220617151943501.png)

#### 3) application/json

![image-20220617152000719](E:\Typora笔记\图片\image-20220617152000719.png)

body格式

![image-20220617152013374](E:\Typora笔记\图片\image-20220617152013374.png)

### ④ User-Agent

字段User-Agent会将创建请求的浏览器和用户代理名称等信息传达给服务器

![image-20220617152038747](E:\Typora笔记\图片\image-20220617152038747.png)

这里的 `Windows NT 10.0;WOW64` 表示操作系统的信息
`AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Safari/537.36` 表示浏览器信息

### ⑤ Referer

表示这个页面是从哪个页面跳转过来的.

![image-20220617152107163](E:\Typora笔记\图片\image-20220617152107163.png)



如果直接在浏览器中输入URL, 或者直接通过收藏夹访问页面时是没有 Referer 的

### ⑥ Cookie

因为HTTP是无状态的协议,无法根据之前的状态进行本次的请求处理
为了保留无状态协议这个特征,于是引入了 Cookie 信息来控制客户端的状态.
Cookie会根据从服务器端发送的响应报文内的一个叫做 Set-Cookie 的首部字段信息,通知客户端保存 Cookie.当下次再给该服务器发送请求的时候,客户端会自动在请求报文中加入Cookie值后发送出去.
服务器端发现客户端发送来的 Cookie 后,会去检查是哪一个客户端发来的连接请求,对比服务器上的记录,最后得到之前的状态信息.
<img src="E:\Typora笔记\图片\image-20220617152145271.png" alt="image-20220617152145271" style="zoom:50%;" />



# HTTP 响应(Response)

## 认识状态码 (status code)

<img src="E:\Typora笔记\图片\image-20220617152243815.png" alt="image-20220617152243815" style="zoom: 50%;" />

### ① 200 OK

> 这是一个最常见的状态码, 表示访问成功.

<img src="E:\Typora笔记\图片\image-20220617152307785.png" alt="image-20220617152307785" style="zoom:50%;" />

### ② 404 Not Found

> 没有找到资源.

![image-20220617152338073](E:\Typora笔记\图片\image-20220617152338073.png)

### ③ 403 Forbidden

> 表示访问被拒绝. 有的页面通常需要用户具有一定的权限才能访问(登陆后才能访问). 如果用户没有登陆直接访问, 就容易见到 403.

<img src="E:\Typora笔记\图片\image-20220617152410032.png" alt="image-20220617152410032" style="zoom:50%;" />



### ④ 500 Internal Server Error

> 服务器出现内部错误. 一般是服务器的代码执行过程中遇到了一些特殊情况(服务器异常崩溃)会产生这个状态码

### ⑤ 302 Move temporarily

> **临时重定向.**
> 重定向就和呼叫转移一样,
> 就是换了个手机号,别人呼叫你旧手机号,会自动转到新手机号上

## 5.2 认识响应正文 (body)

正文的具体格式取决于 Content-Type.

### ① text/html

> body中的数据格式是 HTML

![image-20220617152529866](E:\Typora笔记\图片\image-20220617152529866.png)

### ② text/css

> body中的数据格式是css

### ③ application/javascript

> body中的数据格式是javascript

### ④ application/json

> body中的数据格式是json

# 构造 HTTP 请求

## 通过 form 表单构造 HTTP 请求

### ① 构造 GET 请求

代码:

```html
<form action="http://www.baidu.com" method="GET">
    <input type="text" name="user">
    <input type="password" name="password">
    <input type="submit" value="提交">
</form>
```

### ② 构造 POST 请求

```html
<form action="http://www.baidu.com" method="POST">
    <input type="text" name="user">
    <input type="password" name="password">
    <input type="submit" value="提交">
</form>
```

## 通过 ajax 构造 HTTP 请求

### ① 发送 GET 请求

```javascript
<script>
    // 1. 创建 XMLHttpRequest 对象
    let httpRequest = new XMLHttpRequest();
    // 2. 默认异步处理响应. 需要挂在处理响应的回调函数.
    httpRequest.onreadystatechange = function () {
        // readState 表示当前的状态.
        // 0: 请求未初始化
        // 1: 服务器连接已建立
        // 2: 请求已接收
        // 3: 请求处理中
        // 4: 请求已完成，且响应已就绪
        if (httpRequest.readyState == 4) {
            // status 属性获取 HTTP 响应状态码
            console.log(httpRequest.status);
            // responseText 属性获取 HTTP 响应 body
            console.log(httpRequest.responseText);
        }
    }
    // 3. 调用 open 方法设置要访问的 url
    httpRequest.open('GET', 'http://42.192.83.143:8080/AjaxMockServer/info');
    // 4. 调用 send 方法发送 http 请求
    httpRequest.send();
</script>
```

### ② 发送 POST 请求

```javascript
<script>
    // 1. 创建 XMLHttpRequest 对象
    let httpRequest = new XMLHttpRequest();
    // 2. 默认异步处理响应. 需要挂在处理响应的回调函数.
    httpRequest.onreadystatechange = function () {
        // readState 表示当前的状态.
        // 0: 请求未初始化
        // 1: 服务器连接已建立
        // 2: 请求已接收
        // 3: 请求处理中
        // 4: 请求已完成，且响应已就绪
        if (httpRequest.readyState == 4) {
            // status 属性获取 HTTP 响应状态码
            console.log(httpRequest.status);
            // responseText 属性获取 HTTP 响应 body
            console.log(httpRequest.responseText);
        }
    }
    // 3. 调用 open 方法设置要访问的 url
    httpRequest.open('POST', 'http://42.192.83.143:8080/AjaxMockServer/info');
    // 4. 调用 setRequestHeader 设置请求头
    httpRequest.setRequestHeader('Content-Type', 'application/x-www-formurlencoded');
    // 5. 调用 send 方法发送 http 请求
    httpRequest.send('name=zhangsan&age=18');
</script>
```

### ③ 通过第三方库来封装 ajax

```javascript
<script src="https://releases.jquery.com/git/jquery-git.min.js"></script>
<script>
    $.ajax({
        type: 'GET',
        url:'http://www.baidu.com/index.html',
        success: function(data, status){
            // data 是响应body status 是状态码描述
            console.log(status);
            console.log(data);
        }
    })
</script>
```

##  通过 Java socket 构造 HTTP 请求

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;
import java.nio.charset.StandardCharsets;

public class HttpClient {
    private Socket socket;
    private String ip;
    private int port;

    public HttpClient(String ip,int port) throws IOException {
        socket = new Socket(ip,port);
        this.port = port;
        this.ip = ip;
    }

    public String get(String url) throws IOException {
        StringBuilder request = new StringBuilder();
        // 构造首行
        request.append("Get " + url + " HTTP/1.1\n");
        // 构造 header
        request.append("Host: " + ip + ":" + port + "\n");
        // 构造空行
        request.append("\n");
        // GET 不需要 body, 构造完毕
        OutputStream outputStream = socket.getOutputStream();
        // outputStream 是一个字节流,以字节为单位进行写入,因此需要把 StringBuilfer 转换乘byte[]
        outputStream.write(request.toString().getBytes());

        // 读取响应
        InputStream inputStream = socket.getInputStream();
        // 1M 大小的缓冲区,用来存放响应数据
        byte[] buffer = new byte[1024 * 1024];
        // n 表示实际上读到的字节数
        int n = inputStream.read(buffer);
        return new String(buffer,0,n,"utf-8");
    }

    public String post(String url,String body) throws IOException {
        StringBuilder request = new StringBuilder();
        // 构造首行
        request.append("POST" + url + "HTTP/1.1\n");
        // 构造header
        request.append("Host: " + ip + ":" + port + "\n");
        request.append("Content-Type: text/plain\n");
        request.append("Content-Length: " + body.getBytes().length + "\n");
        // 构造空行
        request.append("\n");
        // 构造 body
        request.append(body);

        // 发送请求
        OutputStream outputStream = socket.getOutputStream();
        outputStream.write(request.toString().getBytes());

        // 读取响应
        InputStream inputStream = socket.getInputStream();
        byte[] buffer = new byte[1024 * 1024];
        int n = inputStream.read(buffer);
        return new String(buffer, 0, n, "utf-8");
    }

    public static void main(String[] args) throws IOException {
        HttpClient httpClient = new HttpClient("42.192.83.143",9090);
        String resp = httpClient.get("/AjaxMockServer/info");
        System.out.println(resp);
//        String resp = httpClient.post("/AjaxMockServer/info","这是正文");
//        System.out.println(resp);
    }
}
```

# HTTPS

## 什么是 HTTPS

HTTPS 也是一个应用层协议. 是在 HTTP 协议的基础上引入了一个加密层(SSL/TLS).

## 为什么引入 HTTPS

因为HTTP是明文传输, 本来要传什么,实际上就传了什么,但是一旦这样传输,在传输的过程中, 被第三方截获到了,就可能造成信息泄露.

于是引入了 HTTPS在HTTP基础上进行了加密,进一步的保护了用户的信息安全.

> 明文: 真正要传输的信息
> 密文: 加密之后的消息
>
> 加密: 就是把 明文 (要传输的信息)进行一系列变换, 生成 密文 .
> 解密: 就是把 密文 再进行一系列变换, 还原成 明文 .
>
> 在这个加密和解密的过程中, 往往需要一个或者多个中间的数据, 辅助进行这个过程, 这样的数据称为 密钥

## HTTP 的工作流程

① 引入对称加密
对称加密其实就是通过同一个 “密钥” , 把明文加密成密文, 并且也能把密文解密成明文.

> 例子: 现有 明文: 1111 密钥: 6666 加密解密过程通过: 按位异或
> A 将明文: 1111 通过 密钥: 6666 加密成 密文:2 发送给B
> B 通过密钥: 6666 对密文: 7773 进行解密 得到 明文: 1111

此时同时也引入了一个问题,当客户端把密钥进行明文传输的时候,也可能被别人截获,再次发送密文,别人就可以通过密钥获取到明文,那此时的加密就没什么作用了

![image-20220617153136828](E:\Typora笔记\图片\image-20220617153136828.png)

解决办法: 对密钥进行加密传输.

### ② 引入非对称加密

非对称加密要**用到两个密钥**, 一个叫做 “公钥”, 一个叫做 “私钥”
公钥和私钥是配对的. 最大的缺点就是运算速度非常慢，比对称加密要慢很多

此时也有一个问题,可能在获取的公钥就是假的.

![image-20220617153204503](E:\Typora笔记\图片\image-20220617153204503.png)

解决办法: 引入证书.

### ③ 引入证书

在客户端和服务器刚一建立连接的时候, 服务器给客户端返回一个 证书.
这个证书包含了刚才的公钥, 也包含了网站的身份信息

![image-20220617153226935](E:\Typora笔记\图片\image-20220617153226935.png)

> 当客户端获取到这个证书之后, 会对证书进行校验(防止证书是伪造的).
>
> 判定证书的有效期是否过期
> 判定证书的发布机构是否受信任(操作系统中已内置的受信任的证书发布机构).
> 验证证书是否被篡改: 从系统中拿到该证书发布机构的公钥, 对签名解密, 得到一个 hash 值(称为数据摘要), 设为 hash1. 然后计算整个证书的 hash 值, 设为 hash2. 对比 hash1 和 hash2 是否相等.如果相等, 则说明证书是没有被篡改过的.

## HTTPS 传输过程

1. 客户端先从服务器那边获取到证书.证书里包含了公钥.
2. 客户端对整数进行校检.
3. 客户端生成一个对称密钥,使用公钥对对称密钥进行加密,发送给服务器
4. 服务器得到这个请求后,使用私钥解密,得到对称密钥.
5. 客户端发出后续的请求,后续的请求都是使用这个对称密钥加密的.收到的数据也都是使用这个对称密钥解密的.