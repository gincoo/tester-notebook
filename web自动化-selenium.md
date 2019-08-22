自动化:由机器设备代替人为自动完成指定目标的过程

自动化测试:由程序代替人为去验证程序功能的过程

为什么要进行自动化测试?

1. 解决-回归测试
2. 压力测试
3. 兼容性测试
4. 提高测试效率,保证产品质量

什么阶段开始自动化测试?

功能测试完毕(手工测试)

手工测试:就是由人去一个个输入测试用例,然后观察结果;

自动化测试所属分类(代码可见度)

1. 黑盒测试
2. 灰盒测试
3. 白盒测试

**提示: Web 自动化测试属于黑盒测试(功能测试)**

优点:

1. 较少时间内运行更多的测试用例
2. 自动化脚本可重复运行
3. 减少人为的错误
4. 测试数据存储

缺点:

1. 不能取代手工测试
2. 手工测试比自动化测试发现的缺陷更多
3. 测试人员技能要求

#### 3. 自动化测试分类

1. Web(UI)自动化测试
2. 接口-自动化测试
3. 移动(app)-自动化测试
4. 单元测试-自动化测试

![1563269345382](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563269345382.png)

什么Web 项目适合做自动化测试?

1. 需求变动不频繁
2. 项目周期长
3. 项目需要回归测试

如何进行 Web 自动化测试?

1. QTP(收费)
2. Selenium (开源)
3. Jmeter(开源,Web,接口,性能)
4. LoadRunner(收费.Web,性能)
5. Robot framework 基于Python 可扩展的( **关键字驱动**) 自动化测试框架

主流工具-汇结:

Web 自动化测试:selenium,robot framework

App端:Appium MonkeyRunner,UIautomation

PC(win32):QTP

接口:Jemeter,Postman,HttpUnit,RESTClient

云平台:Testin Testbird

性能测试: Jemeter,LoadRunner

#### Selenium 特点

1. 开源
2. 跨屏图
3. 多个浏览器测试
4. 多语言
5. 成熟稳定 google 百度 腾讯 都在用
6. 功能强大

#### Selenium 家族

**Selenium Grid 分布式测试,超大规模测试**

**重点:**

1. Selenium IDE
2. Selenium2.0(WebDriver)



#### Selenium IDE 安装与运行

Selenium IDE :是一个 Firefox 插件,用于记录和播放用户与浏览器的交互.(录制 Web 操作脚本)

为社么要学习?

安装地址: 

Version: 2.9.1.1

https://addons.mozilla.org/en-GB/firefox/addon/selenium-ide/versions/

火狐浏览器地址:

下载地址：

- Win版：<http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/35.0.1/win32/zh-CN/Firefox%20Setup%2035.0.1.exe>
- MAC版：<http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/35.0.1/mac/zh-CN/Firefox%2035.0.1.dmg>
- Linux版：<http://ftp.mozilla.org/pub/mozilla.org/firefox/releases/35.0.1/linux-x86_64/zh-CN/firefox-35.0.1.tar.bz2>

运行: Ctrl+Alt+S

35 版本兼容性最好

 #### 定位调试软件

##### FireBug 重要

​	FireBug 差价事火狐一款插件,能够调试所有网站语言,同时也可以快速定位HTML 页面中的元素;

作用:定位元素

**Selenium IDE 提示**

> 录制脚本时候是录制鼠标和键盘的所有再浏览器操作,那么脚本会出现多余的步骤,有时候我们需要手动填写脚本或修改脚本,所有我们有必要对Selenium IDE 脚本编辑与操作有所了解;

#### Selenium IDE 脚本编辑与操作【了解】

目的：手动修改或编写脚本（采用录制方式很容易记录出多余的操作）

单机click 是没有值

##### 编辑一行命令

##### 插入一行命令

右键鼠标 “insert new command” 插入一条新的命令

##### 插入注释 

右键“insert new comment” 插入注释，紫色字体

##### 命令执行

> 选定要执行的命令点击单个执行按钮即可，注意：有一些命令必须依赖于前面命令的运行结果才能成功执行，否则会导致执行失败

#### 4. Selenium IDE 常用命令[了解]

##### 4.1 open(url)命令

作用:打开指定的URL ,URL 可以为相对或是绝对URL

Target:要打开的URL;value 值为空

1. 当Target 为空,将打开Base URL 中填写的页面
2. 当Target 不为空且值为相对路径,将打开Base URL +Target 页面.如,假设 Base URL 为 http://www.zhi97.com, 而Taget为/about.aspx,则执行open命令时,将打开http://www.zhi97.com/about.aspx
3. 当Target以http://卡头是,将忽略Base URL,直接打开Target的网址;

##### 4.2 pause(waitTime)

作用:暂停脚本运行

waitTime:等待时间,单位为ms;//Target=1000

##### 4.3 goBack()

作用:模拟单机浏览器的后退按钮;

提示:由于没有参数,所以Target和Value可不填

##### 4.4 refresh()

作用:刷新当前页;

提示:由于没有参数,所以Target和Value可不填;

##### 4.5 click(locator)

作用:单击一个链接,按钮,复选框或单选按钮;

提示:如果该单击事件导致新的页面加载,命令将会加上后缀"AndWait",即"clickAndWait",或"waitForPageToLoad"

##### 4.6 type(locator,value)

作用:向指定输入域中输入指定值;也可为下拉框,复选框和单选框按钮赋值

Target:元素的定位表达式;

Value:要输入的值;

##### 4.7 close()

作用:模拟用户单击窗口上的关闭按钮

提示:由于没有参数,所以Target和Value可不填

##### #### 回顾 Selenium 家族

需要关注的

1.Selenium2.0(WebDeiver)

提示:

1. Selenium2.0=Selenium1.0+WebDriver
2. Selenium1.0 和WebDeiver 原属于两个不同的东西,由于某种原因已合并
3. Selenium2.0以后我们简称WebDriver

### WebDriver(Selenium2.0)

什么是WebDriver

1. WebDriver 是一种用于web应用程序的自动测试工具;
2. 它提供了一套友好的API
3. WebDriver 完全就是一套类库,不依赖任何测试框架,除了必要的浏览器驱动

说明:

API:应用编程接口说明(WebDriver类库内封装非常多的方法,要使用这些方法,旧需要友好的调用命名规则)

##### 支持的浏览器

1. Firefox(FirefoxDriver) 推荐
2. IE(InternetExplorerDriver)
3. Opera(OperaDriver)
4. Chrome(ChromeDriver)
5. safari(SafariDriver)
6. HtmlUnit(HtmlUnit Driver)

Firefox,Chrome:对元素定位和操作有良好的支持,同时对JavaScript支持也非常好.

IE:只能再Windows平台运行,所有浏览器中运行速度最慢

HtmlUnit:无GUI(界面),运行速度最快

推荐原因

1. Selenium IDE
2. FireBug
3. 对WebDriver API 支持良好

##### 为什么要学习 WebDriver ?

1. 自动化测试概念
2. WebDriver-定位元素
3. WebDriver-操作元素

#### 4. 环境搭建

#### 4.1 Selenium 安装,卸载,查看命令

安装:	pip install selenium == 2.48.0

1. 通用的Python包管理工具.提供了对Python包的查找下载,安装,卸载的功能
2. install: 安装命令
3. elenium==2.48.0:指定安装selenium2.48.0 版本(如果不指定版本默认为最新版本)

卸载:pip uninstall selenium

查看:pip show selenium

##### 4.2 火狐浏览器 推荐

1. FireFox 48 以上版本

   Selenium3.X+ FireFix 驱动-geckodriver

2. Firefox 48 以下版本

   Selenium2.X 内置驱动

##### 谷歌浏览器

Selenium2.x/3.x+Chrome 驱动

每个浏览的驱动版和其他浏览器的不一致

但要与对应的一致

#### 4.5 浏览器-总结

各个驱动下载地址:http://www.seleniumhq.org/download/

1. 浏览器的版本和驱动版本要一致

​	(如果是32bit浏览器而Driver 是64bit则会导致脚本运行失败)

2. 浏览器驱动下载好后需要添加Path 环境变量中,或者直接放到Python 安装目录,因为Python以添加到Path 中
3. 推荐使用火狐浏览器(24,35)版本

#### WebDriver-元素定位

目标了解元素各种定位方法

掌握 id,name,class_name,tag_name,link_text,partial_link_text 定位的使用

为什么要学习元素定位方式

1. 让程序操作指定元素,旧必须先找到此元素
2. 程序不像人类用眼睛直接定位到元素
3. WebDriver 提供了八种定位元素方式

##### 定位方式

1. id
2. name
3. class_name
4. tag_name
5. link_text
6. partial_link_text
7. Xpath
8. css

定位方式分类-汇总

1. id,name,class_name:元素属性定位
2. tag_name:元素标签名称
3. link_text,partial_link_text:超链接定位(a标签)
4. Xpath:元素路径定位
5. css:css选择器定位

![1563334511941](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563334511941.png)

#### id 定位方法 find_element_by_id()

#### id 定位实现 步骤分析

1. 导入selenium 包->from selenium import webdriver
2. 导入time 包->from time import sleep
3. 实例化火狐浏览器->driver=webdriver.Firefox()
4. 打开注册A.html->driver.get(url)
5. 调用id 定位方法->driver.find_element_by_id("")
6. 使用send_keys()方法发送数据-<.send_keys("admin")
7. 暂停3秒->sleep(3)
8. 关闭浏览器->quit()

说明:为了接下来更好而学习体验,我们先暂时使用send_keys()和quit()方法.再2.4节元素操作详解

![1563336830275](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563336830275.png)

##### # ctrl+alt+空格快速导包

##### name 定位

driver.find_element_by_name(名称).send_key(赋值) 

##### class 定位

driver.find_element_by_class_name() 

说明:HTML 规定了class 来指定元素的类名,用法和name,id 类似

前提:元素有class 属性

通过class_name定位电话号码A,并发送1861111111

##### tag_name 定位

说明:HTML本质就是由不同的tag(标签)组成,而每个tage 都是指同一类,所以tag 定位效率低.一般不建议使用;tag_name 定位就是通过标签名来定位

1. find_element_by_tag_name()

   返回:符合条件的第一个标签

2. 如何获取第二个元素?稍后(2.8节)讲解

##### 2.5 link_text 定位

说明:link_text定位于前面4个定位有所不同,它专门用来定位超链接文本(<a"> 标签 </a">)

方法:find_element_by_link_text()

说明:需要传入a 标签全部文本

1. 参考id定位
2. 点击->click()

##### 2.6 partical_link_text 定位

说明:partial_link_text 定位是对 link_text 定位的补充,partial_like_text 为模糊匹配; link_text全部匹配

##### 2.7 find_element[s]_by_XXX()

作用:

1. 查找定位所有符合条件的元素
2. 返回的定位元素格式为数组(列表)格式

说明:

1. 列表数据格式的读取需要指定下标(下标从0开始)

**操作(2.4 tag_name)**

说明:使用tag_name 获取第二个元素(密码框)

代码: driver.find_elements_by_tag_name("input")[1].send_keys("123456")

#### 什么是 Xpath?

1. Xpath 即为XML Path 的简称,它是一种用来确定XML文档中某部分位置的语言.

2. HTML 可以看做是 XML 的一种实现,所以 Selenium 用户可以使用这种强大的语言在Web 应用中定位元素.

XML: 一种标记语言,用于数据的存储和传递.后缀.xml

提示:Xpath 为强大的语言,那是因为它有非常灵活**定位**策略;

##### 思考

Xpath 有哪些策略呢?

#### 2.Xpath 定位策略(方式)

1. 路径-定位
   1. 绝对路径
   2. 相对路径
2. 利用元素属性-定位
3. 层级于属性结合-定位
4. 属性于逻辑结合-定位

#### Xpath 定位 方法

```python
driver.find_element_by_xpath()
```

#### 2.1 路径/绝对路径.相对路径

```
1. 绝对路径:从最外层元素到指定元素之间所有经过元素层级路径;如:/html/body/div/p[2]
   提示:
   1.1. 绝对路径以/开始
   1.2. 使用Firebug可以快速生成,元素Xpath绝对路径
2. 相对路径: 从第一个符合条件元素开始(一般配合属性来区分);
   2.1. 相对路径以//开始,后边必须跟标签名称或*
   2.2. 使用FireBug扩展插件FirePath 可快速生成,元素相对路径
3.Xpath 路径内使用属性时,必须要使用@修饰

提示:为了方便练习Xpath,可以在FireBug内安装扩展插件-FireFinder 插件;

3. 火狐浏览器->组件管理器->搜索FireFinder
```

#### 2.2 利用元素属性

```
说明:快速定位元素,利用元素唯一属性;

示例://*[@id='userA']
```

#### 2.3 层级于属性结合

说明:要找的元素,没有属性,但它的父级有

` 示例://*[@id='p1']/input` 

#### 2.4 属性与逻辑结合

说明:解决元素之间个数相同属性重名问题

`示例://*[@id='telA' and @class='telA'] `

#### 2.5 Xpath-延伸

```xml
//*[text()='xxx'] 	#文本内容是xxx的元素
//*[starts-with(@attribute,'xxx')] 	#属性以xxx开头的元素
//*[contains(@attribute,'xxx')]	#属性中含有xxx的元素
```



### FireFox 旧版本下载地址:

https://ftp.mozilla.org/pub/firefox/releases/ 



### CSS  定位

#### 3.1 什么是 CSS

1. CSS(Cascading Style Sheets)是一种语言,它用来描述HTML 和XML 的元素显示样式;

   css语言书写两个格式:

   ​	卸载HTML语言中.卸载单独文件中 后缀.css

2. 而在CSS语言中有CSS选择器(不同的策略选择元素),在Selenium 中也可以使用这种选择器;

   提示:

   - 在selenium 中极力推荐CSS 定位,因为它比XPath 定位速度要快
   - CSS 选择器语法非常强大,在这里我们只学习在测试中常用的几个

##### CSS定位方法

**driver.find_element_by_css_selector()**

#### CSS 定位常用策略(方式)

1. id选择器
2. class选择器
3. 元素选择器
4. 属性选择器
5. 层级选择器

##### id选择器

说明:根据元素id 属性来选择

```
格式:#id 如: #userA<选择id属性值为userA的所有元素>
```

##### class选择器

根据元素class属性来选择

```
格式:
.class 如: .telA <选择class属性值为telA的所有元素>
```

##### 元素选择器

根据元素的标签名选择

```
格式:
element 如:input<选择所有input元素>
```

##### 属性选择器

根据元素的属性名和值来选择

```
格式:
[attribute=value]如:[type='password']<选择所有type属性值为password的值>
```

##### 层级选择器

根据元素的父子关系来选择

```
格式:
element>element 如:p>input   .返回所有p元素下所有的input元素
提示:
">" 可以用空格代替 如:p input 或者 p [type='password']
```

##### CSS 延伸

```
1.input[type^='p']  type属性以p字母开头的元素
2.input[type$='d']  type属性以d字母结束的元素
3.input[type*='w']	type属性包含w字母的元素
```

![1563347329016](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563347329016.png)

#### Xpath 和 CSS 类似功能对比

![1563347657503](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563347657503.png)

#### 定位(另一种写法)-延伸 [了解]

**说明:调用find_element()方法,通过By来声明定位的方法,并且传入对应的方法和参数(了解)**

##### 导入By类

导包:from selenium.webdriver.common.by  import By

driver.find_element(By.XPATH,...)

**原find的底层**















