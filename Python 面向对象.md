# Python 面向对象

面向过程

- 把完成某个需求的所有步骤,从头到尾逐步实现
- 根据开发需求,将某些功能独立的代码封装成一个又一个函数
- 最后完成的代码,就是顺序地调用不同的函数

面向过程特点:

1. 注重步骤过程,不注重职责份工
2. 如果需求复杂,代码很复杂
3. 开发复杂项目,没有固定套路,开发难度大

面向对象特点

1. 注重对象和职责,不同的对象承担不同的职责
2. 更加适合对复杂需求变化,时专门应对复杂项目开发,提供的固定套路
3. 需要在面向过程基础上,再学习一些面向对象语法

### 类,对象

- 类是图纸,是模板
- 对象是根据图纸制作的飞机

设计类满足的三要素:

1. 类名 
2. 属性
3. 方法

## 基础语法

#### 目标

- `dir` 内置函数
- 定义简单的类(只包含方法)
- 方法中的 self 参数
- 初始化方法
- 内置方法和属性

### 01 dir 内置函数

- **提示**: `__方法名__`格式的方法是 Python 提供的 **内置方法/属性**,.

| 方法名     | 类型 | 作用                                       |
| ---------- | ---- | ------------------------------------------ |
| `__new__`  | 方法 | 创建对象时,会被自动调用                    |
| `__init__` | 方法 | 对象被初始化时,会被调用                    |
| `__del__`  | 方法 | **对象被从内存中销毁前**,会被调用          |
| `__str__`  | 方法 | 返回**对象的描述信息**, print 函数输出使用 |

#### 例子

```python
# coding=utf-8

class Demo:
    
	# 如果存在 __new__ 则接下来的函数都不会进行.
    def __init__(self,name):
        self.name = name
        print('init---%s :'% name)

    def __del__(self):
        print('del---')

    def __str__(self):
        return '123'

hehe = Demo('guagua')
print(hehe)
del hehe
"""
打印结果:
init---guagua :
123
del---
"""
```

#### 1) `__str__` 方法

- 在 Python 中,使用 print 输出 对象变量,默认情况下,会输出这个变量 **引用的对象** 是 **由哪一个类创建的对象**,以及在内存中的地址(十六进制表示)

- 如果在开发中,希望使用 print 输出 **对象变量** 时,能够打印 **自定义的内容**,就可以利用 `__str__` 这个内置方法了
- `__str__` 必须返回一个字符串

###  私有属性和私有方法

应用场景及定义方式

- **私有属性**就是对象不希望公开的**属性**
- **私有方法**就是对象不希望公开的**方法**

**定义方式:**

- 在定义属性或方法时,在 **属性名或者方法名前** 增加 **两个下划线**，定义的就是 **私有** 属性或者方法

```python
class Women:
    def __init__(self,name):
        self.name = name
        self.__age = 18 #私有属性
    
    #私有方法
    def __get_age():
        pass
    
	def secret(self):
        print('年龄是%s' % self.__age)
        
xiaofang = Women('小芳')
print(xiaofang.age)# 私有属性不可外部直接调用，报错
xiaofang.__get_age()# 私有方法不可外部直接调用，报错
xiaofang.secret()#
```

#### 伪私有属性和私有方法

Python 中，并没有 **真正意义** 的 **私有**，以上讲的私有其实都是伪私有

- 在给属性、方法命名时，实际时对名称左了一些特殊处理，使得，外界无法访问到
- 处理方式：在名称前面加上 `_类名 => _类名__名称`
- 处理之后使得能够直接调用私有方法

> 提示：在日常开发中，不要使用这种方式去访问 定义好的 私有的属性和方法

经过改造的上面的例子：

```python
print(xiaofang._Women__age)# 私有被直接调用
xiaofang.Women.__get_age()# 私有被直接调用
```

#### 引用概念的强调

- Python 使用类创建对象之后，tom 变量中记录的是 对象在内存中的地址。
- 也就是 tom 变量引用了 新建的对象
- 使用 print 输出对象变量，默认情况下，是能够输出这个变量 引用的对象 是 由哪一个类创建的对象，以及在内存中的地址（十六进制表示）

> 提示：在计算机中，通常使用 **十六进制** 表示 **内存地址**

- `%d` 可以以 **10进制** 输出数字
- `%x` 可以以 **16进制** 输出数字

`<__main__.Cat object at 0xi9asdiaxxxxx>`

```
tom = Cat()
addr = id(tom)
print("%x" % addr)
print("%d" % addr)
```



## 继承

- 单继承
- 多继承
- 面向对象三大特性
  1. 封装 根据 职责 将 属性 和 方法 封装 到一个抽象的 类 中
  2. 继承 实现代码的重用,相同的代码不需要重复的编写
  3. 多态 不同的对象调用相同的方法，产生不同的执行结果，增加代码的灵活性



#### 单继承

继承的概念、语法和特点

继承的概念：子类 拥有 父类 的所有 方法 和 属性

```python 
class 类名(父类名):
	...
```

- 子类 是 父类的 继承类
- 子类 是 父类的 派生类
- 父类 是 子类的 基类
- 子类 从 父类 派生

##### 方法的重写

- 当父类 的 方法实现不能满足子类需求时，可以对方法 进行重写 override

#### 多继承

- 子类 可以拥有 多个父类，并且具有 所有父类 的属性 和方法

```
class 子类名(父类名1，父类名2...)
	...
```

> 注意：
>
> 开发时候，应尽量避免不同父类 中存在 同名的方法，容易产生混淆。如果父类之间存在同名，尽量避免使用多继承。

#### Python 中的 MRO -- 发给发搜索顺序

- Python 中针对 类提供了一个内置属性 `__mro__` 可以查看 **方法** 搜索顺序
- MRO  是 method resolution order ，主要用于 **在多继承时判断 方法、属性的调用 路径**

```python
print(C.__mro__)
输出结果：
(<class '__main__.C'>,<class '__main__.A'>,<class '__main__.B'>,<class 'object'>)
```

- 在搜索方法时，是按照 `__mro__` 的输出结果从左至右的顺序查找的
- 如果在当前类中 找到方法，就直接执行，不再搜索
- 如果没有找到，就查找下一个类中是否有对应的方法，如果找到，就直接执行，不再搜索
- 如故宫找到最后一个类，还没有找到方法，程序报错

####  新式类与旧式

> object 是 Python 为所有对象提供的基类，提供有一些内置的属性和方法，可以使用 `dir` 函数查看

### 多态

- 不同的 子类对象调用相同的父类方法，产生不同的执行结果
- 增加代码灵活度
- 继承 和 重写父类方法为前提
- 时调用方法的技巧，不会影响到类的内部设计

### 类--特殊对象

- 程序运行时，类 同样会被加载到内存
- 在 Python 中，类 是一个图书的对象 -- 类对象
- 在程序运行时，**类对象（模板）**在内存中 **只有一份**，一个类可以创建多个对象示例
- **模板** 创建 **实例对象**，类对象只有一个，实例对象可以创建多个



#### 类属性和实例属性

- 类属性就是给 类对象中 定义的熟悉感
- 通常记录 与这个类相关的特征
- 类属性 不会用于记录 具体对象的特征

**属性的获取机制**

- **属性的获取**存在一个**向上查找机制**

访问类属性有两种

1. 类名.类属性
2. 对象.类属性（不推荐）

```python
class Tool(object):
	count = 0
    
    def __init__(self,name):
        self.name = name
        Tool.count += 1 #类属性
        
tool1 = Tool("a")
tool2 = Tool("b")
tool3 = Tool("c")

tool3.count == 99 #对象属性 赋值
print(tool3.count)# 打印99
print(Tool.count) # 打印3 tool1,tool2,tool3,
# 因为类声明，Python 解释器会为其在内存开辟空间，它也是个对象。--类对象。
```

#### 类方法 和 静态方法

- 针对 **类对象** 定义的方法

- 类方法需要用 修饰器 `@classmethod` 来标识，告诉解释器这是一个类方法
- 类方法的第一个参数 应该是 `cls`
  - 由 **哪个类** 调用的方法，方法内的 `cls` 就是 **哪一个类的引用**
  - 这个参数和 **实例方法** 的第一个参数是 `self` 类似
  - 使用其他名称也可以，不过习惯使用 `cls`
- 通过 `类名` 调用 **类方法**，调用方法时，不需要传递 `cls` 参数
- 在方法内部
  - 可以通过 `cls`，访问类的属性
  - 也可以通过 `cls`，调用其他的类方法

```python
class Tool(object):
	count = 0
    
    @classmethod
    def show_tool_count(cls):
        print(cls.count)
    
    def __init__(self,name):
        self.name = name
        Tool.count += 1 #类属性
        
tool1 = Tool("a")
print(Tool.show_tool_count) # 打印 1
# 因为类声明，Python 解释器会为其在内存开辟空间，它也是个对象。--类对象。
```

#### 静态方法

- 在开发时，如果需要在 类 中封装一个方法，这个方法：
  - 既不需要访问实例属性，调用实例方法
  - 也不需要访问类属性，类方法

```python
@staticmethod
def 静态方法名():
    pass
```

- 静态方法 需要使用装饰器 `@staticmethod` 来标识，告诉解释器这是一个静态方法

- 通过**类名.**直接调用静态方法，不需要创建 **实例对象**

**案例：**

1. 设计一个 Game 类
2. 属性
   - 定义一个类属性 `top_score` 记录游戏的 历史最高分
   - 定义一个实例属性 `player_name` 记录 **当前游戏的玩家姓名**
3. 方法：
   - **静态方法** `show_help` 显示游戏帮助信息
   - **类方法** `show_top_score` 显示历史最高分
     - 类方法内部调用类属性 `cls.top_score`
   - **实例方法** `start_game` 开始当前玩家的游戏
     - `self.player_name`
   - `__init__` 类设置名称:`self.player_name = player_name`

**小结：**

- **实例方法** 内部需要访问 **实例属性**
  - **实例方法**  内部可以使用 类名.访问类属性
- **类方法** 内部只需要访问类属性
- **静态方法** 内部，不需要访问，**实例属性**和**类属性** 

### 单例

#### 单例设计模式

- 目的：为了让 **类** 创建的对象，在系统中 **只有** **唯一的一个实例**
- 每一次执行类名() 返回的对象，**内存地址是相同的**

#### `__new__` 方法（内部方法）

- 使用 **类名()** 创建对象时，Python 的解释器 **首先** 会调用 `__new__` 方法为对象 **分配空间**
- `__new__` 是一个 由 object 基类提供的 **内置的静态方法**，主要作用有两个：
  - 在内存中为对象 分配空间
  - 返回 对象的引用

> **重写 `__new__` 方法的代码非常固定**

- 重写 `__new__` 一定要 `return super().__new__(cls)`
- 否则 Python 的解释器 得不到 分配了空间的对象引用，就不会调用对象的初始化方法
- 注意：`__new__` 是一个静态方法，在调用时需要主动传递 cls 参数

**重写例子**：

```python
class MusicPlayer(object):
    
    def __new__(cls,*args,**kwargs):
        # 1.创建对象时，new 方法会被自动调用
        # 2.为对象分配空间
        instance = super().__new__(cls)
        # 3.返回对象的引用
        return instance
    
    def __init(self):
        print('初始化播放器')
        
player = MusicPlayer()
print(player)        
```

#### Python 中的单例

```python
class MusicPlayer(object):
    #记录第一个被创建对象的引用
    instance = None
    #记录是否执行过初始化动作
    init_flag = False
    
    def __new__(cls,*args,**kwargs):
        if cls.instance is None:
        	cls.instance = super().__new__(cls)
        return cls.instance
    
    def __init__(self):
        # 1. 判断是否执行过初始化动作
        if MusicPlayer.init_flag:
            return
        # 2. 如果没有执行过开始初始化
        print("初始化播放器")
        # 3.修改类属性的标记
        MusicPlayer.init_flag = True
  
player1 = MusicPlayer()
player2 = MusicPlayer()
```



## 异常

- 异常的概念
- 捕获异常
- 异常的传递
- 自定义异常

### 01 异常的概念

- 通过异常捕获 可以针对突发事件做集中的处理，从而保证程序的稳定性和健壮性

### 02 捕获异常

**基本格式**：

```python
try:
    尝试执行代码
except:
    出现错误处理
```

**错误类型捕获：**

```python
try:
    pass
except 错误类型1:
    pass
except (错误类型2,错误类型3):
    pass
except Exception as result:
    print(位置错误)
```

- 当Python 解释器 抛出异常时，最后一行错误信息的第一个单词，就是错误类型

- 如果希望程序 无论出现任何错误，都不会因为 Python 解释器 抛出异常而被终止，可以再增加一个except （即最后一个Exception）

**异常捕获完整语法**

```python
try:
    # 尝试执行的代码
except 错1:
    pass
except 错2:
    pass
except (错3，错4):
    pass
except Exception as result:
    print(result)
else:
    # 没有异常才会执行的代码
    pass
finally:
    print("无论是否有异常都会执行")
```

### 03 异常的传递

- 异常的传递 -- 当 **函数/方法** 执行 **出现异常**，会 将异常传递 给 函数/方法 的调用以方
- 如果 传递到主程序，仍然没有异常处理，程序才会被终止

> 提示：
>
> - 在开发中，可以在主函数中增加异常捕获
> - 而在主函数中调用的其他函数，只要出现异常都会传递到主函数进行异常捕获

### 04 抛出 raise 异常

- 开发时，如果满足 特定业务需求时，希望抛出异常，可以：
  1. 创建一个 Exception 对象
  2. 使用 raise 关键字抛出
  3. **但不进行捕获**，**由其他函数捕获异常**

```python
def input_password():
    
    pwd = input("请输入密码：")
    if len(pwd)>=8:
        returen pwd
    raise Exception("密码长度不够")#主动抛出异常
    
try:
    print(inptu_password())
except Exception as result:
    print(result)
```

## 模块

> 模块时 Python 程序架构的一个核心概念

- 每一个扩展名 py 结尾的 Python 源码文件 都是一个模块
- 模块名 同样时一个标识符，需要符合命名规则
- 在模块中定义的 全局变量、函数、类 都是提供给外界直接使用的工具
- 模块就好比是工具包。

### 01 导入模块的方式

#### 1） import 导入

```python
import 模块1，模块2 #不推荐使用，需要单独行导入
# 推荐
import 模块1
import 模块2
```

**模块别名**：需要符合大驼峰命名

```python
import 模块名1 as 模块别名
```

### 2) 局部导入

- 如果希望从某一个模块中，导入部分工具，就可以使用 `from ... import` 的方式

- 导入后 不需要通过 模块名
- 可以直接使用 模块提供的工具--全局变量、函数、类

>  注意:
>
> - 如果两个模块，存在同名函数，那么后导入的函数会覆盖先导入的。
> - 新增别名，可避免

**导入全部工具模块**：

```python
from 模块名1 import *
```

### 3） 模块的搜索顺序

- 当前目录搜索指定模块，如果有就直接导入
- 如果没有，再搜索系统目录

Python 中每一个模块都有一个内置属性 `__file__` 可以**查看模块**的**完整路径**

### 4） 原则

#### `__name__`

- 如果直接执行模块`__name__` (即不是外部使用该模块)，永远是执行`__main__`
- 是一个 Python 的内置熟属性，记录着一个字符串
- 如果 是**被其他文件导入的**，`__name__` 就是模块名

所以:

```python
if __name__ = "__main__":
    main() # 进行测试
```

## 包 (Package)

- 包即目录,是一个包含多个模块的特殊目录
- 目录下有一个特殊文件 `__init__.py`
  - 在`__init__.py`文件中 设置 `from . import ....`
  - 导入模块可直接导入模块

### 发布模块 (重要)

#### 01 制作发布压缩包步骤

以 hm_message 为例:

**1) 创建setup.py**

```python
from distutils.core import setup

setup(name="hm_message",# 包名
     version="1.0", #版本 
     description="描述信息", 
     long_description="完整的描述信息",
     author="作者",
     url="主页",
     py_modules=["hm_message.send_message",
                "hm_message.receive_message"])
     )
```

可以参阅官方网站:

https://docs.python.org/2/distutils/apiref.html

#### 2) 构建模块

```python
python3 setup.py build
```

#### 3) 生成发布压缩包

```python
python3 setup.py sdist
```

生成 `hm_message-1.0.tar.gz`

### 02 安装模块

```
tar -zxvf xxxxxx.tar.gz
sudo python3 setup.py install
```

### 03 卸载模块

直接到安装目录把模块目录删除即可

### 04 pip 安装 pygame 游戏开发模块

```
sudo apt install ipython3 # Linux 下安装 iPython
sudo pip install pygame
```



## eval 函数

eval() 函数十分强大 -- **将字符串** 当成 **有效的表达式** 来求值 并 **返回计算结果**

```python
# 基本的数学计算
eval("1 + 1") # 结果: 2

# 字符串重复
eval("*" * 10)
输出 :**********

# 字符串转换成列表
type(eval("[1,2,3,4,5]"))
输出: list

# 将字符串转换成字典
type(eval("{'name':'xiaoming','age':18}"))
输出 dict
```

#### 安全 - 不要滥用 `eval ` (重要)

> 开发时千万不要使用 `eval` 直接转换 `input` 的结果

```python
__import__('os').system('ls') # 会有安全问题,可以看到你的东西
等价于:
import os
os.system("终端命令")

```

直接操作文件有很大的安全问题

