

1. 







#### 简述http协议及常用请求头

#### 列举常见的请求方法

- GET (选择)：从服务器上获取一个具体的资源或者一个资源列表。 
- POST （创建）： 在服务器上创建一个新的资源。
- PUT（更新）：以整体的方式更新服务器上的一个资源。 
- PATCH （更新）：只更新服务器上一个资源的一个属性。
- DELETE（删除）：删除服务器上的一个资源。 
- HEAD ： 获取一个资源的元数据，如数据的哈希值或最后的更新时间。
- OPTIONS：获取客户端能对资源做什么操作的信息。

#### 列举常见的状态码

| 状态码 | 说明                                         |
| :----: | :------------------------------------------- |
|  200   | 请求成功                                     |
|  201   | 请求完成，结果是创建了新资源                 |
|  202   | 请求被接受，但处理尚未完成                   |
|  204   | 服务器端已经实现了请求，但是没有返回新的信息 |
|  301   | 永久重定向                                   |
|  302   | 重定向                                       |
|  304   | 资源未更新                                   |
|  400   | 非法请求                                     |
|  401   | 未授权                                       |
|  403   | 禁止                                         |
|  404   | 没找到                                       |
|  500   | 服务器内部错误                               |
|  501   | 服务器无法识别                               |
|  502   | 错误网关                                     |
|  503   | 服务出错                                     |

#### http和https的区别？

**http:**

1. 超文本传输协议,明文传输
2. 80端口
3. 连接简单且是无状态的

**https:**

1. 需要到ca申请证书,要费用
2. 具有安全性的ssl加密传输协议
3. 端口是443
4. https协议是有ssl+http协议构建的可进行加密传输,身份认证的网络协议,安全

#### 简述websocket协议及实现原理。

WebSocket用于在Web浏览器和服务器之间进行任意的双向数据传输的一种技术。WebSocket协议基于TCP协议实现，包含初始的握手过程，以及后续的多次数据帧双向传输过程。其目的是在WebSocket应用和WebSocket服务器进行频繁双向通信时，可以使服务器避免打开多个HTTP连接进行工作来节约资源，提高了工作效率和资源利用率。

它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话

http://www.ruanyifeng.com/blog/2017/05/websocket.html

#### django中如何实现websocket？

1. 

#### Python web开发中, 跨域问题的解决思路是?

8.请简述http缓存机制。

9.谈谈你所知道的Python web框架。

10.Http和Https的区别？

11.django、flask、tornado框架的比较？

12.什么是wsgi？

#### 列举django的内置组件

1. admin 后台管理
2. url调度器
3. 缓存机制
4. 信号
5. 中间件
6. 用户认证组件—auth模块

14.简述django下的(內建的)缓存机制

15.django中model的SlugField类型字段有什么用途

16.django中想要验证表单提交是否格式正确需要用到form中的那个方法A. form.save()B. form.save(commit=False)C. form.verify()D. form.is_valid()

17.django常见的线上部署方式有哪几种？

18.django对数据查询结果排序怎么做, 降序怎么做？

19.下面关于http协议中的get和post方式的区别, 那些是错误的?(多选)A. 他们都可以被收藏, 以及缓存B. get请求参数放在url中C. get只用于查询请求, 不能用于数据请求D. get不应该处理敏感数据的请求

20.django中使用memcached作为缓存的具体方法? 优缺点说明?

 21.django的orm中如何查询id 不等于5的元素？

22.使用Django中model filter条件过滤方法,把下边sql语句转化成python代码1.select*fromcompanywheretitlelike"%abc%"ormecount>9992.orderbycreatetimedesc;

23.从输入http://www.baidu.com/到页面返回, 中间都是发生了什么？

24.django请求的生命周期？

25.django中如何在model保存前做一定的固定操作,比如写一句日志？

26.简述django中间件及其应用场景？

27.简述django FBV和CBV？

28.如何给django CBV的函数设置添加装饰器？

29.django如何连接多个数据库并实现读写分离？

30.列举django orm 中你了解的所有方法？

31.django中的F的作用？

32.django中的Q的作用？

33.django中如何执行原生SQL？

34.only和defer的区别？

35.selectrelated和prefetchrelated的区别？

36.django中filter和exclude的区别

37.django中values和values_list的区别？

38.如何使用django orm批量创建数据？

39.django的Form和ModeForm的作用？

40.django的Form组件中，如果字段中包含choices参数，请使用两种方式实现数据源实时更新。

41.django的Model中的ForeignKey字段中的on_delete参数有什么作用？

42.django中csrf的实现机制？

43.django如何实现websocket？

44.基于django使用ajax发送post请求时，有哪种方法携带csrf token？

45.django缓存如何设置？

46.django的缓存能使用redis吗？如果可以的话，如何配置？

47.django路由系统中name的作用？

48.django的模板中filter、simpletag、inclusiontag的区别？

49.django-debug-toolbar的作用？

50.django中如何实现单元测试？

51.解释orm中db first 和code first的含义？

52.django中如何根据数据库表生成model类？

53.使用orm和原生sql的优缺点？

54.简述MVC和MTV

55.django的contenttype组件的作用？

56.使用Django中model filter条件过滤方法,把下边sql语句转化成python代码