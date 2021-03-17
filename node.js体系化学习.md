# node.js调试HTTP体系化学习

### HTTP基础概念

#### 请求

（具体在chorme =》 检查 =》network =》 headers =》request headers=》

​     view sourse 中查看）

  **组成**：

- **请求行**（背）： 

​                             请求动词  路径➕查询参数 协议名/版本

- **请求头**：

​                             host：域名、ip

​                             accept： text/html （表示想要接受的内容）

​                             content-type：请求体的格式

- **回车**（无意义 隔开）

- **请求体**（也就是上传内容）

 **细节**

三部分：请求行 请求头 请求体

请求动词：GET(获取内容)/POST (上传内容)/PUT/PATCH/DELETE等

请求体在GET请求中一般为空

文档位置在[RFC 2612 第五章](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)

**标准文档：RFC 2612**（搜索HTTP RFC 2612 中文）

js对大小比较敏感

---

#### 响应

**组成**

- 状态行（背）：

​                         协议名/版本 状态码 状态字符串

- 响应头：

​                           Content-Type ：响应体的格式

-  回车（无意义 隔开）

- 响应体

**细节**

   三部分：状态行、响应头、响应体

   常见状态码是考点

   文档位于 [RFC 2612 第六章](https://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html)

---

### 用curl构造请求

curl -v http://127.0.0.1:8888

**设置请求词**

​                                   curl -v **-X POST** http://127.0.0.1:8888

​                                   即将请求词设置为post，注意大小写

**设置路径和查询参数**

​                                   直接在url后面加                          

**设置请求头**

​                                   -H  ‘Name：value’ 或 --header ‘Name：Value’

​                                   比如你想看accept的值：

​                                 curl -v **-H 'Accept: text/html'**  http://127.0.0.1:8888

**设置请求体**

​                                   -d '内容' 或者 --data‘内容’

---

### 用Node.js读取请求

**读取请求词**

​                       request.method

**读取路径**

​                       request.url 路径，带查询参数

​                       path 纯路径，不带查询参数

​                       query 只有查询参数

**读取请求头**

​                        request.headers['Accept']

**读取请求体**

​                        不解释

---

### 用Node.js设置响应

**设置响应状态码**

​                            response.statusCode=200

**设置响应头**

​                            response.setHeader（"Content-type","text/html"）                        

**设置响应体**

​                            response.write(`内容`) 

​                            注意，是反单引号``

​                            内容可以追加

随笔：curl其实就是个没有页面的浏览器

---

### console.log 调试大法

 `console.log("path:" + path);`

 `console.log("path: === ./style.css")`

 `console.log(path === "./style.css")`

一行一行的path来试试

**第一** 测试path本身根目录： 

​                                  console.log("path:" + path);

**第二** 测试第二个path：

​                                  console.log("path: === ./style.css")

运行后会出现false，如下错误：

  ![](.\picture\6.png)                              

**第三** 找到错误后，看看究竟哪里错了：

​                                  console.log("path:" + path);

​                                  console.log("path: === ./style.css")

​                                  console.log(path === "./style.css")

 注意格式！！！，运行后会出现：

![](.\picture\7.png)

可以看到:

​                                  path：/style.css

​                                  path: ==== ./style.css

两者差别很大，将点去掉即可！

