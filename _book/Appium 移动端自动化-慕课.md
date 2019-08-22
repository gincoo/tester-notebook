

目前常用框架：

Robotium

UiAutomator

Monkey

MonkeyRunner

Instrumentation

Athrun



2个一键自动化测试框架

1个自动化服务



获取app 进程信息:

`adb devices`

获取apk 包信息:

`aapt dump badging xxx.apk`

app UI 层级查看软件:

sdk/tools 路径下: UIAutomator Viewer





在初始化caps 内加入, 可以避免重复安装"noReset" : "true"

使用xpath 定位,最后如果跟上`..`,`/precoding-sibling::` 则是上层父节点

#### WebView 定位

获取webview 思路,先获取父容器:

```
webview = driver.contexts
```

智能等待:

```
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions
```

智能等待:

```python
tost_element = ("xpath","//*[contains(@text,'请输入密码')]")
#等待定时循环查找这个目标tost_element,当能查找到时候
WebDriverWait(driver,持续事件,间隔时间).until(EC.presence_of_element_located(tost_element))
```

#### 多线程 threading

```python
import threading
def sum(a,b):
	print a+b
for i in range(3)
	print i
	threading.Thread(target=sum,args=())
```



## 无界面运行 Appium

需要科学上网,或者使用淘宝的镜像

```
需要翻墙: npm install appium  
淘宝镜像安装cnpm: npm install appium -g cnpm --registrys=http://registry.taobao.org
使用cnpm 安装appium:
cnpm install -g appium 
默认启动 appium:
appium
指定端口启动 appium:
appium -p 4725
另一种监听:
appium -p 4725 -bp 4701
另一种监听:
appium -p 4725 -bp 4701 -U 127.0.0.1:21503
```

### 命令行输入值

```python
import os
print os.system('adb devices') # 括号内为具体命令内容
# 结果:
# 127.0.0.1:21503 devices
# 获取值:
# pirnt os.popen('adb devices').readlines()
class DosCmd:
    def excute_cmd_result(self):
    	result = os.popen('adb devices').readlines()#获取到list
        for i in result:
            if i == '\n':
                continue
			result_list.append(i.strip('\n'))
            

    
```

#### 5-3 server.py

#### 5-4 检测端口是否被占用 : port.py

netstat -ano | findstr 8080

拼接字符串单独使用变量接收

#### 5-6 封装生成启动命令行函数

```
appium -p 4725 -bp 4701 -U 127.0.0.1:21503 --no-reset --session-override
```

#### 5-8 清理 appium 环境

```
tasklist | find "node.exe" 查询
taskkill -F -PID python.exe
```

#### 5-9 通过 yaml 文件 获取命令行数据

启动命令:

```
appium -p 4700 -bp 4701 -U 127.0.0.1:21503
```

创建 一个 .yaml 文件,存储相关的端口等参数

```
__info_0: {bp: '4902',deviceName: '127.0.0.1:21503',port: '4723'}
```

**pip install pyyaml 安装**

```
pip install pyyaml 安装
```

**导入 yaml :** 

```
import yaml
class WriteUserCommand:
	de 
	with open("../config/userconfig.yaml") as fr:
		data yaml.load(fr)#导入的是字典
	print data['user_info_0']['bp']
```









