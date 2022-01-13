语法
--

| 表达式  | 描述                                                   |
| ------  | ------                                                 |
| nodename| 选取次节点的所有子节点                                 |
| /       | 从根节点选取                                           |
| //      | 从匹配选的当前节点选择文档中的节点,而不考虑他们的位置  |
| .       | 选取当前节点                                           |
| ..      | 选取当前节点的父节点                                   |
| @       | 选取属性                                               |

### 获取文本内容:

//span[@class='login-btn login']/text()

### 获取标签属性:

//span[@class='login-btn login’]/@class

节点选择语法
------

| 表达式  | 描述                     |
| ------  | ------                   |
| /bookstore/book[1]                 | 获取属于bookstore子元素的第一个book元素                                     |
| /bookstore/book[last()]            | 获取属于bookstore子元素的最后一个book元素                                   |
| /bookstore/book[position()<3]      | 选取属于bookstore元素的子元素的book元素                                    |
| //title[@lang]                     | 获取所有拥有名为lang的属性的title元素                                      |
| //title[@lang='eng']               | 获取所有title元素,且这些元素拥有值为eng的lang属性                          |
| /bookstore/book[price>35.00]       | 选取booksrote元素的所有book元素,且切中的price元素的值须大于35.00           |
| /bookstore/book[price>35.00/title] | 选取bookstore元素中的book元素的所有title元素,且其中的price元素的值须大于35 |

### 获取多个同类标签中的一个(从1开始)

\# 获取第二个a标签的值

//div[@class='m-left-menu']/ul/a[2]

\# 获取倒数第二个标签的值(last()倒数)

//div[@class='m-left-menu']/ul/a[last()-2]

\# 获取前两个a标签的值position()

//div[@class='m-left-menu']/ul/a[position()\<3]

\# 获取下一页链接

//a[text()='下一页\>']/@href



