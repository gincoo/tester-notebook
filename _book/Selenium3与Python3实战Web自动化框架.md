# Selenium3与Python3实战Web自动化框架

## 1. Selenium 工作原理

![1564068024783](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1564068024783.png)

- Client
  - Visual
- Driver
  - ChromeDriver
    - 360 使用的还是Chrome的内核
  - FirefoxDriver
  - InternetExporerDriver

## 2. 环境搭建

### 2.3 需求分析用例设计

- 慕课网免费课程,加强

### 2.6 title_contains 检查页面是否正确

### 2.8 判断元素是否可见

from selenium.webdriver.support import expected_conditions as EC

```
判断元素是否在显示范围之内: EC.visisblity_of_element_located(需要传递一个元素) 

```

### 2.10 传入的信息与最终展示的不同如何检查

获取邮箱输入框:

`email_element = driver.find_element_by_id("register_email").send_keys("邮箱")`

获取输入的值:

`email_element.get_attribute('value')`

### 2-11 如何生成用户名

random.sample("随机数",生成的数组的元素个数)

[1,2,3,4,5] 的列表

''.join(list),可将数组编程字符串

### 2-13 获取验证码

思路:截取验证码图片,使用第三方验证码处理工具

```
截图:
driver.save_screenshot("E:/imooc.png")
code_element = driver.find_element_by_id("getcode_num")
left = code_element.location['x']
top = code_element.location['y']
right = code_element.size['width']+left
height = code_element.size['height']+top
im = Image.open("E:/imooc.png")
img = im.crop(left,top,right,height)
img.save('E:/imooc1.png')
使用pytesseract 识别图片中的问题
登陆网站按照流程处理

```

### 2-17 注册流程梳理及代码封装

```
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("http://www.t1test.cn/register")
driver.maxmize_window()
time.se
```

### 2-18 以配置文件形式实现定位设计思想

from selenium import webdriver

### 2-19

pip install Configparser

PIL 简单的图片转文字识别



要么是双斜杠,要么是反斜杠

## PO 模型

​	3-7 遗留

```
Traceback (most recent call last):
  File "C:/PythonPJ/Muke/case/first_case.py", line 50, in <module>
    main()
  File "C:/PythonPJ/Muke/case/first_case.py", line 43, in main
    first.test_login_code_error()
  File "C:/PythonPJ/Muke/case/first_case.py", line 31, in test_login_code_error
    code_error = self.business.login_code_error('123@163.com', 'nick', '111111', '1234')
  File "C:\PythonPJ\Muke\business\register_business.py", line 54, in login_code_error
    if self.register_handler.get_user_text('code_text_error', "字符长度必须大于等于4,i一个中文字算2个字符") is None:
  File "C:\PythonPJ\Muke\handle\register_handler.py", line 33, in get_user_text
    text = self.register_page.get_code_error_element().get_attribute('value')
AttributeError: 'NoneType' object has no attribute 'get_attribute'
```

教程说需要清空

**PO思想 :数据,元素,case 分离 ,分别维护**

> 数据,元素,case 分离,分别维护



## UniTest

函数需要以test 命名

```
import unittest
class FirstCase01(unittest.TestCase):
    def testfirst01(self):
        print('testfirst01')
    def testfirst02(self):
        print('testfirst02')    
```

如果 增加 def setUp(self) 函数

结果不同 是case 的前置条件

后置条件: tearDown 

```
setUp
testfirst01
tearDown
setUp
testfirst02
tearDown
```

使用unitest 替代凡夫执行的代码冗余

所有test的前置:装饰器@classmethod

```
class FirstCase01(unittest.TestCase):

    @classmethod
    def setUpClass(cls):
        print('setUpClass\n')

    @classmethod
    def tearDownClass(cls):
        print('tearDownClass')


    def setUp(self) -> None:
        print('setUp')


    def tearDown(self) -> None:
        print('tearDown')


    def testfirst01(self):
        print('testfirst01')

    def testfirst02(self):
        print('testfirst02')


if __name__ == '__main__':
    unittest.main()
```

打印:

setUpClass
setUp
testfirst01
tearDown
setUp
testfirst02
tearDown
tearDownClass



**将所有test定义为一个容器**
suite = unittest.TestSuite()

suite.addTest()

### 4-4 装饰器

```
@classmethod
def setUpClass(cls):
	"""所有case前开始执行"""
def tearDownClass(cls):
	"""所有case之后执行"""

```

#### 4-5 跳过

```
@unitest('跳过这一条')
def test01(self):
```

os.path() 模块

### 4-10 TearDown 中捕获错误信息

python2 方法捕获错误信息:

sys.exc_info()

python3 

for method_name,error in self._outcome.errors:

```
 def tearDown(self):
        """后置函数"""
        time.sleep(1)
        for method_name, error in self._outcome.errors:
            if error:
                case_name = self._testMethodName #获取case名字
                # file_path = os.path.join(os.getcwd(), 'report', case_name + '.png')
                file_path = 'C:/PythonPj/Muke/report/' + case_name + '.png'
                # file_path = '/'.join(file_path.split("\\"))
                self.driver.save_screenshot(file_path)
        self.driver.close()
```

问题:python 在使用os.getcwd()获取当前路径可能不正确,改为使用:os.path.abspath(),在主函数中调用该函数，并传入sys.argv[0]

```
#当前文件的路径
pwd ``=` `os.getcwd()
#当前文件的父路径
father_path``=``os.path.abspath(os.path.dirname(pwd)``+``os.path.sep``+``"."``)
#当前文件的前两级目录
grader_father``=``os.path.abspath(os.path.dirname(pwd)``+``os.path.sep``+``".."``)
```



## 5 数据驱动

**pip install ddt**

#### 5-6 获取excel内容

使用 xlrd 扩展包

``` pip install xlrd``` 

#### xlrd 插件使用方法

```
# 打开excel文件
self.excel_data = xlrd.open_workbook(excel_path)
# table
self.excel_table = self.excel_data.sheets()[index]
# 行数
self.excel_rows = self.excel_table.nrows

 def get_data(self):
        """
        获取excel数据,按照每行一个list,添加到一个新list里
        :return: 返回list
        """
        result = []
        for i in range(self.get_lines()):
            # 一行的数据
            col = self.excel_table.row_values(i)
            result.append(col)
        return result

 def get_lines(self):
    """获取行数"""
    rows = self.excel_table.nrows
    return rows
```



豆瓣 pip install -i https://pypi.douban.com/simple  scrapy

清华大学https://pypi.tuna.tsinghua.edu.cn/simple

中国科技大学https://mirrors.ustc.edu.cn/pypi/web/simple

阿里https://mirrors.aliyun.com/pypi/simple/

## 关键字模型

#### xlutils 插件

pip install xlutils

#### 6-6  getattr() 返回对象属性值



## 7-1 BBD 行为驱动介绍及环境搭建

BBD (Behavior-driven development) 行为驱动开发

像说话一样写case

使用到的:

- Behave 
- Python
- selenium
- pyhamcrest 断言

```
pip install behave
pip install pyhamcrest
```

用到的关键字

- Given

- when

- and

- then


## logging 模块





## 9 持续集成 Jenkins





















