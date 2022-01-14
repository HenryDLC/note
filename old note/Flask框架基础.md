flask框架特点在于只是给开发人员一套最基础的web框架,开发者需要对框架进行配置以及安装各类插件比如数据库ORM插件,迁移插件,模板插件等等使得整个flask项目更加完善

创建项目
====

```python
# 导入
from flask import Flask

# 创建Flask的应用程序
app = Flask(__name__)

@app.route('/')
def index():
    return 'helloworld'

if __name__ == '__main__':
    # 运行当前flask程序
    app.run()
```

七行代码启动一个显示’helloworld’字符串的页面:

导入Flask包后,创建Flask实例对象’app’,通过@app.route()装饰器配置路由函数,通过main方法中的app.run()启动web程序



app = Flask(\_\_name\_\_):
--------------------------

```python
app = Flask(__name__,
            static_url_path='/static',# 静态文件访问 用户访问静态文件的路径
            static_folder='static', # 静态文件所存放的目录, 默认值static 服务器静态文件的路径
            template_folder='templates' # 表示模板文件存放的目录
            )
```

\_\_name\_\_:FLASK对应的模块,可以决定静态文件从哪个位置开始找

static\_url\_path='/static',\# 静态文件访问 用户访问静态文件的路径

static\_folder='static', \# 静态文件所存放的目录, 默认值static 服务器静态文件的路径

template\_folder='templates' \# 表示模板文件存放的目录



加载配置:
-----

```python
# ====加载配置===== #

# 对象中加载配置
class Config(object):
    DEBUG = True
app.config.from_object(Config)

# 文件中加载配置
app.config.from_pyfile('config.ini')

# 环境变量中加载配置
app.config.from_envvar('ENVCONFIG')
```

我们经常需要对Flask进行整体配置,在flask中有三种方法可以加载这些配置

\# 对象中加载配置: 写一个Config类,类属性添加相应的配置

\# 文件中加载配置: 创建配置文件如’config.ini’到特定目录并

\# 环境变量中加载配置:在pycharm或其他IDE 的环境变量中添加变量名(自定义)和配置文件的路径(本质上和文件中加载是一样的)

p.s:很多配置我们不需要写进配置文件中,flask实例对象中就自带了很多配置,我们只需要打开即可使用.如:app.debug = True

创建项目完整代码:
---------

```python
# 导入
from flask import Flask

# 创建Flask的应用程序
# __name__:FLASK对应的模块,可以决定静态文件从哪个位置开始找
app = Flask(__name__,
            static_url_path='/static',# 静态文件访问 用户访问静态文件的路径
            static_folder='static', # 静态文件所存放的目录, 默认值static 服务器静态文件的路径
            template_folder='templates' # 表示模板文件存放的目录
            )


# ====加载配置===== #

# 对象中加载配置
class Config(object):
    DEBUG = True
app.config.from_object(Config)

# 文件中加载配置
app.config.from_pyfile('config.ini')

# 环境变量中加载配置
app.config.from_envvar('ENVCONFIG')

# 常用配置可直接调用app自带方法
app.debug = True

# 使用装饰器与视图函数进行关联
@app.route('/')
def index():
    return 'helloworld'

if __name__ == '__main__':
    # 运行当前flask程序
    app.run(host='127.0.0.1', port='8888', debug=True)
```



路由
==

### 返回字符串

```python
# 返回字符串
@app.route('/demo1')
def demo1():
    return 'demo1'
```

在路由设置中,我么定义好一个路径,该路径当做route()方法参数传递给了视图函数.return返回这个参数的值就可以返回相对应的字符串

### 动态返回接收到的动态参数

```python
# 返回接收到的动态参数
# <>动态路由参数,可以制定类型,视图函数需要接受这个参数
@app.route('/user/<int:user_id>')
def demo2(user_id):
    return 'demo2 %s' % user_id
```

在浏览器中我们给/user/后的url路径传递一个值,并发送给route()方法作为方法的参数.return返回这个参数

\<\>动态路由参数,可以制定类型,视图函数需要接受这个参数(必须接收这个参数)

### 返回响应方式

```python
from flask import Flask, request

# 返回响应方式
@app.route('/demo3', methods=['GET', 'POST'])
def demo3():
    return 'demo3 %s' % request.method
```

导入flask中的request模块

methods=['GET', 'POST'])

通过设置route()方法,指定该视图函数拥有GET/POST两种响应方式

返回值调用request.method方法,获取该视图函数用到了哪个响应方式

### 返回JSON

```python
from flask import Flask, json, jsonify

# 返回json
@app.route('/json')
def demo4():
    json_dict = {
        'name': 'DLC',
        'age': 24
    }
    # json.dumps将字典转换成json
    result_json = json.dumps(json_dict)
    # json.loads将json转换成字典
    result_dict = json.loads(result_json)

    # jsonify()将字典转换成json格式,并且改变响应类型为:Content-type:application/json
    return jsonify(json_dict)
```

导入flask中的json和jsonify模块

json模块:

json.dumps:将字典转换成json

json.loads:将json转换成字典

jsonify模块:

jsonify()将字典转换成json格式,并且改变响应类型为:Content-type:application/json

### 重定向

```python
from flask import Flask, redirect, url_for
# 重定向
@app.route('/redirect')
def demo5():
    # redirect()重定向到任何你想跳转的url
    # url_for:传递指定的视图函数所对应的URL,并且可以携带该URL所需要的参数
    return redirect(url_for('demo2', user_id=123))
```

redirect()重定向到任何你想跳转的url 如:redirect('http://baidu.com')

url\_for:传递指定的视图函数所对应的URL,并且可以携带该URL所需要的参数

### 返回自定义状态码

```python
# 返回自定义状态码
@app.route('/demo6')
def demo6():
    return 'demo6', 11
```

在返回视图函数的同时可以自定义状态码的值返回 作为状态信息

创建项目完整代码:
---------

```python
from flask import Flask, request, json, jsonify, redirect, url_for

app = Flask(__name__)


@app.route('/')
def index():
    return 'index'

# 返回字符串
@app.route('/demo1')
def demo1():
    return 'demo1'

# 返回接收到的动态参数
# <>动态路由参数,可以制定类型,视图函数需要接受这个参数
@app.route('/user/<int:user_id>')
def demo2(user_id):
    return 'demo2 %s' % user_id

# 返回响应方式
@app.route('/demo3', methods=['GET', 'POST'])
def demo3():
    return 'demo3 %s' % request.method

# 返回json
@app.route('/json')
def demo4():
    json_dict = {
        'name': 'DLC',
        'age': 24
    }
    # json.dumps将字典转换成json
    result_json = json.dumps(json_dict)
    # json.loads将json转换成字典
    result_dict = json.loads(result_json)

    # jsonify()将字典转换成json格式,并且改变响应类型为:Content-type:application/json
    return jsonify(json_dict)

# 重定向
@app.route('/redirect')
def demo5():
    # redirect()重定向到任何你想跳转的url
    # url_for:传递指定的视图函数所对应的URL,并且可以携带该URL所需要的参数
    return redirect(url_for('demo2', user_id=123))

# 返回自定义状态码
@app.route('/demo6')
def demo6():
    return 'demo6', 11

if __name__ == '__main__':
    app.run(debug=True)
```

自定义转换器
------

自定义转换器有两种方式:

1) 自定义一个现有的转换器比如正则转换器,更改它的规则

2) 重新编写一个新的转换器并且注册到默认的转换器列表中

### 自定义正则转换器转换规则

1) 导入转换器工具模块BaseConverter

```python
from werkzeug.routing import BaseConverter
```

2) 新建转换器规则类,继承系统中的路由转换器工具模块类,编写正则规则

```python
class RegexConberter(BaseConverter):
    """自定义正则转换器"""
    regex = "[0-9]{6}"
```

3) 更改后的正则转换器注册到系统默认转换器列表中

```python
# 将自定义转换器注册到系统默认转换器列表中
app.url_map.converters['re'] = RegexConberter
```

4) 启用自定义新正则转换器

```python
# 自定义转换器
@app.route('/user/<re:user_id>')
def demo1(user_id):
    return user_id
```

```python
from flask import Flask
from werkzeug.routing import BaseConverter


class RegexConberter(BaseConverter):
    """自定义正则转换器"""
    regex = "[0-9]{6}"


app = Flask(__name__)
# 将自定义转换器注册到系统默认转换器列表中
app.url_map.converters['re'] = RegexConberter


@app.route('/')
def index():
    return 'index'


# 自定义转换器
@app.route('/user/<re:user_id>')
def demo1(user_id):
    return user_id


if __name__ == '__main__':
    app.run(debug=True)
```

### 自定义新的转换器

1) 重写父类\_\_init\_\_方法,目的传进自定义规则的表达式 如:"[0-9]{6}”

url\_map:路由url

\*args:自定义转换器匹配规则

```python
class RegexConberter(BaseConverter):
    """自定义正则转换器"""
    # 重写父类__init__方法,目的传进自定义规则的表达式 如:"[0-9]{6}"
    def __init__(self, url_map, *args):
        super(RegexConberter, self).__init__(url_map)
        self.args = args[0]
```

2) 启动新的自定义转换器,并且传递规则

```python
# 自定义转换器
@app.route('/user/<re("[0-9]{6}"):user_id>')
def demo1(user_id):
    return user_id
```

```python
from flask import Flask
from werkzeug.routing import BaseConverter


class RegexConberter(BaseConverter):
    """自定义正则转换器"""
    # 重写父类__init__方法,目的传进自定义规则的表达式 如:"[0-9]{6}"
    def __init__(self, url_map, *args):
        super(RegexConberter, self).__init__(url_map)
        self.args = args[0]



app = Flask(__name__)
# 将自定义转换器注册到系统默认转换器列表中
app.url_map.converters['re'] = RegexConberter


@app.route('/')
def index():
    return 'index'


# 自定义转换器
@app.route('/user/<re("[0-9]{6}"):user_id>')
def demo1(user_id):
    return user_id


if __name__ == '__main__':
    app.run(debug=True)
```

### to\_python & to\_url

to\_python:

对已经匹配好的参数进行处理,并且返回给视图函数

to\_url:

对无法进行直接匹配的参数进行处理,并且返回给视图函数进行匹配

```python
from flask import Flask, redirect, url_for
from werkzeug.routing import BaseConverter

class ListConverter(BaseConverter):
    # 自定义转换器(匹配列表字符串user1,user2,user3)
    regex = "(\\d+,?)+\\d$"

    def to_python(self, value):
        # 匹配到参数后,对匹配到的参数进行处理,处理后返回给视图函数 如:字符串去逗号,变列表
        return value.split(',')

    def to_url(self, value):
        # 未匹配参数前,对获取到的参数进行处理,处理后进行参数的匹配 如:列表类型转换字符串
        result = ','.join(str(v) for v in value)
        return result

app = Flask(__name__)
# 将自定义转换器注册到系统默认转换器列表中
app.url_map.converters['list'] = ListConverter


@app.route('/')
def index():
    return 'index'


@app.route('/users/<list:user_ids>')
def demo2(user_ids):
    return '%s' % user_ids

@app.route('/demo3')
def demo3():
    return redirect(url_for('demo2', user_ids=[1,2,3,4,5]))


if __name__ == '__main__':
    app.run(debug=True)
```

抛出错误&错误捕获
---------

抛出错误:abort()

导入模块:from flask import abort

在视图函数里主动抛出HTTP指定错误状态码

全局捕获错误:

装饰器的形式传递错误参数,@app.errorhandler(参数)

该参数除了HTTP错误状态码以外,还可以将Python异常作为参数进行全局捕获

```python
@app.errorhandler(404)
def page_not_found(error):
    return "页面丢失404"
```

```python
from flask import Flask, abort

app = Flask(__name__)


@app.route('/')
def index():
    return 'index'


# abort 抛出错误
# 主动抛出HTTP指定错误状态码
@app.route('/demo1')
def demo1():
    abort(404)
    return 'demo1'


# @app.errorhandler() 全局捕获错误
# 除HTTP错误状态码以外还可以在@app.errorhandler()参数里面指定错误信息如:ZeroDivisionError等
@app.errorhandler(404)
def page_not_found(error):
    return "页面丢失404"


if __name__ == '__main__':
    app.run(debug=True)

```

请求钩子
----

@app.before\_first\_request:在第一次请求之前会访问该函数

@app.before\_request:在每次请求之前都会访问该函数

@app.after\_request:在请求之后调用,函数接收一个参数:响应,还需要将响应进行返回

@app.teardown\_request:请求之后执行,如果请求的函数报异常,会把异常传入到此函数

```python
from flask import Flask

app = Flask(__name__)


@app.route('/')
def index():
    return 'index'


@app.before_first_request
def before_first_request():
    """在第一次请求之前会访问该函数"""
    print('before_first_request')


@app.before_request
def before_request():
    """在每次请求之前都会访问该函数"""
    print('before_request')


@app.after_request
def after_request(response):
    """在请求之后调用,函数接收一个参数:响应,还需要将响应进行返回"""
    print('after_request')
    return response


@app.teardown_request
def teardown_request(error):
    """请求之后执行,如果请求的函数报异常,会把异常传入到此函数"""
    print('teardown_request')


if __name__ == '__main__':
    app.run(debug=True)

```

获取请求参数
======

data:获取请求的数据并转换为字符串

form:记录请求中的表单数据

args:记录请求中的查询数据

cookies:记录请求中的Cookie数据

headers:记录请求中的报文头

method:记录请求使用的HTTP方法

url:记录请求的URL地址

files:记录请求上传的文件

```python
from flask import Flask, request

app = Flask(__name__)


@app.route('/')
def index():
    return 'index'


@app.route('/upload', methods=['POST'])
def upload():
    file = request.files.get('pic')
    file.save('aaa.png')
    return 'success'

@app.route('/data', methods=['POST'])
def data():
    data = request.data
    print(data)
    return 'ok'

if __name__ == '__main__':
    app.run(debug=True)
    
```

状态保持
====

Cookie
------

### 设置/获取/删除

```python
from flask import Flask, request, make_response

app = Flask(__name__)

# 获取cookie
@app.route('/')
def index():
    user_id = request.cookies.get('user_id')
    user_name = request.cookies.get('user_name')
    return "user_id : {} user_name:{}".format(user_id, user_name)

# 设置cookie
# max_age=3600 cookie到期时间
@app.route('/login')
def login():
    response = make_response('success')
    response.set_cookie("user_id", "1", max_age=3600)
    response.set_cookie("user_name", "HenryDu", max_age=3600)
    return response

# 删除cookie
@app.route('/logout')
def logout():
    response = make_response('success')
    response.delete_cookie('user_id')
    response.delete_cookie('user_name')
    return response


if __name__ == '__main__':
    app.run(debug=True)

```

session
-------

### 设置

```python
from flask import Flask, session

app = Flask(__name__)
# 使用session必须设置SECRET_KEY
app.config['SECRET_KEY'] = '1234567890'

# 获取session
# session.get('session键名', '如果没有值返回空')
@app.route('/')
def index():
    user_id = session.get('user_id', '')
    user_name = session.get('user_name', '')
    return 'user_id:{}'.format(user_id) + '\n' + 'user_name:{}'.format(user_name)

# 设置session
@app.route('/login')
def login():
    session['user_id'] = '1'
    session['user_name'] = 'HenryDu'
    return 'success'

# 删除session
# session.pop('session名', 删除后返回None,防止session重复删除报错)
@app.route('/logout')
def logout():
    session.pop('user_id', None)
    session.pop('user_name', None)
    return 'success'


if __name__ == '__main__':
    app.run(debug=True)


```

上下文
====

请求上下文
------

请求上下文中的变量

### reques

### session

应用上下文
-----

应用上下文的变量

### current\_app

### g

Flask-script拓展
==============

```python
from flask import Flask
# 导入Flask-script包
from flask_script import Manager

app = Flask(__name__)
# 创建manager类初始化,并将app类传入manager
manager = Manager(app)

@app.route('/')
def inex():
    return 'success'


if __name__ == '__main__':
  # 运行
    manager.run()

# 终端启动命令 -d:debug -p:终端
# python learn_flask.py runserver -d -p 8080
```

jinja2模板
========

准备模板文件
------

### 

* 创建Templates模板文件夹并在pycharm中注册

### ![](resources/A95E0AF4883C1F67D46E3FC6F4D72849.jpg)

### 

* 在模板文件夹中创建html模板文件:index\_templates.html

```python
.
├── __pycache__
│   └── test.cpython-37.pyc
├── learn_flask.py
├── templates
│   └── index_templates.html
```

### 

* 设置模板语言

![](resources/BA32C6C0AEDB200453373890C9539AC5.jpg)

数据使用
----

### 传输数据

```python
from flask import Flask, render_template
from flask_script import Manager

app = Flask(__name__)
manager = Manager(app)


@app.route('/')
def inex():
    return 'success'


@app.route('/test_1')
def test_1():
    list = [1, 2, 3, 4, 5, 6]
    int = 100
    str = 'I love You'
    dict = {'name': {'name1': 'henry', 'name2': 'Tom'}}
    return render_template('index_templates.html', mylist=list, myint=int, mystr=str, mydict=dict)


if __name__ == '__main__':
    manager.run()
```

### 数据取值

```html
<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{#传输数据#}
传输数据: <br>
{{ myint }}<br>
{{ mydict }}<br>
{{ mylist }}<br>
{{ mystr }}<br>
<br>
{#取值#}
取值: <br>
{{ mydict['name']['name1'] }}<br>
{{ mylist[2] }}<br>
{{ mystr[2:6] }}<br>

flask特有:计算数据 <br>
{{ myint * 2 + mylist.2 }}
</body>
</html>
```

### 过滤器

{{ 数据 | 过滤器 }}

```python
@app.route('/test_1')
def test_1():
    list = [1, 2, 3, 4, 5, 6]
    int = 100
    str = '<h1>I love You</h1>'
    dict = {'name': {'name1': 'henry', 'name2': 'Tom'}}
    pric_dict = [{'good_name1':'pc', 'price':4000},{'good_name1':'mac', 'price':3000}]
    return render_template('index_templates.html', mylist=list, myint=int, mystr=str, mydict=dict, myprice=pric_dict)
```

```html
<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{#过滤器#}
过滤器 <br>
<br>
字符串过滤器 <br>
{{ mystr | upper }} <br>
{{ mystr | lower }} <br>
{{ mystr | reverse }} <br>

{#flask特有,多重过滤#}
flask特有,多重过滤 <br>
{{ mystr | reverse | upper }}<br>
<br>
<br>
{#列表过滤器#}
列表过滤器 <br>
{{ mylist | last }} <br>
{{ mylist | length }} <br>
{{ mylist | sort }} <br>


{#html的显示#}
{#如果得到<h1>test<h1/>类似的字符串,默认(escape)会原样显示,如果设置字符串过滤器设置为'safe'则会执行该字符串#}
{{ mystr | escape }} <br>
{{ mystr | safe }} <br>

{#过滤器传值#}
{{ myprice | sum('price') }}
</body>
</html>

```

### 自定义过滤器

```python
# 自定义过滤器
# 方式1:装饰器
@app.template_filter('list_reverse')
def list_reverse(list_data):
    # 使用list()新建一个列表,对新列表进行操作,不影响旧列表数据
    temp = list(list_data)
    temp.reverse()
    return temp
```

```python
# 方式2:直接添加
app.add_template_filter(方法对象, '过滤器名字')
app.add_template_filter(list_reverse, 'list_reverse')
```

控制代码块
-----

```python
@app.route('/test_1')
def test_1():
    list = [
        {
            "id": 1,
            "value": "轻轻的我走了"
        },
        {
            "id": 2,
            "value": "正如我轻轻的来"
        },
        {
            "id": 3,
            "value": "我轻轻的招手"
        },
        {
            "id": 4,
            "value": "作别西天的云彩"
        }
    ]
    return render_template('index_templates.html', mylist=list)
```

### for循环

{% for i in 迭代对象 %}

{% endfor %}

```html
<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{#控制代码块#}
{% for i in mylist %}
    <li>{{ i.value }}</li>
{% endfor %}

</body>
</html>
```

### if判断

{% if 数据 == 1 %}

{% elif 数据 == 2 %}

{% else %}

{% endif %}

| 变量         | 描述                                         |
| -------------- | ---------------------------------------------- |
| loop.index     | 当前循环迭代的次数（从 1 开始）  |
| loop.index0    | 当前循环迭代的次数（从 0 开始）  |
| loop.revindex  | 到循环结束需要迭代的次数（从 1 开始） |
| loop.revindex0 | 到循环结束需要迭代的次数（从 0 开始） |
| loop.first     | 如果是第一次迭代，为 True 。        |
| loop.last      | 如果是最后一次迭代，为 True 。     |
| loop.length    | 序列中的项目数。                       |
| loop.cycle     | 在一串序列间期取值的辅助函数。见下面示例程序。 |

```html
<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{#控制代码块#}
{% for i in mylist %}
    {% if loop.index == 1 %}
    <li style="background-color: red">{{ i.value }}</li>
    {% elif loop.index == 2 %}
    <li style="background-color: green">{{ i.value }}</li>
    {% elif loop.index == 3 %}
    <li style="background-color: orange">{{ i.value }}</li>
    {% else %}
    <li style="background-color: pink">{{ i.value }}</li>
    {% endif %}
{% endfor %}

</body>
</html>
```

模板代码复用
------

### 宏

使用语法:

{% macro %}

{% endmacro %}

引用宏文件:

{% import 'macro.html' as func %}

```html
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<form>
    传统方法:
    <labal>用户名</labal>
    <input type="text" name="username"><br>
    <labal>密码</labal>
    <input type="password" name="password"><br>
    <labal>确认密码</labal>
    <input type="password" name="password2"><br>
    <labal>身份证</labal>
    <input type="text" name="idcard"><br>
    <input type="submit" value="注册"><br>


    <hr>
    宏:
    {% macro input(label='',type='',value='', name='') %}
        <labal>{{ label }}</labal><input type="{{ type }}" name="{{ name }}"><br>
    {% endmacro %}

    <form>
        {{ input('用户名', name='username') }}
        {{ input('密码', name='password', type='password')}}
        {{ input('确认密码',name='password2', type='password') }}
        {{ input(type='submit', value='提交') }}

    </form>


    <hr>
    应用宏文件:
    {% import 'macro.html' as func %}
    <form>
        {{ func.input('用户名', name='username') }}
        {{ func.input('密码', name='password', type='password')}}
        {{ func.input('确认密码',name='password2', type='password') }}
        {{ func.input(type='submit', value='提交') }}
    </form>

</form>
</body>
</html>
```

### 继承

编写父类

```html
{% block 父类名 %}
(调用后被影藏的内容)
{% endblock %}
```

```html
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

我是顶部重复内容
<hr>
{% block contentBlock %}

我是父类中的内容 <br>
{% endblock %}

<hr>
我是底部重复内容

</body>
</html>
```

继承父类&super()方法

{% extends ‘父类文件名.html' %}

{% block 父类名 %}

 {{ super() }} : 需要调用父类里被子类隐藏掉的内容,调用super()方法,作用和python中super方法类似

{% endblock %}

```html
{% extends 'base.html' %}

{% block contentBlock %}
    (通过super()方法调取):
    {{ super() }}
    我是子类中的内容
{% endblock %}
```

### 包含

{% include ‘被包含的文件.html ignore missing %}

ignore missing : 忽略错误文件名

```html
-- 准备被包含的文件'include.html'
<h1>被包含的内容</h1>
```

```html
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

{% include 'include_error.html' ignore missing %}
{% include 'include.html' %}
{% include 'include.html' %}
{% include 'include.html' %}
{% include 'include.html' %}
</body>
</html>
```

模板中特有的变量和函数
-----------

Flask内置的变量在模板中获取

### config

```html
-- 请求flask中的配置信息config
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    {{ config['DEBUG'] }}
</body>
</html>
```

### request

```html
-- 获取flask中的request信息,比如当前url
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    {{ request.url }}
</body>
</html>
```

### session

```python
# 准备session值
from flask import Flask, render_template, session
from flask_script import Manager

app = Flask(__name__)
manger = Manager(app)
app.secret_key= 'uhfrgaugur'


@app.route('/')
def index():
    session['name'] = 'Tom'
    return render_template('index_templates.html')


if __name__ == '__main__':
    manger.run()
```

```html
-- 获取session值
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    {{ session.name }}
</body>
</html>
```

### g变量

应用上下文:g变量

```python
# 准备g变量
from flask import Flask, render_template, session, g
from flask_script import Manager

app = Flask(__name__)
manger = Manager(app)
app.secret_key= 'uhfrgaugur'


@app.route('/')
def index():
    g.name = 'HenryDu'
    session['name'] = 'Tom'
    return render_template('index_templates.html')


if __name__ == '__main__':
    manger.run()

```

```html
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    {{ g.name }}
</body>
</html>
```

### url\_for()

{{ url\_for('index') }}

index:为flask定义的路由函数名(不是路径名)

```html
-- 获取路由地址
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<a href="{{ url_for('index') }}">回到首页</a>
</body>
</html>
```

### get\_flashed\_messages()

获取闪现消息

```python
# 准备闪现消息
from flask import Flask, render_template, session, g, flash
from flask_script import Manager

app = Flask(__name__)
manger = Manager(app)
app.secret_key= 'uhfrgaugur'


@app.route('/')
def index():
    g.name = 'HenryDu'
    session['name'] = 'Tom'
    flash('闪现消息示例')
    return render_template('index_templates.html')


if __name__ == '__main__':
    manger.run()
```

```html
-- 获取闪现消息
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
{% for message in get_flashed_messages() %}
    {{ message }}
{% endfor %}
</body>
</html>
```

WTForm
======

```python
from flask import Flask, render_template, request, flash
from flask_script import Manager

app = Flask(__name__)
manger = Manager(app)

# flask-wtf 模块 python后台方式创建表单并进行表单验证
# 推展阅读:http://www.bjhee.com/flask-ext7.html
from flask_wtf import FlaskForm
# flask内建的表单验证工具
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import InputRequired, EqualTo

# 为session添加复杂度秘钥
app.secret_key = 'uhfrgaugur'
# 暂时取消csrf限制
app.config['WTF_CSRF_ENABLED'] = False


class RegisterForm(FlaskForm):
    username = StringField('用户名', validators=[InputRequired('请输入用户名')], render_kw={'placeholder': '占位文字'})
    password = PasswordField('密码', validators=[InputRequired('请输入密码')])
    password2 = PasswordField('确认密码', validators=[InputRequired('请输入确认密码'), EqualTo('password', '两者密码不一致')])
    submit = SubmitField('注册')


@app.route('/', methods=['GET', 'POST'])
def index():
    registerform = RegisterForm()
    if registerform.validate_on_submit():
        username = registerform.username.data
        password = registerform.password.data
        password2 = registerform.password2.data
        print(username)
        print(password)
        print(password2)
        return 'success'
    else:
        if request.method == 'POST':
            flash('参数错误')

    return render_template('index_templates.html', form=registerform)


if __name__ == '__main__':
    manger.run()

```

```html
<!doctype html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<form method="post">
    {{ form.username.label }}{{ form.username }}<br>
    {{ form.password.label }}{{ form.password }}<br>
    {{ form.password2.label }}{{ form.password2 }}<br>
    {{ form.submit }}
    {% for message in get_flashed_messages() %}
    {{ message }}
    {% endfor %}
</form>
</body>
</html>
```



CSRF攻击
------

```python
from flask import Flask, render_template, request, flash
from flask_script import Manager

app = Flask(__name__)
manger = Manager(app)

# flask-wtf 模块 python后台方式创建表单并进行表单验证
# 推展阅读:http://www.bjhee.com/flask-ext7.html
from flask_wtf import FlaskForm
# flask内建的表单验证工具
from wtforms import StringField, PasswordField, SubmitField
from wtforms.validators import InputRequired, EqualTo

# 为session添加复杂度秘钥
app.secret_key = 'uhfrgaugur'
# 设置csrf
app.config['WTF_CSRF_ENABLED'] = True


class RegisterForm(FlaskForm):
    username = StringField('用户名', validators=[InputRequired('请输入用户名')], render_kw={'placeholder': '占位文字'})
    password = PasswordField('密码', validators=[InputRequired('请输入密码')])
    password2 = PasswordField('确认密码', validators=[InputRequired('请输入确认密码'), EqualTo('password', '两者密码不一致')])
    submit = SubmitField('注册')


@app.route('/', methods=['GET', 'POST'])
def index():
    registerform = RegisterForm()
    if registerform.validate_on_submit():
        username = registerform.username.data
        password = registerform.password.data
        password2 = registerform.password2.data
        print(username)
        print(password)
        print(password2)
        return 'success'
    else:
        if request.method == 'POST':
            flash('参数错误')

    return render_template('index_templates.html', form=registerform)


if __name__ == '__main__':
    manger.run()
```

```html
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<form method="post">
    {{ form.csrf_token() }}
    {{ form.username.label }}{{ form.username }}<br>
    {{ form.password.label }}{{ form.password }}<br>
    {{ form.password2.label }}{{ form.password2 }}<br>
    {{ form.submit }}
    {% for message in get_flashed_messages() %}
    {{ message }}
    {% endfor %}
</form>

</body>
</html>
```

ORM数据库
======

```python
pip install flask-sqlalchemy
pip install flask-mysqldb
```

```python
from flask import Flask, render_template, make_response, request
from flask_script import Manager

app = Flask(__name__)
manager = Manager(app)
app.debug = True
app.secret_key = 'abcdefg'

# 设置mysql连接
app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:707116148@127.0.0.1:3306/learn_flask'
# 是否追踪数据库的修改
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
# 显示原始sql语句
app.config['SQLALCHEMY_ECHO'] = True
# ORM
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy(app)

class Role(db.Model):
    __talbename__ = 'role'

    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(60), unique=True)

    def __repr__(self):
        return 'Role %d %s' % (self.id, self.name)


@app.route('/')
def index():
    return 'ok'


if __name__ == '__main__':
    db.drop_all()
    db.create_all()
    manager.run()
```

Flask信号机制
=========



蓝图
==

1. 导入蓝图
2. 初始化蓝图
3. 蓝图注册url
4. 导入蓝图url
5. 注册蓝图到app

单元测试
====

























\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

insert

0

[{'pid': 8, 'product\_id': 'cp00000008', 'product\_name': '示例产品-机器人5', 'premarks': '产品备注8'}, {'pid': 7, 'product\_id': 'cp00000007', 'product\_name': '示例产品-机器人4', 'premarks': '产品备注7'}, {'p'cp00000006', 'product\_name': '示例产品-笔记本2', 'premarks': '产品备注6'}, {'pid': 5, 'product\_id': 'cp00000005', 'product\_name': '示例产品-笔记本1', 'premarks': '产品备注5'}, {'pid': 4, 'product\_id': 'cp0e': '示例产品-机器人3', 'premarks': '产品备注4'}, {'pid': 3, 'product\_id': 'cp00000003', 'product\_name': '示例产品-机器人2', 'premarks': '产品备注3'}, {'pid': 2, 'product\_id': 'cp00000002', 'product\_name': ': '产品备注2'}, {'pid': 1, 'product\_id': 'cp00000001', 'product\_name': '示例产品-主板', 'premarks': '示例产品备注1'}]

{'product\_id': '', 'product\_name': '', 'premarks': ''}

insert

()

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

[I 190508 10:25:04 web:2246] 200 GET /product (127.0.0.1) 14.49ms

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

modify

8

[{'pid': 8, 'product\_id': 'cp00000008', 'product\_name': '示例产品-机器人5', 'premarks': '产品备注8'}, {'pid': 7, 'product\_id': 'cp00000007', 'product\_name': '示例产品-机器人4', 'premarks': '产品备注7'}, {'p'cp00000006', 'product\_name': '示例产品-笔记本2', 'premarks': '产品备注6'}, {'pid': 5, 'product\_id': 'cp00000005', 'product\_name': '示例产品-笔记本1', 'premarks': '产品备注5'}, {'pid': 4, 'product\_id': 'cp0e': '示例产品-机器人3', 'premarks': '产品备注4'}, {'pid': 3, 'product\_id': 'cp00000003', 'product\_name': '示例产品-机器人2', 'premarks': '产品备注3'}, {'pid': 2, 'product\_id': 'cp00000002', 'product\_name': ': '产品备注2'}, {'pid': 1, 'product\_id': 'cp00000001', 'product\_name': '示例产品-主板', 'premarks': '示例产品备注1'}]

{'product\_id': 'cp00000008', 'product\_name': '示例产品-机器人5', 'premarks': '产品备注8'}

insert

[{'pfid': 1, 'pfield\_z\_name': '长度', 'pfield\_e\_name': 'width', 'pfield\_type': 'float', 'pfield\_default\_value': '0'}, {'pfid': 2, 'pfield\_z\_name': '长度', 'pfield\_e\_name': 'width', 'pfield\_type': 'float', 'ld\_default\_value': '0'}]

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

[I 190508 10:25:06 web:2246] 200 GET /product?command=modify&pid=8 (127.0.0.1) 9.07ms

[I 190508 10:25:08 web:2246] 200 POST /product (127.0.0.1) 7.35ms

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

modify

8

[{'pid': 8, 'product\_id': 'cp00000008', 'product\_name': '示例产品-机器人5', 'premarks': '产品备注8'}, {'pid': 7, 'product\_id': 'cp00000007', 'product\_name': '示例产品-机器人4', 'premarks': '产品备注7'}, {'p'cp00000006', 'product\_name': '示例产品-笔记本2', 'premarks': '产品备注6'}, {'pid': 5, 'product\_id': 'cp00000005', 'product\_name': '示例产品-笔记本1', 'premarks': '产品备注5'}, {'pid': 4, 'product\_id': 'cp0e': '示例产品-机器人3', 'premarks': '产品备注4'}, {'pid': 3, 'product\_id': 'cp00000003', 'product\_name': '示例产品-机器人2', 'premarks': '产品备注3'}, {'pid': 2, 'product\_id': 'cp00000002', 'product\_name': ': '产品备注2'}, {'pid': 1, 'product\_id': 'cp00000001', 'product\_name': '示例产品-主板', 'premarks': '示例产品备注1'}]

{'product\_id': 'cp00000008', 'product\_name': '示例产品-机器人5', 'premarks': '产品备注8'}

insert

[{'pfid': 1, 'pfield\_z\_name': '长度', 'pfield\_e\_name': 'width', 'pfield\_type': 'float', 'pfield\_default\_value': '0'}, {'pfid': 2, 'pfield\_z\_name': '长度', 'pfield\_e\_name': 'width', 'pfield\_type': 'float', 'ld\_default\_value': '0'}]

bug

1. 添加字符串类型数据报错 忘了改哪儿了
2. 主页产品倒叙 order by 排序
3. 无法显示商品页500错误 前端{{ row[field['pfield\_e\_name']] }}
4. 产品管理-添加属性无法删除
5. 多个属性后,无法添加属性 创建字段 一些数据类型不能直接创建 比如数字
6. 多次添加属性,错误,主页无法添加属性数据(但是会展示属性名称)
7. 重复保存数据属性表 出错 206行 sql = 'create table tb\_**’**
8. 点击主页重定向到index,index.html无法显示 main.html \<a href="/"\>\<h1\>\<span\>产品\</span\>管理\</h1\>\</a\>
9. 添加数据没有对数据类型做出提示和判定 对类型进行判定,try是否可以数据转换成str和float
10. 对产品添加属性字段,只填写一个,其他项目字段会为空,但是也会添加. 判定是否为空,如果中文名为空则提示用户错误
11. 添加属性,float类型如果不填写默认值,报错….. 创建表时判定如果没写float类型默认值则默认为0
12. 删除已有数据字段,无法正常提示原因 改成self.render("main.html", qx\_text='不能删除字段，因为该产品内已经有数据
13. 添加重复中文名字段 添加
14. 
15. 判断完中英文名是否重复,即使判定重复也会被添加
16. 无法再创建完表单后继续添加字段
17.























