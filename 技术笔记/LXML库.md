导入lxml的etree库

```python
from lxml import etree
```

利用etree.HTML,将字符串专户为Element对象

Element对象具有xpath方法

```python
# coding=utf-8
from lxml import etree

text = ''' <div> <ul> 
            <li class="item-1"><a>first item</a></li> 
            <li class="item-1"><a href="link2.html">second item</a></li> 
            <li class="item-inactive"><a href="link3.html">third item</a></li> 
            <li class="item-1"><a href="link4.html">fourth item</a></li> 
            <li class="item-0"><a href="link5.html">fifth item</a> 
            </ul> </div> '''

temp_html = etree.HTML(text)
print(temp_html)

print(etree.tostring(temp_html).decode())  #查看经过etree处理后的html
print("-----------------------------------")
# class = item-1 的li下的a的所有的href
href_list = temp_html.xpath("//li[@class='item-1']/a/@href")
print(href_list)

# class = item-1 的li下的a的所有的文本
text_list = temp_html.xpath("//li[@class='item-1']/a/text()")
print(text_list)

# 假设每个li都是一条新闻，把新闻的数据组成一个字典
list_temp = temp_html.xpath("//li[@class='item-1']")
print(list_temp)
for li in list_temp:
    item = {}
    item["href"] = li.xpath("./a/@href")[0] if len(li.xpath("./a/@href")) > 0 else None
    item["title"] = li.xpath("./a/text()")[0] if len(li.xpath("./a/text()")) > 0 else None
    print(item)

```