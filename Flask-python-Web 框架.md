# Flask pythn Web 框架总结

## 一, Flask 介绍

Flask 是一个基于Python 实现的web 开发的'小型轻框架'

### 1. flask介绍

Flask是一个基于Python实现的web开发的'微'框架

[中文文档地址](http://docs.jinkan.org/docs/flask/)

Flask和Django一样，也是一个基于MVC设计模式的Web框架

flask流行的主要原因：

```
a）有非常齐全的官方文档，上手非常方便
b) 有非常好的拓展机制和第三方的拓展环境，工作中常见的软件都有对应的拓展，自己动手实现拓展也很容易
c) 微型框架的形式给了开发者更大的选择空间
```

### 2. 安装 flask

```

```

### 3. 基于flask的最小的应用

创建hello.py文件

```
from flask import Flask

app = Flask(__name__) # flask初始化

@app.route('/')
def gello_world():
    return 'Hello World'

if __name__ == '__main__':
    app.run(debug=True)
```

### 4. 项目使用

```python
# coding=utf-8
import sys
import os
import json

base_path = os.getcwd()
sys.path.append(base_path)
from flask import Flask
from flask import request
from Util.handle_json import HandleJson

app = Flask(__name__)


@app.route('/')
def Home():
    data = json.dumps({
        "username": "1",
        "password": "1"
    })
    return data


@app.route('/passport/user/login', methods=['GET'])
def Login():
    username = request.args.get("username")
    password = request.args.get("password")
    if username and password:
        data = json.dumps({
            "username": username,
            "password": password,
            "code": "200",
            "message": "登陆成功",
            "info": "www.baidu.com"
        })
    else:
        data = json.dumps({
            "message": "请传递参数"
        })
    return data


@app.route('/mock', methods=['POST'])
def mock_data():
    '''
    模拟数据
    imooc.com
    {
        "key":"value"
    }
    '''
    return_data = {
        "message": None
    }
    mock_data = HandleJson().read_json()
    url = request.form.get("url")
    data = request.form.get("data")
    try:
        data = json.loads(data)
        mock_data[url] = data
    except Exception:
        return_data['message'] = "你传递的数据不是json格式"
        return json.dumps(return_data)
    try:
        print("--->", mock_data)
        HandleJson().write_value(mock_data, file_name="/Config/user_data.json")
    except Exception:
        return_data['message'] = "写入数据失败"
        json.dumps(return_data)
    return_data['message'] = "写入成功"
    return json.dumps(return_data)


@app.route('/passport/user/post_login', methods=['POST'])
def post_login():
    request_method = request.method
    if request_method == 'POST':
        username = request.form.get("username")
        password = request.form.get("password")
        data = json.dumps({
            "username": username,
            "password": password,
            "code": "200",
            "message": "登陆成功",
            "info": "www.Imooc.com"
        })
        # return data
    else:
        data = json.dumps({
            "message": "请求不合法"
        })
    return data


# https://www.imooc.com/passport/user/login?username=Mushishi_xu@163.com&password=111111

if __name__ == "__main__":
    app.run(debug=True)

```



具体请看! 非常详细!作者：文化银儿 ：https://www.jianshu.com/p/240d936981a1

