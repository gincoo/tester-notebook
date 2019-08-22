# Jmeter 测试工具

## 环境

Jmeter 版本至少1.6以上.

## Jmeter 两种录制方法

### Badboy-录制

- 独立的测试工具

- 下载: http://www.badboy.com.au/

- 红色按钮录制
- 录制完成后点击工具栏黑色完成录制。选择“文件-->Export to Jmeter...”
- 打开Jmeter 工具，选择“文件”-->“打开”选择刚才保存的文件 .jmx 类型。
- 返回乱码的处理

### Jmeter 录制

![1566294573050](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566294573050.png)

![1566294371132](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566294371132.png)

#### 局域】网（LAN）设置端口要与代理一样

- 默认8080

### 执行顺序

![1566298058328](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566298058328.png)

### 断言，检查点

- 监视器 -->【响应断言】

### 两种参数化方法

- 前置处理器：添加 【用户参数】 
- 元件：【CVS Data Set Config】

### 使用函数助手

- 使用函数助手可以直接生成函数

### 集合点

- 定时器--> 【Synchronizing Timer】
- 注意集合点位置，要放在集合操作之前

- Number of Simulated Users to Group by: 多少个用户到达开始并发

### 检查点

- 添加【响应断言】，添加【断言结果】

- #### **断言持续时间**
  - **不能超过150毫秒**，则可以使用断言持续时间来判断

- #### 返回结果大小断言
  - 断言：【Size Assertion】

### 关联(动态关联)

- loadrunner 通过左右边界，正则。
- Jmeter 使用 正则，xpath（一般xml 比较多）

- ##### 步骤：
  - badboy 录制
  - 找出需要关联的请求(nav.pl)
  - 该请求-->后置处理器》正则表达式处理器》填入内容
    - 正则(.*)  ：【.】 代表任意字符，【\*】代表任意长度
    - 模板：如果前面正则表达式取了不止一个参数，那么这里需要制定参数组别，如果该参数为$1$,表示取得第一个值，$2$表示第二个值
    - 匹配数字：0随机；-1取所有值，以数组形式存储；1，2，3
  - 增加断言
  - 增加断言结果
  - 回放脚本查看是否正确

### 监控图表

- 相比 LoadRunner 稍弱
- 扩展插件
  - JMeterPlugin-Standard-1.2.0.jar包复制到 Jmeter 的 lib 目录下面的 ext 目录下面，重新启动 Jmeter 。
  - 需要将 【ServerAgent-2.2.1.zip】解压后目录及下面的文件复制到我们测试的服务器上，然后点击打开，默认端口 4444 
    - windows 下双击.bat 文件即可
    - 如果是 Linux  将 zip 包传到 linux 下，执行.sh 文件即可
  - JmeterPlugin下载地址：http://jmeter-plugins.org/downloads/all/
  - ServerAgent下载地址：https://jmeter-plugins.org/wiki/PerfMonAgent/
- 监听器 --》【jp@gc-PerfMon Metrics Collector】

![1566358700528](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1566358700528.png)

- 点击 Add Row



### Jmeter 性能测试

- 第一、需要了解被测系统的业务，包括具体业务，每个请求，每个请求参数的含义
- 根据预先设计的场景，进行测试，生成图表

### FTP 程序（文件传输协议）

- FTP 请求
  - Remote File
  - Local File

- 步骤
  - 线程组
  - ftp 请求缺省值（可有可无）
  - ftp请求（get/put 两种）
  - 如果有用户名和密码天上即可

### Jmeter 数据库 mysql

- mysql 驱动【mysql-connector-java.jar】

- 步骤

  - 【测试计划】加入 jar 包

  - jdbc 配置【JDBC Connection Configuration】

    - 一般通常只需填写 Database Connection Configuraion 内容

      - **Database URL**：数据库url，jdbc:mysql://主机ip或者机器名称:mysql监听的端口号/数据库名称， 如：jdbc:mysql://localhost:3306/test

      - **JDBC Driver class**：JDBC驱动 com.mysql.jdbc.Driver

        详细网址：<https://www.cnblogs.com/qianjinyan/p/10244345.html>

      - **username**：数据库登陆的用户名

      - **passwrod**：数据库登陆的密码

  - jdbc 请求

  - 响应断言，断言结果，查看结果树

- 如果需要实现同时多个不同的用户使用不同的SQL，可以通过把整条SQL 语句参数化来实现。例如把SQL 语句放在 csv 文件中，然后在JDBC Request 的 Query 中使用参数代替 ${SQL_Statement}

### Jmeter 分布式性能测试

- java 开发，耗内存，cpu ，所以大并发下还是需要分布式的
- 步骤
  - 关闭防火墙
  - 在需要运行 Jmeter 并作为负载生成器的机器上安装 Jmeter，并确定其中一台机器作为主 controller，其他的机器作为 agent。然后运行所有 agent 机器上的 jmeter-server 文件
  - 在 controller 机器的 Jmeter 的 bin 目录下，找到 jmeter.）properties 文件。修改文件中 【remote_hosts=...】改成我们 agent 压力机的 IP；
  - 启动 controller 机器上的 jmeter 应用，选择菜单》运行》远程启动来分别启动 agent ， 也可以直接选择【远程全部启动】

### Jmeter 监听器

- 种类繁多
- 常用的：
  - 断言结果
  - 查看结果树
  - 聚合报告
  - 用表格查看结果
  - 图形结果
  - aggregate graph 等等

- 指标分析 (Summary Report、聚合报告...)
  - Samples：本次场景中一共完成多少请求
  - Average：平均响应时间
  - Median：响应时间中值为 50%
  - 90% Line：90%响应时间
  - Min
  - Max （以上单位都是毫秒）
  - Error：出错率
  - Throughput：吞吐量
  - KB/sec 流量

#### jtl 文件分析 

- Jmeter 中，结果都存放在 .jtl 文件。这个文件可以提供多种格式的编写，而一般我们都是将其以 csv 文件格式记录
- 只需要选择某个监听器，点击页面中的 configure 按钮。建议勾选：Save Field Name, Save Assertion Failure Message；
- 以上设置后，此时保存下来 jtl 文件会有如下 
  - timeStamp 请求发出绝对时间
  - elapsed 响应时间
  - label 请求标签
  - reponseCode 返回码
  - responseMessage 返回消息
  - threadName 线程
  - dataType 数据类型
  - success 是否成功
  - FailureMessage 失败信息
  - bytes 字节
  - Latency 延迟
