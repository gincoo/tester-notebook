## LoaderRunner 第一天

### 1.1 性能测试基础

​	服务器端性能测试

#### 1.1 什么是性能测试的本质

- **基于协议模拟用户发出请求(业务的模拟), 对服务器形成一定的负载,来测试服务器的性能指标是否满足要求.**
  - 时间性能
  - 空间性能
- 与界面无关

### 1.2 性能测试分类

性能测试方法是通过模拟生产运行的业务压力量和使用场景组合,测试系统的性能是否满足生产性能要求.通俗的说就是要在特定的运行条件下验证系统的能力状态

特点:

1. 这种方法的主要目的是验证系统是否有系统宣称具有的能力
2. 这种方法要事先了解被测试系统经典场景,并具有确定的性能目标
3. 这种方法要求在已经确定的环境下运行

#### 1.2.1 负载测试

通过在被测系统上不断加压,直到性能指标达到极限,例如"响应时间"超过预定指标或某种资源已经达到饱和状态

特点:

1. 这种性能测试方法的主要目的是找到系统处理能力的极限
2. 这种性能测试方法需要在给定的测试环境下进行,通常也需要考虑被测是系统的业务压力量和典型场景,使得测试结果具有业务上的意义
3. 这种性能测试方法一般用来了解系统的性能容量,或是配合性能调优来使用

> 也就是说,这种方法是对一个系统持续不断的加压,看在什么时候已经超出"我的要求或系统崩溃"

#### 1.2.2 压力测试(强度测试)

压力测试方法测试系统在一定饱和状态下,例如 cpu,内存在饱和使用情况下,系统能够处理的会话能力,以及系统是否会出现错误

特点:

1.这种性能测试方法的主要目的是检查系统处于压力性能下时,应用的表现.

2.这种性能测试一般通过负载等方法,使得系统的资源使用达到较高的水平

3.这种性能测试方法一般用于测试系统的稳定性

> 也就是说,这种测试是让系统处在很大强度的压力之下,看系统是否稳定,哪里会出问题

#### 1.2.3 并发测试

并发测试方法通过模拟用户并发访问,测试多用户并发访问同一个应用,同一个模块或者数据记录时是否存在死锁或者其他性能问题;

特点:

1. 这种性能测试方法的主要目的是发现系统中可能隐藏的并发访问时的问题
2. 这种性能测试方法主要关注系统可能存在的并发问题,例如系统中的内存泄露,现成和资源争用方面的问题
3. 这种性能测试方法可以在开发的各个阶段使用需要相关的测试工具的配合和支持

#### 1.2.4 配置测试

配置测试方法通过对被测系统的软\硬件环境的调整,了解各种不同对系统的性能赢下给的程度,从而找到系统各项资源的最优分配原则

特点:

1. 了解各种不同因素对系统性影响的程度,从而判断出最值得进行的调优操作
2. 对系统性能状况有初步了解后进行
3. 用于性能调优和规划能力

#### 1.2.5 可靠性测试

在给系统加载一定业务压力的情况下,使系统运行一段时间,以此检测系统是否稳定

特点:

1. 检验是否支持长期稳定运行
2. 在压力下持续一段时间的运行(2~3天)
3. 测试过程中需要关注系统的运行状况



### 1.3 性能测试指标

#### 1.3.1 响应时间

​	![1563853353029](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563853353029.png)

WT: Web Server Time

AT: App Server Time

DT: Database Time

公式:网络传输时间+服务器处理时间

N1+N2+N3+N4+N5+N6+WT+AT+DT

不包含前端页面渲染时间,到浏览器受到请求后响应数据截止

#### 1.3.2 tps 

tps: 每秒处理的事务数 (transaction per second)

hps: hits per second

吞吐量:描述的时服务器的处理嫩里 Throughput

#### 1.3.3 资源利用率

- 在一定的负载情况下,服务器资源占用情况
- CPU 利用率
  - 不允许超过70-80%
  - 队列长度
- Mem (内存)利用率
  - 80%以下
  - 页交换频率-物理内存和虚拟内存之间交换的频繁程度
- 带宽利用率
  - 100 Mbps=12.5 MB/s
  - 1 Byte(字节) = 8 bit(比特)
  - 100 Mbps
- 如果资源利用率太小,造成资源浪费



#### 1.3.4 用户数

**并发用户数:**

- **在同一时间向服务器发送请求的用户数量**
- 与每秒的并发请求数不同,一定要确认需求的目的时并发用户数还是并发请求数.

理发案例: 同时进店理发顾客数-> **并发用户数**

从进店到完成理发时间-> **响应时间**

```
总结: 理发店类似服务器运行的程序
顾客: 从客户端发来的请求
由多个浏览器同时发送到服务器的任务:并发用户
服务程序处理一个浏览器请求的时间:平均事务响应时间,特点:随着并发用户的增加而增加
单位时间内服务程序完成客户端请求的数量->单位事务数
随着并发用户的增加而增大,当并发用户数量达到一定量后不再增加
```



### 2  性能测试流程

#### 2.1 需求分析

##### 2.1.1测试对象

1. 常用的
2. 核心的,重要的
3. 数据量,并发量

##### 2.1.2 确定性能指标

###### 2.1.2.1 吞吐量,TPS-服务器每秒处理请求数量

###### 2.1.2.2响应时间

1. 从浏览器发出请求,服务器处理,受到响应所需要的处理时间

###### 2.1.2.3 用户数

###### 2.1.2.4 资源利用率

###### 2.1.2.5 例子1:要求每天完成交易额2亿

1. 客单价:
   1. 200-500-以300计算
   2. 采用28定律换算得出,以24小时计算
2. 求每秒钟最大交易数-大概每秒最大交易数30个(如使用平均会小很多)
3. 2/8原则:80%的用户请求,集中在20%的热点数据上,或时间段;

###### 2.1.2.6 例子2: 每天8小时系统支持500万用户访问

1. 先分析流量分布,再根据2/8定律估算每秒请求: 500*0.8(80%用户访问量)/1.6小时(8小时20%)/3600秒=694次. (计算得出服务器需要支持694次,每小时的平均负载*4)
2. 500万再8小时内完成,500万/8*3600,(一般不采用,除非系统负载比较平稳/平均.这样算出的结果会偏小)

##### 2.1.3 测试场景

1. ###### 3.1 单一场景

   1. 登陆
   2. 注册
   3. 搜索
   4. 添加购物车
   5. 下单,支付

2. ##### 3.2 混合场景

   1. 用户使用场景
   2. 系统使用场景

#### 2.2 测试计划

1. 测试目标
2. 测试人员组织
3. 压测进度安排
4. 压力机
   1. 配置
   2. 要求
   3. 数量
5. 风险

#### 2.3 测试方案

##### 2.3.1 测试工具

1. LoadRunner- HP:ALM(缺陷管理工具)\QTP(自动化测试工具)
2. Jmeter

##### 2.3.2 测试环境

1. 数据库
2. 服务器
3. 架构设计
4. 有条件的情况下尽量和生产环境一致

##### 2.3.3 测试策略

1. 单一场景
2. 混合场景

##### 2.3.4 监控工具

1. Linux
   1. nmon
   2. rpc
   3. jvisualVm
   4. Spotlight
2. windows
   1. Spotlight
   2. perfmon.exe

#### 2.4 用例设计

##### 测试脚本

![1563857851033](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563857851033.png)

##### 场景设计

![1563857989462](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563857989462.png)

##### 测试执行

###### 脚本编写

###### 场景监控设计

###### 运行场景

###### 监控场景

###### 测试报告

#### 2.5 定位分析问题

##### 后端

1. 代码
2. 软件,数据库,应用该服务器
3. 硬件 

##### 前端

##### 网络

### 3 工具介绍

### LoadRunner  

##### 安装

- 完整安装必须要在 windows 下
- windows 只支持专业版和旗舰版(家庭版无管理员权限)
- 浏览器: IE 8/9【只支持IE9以下的浏览器】
- linux 不支持完整安装 LoadRunner，只可以安装其中的一个功能 -- Load Generator压力机

##### 组成 

- 三大组件
  - VuGen（Virtual User Generator）虚拟用户发生器，编写脚本
  - Controller 控制运行脚本
  - Analysis 分析器



## LoadRunner 三大组件

### 组件 -- VuGen

Web Tours 默认的浏览器打开文件

默认用户名: jojo , 密码：bean

录制时的浏览器如果是64位的系统，一定要选择program file(x86)下面的 ie 浏览器

VuGen 的脚本分为三个部分：Vuser_init,Action,Vuser_end。其中Vuser_init和Vuser_end 都只能存在一个，而Action 可分成无数多个部分，可以通过点击旁边的[new]按钮来创建Action,在迭代执行测试脚本时，Vuser_init和Vuser_end 中的内容只会执行一次，迭代的是Action部分。

#### 录制脚本不同级别的却别：

Options->Recording Options ->Recording

- HTML

  - 第一个选项：

    所有的连带请求都以一个函数的形式来处理，根据动作不同来区分。（按照页面内容来操作生成的脚本）

  - 第二个选项：

    相比第一个选项的函数数据内容会更多一点。（以接口请求数据来封装）

- URL

  - 因为请求网址的时候会有很多连带接口请求
  - URL的方式，会将每一个的接口请求的 URL ，都单独用函数的形式封装起来

### 组件 -- Controller 

Tools->Create Scenario

- Goal Oriented Scenario:目标场景
- Manual Scenario：手工场景
  - Number of Vusers：虚拟用户数量
- Load Generator：压力机
- Group Name：脚本名称
- Result Directory：结果目录

#### 打开 Controller 页面：

##### Design

Global Schedule：全局清单

- Initalize：初始化运行 脚本中的 vuser_init() 部分
- Start Vusers：
  - EditAction 配置虚拟用户相关内容
    - simultaneously：同时加载所有用户
    - 每隔一段时间加载用户
- Duration: 持续运行 Action() 脚本时间
- Stop Vusers: 运行 vuser_end() 脚本部分

##### Run

开始--->停止--->Result 菜单--->Analyze Results

 Start Scenario：开始运行场景

###### 四张表

Running Vusers -- whole scenario

Trans Response Time -- whole scenario

Hits per Second -- whole scenario

Windows Resources -- Last 60 sec

###### Stop 停止后

### 组件 -- Analyze Results  -- 分析器

Reports :报告

- summary report ：概要报表

Graphs：图表

- Running Vusers:
- Hits per Second：每秒命中
- Throughput：吞吐量
- Transaction Summary：事务摘要
- Average Transaction Response Time：平均事务响应时间

action 与 Controller 中场景运行策略间的对应关系



## 案例分析

#### 案例1：

如果性能测试只测试订票的过程的响应时间，如何开发脚本？

- 将登陆和退出的脚本放在init 和 end 当中，具体想要测试的放在Action  脚本中

#### 案例2：

上面的订票过程我想把订票过程分别计时怎么办？



# day2

Vuser菜单--->Runtime Settings:

- RunLogic: 迭代次数：Generate Run Logic
- Pacing 运行脚本的节奏控制时机：
  - As soon as the previos iteration ends:一旦previos迭代结束
  - After the previous iteration ends:在上一次迭代结束后
  - provided that the previous iteration ends by that time:前提是上一次迭代在那个时候结束

-  Log
  - Send messages only when an error occurs :出错的时候才出现日志
  - Always send messages: 总是有日志
  - Extended Log ：扩展日志
    - Parameter substitution：将参数输出到日志中
    - Data returned by server ：服务器返回：将服务器返回给客户端的数据输出到日志文件中
    - Advanced trace：高级：所有的虚拟用户信息和函数调用输出到日志文件中
- Think Time
  - Ignore think time : 忽略等待时间
  - Replay think time ：
    - As recorded 与录制时间一致
    - Multiply recorded think time by :原有时间的倍数
    - Use random percentage of recorded think time:使用录制时间的随机百分比范围
    - Limit think time to xx seconds ：具体设定
  - 作用：更加真实的去模拟用户操作之间的延迟
- Preferences 参数选择
  - checks：启用，关闭图片和文本检查
  - Generate Web performance graphs：生成Web性能图
  - Advanced 高级的

- Miscellaneous:多线程的

  - Error Handling

  - Multithreading

    - **进程**方式运行虚拟用户

      - 进程独享一块内存，比较稳定，大约占用4M以上
      - 内存资源浪费，可以模拟的虚拟用户少

    - **线程**方式虚拟用户

      - 线程之间共享一块内存们可以模拟的虚拟用户多，大约占用1M~2M
      - 线程之间容易发生资源竞争，出现进程阻塞不稳定


### 学习函数

#### web_url

- 作用：模拟浏览器发出 get 请求 
- 用法：
  - 步骤名称：”访问首页“
  - 请求地址：”URL=http://www.baidu.com“ ，通过抓包或接口文档获取
  - LAST);

#### web_submit_data()

- 作用：模拟浏览器发出 get/post 请求
- 用法：
  - 步骤名称
  - 请求地址：”Action=http://www.baidu.com“,
  - 请求方法："Method=POST"  ，(只支持get 和post)
  - 请求模式："Mode=HTTP/HTML",
  - 表单数据Data: 抓包工具获取
    - ITEMDATA，”Name=xxx“,"Value=xxx",ENCITEM
  - LAST);

> 在编写脚本时候**点击菜单Insert** -->New Step-->Add Step:提供了非常多的函数

#### web_custom_request() （重点）

- 作用：模拟浏览器HTTP 支持的任何方式的请求
- 比上面用法多了一个Body 请求正文
- 注意：函数中mode 为http时，Test-results 中看不到浏览器中的页面

IShop 案例 使用XAMPP Control Panel v3.2.1

### 参数化设置

如何让很多不同的用户名密码的用户进行登陆？

- 让脚本使用批量的变化的数据测试，实现模拟不同数据/用户的行为

>  自动化思想：数据和代码分离

##### Parameter List:

--->New--->

脚本中右键所需参数：-->Replace with a Parameter :选择参数名称

`”Value={username}“`

获取变量值` lr_eval_string("{username}")`

输出log取到的用户名的值：

```
lr_output_message("获取到的值为:",lr_eval_string("{username}"))
```

双击选中函数按 ***F1*** 可以查看 API

多次操作才会取多个参数

- Select next row:  顺序
  - Squential 顺序
  - Random 随机
  - Unique 唯一
  - Same line as xxx

- **【A】**Update value on：

  - Each iteration 每次迭代时。
  - Each occurrence 每次发生时。（每次取值时）
  - Once 每次都一样

- **【B】**When out of values：当超过值的最大数量时候

  - Abort Vuser：中止 Vuser
  - Continue in a cyclic manner：以循环方式继续
  - Continue with last value：继续最后一个值

- Allocate Vuser values in the Controller：在控制器中分配Vuser值

  > 例子：10个数据，2个用户平均最多5次

  - Automatically allocate block size：自动分配块大小
  - Allocate [xxx] values for each Vuser：为每个虚拟用户分配

- #### A1B1：每次迭代内取值不变，下一次迭代才换值

- #### A1B2：每次取值取下一个值

- #### A1B3：值不变

- #### A2B1：每次迭代才会取随机取值，一次迭代内的都是一样的值

- #### A2B2：每次取值都会随机取

- #### A2B3：每次发生随机取值，之后本次脚本执行内永远不变。下次执行脚本才改变

- #### A3B1：每次迭代，唯一取值，迭代内值不会重复

- #### A3B2:.....见 思维导图



#### 跨 Action 可共同使用参数,但不可共同使用变量



#### 

输入用户名和密码进行登陆:

- 需要实时的获取上一个请求的响应数据终得userSession 对应的值，放到登陆的请求数据中即可
- 实时取值的方式：关联

- 需要实时的获取上一个请求的响应数据中的userSession 对应的值,放到登陆的请求数据中即可
- 如果知道如何取值那么就可以实现登陆成功
- **实时取值的方式:【关联】**

- 该关联函数：带有reg字样，凡是带有reg字样的函数我们都成为注册型函数

- 注册型函数的特点：哪一个请求响应数据中，有我们需要的数据，那么该函数就放在请求的前面，放在web_url() 请求函数的前面。中间不能有其他函数。

- **web_reg_save_param() 关联函数**，取匹配相关参数session

  ![1566188925285](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566188925285.png)

   

#### 高级关联

```
高级关联使用时：将Instance:设置为all。取到的就是数组
lr_paramarr_idx("fights",4);
lr_paramarr_len()//获取值的数量
lr_paramarr_random()//获取数组中的随机一个元素

char * str;
str = lr_paramarr_idx("fights",4); //变量定义必须放在首行
//str 的值为字符串，而非参数，所以不能直接将字符串放入下面的代码中
lr_save_string("helloworld","aaa");//将helloworld放入参数 aaa 中

注意：关联和具体代码中间不能有代码

```

#### 事务

duration:0.4678 Wasted Time:0.0077

实际事务时间=duration 持续时间 -waster time 浪费的时间

```
lr_end_transaction("login",LR_AUTO);//在这里LR_AUTO判断的是服务器的返回状态码，而并没有判断该业务是否成功
内部实现：
code = web_get_int_property(HTTP_INFO_RETURN_CODE)
//PASS：通过。FAIL：错误。
if(code==200){
    lr_end_transaction("login",LR_PASS);
}else{
    lr_end_transaction("login",LR_FAIL)
}
```

##### web_reg_find() 解决方案：

- 通过添加检查点的方式来验证业务是否成功，如果存在要检查的内容那么就给一个状态 LR_PASS,否则给 LR_FAIL。
- 检查点函数：web_reg_find()---->带有 reg 的为注册型函数---
- 特点：如果某一请求的响应数据中有想要的数据，就将该函数放在请求前面。

![1566199056875](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566199056875.png)

- 生成的检查点函数：

![1566199122647](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566199122647.png)

方法：

```
if(atoi(lr_eval_string("{number}"))>0){//atoi字符串转证书
    lr_end_transaction("login",LR_PASS);
}else{
    lr_end_transaction("login",LR_FAIL);
}
```

- atoi()字符串转整数
- itoa()整数转字符串

##### Create Scenario 创建。多虚拟用户模拟数据

- Select Scenario TYpe
  - Manual Scenario。

选择脚本

**web_reg_find  函数和 web_find 普通函数的区别；**

使用时，必须启用image and text checks图片和文本检查项

不建议使用。

```
web_find("web_find","LeftOf=,"What=Welcome,jojo",LAST)
```

#### 思考时间

`lr_think_time(秒数)`

### 压力曲线分析图（重点）

![1566206457793](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566206457793.png)

纵轴：

- Utilization: 服务器资源  （内存，CPU）
- Throughput: 吞吐量
- Response：响应时间

横轴：

- 用户并发数

#### 曲线图主要分三个区域：（不断加压的过程，看它的变化情况）

- light load：轻压力区。（用户数和纵轴资源等正比）
  - 并发测试区
- 第一个拐点（最佳用户并发点）
  - 最佳并发用户点
  - 在这个点之前可以做并发测试
  - 吞吐不再明显增加
  - 请求数也不再变了

- heavy load：重压力区。
  - 服务器处理不过来那么大量的请求，需要等待，但服务器还没挂
  - 压力测试区
- 第二个拐点。（最大并发用户数点点）
  - 逐步的加压
  - 达到最大并发用户数
  - 超过服务器就崩掉
- buckle load：（第二个拐点）
  - 随着并发用户数增加，响应时间急剧增长，服务器已经无法处理。吞吐量降低，服务器崩溃。

**通过 Controller 负载测试来找以上的各个拐点**，前提脚本没有问题。



#### Controller 并发控制时

- Duration 和 Iteration 迭代次数都有值的情况下，按Duration 走

- Details-->Group Information

  ![1566208251799](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566208251799.png)

  - View Script
  - RUnTIme Setting
  - Refresh 
    - 脚本
    - 运行时设置



##### 压力机查看：

![1566208288980](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566208288980.png)

![1566208209239](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566208209239.png)

- add 可添加新的压力机：
  - Name: 192.xxxxx目标电脑机器 IP 地址。
  - 如果目标地址有loadrunner 就能链接上
  - 出现Failed原因：目标机器需要开启压力机代理:
    - 开始菜单 ：HP LoadRunner--> Advanced Settings --> LoadRunner Agent Process
  - 

##### Global Schedule :

- 增加：逐步增加并发用户（防止服务器崩溃）
- 结束：逐步减少并发用户

## Day-05

#### New Scenario

Select Scenario Type

- Manual Scenario
  - Manage your load test by specifying the bumber of virtual users to run
  - Use the Percentage Mode to distribute the Vusers among the scripts
- Goal-Oriented Scenario
  - Allow LoadRunner Controller to create a scenario based on the goals you specify

#### Controller 场景策略方案

#### 联机负载

Scenario--> Convert Scenario to the Percentage Mode:转换场景到百分比模式

ctrl+H 替换

调整百分比模式后,可以多台机器压测服务

#### IP 欺骗

问:每一个虚拟用户的 IP 是多少?

有些网站不允许多用户同一个IP连续访问,所以需要 IP 欺骗.

控制面板-> 本地连接-->Internet 协议-->高级 TCP/IP 设置;这里添加IP.

为每一个用户分配 IP

#### IP wizard

![1566276716817](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566276716817.png)

保存写入IP:

![1566276800607](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566276800607.png)

然后可以在本地链接--> 网络链接-->详细信息或者高级可以查看设置的IP地址。

##### Enable IP Spoofer 启用 IP 器件

Tools--> Export mode 打勾启用专家模式。

#### 图表监控

对应图表-->右键选择 Add Measurements：

Add 输入服务器IP地址：

![1566278645074](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566278645074.png)

常见的：

![1566278755718](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566278755718.png)

#### vuser-hits-hps-rt-throughput

- hits/s 并发数，

- tps每秒钟通过事务数



#### 添加服务器资源监控时，系统提示：

```
Monitor name :windows Resources.Cannot connect to machine Reason 拒绝访问：
解决方法：
1.运行中输入 services.msc 打开服务对话框，开启
Remote Procedure Call(RPC)、
Remote Procedure Call(RPC) Locator
Remote Registry
WMI Performance Adapter、Workstation 服务
2、打开组策略 gpedit.msc，进入目标机的”计算机配置“--windows配置--安全配置--本地策略，选择并点击”安全选项“，把”策略“中的”网络访问：本地在港元的共享模式和安全模式“修改成”经典-本地用户自己的身份验证“
3、i将目标服务器c$实现共享：在cmd命令行中执行：net share c$=c:
4、在测试计的”运行“中输入：\\目标机IP\c$，点击确定后，要输入目标及的用户名和密码，查看是否能看到共享磁盘c$,（如果不可以则使用命令符cmd 输入net use \\IP地址\ipc$ /user:administrator *** (监控的主机必须和服务器建立$ipc连接)）

```

### Analysis 分析

![1566285208963](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566285208963.png)

- 吞吐率与实际网络贷款作比较
- Totoal Hits: 请求数
- Average Hits per Second: 每秒钟的请求数

![1566285190327](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566285190327.png)

- 响应时间与不懂得人看平均值。
  - 给技术员运维人员看懂得人看大部分在哪个时间点内，不看平均值

- 90 Percent 给技术员看，
  - 可以通过View->Filter 过滤修改值、

图表右键都能够过滤









