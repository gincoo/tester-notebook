# Python 语言

## Python 开发环境

###  计算机组成

![1563166342399](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563166342399.png)

编程语言(计算机语言)是人们为了控制计算机,而设计的一种符号和文字的组合,从而实现向计算机发出指令.

- 形式是符号和文字的组合
- 目的是为了控制计算机硬件

Python 语言就是一种编程语言,由符号和文字组成的,使用Python 语言的目的就是为了控制计算机硬件进行工作

#### 1.2.2 解释器

将文字和符号转换为机器指令,这个负责转换的去恶色叫做解释器解释器本质上就是一个运行在操作系统上的程序

![1563167314873](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563167314873.png)

解析器负责翻译编程语言

1. 知道编程语言的作用

2. 知道编程语言和解析器之间的关系
3. 知道Python解释器种类
4. 知道解释器和操作系统的关系

#### 环境搭建

Python 包含两个部分

编辑器和解释器



PyCahrm (IDE)

Python 的作者,Gruido von Rossum 吉多,范,罗苏姆,龟叔.荷兰人,

1991年诞生,由C语言实现

Python 由两个版本,Python2和Python3,最新版本分别为2.7.15和3.6.5

版本根据anaconda使用?

##### 注释

 #单行注释

""" 多行注释  """

##### 变量

变量会申请一块内存 10,变量存储需要的临时数据

a =10 重建一个新的变量,并且赋值操作

a=100 重新赋值

注释快捷键 ctrl+ /

变量是用来临时存储程序运行中所需要的一些数据的

数据类型

 - 数字型
    - 整数型
    - 小数型

- 布尔类型bool

- 字符串str 文本型

type(参数) 函数用来检查相应的

python 里面定义变量不需要指定类型,根据赋的值来推断变量模型

##### 算术预算符

```
+ 
- 
* 
/
//整除 (商) 返回除法的整数部分 9//2=4
% 取余数 9%2=1
** 幂 次方 2**3 = 8
```

##### 符合赋值运算符

> 字符串和数字之间不能进行加减运算,但可以相乘,相当于复制

##### 格式化输出联系

```python
print("我的名字叫 %s ,请多多关照" % name)
print("学号是%06d"% student_no)
print("苹果单价 %.02f 元/斤,购买 %.02f 斤,需要支付 %.02f 元"%(price,weight,money))
苹果单价9.00元/斤,购买了5.00斤,需要支付45.00元
print("数据比例是%.02f%%"%(scale*100))
```

##### 键盘输入

input_content = input("请输入您的名字")

print('欢迎您 %s !'%intput_content)

##### 变量的类型转换

int(val),将变量val 转换为 int 类型

float(val),str(val)

##### if语句

```
if 3>2:
    print()
elif 3<2:
    print()
else:
    print()
```

while 循环 continue 跳过,break退出循环

while 可嵌套循环

##### 函数

def 函数名(a,b,c)

​	函数体

​	return

##### 容器

##### 字符串截取

字符串提供了一种语法,用来获取

user_email ="simagousheng@itcast.cn"

print(user_email[0])

print(user_email[0:4])

print(user_email[0:12])

##### 获得容器元素的个数

string_length = len(user_email)

print(user_email[13:string_length])

起始值不写表示从0开始

结束值不写表示到最后

**步长**

最后一个参数值,表示间隔多少取一个数

user_email[0:12:2] = smguhn

user_email[-5:-1]=st.cn   

-1从末端数起第一位:

user_email[6:1:-1]

字符串逆序:

user_email[::-1]

#### str.find(参数)函数

```python
position = user_email.find('@')
int position == -1:
	print('@不存在,邮箱不合法!')
else:
	print('@的位置是:',position)
```

#### .split(参数):分片

拆分成['aa','bb','cc','dd']

#### .count(参数):判断有多少个char

#### .strip() :去除两头空格

username = "    asdasd    "

new_username = username.strip()

print(username)  原字符变量不会修改  **结果不变**

print(new_username) 结果去除了两头的空格

#### ctrl+q :函数文档

#### 函数:单一职责原则



### 容器概述

![1563242582121](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563242582121.png)

1. 序列式容器中的元素在存放时都是连续存放的,包括**字符串,列表,元组.**
2. 非序列式容器在存储元素时不是连续存放的,包括**字典,集合**

**序列式容器支持根据下表存期元素**

##### 字符串遍历

```python
my_str = 'hello'
for abc in my_str:
    print(abc)
```

##### 字符串替换 str.replace('妮','泥')

str.replace('妮','泥',0) 第一位的

##### 字符串的特点

python 与 java 一样,原定义的字符串是不允许修改的

比如 my_str = 'abcd'

my_str[0] = 'Q' 报错.不可以赋值修改

#### 元组

##### 不可修改的列表

列表用中括号[]

**元组用小括号**

(10,20,30,40)

> 注意:元组中如果只有1个元素的话,需要在元素后加逗号

元组可以嵌套元组,如:((1,2),(10,20))

元组中的元素不能修改

#### 列表

列表属于序列式容器,支持索引,切片

**对于列表而言,尾部插入数据的效率要高一些,不需要移动元素,指定位置插入效率较低**

位置删除在尾部删除效率比较高,不需要移动元素

列表支持:位置删除(尾部删除,指定位置删除)值删除

缺点:根据关键字查找效率低

列表根据索引查找效率很高

```python
my_list=[[1,2,3,],[4,5,6],[1,2,3]]
my_list=['Trump',60,3.14,[1,2,3]]
print(my_list[:2])
#append 在列表尾部追加插入元素
my_list.append(10)
#insert 在指定位置插入元素
my_list.insert(0,100) #0位置插入值100
#pop 删除指定位置元素,默认删除最后一个位置元素
my_list.pop()
my_list.pop(1)
#remove 移除 根据值删除
my_list.remove(200)
#clear 清除清空列表数据
my_list.clear()
#sort 对列表进行排序,默认是从小到大
my_list.sort()
my_list.sort(reverse=True) #将函数的 reverse 的默认值改成True 即可实现从大到小
#reverse 将列表按照原有顺序逆序排序,颠倒
my_list.reverse()
#extend 将一个列表中的所有元素追加到当前列表的尾部
my_list.extend(list)
#判断元素是否存在列表中:
if a in list:
    

```



#### 字典

查找快,但占空间

**大括号**

```python
语法:
my_dict = {key:value,key2:value2}
```

**字典属于非序列式容器,占内存,但是是效率高,属于空间换时间**

注意:键一般是唯一的,如果最后的重新赋值会覆盖前面

```python
persion={'name':'张三','age':20,'sex':'男',100:101}
# 如果 key 不存在会报错
print(person['name'])
# 如果 key 不存在可以设置默认值
print(persion.get('gender','default'))
# 添加元素 存在替换,不存在更新
persion['school']='123'
# del 删除元素 
del person['age'] #将对应键的"键和值"都删除
# 清空字典
person.clear()
# 默认只能遍历出来键
for val in my_dict:
    print(val)
# 遍历
my_dict = {'aaa':10,'ccc':30,'bbb':20}
key_list = my_dict.keys()
['aaa','ccc','bbb']
value_list = my_dict.values()
[10,30,20]
key_value_list = my_dict.items()
[('aaa',10),('ccc',30),('bbb',20)]

```

##### 字符中的 \t 代表 Tab 键



#### 文件

二进制模式和文本模式

在python,使用open函数,可以打开一个已经存在的文件,或者创建一个新文件,使用close 方法来关闭一个文件

1. 什么是文件 ,文件的作用就是计算机存储数据
2. 如何打开关闭文件
3. 文件打开模式的区别
4. 如何在程序中进行文件读写
5. 知道文件,目录管理操作

在python ,使用open 函数,可以打开一个已经存在的文件,或者创建一个文件

```python
#打开文件
f = open('text.txt,'w) # 返回文件对象
#关闭文件
f.close 
# 写入文件
f.write("1231232131\n")
```

![1563262056016](C:\Users\89463\AppData\Roaming\Typora\typora-user-images\1563262056016.png)

**文本模式和二进制模式的区别**

##### 打开文件用的文本模式,会进行换行符的转换:

> 程序:hello world\n
>
> ->windows hello world\r\n
>
> ->mac hello world \r
>
> ->linux hellow world\n
>
> 如果使用二进制模式不会转换



##### 2.读取文件数据

```python
f = open('b.txt','r')
mycontent = f.read()
f.close()
print(mycontent)
```

##### 3.文件读写方法

##### writelines

```python
f = open('b.txt','r')
mycontent = f.read()
f.close()
print(mycontent)
```

##### 文件拷贝

#### 文件操作 os 模块

1. 知道如何删除文件

2. 知道如何获得文件名列表

3. 知道重命名文件

4. 知道如何创建和删除文件

   **批量操作等**

文件操作相关模块

```python
import os
#改名:
os.rename('11[附件].html','index.html')
#创建目录:
os.mkdir('abc')
#删除目录:
os.rmdir('abc')
#获得指定目录下的文件列表:
os.listdir()
#获得和设置工作目录 默认为当前工程.py文件的目录路径:
os.getcwd()
```





```
#当前文件的路径
pwd ``=` `os.getcwd()
#当前文件的父路径
father_path``=``os.path.abspath(os.path.dirname(pwd)``+``os.path.sep``+``"."``)
#当前文件的前两级目录
grader_father``=``os.path.abspath(os.path.dirname(pwd)``+``os.path.sep``+``".."``)
```