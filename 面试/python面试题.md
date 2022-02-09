1. 一行代码实现1--100之和

   ```python
   sum([i for i in range(1,101)])
   ```

2. 如何在一个函数内部修改全局变量

   ```python
   global
   ```

3. 列出5个python标准库

   ```python
   import os
   import sys
   import re
   import math
   import datetime
   ```

4. 字典如何删除键和合并两个字典

   ```python
   dict_1 = {"name_1":"peter", "age_1":30}
   dict_2 = {"name_2":"Tom", "age_2":29}
   
   # 合并
   dict_1.update(dict_2)
   print(dict_1)
   
   # 删除键
   dict_1.pop("name_1")
   print(dict_1)
   ```

   

5. 谈下python的GIL

   > GIL 是python的全局解释器锁
   >
   > > 一个进程里多个现成因为GIL锁只能先后进行
   > >
   > > 多个进程可以同时进行
   >
   > GIL 是python的全局解释器锁，同一进程中假如有多个线程运行，一个线程在运行python程序的时候会霸占python解释器（加了一把锁即GIL），使该进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程运行。所以在多线程中，线程的运行仍是有先后顺序的，并不是同时进行。
   >
   > 多进程中因为每个进程都能被系统分配资源，相当于每个进程有了一个python解释器，所以多进程可以实现多个进程的同时运行，缺点是进程系统资源开销大

   

6. python实现列表去重的方法

   ```python
   a = [1,2,3,4,4,5]
   print(list(set(a)))
   ```

7. fun(\*args,\*kwargs)中的*args,**kwargs什么意思？

   > \*args:不定长参数
   >
   > \**kwargs:不定长字典参数

   

8. python2和python3的range（100）的区别

   > python2返回列表
   >
   > python3返回迭代器（节省资源）

9. 一句话解释什么样的语言能够用装饰器?

   > 函数可以作为参数传递的语言，可以使用装饰器

10. python内建数据类型有哪些

    > 整型--int
    >
    > 布尔型--bool
    >
    > 字符串--str
    >
    > 列表--list
    >
    > 元组--tuple
    >
    > 字典--dict

11. 简述面向对象中__new__和__init__区别

    > __init__是初始化方法，创建对象后，就立刻被默认调用了，可接收参数，如图
    >
    > 1、__new__至少要有一个参数cls，代表当前类，此参数在实例化时由Python解释器自动识别
    >
    > 2、__new__必须要有返回值，返回实例化出来的实例，这点在自己实现__new__时要特别注意，可以return父类（通过super(当前类名, cls)）__new__出来的实例，或者直接是object的__new__出来的实例
    >
    > 3、__init__有一个参数self，就是这个__new__返回的实例，__init__在__new__的基础上可以完成一些其它初始化的动作，__init__不需要返回值
    >
    > 4、如果__new__创建的是当前类的实例，会自动调用__init__函数，通过return语句里面调用的__new__函数的第一个参数是cls来保证是当前类实例，如果是其他类的类名，；那么实际创建返回的就是其他类的实例，其实就不会调用当前类的__init__函数，也不会调用其他类的__init__函数。

12. 简述with方法打开处理文件帮我我们做了什么？

    ```python
    with open('./test_runoob.txt', 'w') as file:
        file.write('hello world !')
    ```

    > with 语句实现原理建立在上下文管理器之上。
    >
    > 上下文管理器是一个实现 **__enter__** 和 **__exit__** 方法的类。
    >
    > 使用 with 语句确保在嵌套块的末尾调用 __exit__ 方法。
    >
    > 这个概念类似于 try...finally 块的使用。

13. 列表[1,2,3,4,5],请使用map()函数输出[1,4,9,16,25]，并使用列表推导式提取出大于10的数，最终输出[16,25]

    ```python
    list = [1,2,3,4,5]
    def fn(x):
    	return(x ** 2)
    
    res = map(fn, list)
    res = [i for i in res if i > 10]
    print(res)
    ```

14. python中生成随机整数、随机小数、0--1之间小数方法

    ```python
    import random
    
    print(random.uniform(0, 1))
    ```

15. 避免转义给字符串加哪个字母表示原始字符串？

    > r , 表示需要原始字符串，不转义特殊字符

    ```python
    print(r"\n")
    ```

16. \<div class="nam">中国\</div>，用正则匹配出标签里面的内容（“中国”），其中class的类名是不确定的

    ```python
    import re
    str = '<div class="nam">中国</div>'
    res = re.findall(r'<div class=".*">(.*?)</div>', str)
    print(res)
    ```

17. python中断言方法举例

    >assert（）方法，断言成功，则程序继续执行，断言失败，则程序报错
    >

18. 数据表student有id,name,score,city字段，其中name中的名字可有重复，需要消除重复行,请写sql语句

    ```sql
    select distinct name from student;
    ```

19. 10个Linux常用命令

    > cd
    >
    > ls
    >
    > ll
    >
    > rm
    >
    > tar
    >
    > vi
    >
    > vim
    >
    > cp
    >
    > mv
    >
    > unzip
    >
    > wget

20. python2和python3区别？列举5个

    > Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')
    >
    > Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比如 print 'hi'
    >
    > python2 range(1,10)返回列表，python3中返回迭代器，节约内存
    >
    > python2中使用ascii编码，python中使用utf-8编码
    >
    > python2中unicode表示字符串序列，str表示字节序列
    >
    > python3中str表示字符串序列，byte表示字节序列
    >
    > python2中为正常显示中文，引入coding声明，python3中不需要
    >
    > python2中是raw_input()函数，python3中是input()函数

21. 列出python中可变数据类型和不可变数据类型，并简述原理

    > 不可变数据类型：数值型、字符串型string和元组tuple
    >
    > 不允许变量的值发生变化，如果改变了变量的值，相当于是新建了一个对象，而对于相同的值的对象，在内存中则只有一个对象（一个地址），如下图用id()方法可以打印对象的id
    >
    > 
    >
    > 可变数据类型：列表list和字典dict；
    >
    > 允许变量的值发生变化，即如果对变量进行append、+=等这种操作后，只是改变了变量的值，而不会新建一个对象，变量引用的对象的地址也不会变化，不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象

22. s = "ajldjlajfdljfddd"，去重并从小到大排序输出"adfjl"

    ```python
    str = 'ajldjlajfdljfddd'
    li = list(set(str))
    print(sorted(li))
    ```

23. 用lambda函数实现两个数相乘

    ```python
    fun = lambda x, y: x * y
    print(fun(2, 3)) 
    ```

24. 字典根据键从小到大排序

    ```python
    dict1={'a':2,'e':3,'f':8,'d':4}
    list1= sorted(dict1.keys(),reverse=False)
    dict = {}
    for i in list1:
        dict[i] = dict1[i]
        
    print(dict)
    ```

25. 利用collections库的Counter方法统计字符串每个单词出现的次数"kjalfj;ldsjafl;hdsllfdhg;lahfbl;hl;ahlf;h"

    ```python
    from collections import Counter
     
    a = "kjalfj;ldsjafl;hdsllfdhg;lahfbl;hl;ahlf;h"
    res = Counter(a)
    print(res)
    ```

26. 字符串a = "not 404 found 张三 99 深圳"，每个词中间是空格，用正则过滤掉英文和数字，最终输出"张三  深圳"

    ```python
    import re
    S = "not 404 found 张三 99 深圳"
    L = re.split("[\d+|(a-z)+]", S)  # ['', '', '', ' ', '', '', ' ', '', '', '', '', ' 张三 ', '', ' 深圳']
    print("".join(L).strip())
    ```

27. filter方法求出列表所有奇数并构造新列表，a =  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    ```python
    a = [1,2,3,4,5,6,7,8,9,10]
    
    def func(n):
        return n%2 ==1
    
    list1 =list(filter(func,a))
    
    print('filter奇数组表结果:',list1)
    ```

    

28. 列表推导式求列表所有奇数并构造新列表，a =  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    ```python
    a = [1,2,3,4,5,6,7,8,9,10]
    
    list = [i for i in a if i%2==1]
    print(list)
    ```

29. 正则re.complie作用

    > re.compile是将正则表达式编译成一个对象，加快速度，并重复使用
    >

30. a=（1，）b=(1)，c=("1") 分别是什么类型的数据？

    > 元组
    >
    > 整型
    >
    > 字符串

31. 两个列表[1,5,7,9]和[2,2,6,8]合并为[1, 2, 2, 5, 6, 7, 8, 9]

    ```python
    li_1 = [1,5,7,9]
    li_2 = [2,2,6,8]
    li = li_1 + li_2
    print(sorted(li))
    ```

32. 用python删除文件和用linux命令删除文件方法

    ```python
    os.remove() # 删除文件
    os.unlink() # 删除文件。 它是remove（）方法的Unix名称。
    shutil.rmtree() # 删除目录及其下面所有内容。
    pathlib.Path.unlink() # 在Python 3.4及更高版本中用来删除单个文件pathlib模块。
    ```

    ```shell
    rm -rf xxx.xx
    ```

    

33. log日志中，我们需要用时间戳记录error,warning等的发生时间，请用datetime模块打印当前时间戳 “2018-04-01 11:38:54”

    ```python
    import datetime
    
    date=str(datetime.datetime.now().strftime('%y-%m-%d %H:%M:%s'))+' 星期'+str(datetime.datetime.now().isoweekday())
    
    print(date)
    ```

34. 数据库优化查询方法

    > 外键、索引、联合查询、选择特定字段等等
    >

35. 请列出你会的任意一种统计图（条形图、折线图等）绘制的开源库，第三方也行

    > pychart、matplotlib
    >

36. 写一段自定义异常代码

    ```python
    def fn():
    	try:
    		for i in range(5):
    			if i > 2:
    				raise Exception("数字大于2了")
    	except Exception as ret:
    		print(ret)
    		
    fn()
    ```

    

37. 正则表达式匹配中，（.*）和（.*?）匹配区别？

    > (. *）是贪婪匹配，会把满足正则的尽可能多的往后匹配
    >
    > （. * ?）是非贪婪匹配，会把满足正则的尽可能少的匹配

38. 简述Django的orm

    > ORM：对象关系映射(Object Relational Mapping，简称ORM)
    >
    > 作用：根据类生成表结构，将对象、列表的操作转换成对象的SQL语句，将SQL语句查询的结果转换为对象或列表
    >
    > 优点：极大的减轻开发人员的工作量，不需要面对因数据库的变更而导致代码无效再修改代码

    > ORM，全拼Object-Relation Mapping，意为对象-关系映射
    >
    > 实现了数据模型与数据库的解耦，通过简单的配置就可以轻松更换数据库，而不需要修改代码只需要面向对象编程,orm操作本质上会根据对接的数据库引擎，翻译成对应的sql语句,所有使用Django开发的项目无需关心程序底层使用的是MySQL、Oracle、sqlite....，如果数据库迁移，只需要更换Django的数据库引擎即可

39. [[1,2],[3,4],[5,6]]一行代码展开该列表，得出[1,2,3,4,5,6]

    ```python
    li = [[1,2],[3,4],[5,6]]
    res = []
    for i in li:
    	for j in i:
    		res.append(j)
    		
    print(res)
    ```

    

40. x="abc",y="def",z=["d","e","f"],分别求出x.join(y)和x.join(z)返回的结果

    ```python
    x="abc"
    y="def"
    z=["d","e","f"]
    
    print(x.join(y))
    print(x.join(z))
    
    # dabceabcf
    # dabceabcf
    ```

41. 举例说明异常模块中try except else finally的相关意义

    > - try..except..else没有捕获到异常，执行else语句 
    > - try..except..finally不管是否捕获到异常，都执行finally语句

    ```python
    try:
        number = 100
        print(number)
    except Exception as err:
        print('产生了错误：%s',err)
    else:
        print('没有捕捉到错误')
        
        
    try:
        number = 100
        print(number)
    except Exception as err:
        print('产生了错误：%s',err)
    finally:
        print('无论是否捕捉到错误，都执行finally')
    ```

    

42. python中交换两个数值

    > a, b = b, a

43. 举例说明zip（）函数用法

    > zip()参数可以接受任何类型的序列，同时也可以有两个以上的参数;当传入参数的长度不同时，zip能自动以最短序列长度为准进行截取，获得元组

    ```python
    a = ['b','c','d']
    b = [1,1,1,1,5]
    res = zip(a,b)
    
    for i in res:
    	print(i)
      
     
    # ('b', 1)
    # ('c', 1)
    # ('d', 1)
    ```

    

44. a="张明 98分"，用re.sub，将98替换为100

    ```python
    import re
    
    a="张明 98分"
    res = re.sub(r'[0-9]+', "100", a)
    print(res)
    ```

    

45. 写5条常用sql语句

    ```sql
    truncate table student_info;
    SELECT COUNT('hobby') FROM student_info;
    SELECT COUNT(id) FROM students;
    select distinct name from student;
    select * from student;
    ```

    

46. a="hello"和b="你好"编码成bytes类型

    ```python
    a=b"hello"
    b="你好".encode()
    
    print(a)
    print(b)
    print(type(a))
    print(type(b))
    
    '''
    b'hello'
    b'\xe4\xbd\xa0\xe5\xa5\xbd'
    <class 'bytes'>
    <class 'bytes'>
    '''
    ```

    

47. [1,2,3]+[4,5,6]的结果是多少？

    ```python
    [1,2,3,4,5,6]
    ```

    

48. 提高python运行效率的方法

    > 1、使用生成器，因为可以节约大量内存
    >
    > 2、循环代码优化，避免过多重复代码的执行
    >
    > 3、核心模块用Cython  PyPy等，提高效率
    >
    > 4、多进程、多线程、协程
    >
    > 5、多个if elif条件判断，可以把最有可能先发生的条件放到前面写，这样可以减少程序判断的次数，提高效率

49. 简述mysql和redis区别

    > redis： 内存型非关系数据库，数据保存在内存中，速度快
    >
    > mysql：关系型数据库，数据保存在磁盘中，检索的话，会有一定的Io操作，访问速度相对慢

50. 遇到bug如何处理

    > 1、细节上的错误，通过print（）打印，能执行到print（）说明一般上面的代码没有问题，分段检测程序是否有问题，如果是js的话可以alert或console.log
    >
    > 2、如果涉及一些第三方框架，会去查官方文档或者一些技术博客。
    >
    > 3、对于bug的管理与归类总结，一般测试将测试出的bug用teambin等bug管理工具进行记录，然后我们会一条一条进行修改，修改的过程也是理解业务逻辑和提高自己编程逻辑缜密性的方法，我也都会收藏做一些笔记记录。

51. 正则匹配，匹配日期2018-03-20

    ```python
    import re
    
    str = '正则匹配，匹配日期2018-03-20'
    s = re.compile(r"(\d{4}-\d{1,2}-\d{1,2})").findall(str)
    
    print(s)
    ```

52. list=[2,3,5,4,9,6]，从小到大排序，不许用sort，输出[2,3,4,5,6,9]

    ```python
    list= [2,3,4,9,6]
    new_list = []
    def get_min(x):
        a = min(x)
        x.remove(a)
        new_list.append(a)
        if len(x)>0:
            get_min(x)
        return new_list
    
    new_List = get_min(list)
    print(new_List)
    ```

    

53. 写一个单列模式

    > - 因为创建对象时**new**方法执行，并且必须return 返回实例化出来的对象所cls.__instance是否存在，不存在的话就创建对象，存在的话就返回该对象，来保证只有一个实例对象存在（单列），打印ID，值一样，说明对象同一个

    ```python
    class Singleton(object):
        __instance = None
        def __new__(cls,age,name):
            if not cls.__instance:
                cls = object.__new__(cls)
            return cls.__instance
    a = Singleton(18,'donge')
    b = Singleton(8,'hau')
    print(id(a))
    print(id(b))
    ```

54. 保留两位小数

    ```python
    # 字符串
    a = "%.2f"%1.4546464
    
    # float
    b = 1.6555
    print(round(b,2))
    ```

55. 求三个方法打印结果

    > fn("one",1）直接将键值对传给字典；
    > fn("two",2)因为字典在内存中是可变数据类型，所以指向同一个地址，传了新的额参数后，会相当于给字典增加键值对
    > fn("three",3,{})因为传了一个新字典，所以不再是原先默认参数的字典

    ```python
    def fn(i,j,dic={}):
        dic[i] = j
        print(dic)
        
    fn("one",1) # {'one': 1}
    fn("two",2) # {'one': 1, 'two': 2}
    fn("three",3,{}) # {'three': 3}
      
    ```

    

56. 列出常见的状态码和意义

    > 200 OK 
    >
    > 请求正常处理完毕
    >
    > 204 No Content 
    >
    > 请求成功处理，没有实体的主体返回
    >
    > 206 Partial Content 
    >
    > GET范围请求已成功处理
    >
    > 301 Moved Permanently 
    >
    > 永久重定向，资源已永久分配新URI
    >
    > 302 Found 
    >
    > 临时重定向，资源已临时分配新URI
    >
    > 303 See Other 
    >
    > 临时重定向，期望使用GET定向获取
    >
    > 304 Not Modified 
    >
    > 发送的附带条件请求未满足
    >
    > 307 Temporary Redirect 
    >
    > 临时重定向，POST不会变成GET
    >
    > 400 Bad Request 
    >
    > 请求报文语法错误或参数错误
    >
    > 401 Unauthorized 
    >
    > 需要通过HTTP认证，或认证失败
    >
    > 403 Forbidden 
    >
    > 请求资源被拒绝
    >
    > 404 Not Found 
    >
    > 无法找到请求资源（服务器无理由拒绝）
    >
    > 500 Internal Server Error 
    >
    > 服务器故障或Web应用故障
    >
    > 503 Service Unavailable 
    >
    > 服务器超负载或停机维护

57. 分别从前端、后端、数据库阐述web项目的性能优化

    > 前端优化：
    >
    > 1、减少http请求、例如制作精灵图
    >
    > 2、html和CSS放在页面上部，javascript放在页面下面，因为js加载比HTML和Css加载慢，所以要优先加载html和css,以防页面显示不全，性能差，也影响用户体验差
    >
    > 
    >
    > 后端优化：
    >
    > 1、缓存存储读写次数高，变化少的数据，比如网站首页的信息、商品的信息等。应用程序读取数据时，一般是先从缓存中读取，如果读取不到或数据已失效，再访问磁盘数据库，并将数据再次写入缓存。
    >
    > 2、异步方式，如果有耗时操作，可以采用异步，比如celery
    >
    > 3、代码优化，避免循环和判断次数太多，如果多个if else判断，优先判断最有可能先发生的情况
    >
    > 
    >
    > 数据库优化：
    >
    > 1、如有条件，数据可以存放于redis，读取速度快
    >
    > 2、建立索引、外键等

58. 使用pop和del删除字典中的"name"字段，dic={"name":"zs","age":18}

    ```python
    dic_1={"name":"zs","age":18}
    dic_1.pop("name")
    print(dic_1)
    
    dict_2={"name":"zs","age":18}
    del dict_2['name']
    print(dict_2)
    ```

59. 列出常见MYSQL数据存储引擎

    > InnoDB：支持事务处理，支持外键，支持崩溃修复能力和并发控制。如果需要对事务的完整性要求比较高（比如银行），要求实现并发控制（比如售票），那选择InnoDB有很大的优势。如果需要频繁的更新、删除操作的数据库，也可以选择InnoDB，因为支持事务的提交（commit）和回滚（rollback）。 
    >
    > 
    >
    > MyISAM：插入数据快，空间和内存使用比较低。如果表主要是用于插入新记录和读出记录，那么选择MyISAM能实现处理高效率。如果应用的完整性、并发性要求比 较低，也可以使用。
    >
    > 
    >
    > MEMORY：所有的数据都在内存中，数据的处理速度快，但是安全性不高。如果需要很快的读写速度，对数据的安全性要求较低，可以选择MEMOEY。它对表的大小有要求，不能建立太大的表。所以，这类数据库只使用在相对较小的数据库表。

60. 计算代码运行结果，zip函数历史文章已经说了，得出[("a",1),("b",2)，("c",3),("d",4),("e",5)]

    > 不懂
    >
    > 参考：https://www.heywhale.com/mw/project/603dca4e04f2500015a27ce5

61. 简述同源策略

    > 同源策略需要同时满足以下三点要求： 
    >
    > 1）协议相同 
    >
    >  2）域名相同 
    >
    > 3）端口相同 
    >
    >  http:www.test.com与https:www.test.com 不同源——协议不同 
    >
    >  http:www.test.com与http:www.admin.com 不同源——域名不同 
    >
    >  http:www.test.com与http:www.test.com:8081 不同源——端口不同

62. 简述cookie和session的区别

    > 1，session 在服务器端，cookie 在客户端（浏览器）
    >
    > 2、session 的运行依赖 session id，而 session id 是存在 cookie 中的，也就是说，如果浏览器禁用了 cookie ，同时 session 也会失效，存储Session时，键与Cookie中的sessionid相同，值是开发人员设置的键值对信息，进行了base64编码，过期时间由开发人员设置
    >
    > 3、cookie安全性比session差

63. 简述多线程、多进程

    > 进程：
    >
    > 1、操作系统进行资源分配和调度的基本单位，多个进程之间相互独立
    >
    > 2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制
    >
    > 线程：
    >
    > 1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源
    >
    > 2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃
    >
    > 应用：
    >
    > IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间
    >
    > CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势

64. 简述any()和all()方法

    > any():只要迭代器中有一个元素为真就为真
    >
    > all():迭代器中所有的判断项返回都是真，结果才为真
    >
    > python中什么元素为假？
    >
    > 答案：（0，空字符串，空列表、空字典、空元组、None, False）
    >

65. IOError、AttributeError、ImportError、IndentationError、IndexError、KeyError、SyntaxError、NameError分别代表什么异常

    > IOError：输入输出异常
    >
    > AttributeError：试图访问一个对象没有的属性
    >
    > ImportError：无法引入模块或包，基本是路径问题
    >
    > IndentationError：语法错误，代码没有正确的对齐
    >
    > IndexError：下标索引超出序列边界
    >
    > KeyError:试图访问你字典里不存在的键
    >
    > SyntaxError:Python代码逻辑语法出错，不能执行
    >
    > NameError:使用一个还未赋予对象的变量

66. python中copy和deepcopy区别

    > 1、复制不可变数据类型，不管copy还是deepcopy,都是同一个地址当浅复制的值是不可变对象（数值，字符串，元组）时和=“赋值”的情况一样，对象的id值与浅复制原来的值相同。
    >
    > 2、复制的值是可变对象（列表和字典）
    >
    > 浅拷贝copy有两种情况：
    >
    > 第一种情况：复制的 对象中无 复杂 子对象，原来值的改变并不会影响浅复制的值，同时浅复制的值改变也并不会影响原来的值。原来值的id值与浅复制原来的值不同。
    >
    > 第二种情况：复制的对象中有 复杂 子对象 （例如列表中的一个子元素是一个列表）， 改变原来的值 中的复杂子对象的值  ，会影响浅复制的值。
    >
    > 深拷贝deepcopy：完全复制独立，包括内层列表和字典

67. 列出几种魔法方法并简要介绍用途

    > __init__:对象初始化方法
    >
    > __new__:创建对象时候执行的方法，单列模式会用到
    >
    > __str__:当使用print输出对象的时候，只要自己定义了__str__(self)方法，那么就会打印从在这个方法中return的数据
    >
    > __del__:删除对象执行的方法

68. C:Users y-wu.junyaDesktop>python 1.py 22 33命令行启动程序并传参，print(sys.argv)会输出什么数据？

    > 文件名和参数构成的列表

69. 请将[i for i in range(3)]改成生成器

    > 1、列表表达式的【】改为（）即可变成生成器
    >
    > 2、函数在返回值得时候出现yield就变成生成器，而不是函数了；

    ```python
    (i for i in range(3))
    ```

70. a = "  hehheh  ",去除收尾空格

    ```python
    a = "  hehheh  "
    print(a.replace(" ", ""))
    ```

71. 举例sort和sorted对列表排序，list=[0,-1,3,-10,5,9]

    ```python
    list=[0,-1,3,-10,5,9]
    print(sorted(list))
    ```

72. 对list排序foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4],使用lambda函数从小到大排序

    ```python
    foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4]
    sorted(foo, key=lambda x: x)
    sorted(foo, key=lambda x: x, reverse=True)

73. 使用lambda函数对list排序foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4]，输出结果为[0,2,4,8,8,9,-2,-4,-4,-5,-20]，正数从小到大，负数从大到小

    ```python
    # 要点：x<0 将列表正数放前面负数放后面；abs(x) 再按绝对值大小排序
    foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4]
    # 1.先按照绝对值大小进行排序获得新列表，再按照正数在前负数在后排序
    sorted(sorted(foo,key=lambda x:abs(x)),key=lambda x:x<0)  # [0,2,4,8,8,9,-2,-4,-4,-5,-20]
    # sorted(sorted(foo,key=lambda x:abs(x)),key=lambda x:x>=0)  # [-2,-4,-4,-5,-20,0,2,4,8,8,9]
    
    # 2.传两个条件，x<0和abs(x)；sorted() 中key的排序规则可以有多个
    sorted(foo,key=lambda x:(x<0, abs(x)))  # 
    # [0,2,4,8,8,9,-2,-4,-4,-5,-20]
    ```

74. 列表嵌套字典的排序，分别根据年龄和姓名排序foo = [{"name":"zs","age":19},{"name":"ll","age":54},{"name":"wa","age":17},{"name":"df","age":23}]

    ```python
    foo = [{"name": "zs", "age": 19}, {"name": "ll", "age": 54},{"name": "wa", "age": 17}, {"name": "df", "age": 23}]
    
    a = sorted(foo, key=lambda x: x['age'], reverse=True)
    print('按照年龄倒序排列：', a)
    
    a = sorted(foo, key=lambda x: x['name'])
    print('按照姓名排序：', a)
    ```

75. 列表嵌套元组，分别按字母和数字排序

    ```python
    foo = [("zs",19),("ll",54),("wa",17),("df",23)]
     
    # 按照年龄排序
    a = sorted(foo,key=lambda x:x[1],reverse=True)
    print(a)
    # 按照字母排序
    b = sorted(foo,key=lambda x:x[0])
    print(b)
    ```

76. 列表嵌套列表排序，年龄数字相同怎么办？

    ```python
    foo = [["zs",19],["ll",54],["wa",17],["sd",17],["df",73],["df",45]]
    res=sorted(foo,key=lambda x:(x[1],x[0]))
    print(res)
    ```

77. 根据键对字典排序（方法一，zip函数）(不懂)

    ```python
    foo={"name":"zs","age":19,'city':"shanghai","sex":"F"}
    k=zip(foo.keys(),foo.values())
    kk=[x for x in k]
    ss=sorted(kk,key=lambda x:x[0])
    new_dict={}
    for i in ss:
            new_dict.setdefault(i[0],i[1])
    print(new_dict)
    ```

78. 根据键对字典排序（方法二,不用zip)（不懂）

    ```python
    foo={"name":"zs","age":19,'city':"shanghai","sex":"F"}
    k=sorted(foo.keys())
    new_dict={}
    for i in k:
            new_dict.setdefault(i,foo[i])
    
    print(new_dict)
    ```

79. 列表推导式、字典推导式、生成器

    ```python
    import random
    td_list=[i for i in range (10) ]
    print("列表推导式",td_list,type(td_list))
    ge_list=(i for i in range(10))
    print("生成器",ge_list)
    dic={k:random.randint(4,9) for k in ["a", "b", "c", "d"]}
    print("字典推导式",dic, type(dic))
    
    '''
    列表推导式 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] <class 'list'>
    生成器 <generator object <genexpr> at 0x100e6d2e0>
    字典推导式 {'a': 4, 'b': 5, 'c': 4, 'd': 8} <class 'dict'>
    '''
    ```

80. 最后出一道检验题目，根据字符串长度排序，看排序是否灵活运用

    ```python
    a=['ab','abc','a','djkj']
    
    b=sorted(a,key=lambda x:len(x)) #sorted有返回值，不改变a本身
    print(a,b)
    a.sort(key=len) #sort无返回值，在a自身修改
    print(a)
    ```

81. 举例说明SQL注入和解决办法

    > 解决方式：通过传参数方式解决SQL注入

82. s="info:xiaoZhang 33 shandong",用正则切分字符串输出['info', 'xiaoZhang', '33', 'shandong']

    ```python
    import re
    
    s="info:xiaoZhang 33 shandong"
    res=re.split(r":| ",s) #|表示或，根据冒号或者空格切分
    print(res)
    ```

83. 正则匹配以163.com结尾的邮箱

    ```python
    import re
    
    email_list= ["xiaoWang@163.com","xiaoWang@163.comheihei", ".com.xiaowang@qq.com" ]
    for email in email_list:
            ret = re.match("[\w]{4,20}@163\.com$",email)
    if ret:
            print("%s 是符合规定的邮件地址，匹配后结果是:%s" % (email,ret.group()))
    else:
            print("%s 不符合要求" % email)
    ```

84. 递归求和

    ```python
    def get_sum(num):
        if num >= 1:
            res = num + get_sum(num - 1)
        else:
            res = 0
        return res
    
    res = get_sum(10)
    print(res)
    ```

85. python字典和json字符串相互转化方法

    ```python
    import json
    
    dic = {"name":"zs"}
    res = json.dumps(dic)
    print(res,type(res))
    ret = json.loads(res)
    print(ret,type(ret))
    
    '''
    {"name": "zs"} <class 'str'>
    {'name': 'zs'} <class 'dict'>
    '''
    ```

86. MyISAM 与 InnoDB 区别：

    >  1、InnoDB 支持事务，MyISAM 不支持，这一点是非常之重要。事务是一种高级的处理方式，如在一些列增删改中只要哪个出错还可以回滚还原，而MyISAM就不可以了；
    >
    > 2、MyISAM 适合查询以及插入为主的应用，InnoDB 适合频繁修改以及涉及到安全性较高的应用；
    >
    > 3、InnoDB 支持外键，MyISAM 不支持；
    >
    > 4、对于自增长的字段，InnoDB 中必须包含只有该字段的索引，但是在 MyISAM表中可以和其他字段一起建立联合索引；
    >
    > 5、清空整个表时，InnoDB 是一行一行的删除，效率非常慢。MyISAM 则会重建表；

87. 统计字符串中某字符出现次数

    ```python
    str="张三 哈哈 张三 呵呵 张三"
    res=str.count("张三")
    print(res)
    ```

88. 字符串转化大小写

    ```python
    str="HHaa"
    
    print(str.upper())
    print(str.lower())
    ```

89. 用两种方法去空格

    ```python
    str="hello world ha ha"
    
    res=str.replace(" ","")
    print(res)
    
    list=str.split(" ")
    res="".join(list)
    print(res)
    ```

90. 正则匹配不是以4和7结尾的手机号

    ```python
    import re
    
    tels=["13100001234","18912344321","10086","18800007777"]
    
    for tel in tels:
        ret=re.match("1\d{9}[0-3,5-6,8-9]",tel)
    if ret:
        print("结果是：",ret.group())
    else:
        print("%s不是想要的手机号" % tel)
    ```

91. 简述python引用计数机制

    > python垃圾回收主要以引用计数为主，标记-清除和分代清除为辅的机制，其中标记-清除和分代回收主要是为了处理循环引用的难题。
    >
    > 引用计数算法
    >
    > 当有1个变量保存了对象的引用时，此对象的引用计数就会加1
    >
    > 当使用del删除变量指向的对象时，如果对象的引用计数不为1，比如3，那么此时只会让这个引用计数减1，即变为2，当再次调用del时，变为1，如果再调用1次del，此时会真的把对象进行删除

92. int("1.4"),int(1.4)输出结果？

    ```python
    print(int("1.4")) #报错ValueError
    
    print(int(1.4)) # 1
    ```

93. 列举3条以上PEP8编码规范

    > 1、顶级定义之间空两行，比如函数或者类定义。
    > 2、方法定义、类定义与第一个方法之间，都应该空一行
    > 3、三引号进行注释
    > 4、使用Pycharm、Eclipse一般使用4个空格来缩进代码

94. 正则表达式匹配第一个URL

    > findall结果无需加group(),search需要加group()提取

    ```python
    import re 
      
    def Find(string): 
        # findall() 查找匹配正则表达式的字符串
        url = re.findall('https?://(?:[-\w.]|(?:%[\da-fA-F]{2}))+', string)
        return url 
          
    string = 'Runoob 的网页地址为：https://www.runoob.com，Google 的网页地址为：https://www.google.com'
    print("Urls: ", Find(string)[0])
    ```

95. 正则匹配中文

    ```python
    import re
    
    title="你好，hello，世界"
    res=re.compile(r'[\u4e00-\u9fa5]+')
    result=res.findall(title)
    print(result)
    ```

96. 简述乐观锁和悲观锁

    ```python
    悲观锁, 就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。
    
    乐观锁，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制，乐观锁适用于多读的应用类型，这样可以提高吞吐量
    ```

97. r、r+、rb、rb+文件打开模式区别

    | 模式 | 描述                                                         |
    | ---- | :----------------------------------------------------------- |
    | t    | 文本模式 (默认)。                                            |
    | x    | 写模式，新建一个文件，如果该文件已存在则会报错。             |
    | b    | 二进制模式。                                                 |
    | +    | 打开一个文件进行更新(可读可写)。                             |
    | U    | 通用换行模式（不推荐）。                                     |
    | r    | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
    | rb   | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。 |
    | r+   | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
    | rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。 |
    | w    | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
    | wb   | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
    | w+   | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
    | wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
    | a    | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
    | ab   | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
    | a+   | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |

98. Linux命令重定向 > 和 >>

    > Linux 允许将命令执行结果 重定向到一个文件
    >
    > 将本应显示在终端上的内容 输出／追加 到指定文件中
    >
    > \> 表示输出，会覆盖文件原有的内容
    >
    > \>> 表示追加，会将内容追加到已有文件的末尾
    >
    > 用法示例：
    >
    > 将 echo 输出的信息保存到 1.txt 里echo Hello Python > 1.txt
    >
    > 将 tree 输出的信息追加到 1.txt 文件的末尾tree >> 1.txt

99. 正则表达式匹配出\<html>\<h1>www.baidu.com\</h1>\</html>

    ```python
    import re
    
    source = "<html><h1>www.baidu.com</h1></html>"
    pat = re.compile("<html><h1>(.*?)</h1></html>")
    print(pat.findall(source)[0])
    ```

100. python传参数是传值还是传址？

     > Python中函数参数是引用传递（注意不是值传递）。对于不可变类型（数值型、字符串、元组），因变量不能修改，所以运算不会影响到变量自身；而对于可变类型（列表字典）来说，函数体运算可能会更改传入的参数变量。

101. 求两个列表的交集、差集、并集

     ```python
     a= [1,2,3,4]
     b= [4,3,5,6]
     
     jj1=[i for i in a if i in b] #在a中的i，并且也在b中，就是交集
     jj2=list(set(a).intersection(set(b)))
     bj1=list(set(a).union(set(b)))
     cj1=list(set(b).difference(set(a)))
     cj2=list(set(a).difference(set(b)))
     
     print("交集", jj1)
     print("交集", jj2)
     print("并集", bj1)
     print("差集", cj1)
     print("差集", cj2)
     ```

102. 生成0-100的随机数

     ```python
     import random
     
     res1=100* random. random( ) #随机小数 random.random()生成0-1之间的随机小数，所以乘以100
     res2= random.choice( range(0,101)) #随机整数
     res3= random.randint(1,100) #随机整数
     
     print(res1)
     print(res2)
     print(res3)
     ```

103. lambda匿名函数好处

     > 精简代码，lambda省去了定义函数，map省去了写for循环过程
     >

104. 常见的网络传输协议

     > UDP、TCP、FTP、HTTP、SMTP等等
     >

105. 单引号、双引号、三引号用法

     > 1、单引号和双引号没有什么区别，不过单引号不用按shift，打字稍微快一点。表示字符串的时候，单引号里面可以用双引号，而不用转义字符,反之亦然。'She said:"Yes." ' or  "She said: 'Yes.' "
     >
     > 2、但是如果直接用单引号扩住单引号，则需要转义，像这样： ' She said:'Yes.' '
     >
     > 3、三引号可以直接书写多行，通常用于大段，大篇幅的字符串
     >
     > """
     >
     > hello
     >
     > world
     >
     > """

106. python垃圾回收机制

     > python垃圾回收主要以引用计数为主，标记-清除和分代清除为辅的机制，其中标记-清除和分代回收主要是为了处理循环引用的难题。
     >
     > 引用计数算法
     > 当有1个变量保存了对象的引用时，此对象的引用计数就会加1
     >
     > 当使用del删除变量指向的对象时，如果对象的引用计数不为1，比如3，那么此时只会让这个引用计数减1，即变为2，当再次调用del时，变为1，如果再调用1次del，此时会真的把对象进行删除

107. HTTP请求中get和post区别

     > 1、GET请求是通过URL直接请求数据，数据信息可以在URL中直接看到，比如浏览器访问；而POST请求是放在请求头中的，我们是无法直接看到的；
     >
     > 2、GET提交有数据大小的限制，一般是不超过1024个字节，而这种说法也不完全准确，HTTP协议并没有设定URL字节长度的上限，而是浏览器做了些处理，所以长度依据浏览器的不同有所不同；POST请求在HTTP协议中也没有做说明，一般来说是没有设置限制的，但是实际上浏览器也有默认值。总体来说，少量的数据使用GET，大量的数据使用POST。
     >
     > 3、GET请求因为数据参数是暴露在URL中的，所以安全性比较低，比如密码是不能暴露的，就不能使用GET请求；POST请求中，请求参数信息是放在请求头的，所以安全性较高，可以使用。在实际中，涉及到登录操作的时候，尽量使用HTTPS请求，安全性更好。

108. python中读取Excel文件的方法

     ```python
     # 未验证
     import openpyxl
     
     # Define variable to load the wookbook
     wookbook = openpyxl.load_workbook("sales.xlsx")
     
     # Define variable to read the active sheet:
     worksheet = wookbook.active
     
     # Iterate the loop to read the cell values
     for i in range(0, worksheet.max_row):
         for col in worksheet.iter_cols(1, worksheet.max_column):
             print(col[i].value, end="\t\t")
         print('')
     ```

     

109. 简述多线程、多进程

     > 进程：
     >
     > 1、操作系统进行资源分配和调度的基本单位，多个进程之间相互独立
     >
     > 2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制
     >
     > 
     >
     > 线程：
     >
     > 1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源
     >
     > 2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃
     >
     > 应用：
     >
     > IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间
     >
     > CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势

110. python正则中search和match

     > match()和search()两者都是测试正则表达式与字符串是否匹配。不同的是，match() 如果在字符串的开头有0个或更多个字符，符合正则表达式模式，返回相关匹配的实例对象，如果字符串不符合正则表达式模式则返回None；而search()则不同，扫描整个字符串，如果产生了一个匹配正则模式就寻找到这个位置，返回相关匹配的对象。如果没有位置能够匹配这个模式则返回None。



其余80题见：https://juejin.cn/post/6982089270722822181









