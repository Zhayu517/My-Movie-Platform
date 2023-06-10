# 基于Spring Boot的社区交流平台。包含电影，音乐和书籍的Java web应用

## 微生活
视频教程：https://www.bilibili.com/video/BV1VN411k7Ab/

个人主页： https://wsk1103.github.io/

详细的设计报告在文章后半部分

### 喜欢就点一下Star，谢谢亲的支持
### Java 1.8
### 框架：使用Spring Boot 集成Spring,Spring MVC,MyBatis(前期),Spring Data(后期)
### 数据库:MySQL 5.6
### 缓存:Redis 4.0
### 版本控制:Maven 3.5
### 页面解析框架:Thymeleaf
### 负载均衡:Nginx - 端口80(可有可无)
### 服务器:Tomcat 端口8080和8181(可以使用单个tomcat)
## PS：音乐来源-网易云；电影来源-豆瓣、猫眼；书籍来源-豆瓣(豆瓣接口不再对个人开放，故只剩音乐)

==================================================
##### 项目结构
    com.wsk.life
        aspect:切面应用
        bean:回显的实体类
            celebrity:json影人条目信息
            maoyan:猫眼
                cinema:json单个电影院信息
                cinemas:json多个电影院信息
                movie:json电影信息
        config:spring启动加载配置
        controller:链接控制
            webSocket:websocket相关配置和实现
        dao:Mybatis接口
        error:自定义异常处理
        music:网易云音乐
            bean:网易云音乐json解析类
            entity:数据库实体类
            service:操作数据库
            thread:线程相关
        pojo:电影相关的数据库实体
        redis:redis操作类
            impl:接口的实现
        service:电影相关的服务操作
            impl:接口的实现
        session:session存活时间配置
        springdata:网易云音乐spring data操作
            entity:网易云音乐的数据库实体类
        task:自定义的定时器
            entity:数据库实体类
            runnable:任务
            service:数据库相关操作
            tool:工具类
        token:token生成器
        tool:工具类
            bean:百度图片识别json结果
        write:文件读写操作
     resources
        mapping:mybatis相关的xml文件
        static:静态资源文件
            css:样式
            image:本地图片
            js:JAVASCRIPT
        templates:页面
            forget:忘记密码
            hot:热门电影
            information:个人相关信息详情
            movie:电影相关信息
            registered:注册
            setting:设置

### 1. 系统结构
![这里写图片描述](https://img-blog.csdn.net/20180618145939784?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
### 2. 业务流程
##### 客户端
![这里写图片描述](https://img-blog.csdn.net/2018061814533397?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
##### 管理员
![这里写图片描述](https://img-blog.csdn.net/2018061814544196?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
### 4. 数据库
（1）	数据库表汇总  
  数据库表汇总  

|名称 |	表名 |	注释 |
|:------:|:------:|:------:|
|管理员操作记录表|	adminaction|	记录管理员操作|
|管理员信息表	|admininformation|	记录管理员信息|
|书籍表	|book	|记录书籍、图书|
|户收藏表|	collectioncritic|	记录用户收藏的信息|
|说说评论表|	commentcritic	|记录说说的评论|
|举报信息表	|critic_report|	记录举报信息|
|点赞信息表|	goodcritic|	记录说说的点赞情况|
|积分来源表|	integralsource|	记录积分的来源|
|通讯信息表|	message|	记录用户之间的通讯|
|电影名称表|	moviename	|记录电影名|
|好友表|	myfriends	|记录用户之间的好友关系|
|任务表|mytask|	记录后台定时任务|
|任务错误信息表|mytaskerror|记录后台任务错误信息|
|任务日志表|mytasklog|记录后台任务运行情况|
|说说表|publishcritic|记录用户发布的说说|
|用户信息表|userinformation|记录用户的信息|
|用户信誉积分表|userintegral|记录用户的信誉积分|
|用户等级表|userlevel|记录用户的等级|
|用户密码表|userpassword|记录用户的密码|
|用户二维码表|userqrcode|记录用户的二维码|
|音乐专辑表|wangyialbum|记录音乐专辑|
|音乐信息表|wangyimusic|记录音乐信息|
|音乐歌手表|	wangyisinger|记录歌手信息|
### 5. 部分流程图
###### 5.1 用户登录  
![这里写图片描述](https://img-blog.csdn.net/20180618151312585?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
###### 5.2 发表说说  
![这里写图片描述](https://img-blog.csdn.net/20180618151357676?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
###### 5.3 欣赏电影，聆听音乐，阅读书籍  
![这里写图片描述](https://img-blog.csdn.net/20180618151524541?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
###### 5.4 用户信息互动  
![这里写图片描述](https://img-blog.csdn.net/20180618151617421?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
###### 5.5 管理管理用户，说说和举报审核  
![这里写图片描述](https://img-blog.csdn.net/20180618151652305?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
### 6 具体实现细节
##### 6.1 项目技术架构
##### 6.2 登录界面的实现  
![这里写图片描述](https://img-blog.csdn.net/20180618152722694?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![这里写图片描述](https://img-blog.csdn.net/20180618152801452?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![这里写图片描述](https://img-blog.csdn.net/20180618152827153?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
##### 6.3 首页的实现  
![这里写图片描述](https://img-blog.csdn.net/20180618152855194?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图17 首页界面  

##### 6.4 热门说说
![这里写图片描述](https://img-blog.csdn.net/20180618152914159?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图18 热门说说  

##### 6.5 用户之间的通讯
![这里写图片描述](https://img-blog.csdn.net/20180618152929210?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图19 用户通讯  

##### 6.6 用户个人中心设置
![这里写图片描述](https://img-blog.csdn.net/20180618152942219?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图20 个人设置中心  
##### 6.7 个人主页
![这里写图片描述](https://img-blog.csdn.net/20180618152953528?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图21 个人界面  

##### 6.8 我的说说，评论，收藏，点赞
![这里写图片描述](https://img-blog.csdn.net/20180618153010511?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图22我的说说  

![这里写图片描述](https://img-blog.csdn.net/20180618153024433?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图23 我的评论  

![这里写图片描述](https://img-blog.csdn.net/20180618153036438?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图24 我的收藏  

![这里写图片描述](https://img-blog.csdn.net/20180618153048773?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图25 我的点赞  

##### 6.9 说说评论
![这里写图片描述](https://img-blog.csdn.net/20180618153116148?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图26 评论界面  

##### 6.10 搜索
![这里写图片描述](https://img-blog.csdn.net/20180618153129753?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图27 搜索  

![这里写图片描述](https://img-blog.csdn.net/20180618153141333?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图28 电影搜索结果  
![这里写图片描述](https://img-blog.csdn.net/20180618153154244?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图29 电影详情  

![这里写图片描述](https://img-blog.csdn.net/20180618153204903?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

 图30 音乐搜索  
![这里写图片描述](https://img-blog.csdn.net/20180618153218155?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图31 图书搜索  

##### 6.11 音乐系统
![这里写图片描述](https://img-blog.csdn.net/20180618153230274?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图32 热门音乐  

##### 6.12 图书系统
![这里写图片描述](https://img-blog.csdn.net/20180618153243412?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图33 图书推荐  
![这里写图片描述](https://img-blog.csdn.net/20180618153256371?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图34 图书详细信息  

##### 6.13 查看正在上映的电影
![这里写图片描述](https://img-blog.csdn.net/20180618153309202?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图35 热映电影详情  
![这里写图片描述](https://img-blog.csdn.net/20180618153320165?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
图36 热映电影评论  

### 7 备注


### 首次启动项目
1. win系统安装Java 1.8 ， IDEA软件，MySQL数据库，redis，Nginx。
2. 打开MySQL，执行sql文件，将数据导入到MySQL中。
3. 将项目导入到IDEA中，构建为MAVEN项目。  
4. 配置Nginx文件，使其负载均衡。
4. 待项目构建完成后，运行redis和Nginx（或者跳过Nginx）。
6. 修改resource文件中的application.properties，配置其中的数据库信息
7. 修改com.wsk.movie.email.Send文件中的用户账号和密码信息。
8. 由于使用了百度提供的图片识别功能，所以需要修改com.wsk.movie.tool.AuthService中百度提供的clientId和clientSecret（或者直接注释掉该类）
8. 将image.rar文件解压到D:/image，这个文件是存放图片和敏感词的重要文件。
5. 运行com.wsk.movie.MovieApplication的main方法。
6. 访问localhost

---------------------
------------------
--------------------------
摘        要
随着日益增长的生活水平，越来越多的人们喜欢上了看电影、听音乐和阅读，并且在看电影、听音乐和阅读后，也会根据此时此景来“吟诗一首”，因此开发了此系统平台。该系统为一款旨在为用户提供一个寻找知己和抒发情感的平台。在本系统中，用户可以抒发观摩电影后、阅读书籍和聆听音乐后的情感，用户之间的信息交流和互动，电影、音乐和书籍的搜索后的看、听。管理员端可以监督管理用户，加强安全防护。 

后端为了提高性能和用户体验，该系统平台使用Spring Boot集合Spring，Spring MVC和MyBatis框架做基础，并且集成Spring Data框架，MySQL做数据持久化，Redis缓存提高速度，反向代理和负载均衡为Nginx，Dubbo分布式开发，服务器使用目前较流行的Tomcat。

前端使用Thymeleaf解析页面和使用HTML5和CSS3进行设计，应用jQuery实现了页面延迟异步加载。在样式上，遵循自己动手设计的原则，实现了动态效果等等。在用户操作上，尽量使用户进行最少的操作，而达到想要的目的。

关键词：“书影乐”系统  Spring  Java EE  Redis  Nginx 

Abstract
With the increasing standard of living, more and more people enjoy watching movies, listening to music and reading. They will also express feelings at this time when they watchg movies, listen to music and read. Therefore, this system platform was developed. The system is a platform designed to provide users with a way to find and develop their feelings. In this system, users can express emotions after watching movies, reading books and listening to music. Users can exchange information and interact with each other. Users can look over related informations online and listen to music and enjoy movie trailers when they search for movies, music and books. The administrator not only can supervise and manage users, but also strengthen security protection.

In oder to improve system performance and user experience, the platform not only uses Spring Boot to integrate Spring, Spring MVC and MyBatis frameworks, but also integrates the Spring Data framework. MySQL does data persistence, Redis cache which can improve system speed. And reverse proxy and load balancing is Nginx. Distributed development is Dubbo,  and server use the Tomcat which is popular at present. 

The front-end uses Thymeleaf to parse the web pages, and uses HTML5 and CSS3 for design it. jQuery realizes delayed asynchronous loading of the web pages. In style of the web pages and following the principles of designing by myself, I achieved dynamic effects and so on. In user operations, try to minimize the user's operations and achieve the desired purpose.

Keywords: Book,Movie,Music system;Spring; Java EE; Redis; Nginx; 

1前言
1.1研究目的与意义
随着日益增长的生活水平电影院的剧增，越来越多的人儿喜欢上了看电影、听音乐和阅读，并且在看电影、听音乐和阅读后，也会根据此时此景来“吟诗一首”。这个时候，一个“书影乐”系统就此而生了。有的时候人们发表说说只希望自己的好友看到，所以一个好友之间的应用也很重要；有的时候发表的说说希望得到大众的赞许，所以一个所有用户之间的应用也很重要。在这种情况下，“书影乐”系统就显得非常重要了。用户在看电影、听音乐和阅读之前，有时候想看看好友或者大众对某电影、音乐、书籍的评价和评论，就可以使用该“书影乐”系统。
目前许多软件或者应用只关注对电影、音乐和书籍主题的探讨，而忽略了个人、好友和大众之间的关系圈，使得用户体验比较低。因此，一个独立的、沟通的、微博类型的应用系统就能比较好的解决这些问题。
所以，为广大用户提供一个极具个性化的思想交流平台，不仅可以寻找同道中人，还可以促进好友之间的思想交融，碰撞出友谊的花火。
本系统为广大用户提供一个对电影、音乐和书籍的搜索和探讨，用户之间动态交流的平台。本系统以“用户即上帝”为本，在所有的设计上，都必须考虑用户体验，使用户能够在第一时间找到自己想要的，让用户感受到“无须出门，便知天下事”的乐趣。
1.2研究现状
目前，国内的情况比较多的是只做关于电影、音乐或者书籍之类的软件应用，例如优酷，酷狗和读书类等软件。这些软件平台功能单一，充斥着无穷无尽的广告，同时也缺少用户之间的交流互动，使用户无法寻找志同道合的好友，因此用户的体验也不是很好。另一方面，像豆瓣这种软件平台，功能繁杂，用户参差不齐，用户之间的交流也是少之又少，很多用户基本就只想看看某部电影或者书籍的评分而已，完全不理会其他，缺少了用户之间的互动。
另一方面，就技术来说，功能过于复杂，那么开发成本也就越高，功能过于单一，用户体验又不高。而且相比较与APP，APP的开发需要适应不同的手机系统，例如对于Android系统，开发人员需要使用Kolin，对于IOS系统，需要学习Swift或者OC。但是随着时代和技术的发展进步，Java做后台开发和HTML和CSS做前端开发，势必成为一个国际趋势。因为Java在性能和安全性上，优于其他的系统，特别是在Linux系统上，Java更是佼佼者。所以目前国内许多的大公司，例如京东淘宝，都是首选Java。因此使用Java开发一个系统平台，是非常可靠的。
1.3论文结构
第一章是前言，讲述本论文的研究对象——“书影乐”系统的研究背景，国内外研究现状和本论文研究的目的及意义，我们可以很明显的得出一个“书影乐”系统的出现，必会引领时代的潮流。
第二章是可行性分析，通过系统定义进一步对系统进行可行性分析，系统的可行性分析主要包括经济上的可行性、技术上的可行性、操作上的可行性和法律上的可行性。通过可行性研究，表明“书影乐”的实现是可行的。
第三章是需求分析，对系统的两个平台——客户端和管理端所需实现的各个模块和功能进行初步的分析。章节最后介绍了系统实现中使用到的工具及技术。
第四章是概要设计，在第三章中需求分析的基础上，对系统进行进一步研究，通过分析系统各功能需要用到的数据及数据间的关系，建立模型和设计数据库E-R图，并完成数据库表结构的设计。同时按业务功能对系统进行模块的划分，明确各模块所需实现功能。
第五章是详细设计，对概要设计进行细化，阐明系统的两个平台——客户端和管理端所具有的功能，并通过流程图展示各子平台的业务流程。
第六章是系统实现，展示系统的操作界面，对界面中各个部分的功能进行详细介绍，并说明具体的操作方法及操作注意事项。
第七章是结语部分，对该系统平台进行总结。

2可行性分析
2.1技术可行性
基于SSM的“书影乐”系统展示网站的技术能力主要有软件开发过程中所需要的技术保障，编程人员的技术，网站的管理维护等各个方面。
（1）软件开发过程中所需要的技术保障：目前Java开发语言所需要的IDE一般是eclipse和IDEA这2种，在使用上，IDEA的体验和开发速度明显是优于Eclipse的，所以开发人员需要购买IDEA开发工具。运用开发过程中所需要的编程语言和开发框架，例如Spring全家桶（Spring， Spring MVC，Spring Boot，Spring Data）, MyBatis, Dubbo等。
（2）软件以及硬件需求：与服务器，开发笔记本或者台式电脑，网络等硬件设备。使用Windows10系统和PowerDesigner，Tomcat，MySQL，Java，IDEA等应用软件。
（3）技术支持：目前，绝大部分的Java EE开发框架等十分成熟，并且开发人员的实力强劲，可以很轻易的便实现相应的插件或者框架。
终上所述，得出如下结论：该系统平台在技术上的实现的没有问题的。
2.2经济可行性
该系统主要用于用户及时感受的抒发，是一个非盈利的平台。为了提高用户的体验，不需要接入广告等经济来源的无关紧要的东西，完全是由开发人员设计的。在用户需要搜索信息资源的时候，即可以免费的搜索相应的内容，大大的提高了用户的体验，节约了某些不必要的人力资源和时间成本。
终上所述：该系统是经济上可行的。
2.3操作可行性
操作可行性的目的是使用户在使用该系统平台的时候，能够操作简单明了，并且用户体验高。所以在设计界面以及功能的设计时，非常充分的考虑到用户的习惯和爱好，使得操作简单，门槛低，数据信息丰富安全等。这一切的最终目的就是极大的提高用户体验。
因此得出结论：该系统平台可行。
2.4法律可行性 
本系统平台是一个基于免费和开源的框架上进行开发设计的，在法律上没有任何的侵权行为。
故，在法律上是可行的。
2.5可行性分析结论
可行性研究结论：可行。
可行性研究说明：通过以上各方面的分析，本系统平台的开发在技术、操作、经济和法律上，都是可行的。本系统旨在为广大用户提供一个极具个性化的思想交流平台，不仅可以寻找同道中人，还可以促进好友之间的思想交融，碰撞出友谊的花火。
3系统需求分析
需求分析就是要确定我们需要做什么，怎么做，做更好。需求对系统提出了较完整、准确、清晰和具体的描述，因此，我们需要去了解用户的需求，明确用户的需求，最终实现用户的需求，并且提高用户的体验。
3.1用户需求分析
本设计所开发的系统平台，旨在为用户提供一个极具个性化的思想交流平台。在设计上，使用Dubbo[1]提高容灾性，SSM[2,3]搭建框架构建后台，Tomcat是目前的主流开源服务器，担当该系统平台的服务器是不二之选[4]，Redis、NGINX[5]提高访问速率。前端使用HTTM5和CSS3进行相应的设计。本设计从用户和管理员这两方面入手。在用户这一方面，主要是提高用户体验和着重用户的情感交流；在管理员这一方面，主要是提高管理员监控用户的效率，对系统的安全进行适当的维护。
系统的机构化设计的使用的描述方式我们一般使用的是业务流程图。通过业务流程图我们可以很明确各个模块功能之间的交流。
该系统的客户端业务流程图如图1
![这里写图片描述](https://img-blog.csdn.net/2018061814533397?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
管理员客户端的业务流程图如图2
![这里写图片描述](https://img-blog.csdn.net/2018061814544196?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
3.2系统功能分析
建立一个用户可以自用评论电影的平台，通过Ajax局部刷新，遵循用户至上的原则，实现网站更人性化，具有更好的互动性。
	以下为总体设计需求
1233.13.2（1）通过手机号码注册登录账号
每个手机号码只可以注册一个账号，并且通过账号完善个人信息和浏览商品，发布商品等，注册时需要通过手机号码获取验证码进行验证才能注册。
（2）实现说说首页
首页主要是展示个人和好友所有发布过的说说，并且在首页可以进行其他很多的操作，例如发布说说，点赞说说，收藏说说，评论说说，搜索用户、电影、说说等等。基本所有的功能首页都有。
（3）个人信息
通过查看个人信息，可以选择关注或者取消关注，给其发私信，和举报该用户。在该界面，用户可以看到该用户的基本信息和标识为所有人的说说。用户可以直接在该说说上直接对用户进行关注或者取消关注和举报。
（4）搜索用户，搜索电影，搜索说说，搜索音乐，搜索图书
用户是使用搜索功能的时候，会自动为用户显示提示，提高用户的体验。并且支持模糊查询，在模糊查询的时候，为了提高查询速度，使用缓存。
（5）查看热门说说
直接显示所有的热门说说，排序规则为自己设计的一个算法，通过点赞数、评论数、收藏数进行加权分配，然后将结果显示出来。
（6）发表说说
发表说说后，可以通过选择该说说的标识，例如朋友圈或者所有人，如果是朋友圈的话，那么就只有好友之间才能看到，所有人就会被所有人看到。发表的说说还可以设置评论权限。
（7）关注好友，取消关注
用户之间的关注或者取消关注，通过关注好友，可以看到好友发布的信息，并且当好友发布的说说标记为朋友圈的时候，只有好友之间才能看得到。
（8）好友之间的通讯
好友之间可以互相发送信息，当用户登录后，如果有好友发送信息过来，则可以看到好友发送过来的信息，点击后就可以查看该信息，然后进行信息之间的交流。
（9）点赞说说
如果用户觉得某条说说比较有意思或者其他，就可以为该说说进行点赞，点赞的结果是人人都可以看到的
（10）收藏说说
如果用户觉得某条说说值得收藏，那么用户就可以将该说说进行收藏，收藏后就会被存储起来，用户就可以直接通过查看自己的收藏的说说，进而直接找到以前所收藏的说说。
（11）评论说说
用户可以直接对已经发布出来的说说进行评论，评论的结果是人人都可以看到的。
（12）聆听音乐
用户可以直接在线聆听应用，并且发表即时感受
（13）阅读书籍
用户在线查看书籍
（14）管理员端-用户管理
管理员可以直接查看或者通过搜索查看用户的相关信息，然后对该用户进行相应的操作，例如禁止该用户发布说说或者禁用该账号等等。
（15）管理员端-说说管理
管理员可以查看所有说说或者搜索特定的说说进行查看，然后对该说说进行相应的操作。例如删除该说说等等。
（16）管理员端-日志管理
管理员通过查看日志信息，可以观察用户的登录时间分布和用户动态分布等等。
（17）管理员端-举报管理
该系统有举报功能，被举报过的信息会由管理员进行审核，如果确实存在问题，则会被删除等。
（18）管理员端-个人信息
管理员修改个人信息，例如账号密码等等。

4概要设计
系统概要设计的目的是对系统平台进行相应的物理设计的阶段确定明确的开发任务和目标，最后进行总体设计[6]。完成各个模块的功能设计和绘制数据的处理流程。以下是对该系统平台的2个功能端进行分析：客户端和管理端。
4.1系统结构设计
系统涉及用户角色有“用户”和“管理员”。其系统模块图如图3显示：
![这里写图片描述](https://img-blog.csdn.net/20180618145939784?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dzazExMDM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
4.2功能模块设计
本系统可以分为以下几大功能模块：
1.2.3.4.4.1.4.2.（1）登录界面 
用户通过手机号码和密码进行登录，登录之后显示首页。当用户没有账号的时候，提示用户进行注册，从登录界面切换到注册界面，注册需要通过手机号码获取验证码，后台通过页面传递的手机号码，随机生成4位数的验证码并且缓存，之后通过发送139邮箱的方式发送到指定的手机，手机收取到验证码之后输入验证码提交，判断是否正确，正确则注册成功，失败则注册失败。用户注册完之后直接跳转到首页。
（2）个人主页
主页是显示好友和自己的所有说说的，用户自己也可以发布说说，负责显示说说信息，以及显示本网站的网站信息，导航栏负责跳转到各个页面，没有登录显示按钮可以让用户进行登陆和注册。已登录的用户显示用户名，并且可以发布说说，查看个人信息等。进入首页的时候，通过Ajax获取数据库中存在的说说数据集合，并且刷新页面的内容，点击说说之后跳转到用户详细信息模块。
（3）用户主页
显示个人信息，例如用户名、住址、生日、发布过的说说、爱好、简介等等，显示之后还需要支持对于数据进行修改，修改之后，要同步修改页面的信息，这需要用到Ajax进行数据的提交，并且进行页面的局部刷新。还有密码的修改，密码修改的时候，也需要使用到手机验证码。负责显示指定的说说详细信息，包括图片、点赞数量，收藏数量，所有评论等，当一个说说被点击之后，通过返回的id查询到这个数据集合，跳转到说说详细信息的页面，说说的发布者可以在下方查看留言，并且与其他评论者进行交流。将对应的信息显示出来，并且提供点赞，收藏等功能。说说详细信息下方显示其他用户的评论，并且已经登录的用户可以对这条说说进行评论，所有人都可以在下方查看留言。说说发布者可以在下方查看评论，最终与评论者进行互动。
（4）说说信息
负责显示指定的说说详细信息，包括图片、点赞数量，收藏数量，所有评论等，当一个说说被点击之后，通过返回的id查询到这个数据集合，跳转到说说详细信息的页面，说说的发布者可以在下方查看留言，并且与其他评论者进行交流。将对应的信息显示出来，并且提供点赞，收藏等功能。说说详细信息下方显示其他用户的评论，并且已经登录的用户可以对这条说说进行评论，所有人都可以在下方查看留言。说说发布者可以在下方查看评论，最终与评论者进行互动。
（5）搜索
每一个页面左中部都存在一个搜索输入框，用户通过输入模糊的说说、用户名、电影名，音乐，图书等信息，后台数据库通过查询过滤相关的信息，并且显示出来给用户查看，显示出来的说说点击之后可以显示说说的详细信息。在搜索的时候，会自动提示补全搜索信息。显示出来的电影可以直接查看电影的详情，然后直接到相应的网站进行电影观看。显示出来的用户可以直接查看该用户所有发布过的说说。搜索音乐可以在线聆听音乐，图书可以在线阅读。
（6）信息交互
通过给特定用户发送信息，然后实现信息之间的交流，就像微信，QQ等等。使用的原理是Websockt。
（7）账号设置
显示个人信息，例如用户名、住址、生日、发布过的说说、爱好、简介等等，显示之后还需要支持对于数据进行修改，修改之后，要同步修改页面的信息，这需要用到Ajax进行数据的提交，并且进行页面的局部刷新。还有密码的修改，密码修改的时候，也需要使用到手机验证码。
（8）我的评论，点赞，收藏
显示所有我评论过的说说，点赞的说说和收藏的说说，通过点击对应说说，就可以直接进入到该说说的详细信息，负责显示指定的说说详细信息，包括图片、点赞数量，收藏数量，所有评论等，当一个说说被点击之后，通过返回的id查询到这个数据集合，跳转到说说详细信息的页面，说说的发布者可以在下方查看留言，并且与其他评论者进行交流。将对应的信息显示出来，并且提供点赞，收藏等功能。说说详细信息下方显示其他用户的评论，并且已经登录的用户可以对这条说说进行评论，所有人都可以在下方查看留言。说说发布者可以在下方查看评论，最终与评论者进行互动。
（9）热门说说
通过设计算法，将属于热门的说说的展现出来。
（10）音乐系列
该模块包含3个小模块，分别为热歌榜单，飙升榜单和新歌榜单。进入相应的模块，既可以聆听相应的音乐。还可以查看音乐的信息和评论等等。
（11）图书系列
进入该模块后，系统会根据用户平时喜欢搜索、观看的数据类型进行相应的显示。
（12）管理员-用户管理
管理员可以直接查看或者通过搜索查看用户的相关信息，然后对该用户进行相应的操作，例如禁止该用户发布说说或者禁用该账号等等。被禁用的用户在登录的时候会显示相应的提示，第一次会禁止使用1天，第二次会禁止使用2天，第三次会禁止使用4天，依次类推，规律是2n-1（其中n为次数）
（13）管理员-说说管理
管理员可以查看所有说说或者搜索特定的说说进行查看，然后对该说说进行相应的操作。例如删除该说说等等。被标记的说说会扣除用户相应的人品积分。当人品积分被扣除到一定程度的时候，会被禁止使用。
（14）管理员-举报管理
该系统有举报功能，被举报过的信息会由管理员进行审核，如果确实存在问题，则会被删除等。然后扣除人品积分。
（15）管理员-日志管理
管理员通过查看日志信息，可以观察用户的登录时间分布和用户动态分布等等。然后维护人员可以更好的设置控制并发。
（16）管理员-个人信息
管理员修改个人信息，例如账号密码等等。

4.3数据库设计
数据库设计是组成系统的重要成分，其主要目的就是存放数据，将数据持久化。根据系统的需求我们可以设计出对应的数据库[7]。
12344.14.24.34.3.1 项目实体E-R图
本系统抽象出来的实体对象共计27个，由于数据库表的数量多，所以在这里只列出比较重要且有代表性的表，分别为用户信息主表，说说表，音乐信息表，管理员信息表和通讯表。具体有如下实体：
（1）用户信息表是整个系统的核心，包括用户id，地址，简介，生日，创建时间，标签，用户名，手机号码，性别，修改时间，头像。其E-R图如4所示：


图4 用户信息表 E-R图

（2）说说表
说说表是存放用户发表的说说内容，包含了id,说说内容，点赞次数，是否私有，附带图片，发布时间，说说标题，用户id，修改时间，是否禁用，附带的缓存图片地址，其E-R图见图5。


图5 说说 E-R图

（3）音乐信息表
音乐信息表是存放所有音乐的表，其中音乐是从网易云下载到服务器的，包含了id,歌曲id（对应网易云音乐id），歌曲名，歌手id（包含多个），专辑id，标签，播放地址，图片地址，其E-R图见图6。

图6 音乐信息 E-R图

（4）管理员信息表
管理员信息表是存放管理员信息数据，包含了id，管理员姓名，密码，电话，创建时间，修改时间，邮箱，住址，其E-R图见图7。


图7 管理员信息 E-R图

（5）通讯信息表
通讯信息表是存放用户直接信息的传递，包含了id，发送用户id，接收用户id，发送时间，信息内容，是否已读，其E-R图见图8。


图8 通讯信息 E-R图

4.3.2 数据库表设计
系统中用到了27个数据表，其中包括了管理员操作记录表，管理员信息表，书籍表，签到表，收藏信息表，评论信息表，举报信息表，点赞信息表，积分表，信息通讯表，电影名称表，好友表，任务表，任务记录表，任务异常表，说说表，用户信息表，用户信誉积分表，用户等级表，用户密码，用户二维码表，音乐专辑表，音乐信息表，音乐歌手表等。由于涉及的表数量过多，所以只列出几个较为关键的数据库表，分别为用户信息表，说说表，音乐信息表，通讯信息表和管理员信息表。
数据库表的设计思想主要是参考阿里巴巴的开发手册进行设计的，在性能上，建立了适当的索引，增强了查询速度，并且自己设计了许多的算法对后台数据的处理进行优化等等。

（1）数据库表汇总

表1 数据库表汇总
名称	代码	注释
管理员操作记录表	adminaction	记录管理员操作
管理员信息表	admininformation	记录管理员信息
书籍表	book	记录书籍、图书
户收藏表	collectioncritic	记录用户收藏的信息
说说评论表	commentcritic	记录说说的评论
（续上表）		
举报信息表	critic_report	记录举报信息
点赞信息表	goodcritic	记录说说的点赞情况
积分来源表	integralsource	记录积分的来源
通讯信息表	message	记录用户之间的通讯
电影名称表	moviename	记录电影名
好友表	myfriends	记录用户之间的好友关系
任务表
任务错误信息表
任务日志表
说说表
用户信息表
用户信誉积分表
用户等级表
用户密码表
用户二维码表
音乐专辑表
音乐信息表
音乐歌手表	mytask
mytaskerror
mytasklog
publishcritic
userinformation
userintegral
userlevel
userpassword
userqrcode
wangyialbum
wangyimusic
wangyisinger	记录后台定时任务
记录后台任务错误信息
记录后台任务运行情况
记录用户发布的说说
记录用户的信息
记录用户的信誉积分
记录用户的等级
记录用户的密码
记录用户的二维码
记录音乐专辑
记录音乐信息
记录歌手信息

（2）用户信息表，如表2所示。

表2 用户信息表
名称	代码	外键	主键	数据类型
用户编号	id	否	是	int(11)
修改时间	modify	否	否	datetime
用户名	username	否	否	varchar(50)
用户手机	phone	否	否	char(11)
用户简介	autograph	否	否	varchar(255)
用户标签	label	否	否	varchar(255)
用户住址	address	否	否	varchar(255)
用户生日	birthday	否	否	datetime
用户性别	sex	否	否	varchar(2)
用户创建时间	createtime	否	否	datetime
用户头像	avatar	否	否	varchar(255)

（3）说说表，如表3所示。

表3 说说表
名称	代码	外键	主键	数据类型
编号	id	否	是	int(11)
修改时间	modify	否	否	datetime
内容	critic	否	否	varchar(255)
点赞数量	good	否	否	int
是否私有	isPrivate	否	否	int
图片地址	picture	否	否	varchar(255)
说说标题	title	否	否	varchar(255)
发表用户id	uid	否	否	int
是否禁止	allow	否	否	int
缓存图片地址	thumbnails	否	否	varchar(255)

（4）音乐信息表，如表4所示。

表4 用户信息表
名称	代码	外键	主键	数据类型
编号	id	否	是	int(11)
音乐id	singid	否	否	int(11)
歌曲名	name	否	否	varchar(50)
歌手id	singerid	否	否	varchar(255) 
专辑id	albumid	否	否	int(11)
类型	alias	否	否	varchar(255)
播放地址	url	否	否	varchar(255)
图片地址	picurl	否	否	varchar(255)

（5）通讯信息表，如表5所示。

表5 用户信息表
名称	代码	外键	主键	数据类型
编号	id	否	是	int(11)
（续上表）				
发送用户id	uid	否	否	int(11)
接收用户id	fid	否	否	int (11)
发送时间	modified	否	否	datatime
信息内容	message	否	否	varchar(255)
是否已读	onread	否	否	int(11)

（6）管理员信息表，如表6所示。

表6 用户信息表
名称	代码	外键	主键	数据类型
编号	id	否	是	int(11)
修改时间	modified	否	否	datetime
管理员姓名	name	否	否	varchar(50)
密码	password	否	否	varchar(20)
手机	phone	否	否	varchar(11)
邮箱	email	否	否	varchar(255)
用户住址	address	否	否	varchar(255)
创建时间	createtime	否	否	datetime
性别	sex	否	否	varchar(2)

5详细设计
后台为了提高性能，使用了一些目前属于比较好的设计模式，例如工厂方法模式，代理模式，备忘录模式，单例模式等等。在分布式上，使用的是Dubbo框架。为了考虑Session共享，使用Redis来存储Session数据，因为Redis的性能非常高，所以在高并发下，性能并不会成为瓶颈。考虑到分布式，所以必须设置一个全局主键id策略。在全局主键id策略上，还是一样使用了Redis来生成唯一主键，因为Redis是单线程的，并且自增的步长可以自己设置，所以Redis并不会产生id冲突。
为了记录用户使用情况，应用了Spring的AOP进行日志记录。在用户每次访问API的时候，在这些API上添加AOP功能，将用户操作记录进相应的日志。为了防止用户因为某些操作不当而产生的错误码，导致后台直接将这些错误码反馈给用户，这个时候，就需要编写一个全局异常处理功能，当每次发生错误的时候，都会调用该异常处理，返回特定的错误信息，告知用户操作不当。
网站加载图片的时候，通常耗费的主要流量和影响速度的原因之一就是这个，所以后台使用Thumbnailator.jar里面的方法对图片进行适当的压缩，在前端显示的时候，主要显示的压缩后的图片，当鼠标移到图片上的时候，那么通过Ajax显示未被压缩过的图片的放大版。这样，既可以节省带宽，又可以提高用户的体验。
为了防止XSS攻击，在每次需要将数据存储到数据库的时候，都需要对文字信息进行过滤；对于CSRF攻击，使用的是表单token和验证码。并且用户有时候会重复提交，所以使用token防止用户重复提交。在密码加密算法上，直接使用MD5进行不可逆加密。信息过滤和反垃圾是目前一个比较主流的问题，使用的过滤算法是DFA算法进行敏感词过滤。
5.1用户登录
 用户需要验证密码才能登录[8,9]，密码是使用MD5进行加密的，所以如果入侵了数据库，也无法获取用户的原始密码。如果用户名密码匹配错误，则会相应的提示用户，如果用户被禁用了，系统也会提示用户。流程图如下：


图9 登录流程

5.2发表说说
用户登录登录后，即可以发布即时感慨，抒发己见，寻找志同道合的好友，一起品味。发布说说的时候，后台需要进行信息安全处理和过滤。只有合法的说说才能被发表。当然用户可以举报那些违规的说说或者违规的账号，后台一旦审核无误，会对被举报的用户进行相应的操作。

图10 发表说说流程

5.3欣赏电影，聆听音乐，阅读书籍
用户在线直接通过搜索功能进行相应系列的搜索或者按照系统的推荐算法[10,11]推荐合适的内容给用户，然后用户就可以在线愉悦身心，发表即时感慨。

 
图11 多功能操作流程

5.4用户信息互动
用户之间在线进行信息交流，后台会对这些信息进行相应的过滤和安全处理。实现这一机制的原理是使用WebSockt，WebSockt会一直和后台保持连线的状态，只要用户在线，该连接就一直都在，但是如果用户5分钟之内没有活动，那么该连接会被强制关闭，这个时候只能通过重新登录来重连WebSockt，这样设计的目的主要是为了防止后台连接数过大，导致后台内存溢出或者奔溃。用户之间的即时通讯的信息，必须要进行安全处理和敏感词过滤，这些安全方面的东西处理完成之后，才能将信息传达给接收人，接收人接收消息后，同样可以给发送人发送信息，流程是一致，或者直接关闭会话框，但是即时关闭会话框，如果收到新的消息，还是会提醒用户有信息。

图12 信息互动流程

5.5管理管理用户，说说和举报审核
每一个系统都是需要后台进行管理的，后台的职能就是数据的管理和维护，其主要目的是安全。通过管理每一个用户，每一天说说等等，实现了系统的相对稳定。管理员可以对用户进行审核，如果发现该用户存在违规或者违法的行为，管理员有权对其进行禁用的操作，当然，操作人员的这些操作会被记录在数据库的，以便后台查询。在说说维护这一方面，如果某条说说违规违法，管理员有权删除该说说。在用户举报方面，管理员的权利都是一样的。

6 系统实现
6.1软件开发说明
1234566.16.1.1核心开发技术介绍
（1）Spring Boot
Spring Boot 是基于Spring的全新框架，该框架的设计目的是简化新的Spring应用来搭建开发所需要的框架。该框架使用了特定的配置方式，因此，开发人员不需要编写重复的框架配置文件。我的个人理解是，Spring Boot并不是什么新的框架，而是一个集合体，集合了目前主流框架，并且默认配置了这些框架的使用方式。
总之，Spring Boot可以很轻松的创建Spring-powered，应用和服务，并且是以最小的麻烦创建的。它采用Spring平台的风格，以便新用户和现有用户可以快速找到他们的需求。
（2）Redis
Redis是一个开源的项目，使用的是内存数据结构存储，用作数据库和缓存。它支持5种数据结构，分别为String，hash，list，set，zset。Redis 了提供高可用性，并通过Redis群集实现自动分区。
总结：Redis是基于内存的非关系型数据库，支持多种脚本，其执行性能非常高，比MySQL快很多。并且Redis是单线程的，所以不需要担心数据冲突。
（3）SSM
SSM，即Spring + Spring MVC + MyBatis，是目前较为流行的一种Web应用程序开源框架。其中Spring是一个轻量级的IOC和AOP的容器框架。Spring MVC分离了Model，View和Controller，从而通过代码可以很容易的扩展和维护相应的功能。支持SQL查询、存储过程和高级映射的优秀持久层框架，就是MyBatis。
6.1.2　项目技术架构
本系统平台使用的后台操作系统为Windows 10，框架的搭建使用的是Spring Boot集成SSM和Dubbo ，服务器为Tomcat，负载均衡为Nginx，数据库使用MySQL，缓存为Redis，页面解析框架为Themyleaf和jQuery。开发工具为IntelliJ IDEA，该软件为付费软件，价格为$499/年，虽然看起来是贵了点，但是该软件开发速度和体验极佳。
6.2登录界面的实现
在浏览器的中间搭建一个登录表单，这样看上去非常的简洁，让人很舒畅。用户通过手机号码和密码进行登录，登录之后显示首页。当用户没有账号的时候，提示用户进行注册，从登录界面切换到注册界面，注册需要通过手机号码获取验证码，后台通过页面传递的手机号码，随机生成4位数的验证码并且缓存，之后通过发送139邮箱的方式发送到指定的手机，手机收取到验证码之后输入验证码提交，判断是否正确，正确则注册成功，失败则注册失败。用户注册完之后直接跳转到首页。
登录界面需要7个页面，第一个是登录界面，显示手机号码和密码的组件，并且需要底部添加注册按钮，以及忘记密码。第二个是注册界面，注册界面首先提供用户输入手机号码以及验证码，获取验证码的按钮，获取之后跳转到下一步，也就是输入密码界面。输入密码界面需要两次确认密码，输入确认之后就是跳转到首页。最后一个界面是忘记密码，同样通过输入手机号码获取验证码即可。
登录首页图14，可以记住账号密码然后一周内自动登录，使用的技术是Cookies。后台先获取该网页的Cookies，然后解析该Cookies，然后再验证用户账号密码是否正确，如果正确，则立刻跳转到登录成功的页面，并且将该用户的信息存储到服务器的Session中，方便以后的操作验证用户信息和判断用户是否是登录状态。


图14 登录首页

忘记密码界面如图15，通过手机获取验证码进行密码修改。手机验证码的发送使用的是本地自己服务器发出的验证码信息，将验证码信息存储到Redis中，便可以实现分布式共享。
注册账号的机制和忘记密码的机制的一致的。


图16 注册账号

6.3首页的实现
首页中包含的功能非常的多，例如导航栏必须要的，导航栏里面就包含了首页、热门、信息、设置等等。通过导航栏可以跳转到其他的页面。首页中可以发布说说，查看说说，查看我的点赞，我的收藏，我的评论，好友信息之间的交互，搜索电影、说说、用户等等。主页是显示好友和自己的所有说说的，用户自己也可以发布说说，负责显示说说信息，以及显示本网站的网站信息，导航栏负责跳转到各个页面，没有登录显示按钮可以让用户进行登录和注册。已登录的用户显示用户名，并且可以发布说说，查看个人信息等。进入首页的时候，通过Ajax获取数据库中存在的说说数据集合，并且刷新页面的内容，点击说说之后跳转到用户详细信息模块。
首页中还存在着许多的小细节，例如通过点击右下角的箭头可以直接返回顶部。点击说说右上角的“Ⅲ”还可以对说说进行操作，例如删除，转为朋友圈，添加关注，取消关注等等。并且当滑动条滑动到一定距离的时候，界面自动加载其他说说，极大的提示了用户体验。
首页界面如图17：


图17 首页界面

6.4热门说说
进入该界面的时候，后台会根据一个算法自动从数据库中选择被认为是热门的说说，然后展示给用户。
导航栏里面就包含了首页、热门、信息、设置等等。通过导航栏可以跳转到其他的页面。热门中可以发布说说，查看说说，查看我的点赞，我的收藏，我的评论，好友信息之间的交互，搜索电影、说说、用户等等。热门是显示所有说说的，用户自己也可以发布说说。负责显示说说信息，以及显示本网站的网站信息，导航栏负责跳转到各个页面，没有登录显示按钮可以让用户进行登陆和注册。已登录的用户显示用户名，并且可以发布说说，查看个人信息等。进入首页的时候，通过Ajax获取数据库中存在的说说数据集合，并且刷新页面的内容，点击说说之后跳转到用户详细信息模块。
热门说说界面如图18


图18 热门说说

6.5用户之间的通讯
在关注列表中，点击用户名，然后再点击“私信”，就可以与好友进行通讯，在通讯中，还可以通过点击用户名直接跳转到用户主页。用户之间的信息交互就和QQ一样，使用的原理是WebSockt。先将发送的信息存储到数据库中，并且标记为未读，当好友登录的时候，轮番查询数据库，如果有未读信息，则在导航栏的信息处显示有新信息，通过点击该信息，可以直接查看好友发送过来的信息，接着就可以发送信息回去，信息之间的发送是实时的，效率非常的高。
用户之间的通讯界面如图19

图19 用户通讯

当然，在信息互相发送的期间，还需要对信息中的敏感词进行过滤，过滤使用的算法是DFA算法，其中的敏感词会被替换成**。
6.6用户个人中心设置
进入到账号设计界面中，显示个人信息，例如用户昵称、手机号码、性别、生日、简介、住址等，显示之后还需要支持对于数据进行修改，修改之后，要同步修改页面的信息，这需要用到Ajax进行数据的提交，并且进行页面的局部刷新。
所有信息采用jQuery的EasyUI中的Accordion显示，标题显示信息，而底部内容则显示修改的组件，之后Ajax修改具体信息后需要将对应的新的内容，采用jQuery显示到标题中。
在修改密码的时候，还需要使用手机号码进行验证码核对。导航栏和侧边栏依旧集齐了很多完美的功能，并且实现了许多的小细节。
个人中心界面如图20


图20 个人设置中心

6.7个人主页
进入到个人主页的时候，如果该用户已经被“我”所关注，那么就可以通过点击“×关注”来取消关注，反正则可以通过点击“+关注”来添加关注，关注后就可以在“我的首页”查看到该用户发表的实时说说。在个人主页中，显示的是当前所在用户的所有说说，通过点击说说右上角的“Ⅲ”，可以快捷的对该用户、该说说进行操作，例如举报、取消关注、添加关注等等操作。
个人界面，在该界面可以很清晰的知道目前自己的发表说说的情况。

图21 个人界面

6.8我的说说，评论，收藏，点赞
直接查看我发表过的说说，可以直接对这些说说进行相应的操作。导航栏和侧边栏依旧集齐了很多功能，并且实现了许多的小细节。
在我的说说界面，用户可以直接对已经发表过的说说进行点赞，评论和收藏。如果我发布过的说说是属于所有人可见的情况下，还可以直接将该说说操作成只有好友可见。具体的操作方法是点击该说说上方的“Ⅲ”，在弹出的下拉菜单中，选择“转朋友圈”，那么这条说说就只有好友之间可以互相看到。
如果用户认为该说说不喜欢，那么用户可以直接删除该说说，操作同样是点击说说上方的“Ⅲ”，在弹出的下拉菜单中选择“删除”，操作后该说说就会被删除，删除的操作在后台中是多线程进行的，所以用户不需要等待。
我的说说界面如图22。


图22我的说说

查看我对哪些说说做出了评论，然后评论之间的互动。
在我的评论界面，可以查看到所有我以前评论过的说说及其评论，并且在该界面中，用户可以直接点击原来的那条评论，就可以进入到该说说的具体情况，在该具体情况的界面中，可以看到该说说的发布者的具体信息和该说说的所有评论，在该界面中，用户还可以继续评论该说说。
当用户任务说说的评论不合适或者不喜欢的时候，用户可以直接删除该评论。具体的操作依旧是点击对应说说上方的“Ⅲ”，在弹出的下拉菜单中，选择点击“删除”，既可以实现该说说的评论的删除操作。
删除操作过程中，是后台多线程操作的。在页面该评论是会被直接删除，使用的是jQuery删除div，然后后台多线程操作数据库。
我的评论界面如图23。

图23 我的评论

直接查看了我收藏过的说说，然后对这些说说进行操作。被我收藏过的说说，相应的位置会显示为绿色。
在我的收藏界面中，用户可以通过点击对应说说下方的“收藏”按钮，对该说说进行取消收藏操作，取消收藏操作后，在侧边栏的对应“我的收藏”的数字会对应进行“-1”操作。
说说被用户收藏后，该说说下方的“收藏”按钮中的字体会显示成绿色，取消收藏后，该字体会重新变回黑色。
在“我的收藏”界面中，用户还可以和往常一样，对说说进行各种各样的操作。如果该说说是用户自己本身发布的，那么该用户可以直接删除该说说等操作。如果该说说是其他用户发布的，那么该用户可以直接取消关注好友，或者举报该说说，查看该说说的发布者的信息等等。
在用户举报说说后，后台会记录用户的举报信息，然后管理员审核举报信息并进行相应的操作。
我的收藏界面如图24。


图24 我的收藏

查看我点赞过哪些说说，然后对这些说说进行相应的操作。如果被我点赞过的说说，相应的位置会变为绿色。
在“我的点赞”界面中，如果用户点赞了一条说说，那么在侧边栏中，“我的说说”这个位置后面的数字就会相应的进行“+1”操作，如果用户取消了点赞，那么进行的就像相应的“-1”操作。
用户点赞后的说说，在数据库中，相应的数据会进行“+1”操作，在热门的信息中，显示热门的说说主要是依靠该点赞的次数和发布的时间进行排序的。
其余的操作和在“我的收藏”界面介绍的功能是类似的。
我的点赞界面如图25。

图25 我的点赞

6.9说说评论
查看说说及其评论，然后对该说说进行评论，或者是评论之间的互动。只有当评论内容这个输入框有输入信息的时候，评论按钮才能被点击。
在用户评论说说的时候，后台会使用DFA算法对该说说进行敏感词过滤。该算法会将敏感词替换成**字符。
在该页面中，最上方显示的是该说说发布者的详细信息。如果该说说不是登录的用户本人，并且和用户不是好友关系，那么该说说的发布者的详细信息的头像下方会有“+关注”，“私信”和“举报”三个按钮。
说说评论界面如图26。

图26 评论界面

6.10搜索
搜索可以搜索说说、电影、用户、音乐和图书。在搜索的输入框输入信息的时候，会自动类似百度那样自动提示，极大的提高了用户体验。
搜索电影后，会直接跳转到所搜索电影的详情界面，在该界面中，可以直接查看该电影的详情，例如导演、主演、评分、简介等等，然后还直接在该页面直接进入到电影的播放地址。就是非常的方便，用户体验非常的高。在最下方，可以直接对该电影进行发表说说。非常方便。
在搜索用户的时候，支持模糊查询，会直接显示所有与搜索信息有相关的用户名，然后可以直接添加该用户为好友或者发送私信。
在搜索说说的时候，支持模糊查询，可以直接显示所有与搜索信息有相关的说说，搜索后，可以对说说进行操作，例如点赞，收藏或者评论等等。
搜索界面如图27。

图27 搜索

搜索电影“泰坦尼克号”结果如图28。


图28 电影搜索结果

 进入“泰坦尼克号”电影详情。

图29 电影详情

搜索音乐，搜索音乐的时候，如果数据库相应的查询结果数据大于5首，那么直接从数据库获取音乐，如果少于5首，那么访问网易云的API，再将查询的数据存到数据库和缓存。


 图30 音乐搜索
搜索图书，搜索图书使用的是豆瓣提供的免费API，如果数据库存在搜索结果大于5条，那么直接读取数据库的信息；如果少于5条，那么访问豆瓣提供的免费API，将结果展示给用户，并且后台使用多线程进行数据存储。
如图31 搜索redis关键字。


图31 图书搜索

6.11音乐系统
音乐系统包含了3个模块，分别为热歌榜单，飙升榜单，新歌榜单。
通过直接点击相应的链接就可以进入相应的页面。该页面的所有歌曲都是同步网易云音乐相应的功能。在该界面，通过点击相应的音乐，既可以实现在线播放。使用网易云音乐的时候，每次都需要对音乐进行解密，会比较耗时，所以后台会自动下载相应的歌曲到服务器，然后下次直接访问该服务器的音乐，实现了低耗时，并且使用了Redis缓存，在访问速度上也是有了一个质的飞跃。
在线音乐播放界面如图32。

图32 热门音乐

6.12图书系统
点击导航栏的“图书”，网页就会自动跳转到图书界面，在该界面中，图书的信息都是从数据库中读取的，而数据库的数据来源是豆瓣。用户每次搜索图书的时候，如果数据库搜索不到相应的信息，就会访问豆瓣提供的API，然后将对应的信息存储到数据库和缓存系统，以便下次访问的时候不需要再访问豆瓣API，加快了访问速度，提高用户体验。
在显示推荐书籍的时候，使用的是一个随机的算法，随机从数据库获取10本书籍，然后显示到页面中。因为使用的是随机算法，所以用户在每次点击的时候，都会显示不用的推荐书籍列表。
在该界面中，用户可以直接点击相应的书籍，然后进入到数据的详细信息界面查看相关的信息。




图33 图书推荐

点击相应的图书标题，可以查看该图书的详细信息。然后还可以对该图书发表说说，抒发即时感受。
在该界面中，包含的部分有书籍的中文名称，原作名词，作者，译者，评分，出版社，出版时间，页数，价格等信息。
其中还有具体的信息，书籍内容简介，作者简介和书籍的目录。通过这些信息，用户可以进一步的了解该书籍的信息。
在最底部，是发布说说的功能，该功能和首页中的发布说说功能是一致的。其中的书籍名称会被自动填充为当前书籍的名称，当然，这个是可以被更改的。
书籍具体内容如图34所示。

图34 图书详细信息

6.13查看正在上映的电影
在该页面中，可以查看正在上映的电影的详细信息，并且观看最新预告片。这些信息的来源是猫眼电影。通过解析猫眼电影提供相应的API，将数据展示给用户，并且将数据存储到数据库和缓存。用户在下次访问的时候，直接读取缓存或者数据库，提高响应速度和用户体验。
该页面包含了电影名，导演，主演，电影类型，电影是否是2/3D，地区，评分，上映时间等。
具体的内容有电影的简介，预告片和评论。其中评论分为热门评论和最新评论。
在预告片模块中，用户可以在线观看电影的预告片。在评论模块中，用户可以查看其他用户对这部电影的评论，或者自己发布属于自己的评论。 
电影详细信息如图35。

图35 热映电影详情

在这里，我们可以查看其他用户对该电影的即时感受，来查看该电影是否是自己喜欢的类型，并且寻找志同道合的朋友，一起碰撞出感情的花火。
在电影的评论模块中，分为热门评论和最新评论，这些评论都是从猫眼提供的API中获取得到的。其中热门评论是被点赞最多次的，也就代表着这些评论被大多数人所赞同。
在该模块中，用户名称是来自猫眼API中的用户，并不是该系统平台的用户，所以无法查看用户的具体信息。
当页面向下拉取到一定位置的时候，侧边栏的搜索功能模块会一直悬浮在一个固定的位置，这样设计的目的是可以使用户在任何地方都可以搜索自己想要的信息。
热映电影评论如图36。

图36 热映电影评论

6.14管理员查看所有用户
管理员登录后，可以查看所有用户的信息，然后对该用户进行相应的操作，例如禁用账号等等。该功能模块支持搜索用户。


图37 用户管理
6.15管理员查看违规说说和用户
管理员可以直接可以查看所有的说说，然后对说说进行审核，并且查看相应用户的信息，然后对说说或者用户进行操作。当然，该页面也支持搜索。


图38 信息审核

6.16管理员举报处理
管理在线查看用户举报的说说，然后进行审核操作。


图39 举报处理
7结语
该系统平台，适用的用户非常广泛，特别是喜欢社交和寻找志同道合的好友。通过使用该系统平台，在生活娱乐上，不仅可以分享实时的感受，还可以和好友一起引发共鸣。
在该系统平台的开发中，使用了目前比较流行的Spring Boot，Spring MVC，Spring，MyBatis，Nginx，Redis，MySQL等等，在学习和使用的过程中，使用框架确实能诶开发者带来开发和维护上的便捷，并且在系统的安全和性能上也有了相对的提高。通过本次设计开发，可以得出结论：该系统平台能够给用户带来一种美的享受的同时，还能保护好用户的信息，防止信息泄漏。
自己也有很大的收获，虽然我们可以用一些方法和技术来完成某一项功能，但是这种技术和功能是的代价却是许多重复性代码、难以维护和用户体验性不好，所以这是一种不值得我们去提倡和使用的。对于一个好的系统，并不仅仅是我们实现了功能就可以的，虽然实现功能在开发中是最基本的要求，但是良好的系统维护性、代码的可读性和优秀的用户体验是非常重要。一个系统的好坏，是可以让用户尽可能的少输入，达到最大化的利益。


参　考　文　献
[1]百度百科. https://baike.baidu.com/item/Dubbo/18907815[EB/OL]. 2017-11-9.
[2]百度百科. https://baike.baidu.com/item/spring/85061?fr=aladdin[EB/OL]. 2017-11-9.
[3]百度百科. https://baike.baidu.com/item/spring%20MVC/5627187?fr=aladdin[EB/OL]. 2017-11-9.
[4]刘光瑞. Tomcat架构解析[M]. 人民邮电出版社, 2017.
[5]苗泽. Nginx高性能Web服务器详解[M]. 电子工业出版社, 2013.
[6]杨开振,周吉文,梁华辉,谭茂华. Java EE互联网轻量级框架整合开发SSM框架(Spring MVC+Spring+MyBatis)和Redis实现[M]. 电子工业出版社, 2017.
[7](美)施瓦茨,(美)扎伊采夫,(美)特卡琴科. 高性能MySQL(第三版)[M]. 机械工业出版社, 2013
[8]David Flanagan. JavaScript权威指南(第6版)[M]. 机械工业出版社, 2012.
[9]达科特(Duckett J). Web设计与前端开发秘籍：HTML & CSS 设计与构建网站[M]. 清华大学出版社, 2013.
[10]布洛克(Joshua Bloch). Effective Java中文版(第2版)[M]. 机械工业出版社, 2009.
[11]Thomas H.Cormen,[美]Charles E.Leiserson,[美]Ronald L.Rivest,[美]Clifford Stein. 算法导论(原书第3版)[M]. 机械工业出版社, 2012.



致　　　　谢
世界真美好！



