HTML标签:
-------

 尖括号”\<“开头

 \<标签名\>\</标签名\>

 属性:

 \<标签名 属性\>\</标签名\>

常用标签:
-----

```html
<!--常用标签:-->
<head><!--标题标签-->
  <titile><!--头部标签--></title>    
</head>   
<bodu><!--页面内容标签-->
</body>

```

标题标签:

```html
<body>
    <h1>标题标签</h1>
    <h2>标题标签2</h2>
</body>
```

链接标签

```html
<body>
    <!-- href:链接路径(网址)
    _blank 空白页面 -->
    <a href="../Desktop/text" target="_blank">链接标签</a>
    <a href="baidu.com">百度链接</a>
</body>
```

图片标签:

```html
<body>
    <!-- src:图片地址
    alt:图片备注(图片不存在提示,爬虫) 
    title:鼠标悬浮提示
    width:height:(指定图片长宽)
    -->
    <img src="./DSC_9025.jpg" alt="图片" title="一个图片" width="120px" height="100px">
</body>
```

换行标签:

段落标签:

```html
<body>
    <!-- 换行标签<br />(单标签) -->
    <!-- 段落标签 <p> </p> -->
    <p>testtesttest</p>
    <p>testtesttest</p>
    <p>testtest<br />test</p>

    <!-- 字符实体 -->
    <!-- 
    > &gt;
    < &lt;
    空格 &nbsp -->
    <p>&nbsp&nbsp&nbsp&nbsptesttesttest</p>
    <p>testtesttest</p>

</body>
```

div标签

span标签

```html
<body>
    <!-- div标签 span标签 没有语义 经常使用 用于布局
    <div>div标签</div> 
    <span>人工智能</span>
    div 布局的时候使用
    span 某段内容
    -->
</body>
```

CSS:
====

行内式

嵌入式

外链式

```html
    <style>
        p{
            font-size: 50px;
            font-family: "Microsoft Yahei";
            flood-color: red;
            /* 行高 :上顶点 + 文字宽度 + 下底点 = 行高*/
            line-height: 50px;

            /* 添加下划线 */
            text-decoration: underline;
        }

        a{
            /* 去掉下划线 */
            text-decoration: none;
        }
    </style>
</head>
<body>
    <p>段落标签</p>
     <a href="">更多&gt;&gt;</a>

</body>
```

### div边距margin:

```html
  <style>
       div{
           width: 100px;
           height: 100px;
           background-color: red;
            /* 边距 */
           margin-top: 30px;
           margin-left: 100px;
           margin-right: 100px;
           margin-bottom: 100px;

           /* 连写 */
           margin: 40px;
            /* 上下 左右 */
           margin: 10px 20px;
            /* 上 左右 下 */
           margin: 10px 20px 30px;
            /* 上 右 下 左 顺时针*/
           margin: 10px 20px 30px 50px;

           /* 元素(标签 标记) 水平居中 */
           /* 系统自动计算 */
           margin: 0 auto;
           


       }
    </style>
</head>
<body>
    <div>第一个</div>
    <div>第二个</div>

</body>
```

### 内边距:padding

```html
 <style>
       div{
           width: 300px;
           height: 300px;
           background-color: red;

           /* 内边距padding */
           padding-top: 10px;
           padding-left: 5px;
           padding-right: 5px;
           padding-bottom: 10‰px;


       }
    </style>
</head>
<body>
    <div>div的文字内容只是一部分div的文字内容只是一部分div的文字内容只是一部分
        div的文字内容只是一部分div的文字内容只是一部分div的文字内容只是一部分
        div的文字内容只是一部分div的文字内容只是一部分div的文字内容只是一部分
        div的文字内容只是一部分div的文字内容只是一部分</div>

</body>
```

### 示例:今日头条

```html
 <style>
        

        .box{
            /* 最外侧div */
            width: 285px;
            height: 410px;
            background-color: grey;
            /* 上下文字边框 */
            border-top: 1px solid red;
            border-bottom: 1px solid red;
        }

        img{
            width: 285px;
            height: 100;
        }
        .head{
            height: 40px;
        }

         .head h1{
            font-size: 16px;
            font-family: "microsoft yahei";
            color: #172c45;

            /* 左浮动 */
            float:left;
        }
        .head a{
            font-size: 12px;
            font-family: "microsoft yahei";
            color: #172c45;
            text-decoration:none;

            /* 右浮动 */
            float: right;

            /* 文字上下居中 */
            line-height: 40px;

        }

        .box p{
            font-size: 12px;
            font-family: "microsoft yahei";
            color: black;


        }




    </style>

</head>

<body>
    <div class="box">


        <!-- 头部 -->
        <div class="head">
            <h1>今日头条</h1>
            <a href="baidu.com">更多&gt;&gt;</a>
        </div>


        <!-- 图片 -->
        <img src="./background-cover.jpg" alt="图片" title="背景图片">

        <!-- 段落 -->
            <p>
                &nbsp;&nbsp;&nbsp;&nbsp; 
                测试测试测试测试测试测试测试
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试 
                测试测试测试测试测试测试测试
            </p>

    </div>
```

### 文本对齐 首行缩进:

```html
    <style>
        .box{
            width: 500px;
            height: 1000px;
            background-color: black;

            /* 文本对齐 */
            text-align: left;

            /* 首行缩进 默认16px*/
            text-indent: 21px;
            text-indent: 2em;

            /* 斜体 */
            font-style: italic;

            /* 是否加粗 */
            font-weight: bold;

            /* 文字大小/字体/行距 */
            font-size: 20px;
            font-family: "microsoft yahei";
            line-height: 20px;
            
        }
        
    </style>
```

### 选择器:ID选择器/类选择器/层级选择器/伪类选择器/集合选择器

```html
    <style>
        /* ID选择器 */
        #test01{
            color: blue;
        }
        /* 类选择器 */
        .test02{
            color: gold;
        }
        /* 层级选择器 */
        p span{
            color:green;
        }

        /* 并集选择器 */
        /* strong 重要的内容 默认加粗 */
        span,strong{
            color: red;
        }        
        
        /* 伪类 选择器 
        鼠标选择器
        before:
        after
        */
        a:hover{
            color: orange;
        }
        a:before{
            content: "前面增加的内容"
        }
        a:after{
            content: "后面增加的内容";
        }

        .test03{
            /* 斜体 */
            font-style: italic;
            /* 加粗 */
            font-weight: bold;
        }
    </style>
```

### 元素溢出:overflow:

```html
<style>
       .box{
           width: 200px;
           height: 200px;
           border: 1px solid red;

           /* 元素溢出 */
           /* 全部可见 */
           overflow: visible;
           /* 隐藏,删除多余内容 */
           overflow: hidden;
           /* 滚动查看 */
           /* overflow: auto; */
           overflow: scroll;
       }
       
    </style>
```

### 列表:ol/ul/定义列表

```html
<div class="box">
        <!-- 1)有序列表 
        ol li 组标签
        ol order list
        li lis
        -->
        <ol type="i">
            <li>test01</li>
            <li>test02</li>
            <li>test03</li>
        </ol>

        <!-- 2)无序列表 
        ul li
        ul unorder list
        li list

        type=disc/square/circle

        经常使用无序列表
        -->

        <ul type="circle">
            <li>test01</li>
            <li>test02</li>
            <li>test03</li>
        </ul>
        
        <!-- 定义列表
    dl defination list
    dd defination description 内容
    -->
    <dl>
        <dt>高级会员</dt>
        <dd>海量大片无限量</dd>
        <dd>海量大片无限量</dd>
        <dd>海量大片无限量</dd>

    </div>
```

### 

### input表单用法:

**Type:属性:**

**text**

**hidden**

**button**

**Password**

**r****adio**

**f****ile**

**checkbox**

**Submit + reset**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>06-表单1</title>
</head>
<body>
        <!-- 06-表单1
        action: 提交网址  默认是当前网址; 自定义
        method:默认:"get" post
        -->
        <form action="" method="post">

            <p>
                <!-- 1.用户名 -->
                <label for="xx">用户名:</label>
                <input id="xx" type="text" placeholder="请输入用户名" name="username">
            </p>
            
           <p>
                <!-- 2.密码 -->
                <label for="">密&nbsp;&nbsp;&nbsp;码:</label>
                <input type="password" name="pwd">
           </p>

           <p>
                <!-- 3.性别 -->
                <label for="">性&nbsp;&nbsp;&nbsp;别 :</label>
                <input type="radio" name="sex" value="0">男
                <input type="radio" name="sex" value="1">女
           </p>

           <p>
                <!-- 4.爱好-->
                <label for="">爱&nbsp;&nbsp;&nbsp;好 :</label>
                <input type="checkbox" name="like" value="0">妹子
                <input type="checkbox" name="like" value="1">汉子
                <input type="checkbox" name="like" value="2">健身
                <input type="checkbox" name="like" value="3">游泳
           </p>

           <p>
                <!-- 5.上传文件 -->
                <label for="">玉&nbsp;&nbsp;&nbsp;照:</label>
                <input type="file" name="file">
           </p>

           <p>
                <!-- 6.下拉列表 -->
                <label for="">籍&nbsp;&nbsp;&nbsp;贯:</label>
                <select name="address" id="">
                    <option value="0">北京</option>
                    <option value="1">上海</option>
                    <option value="2">广州</option>
                    <option value="3" selected="selected">深圳</option>
                </select>
           </p>

           <p>
                <!-- 7.文本域
                cols="30" rows="10"
                -->
                <label for="">个人描述:</label>
                <textarea name="info" id="" ></textarea>
           </p>

           <!-- 10.隐藏域 -->
           <input type="hidden" name="isVip" value="yes">
           <!-- 11.普通按钮 -->
           <input type="button" value="普通按钮">

            <!-- 8.注册 -->
            <input type="submit" value="注册">
            <!-- 9.重置 -->
            <input type="reset">

        </form>
    
</body>
</html>
```

盒子模式:
-----

盒子的真是高度 = border的上下 + padding的上下 + 内容;

盒子的真是宽度 = border的左右 + padding的左右 + 内容

```html
<style>
        .box{
            height: 200px;
            width: 200px;
            background: red;

            /* 边框border */
            border-top: 20px solid green;
            border-bottom: 20px solid gold;

            /* 内边距 */
            padding-left: 40px;
            padding-right: 40px;

            /* 外边距 (不会影响div大小)*/
            margin-top: 100px;
            
            /* 盒子的真是高度 = border的上下 + padding的上下 + 内容;
            盒子的真是宽度 = border的左右 + padding的左右 + 内容 */

            

        }
    </style>

</head>
<body>
    <div class="box">
         To run the visualization locally you just need a server to serve all the files from the dist directory. You can run npm
        install then npm run serve if you don't have one handy. To see the visualization, visit http://localhost:8080/ on
        your browser. When

    </div>
```

### Margin技巧:

```html
<style>
        .box1{
            width: 200px;
            height: 200px;
            border: 10px solid green;

            /* 元素居中 */
            /* margin: 0 auto; */

            margin-top: 100px;
        }

        .box2{
            width: 200px;
            height: 200px;
            border: 10px solid green;
            
            /* 负值 合并边框 */
            margin-top: -10px;
        }

    </style>
</head>
<body>
    <div class="box1"></div>
    <div class="box2"></div>

</body>
```

### Margin样例:

```html
<style>
        .box{
            width: 200px;
            height: 154px;
            border: 1px solid green;
        }
        .box div{
            height: 30px;
            border-top: 1px solid green;
            background-color: gold;

        }
        .box .first{
            margin-top: -1px;
        }
    </style>
</head>
<body>
    <div class="box">
        <div class="first"></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </div>
```

### 垂直外边距合并:

垂直外边距合并:谁大取谁

```html
    <style>
        .box{
            width:100px;
            height: 100px;
            border: 10px solid red;

            /* 垂直外边距合并:谁大取谁 */
            margin-bottom: 20px;
        }

        .box1{
            width:100px;
            height: 100px;
            border: 10px solid orange;

            margin-top: 100px;
        }
    </style>
</head>
<body>
    <div class="box"></div>
    <div class="box1"></div>

</body>
```

### 垂直外边距案例:

```html
    <style>
        .box{
            width: 500px;
            border: 1px solid black;
        }
        .box div{
            /* 垂直外边距合并 两边相等 取一个 */
            margin: 20px;
        }
    </style>



</head>
<body>
    <div class="box">
        <div>背景 之前一直用云笔记保存自己的笔记，因为是写给自己看的，
            所以没有那么用心写。平时大多时间投入到学习上，
            感觉青春期都没留下什么东西，看日志又都是一些零碎</div>
        <div>背景 之前一直用云笔记保存自己的笔记，因为是写给自己看的， 
            所以没有那么用心写。平时大多时间投入到学习上， 感觉青春期都没留下什么东西，看日志又都是一些零碎</div>
        <div>背景 之前一直用云笔记保存自己的笔记，因为是写给自己看的， 所以没有那么用心写。平时大多时间投入到学习上， 感觉青春期都没留下什么东西，看日志又都是一些零碎</div>
        <div>背景 之前一直用云笔记保存自己的笔记，因为是写给自己看的， 所以没有那么用心写。平时大多时间投入到学习上， 感觉青春期都没留下什么东西，看日志又都是一些零碎</div>
    </div>
```

### margin-top塌陷:

```html
    <style>
    .box{
        width: 400px;
        height: 400px;
        background-color: red;
    }

    .box1{
        width: 100px;
        height: 100px;
        background-color: green;

        /* margin-top塌陷:
        margin 在没有找到borde padding时 
        已浏览器边框为基准
         */

         /* 解决margin-top塌陷问题: */
         /* 1.设置border padding边界 
        border:1px solid green;
        padding: 1px;
         */
        
        /* 2.设置overflow (元素溢出 hidden(元素删除)
        overflow: hidden;
        */

        margin-top: 100px;
    }
        /* 3.通过伪类 
        clearfix:{
            约定俗成clearfix伪类名(需要和div 关联)
        }
        .box:before{
            content:"";
            display: table;
        }

        */

        

    </style>


</head>
<body>
    <div class="box">
        <div class="box1">

        </div>
    </div>
</body>
```

### 块元素特点:

块元素特点

 1.默认宽度 父元素的百分百 一致

 2.霸占一行

 3.支持全部样式

```html
<style>
        /* 块元素特点
        1.默认宽度 父元素的百分百 一致
        2.霸占一行
        3.支持全部样式
         */
        .box{
            width: 100px;
            height: 50px;
            background-color: red;
        }
        
    </style>
</head>
<body>
    <div class="box"></div>
    <span>abc</span>
    <!-- 常用块元素 -->
    <p>段落</p>
    <h1>标题标签</h1>
    <ol>
        <li>有序列表1</li>
        <li>有序列表2</li>
        <li>有序列表3</li>
        <li>有序列表4</li>
        <li>有序列表5</li>
    </ol>

    <ul>
        <li>无序列表1</li>
        <li>无序列表2</li>
        <li>无序列表3</li>
    </ul>

    <dl>
        <dt>title</dt>
        <dd>定义列表</dd>
        <dd>定义列表</dd>
        <dd>定义列表</dd>
    </dl>

    <form action="">
        <label for="">标注</label>
        <input type="text">
    </form>
```

### 初始化样式重置:

```html
<style>
        p,h1,h2,h3,h4,h5,h6,ol,li,dl,dt,dd,form{
            margin: 0;
            padding: 0;
        }
        h1,h2,h3,h4,h5,h6{
            font-weight: normal;
            font-size: 100%;
        }

</style>
```

### 行内元素特点:

```html
    <style>
        span{
            /* 行内元素特点
            1.排列一行 遇到边界
            2.宽高 由内容决定
            3.不支持宽高,不支持margin上下
            3.不支持padding 上下(有问题)
            */
            background-color: red;
            width: 200px;
            height: 200px;
            /* 不支持宽高,不支持margin上下 */
            /* margin:100px 200px; */
            padding: 50px 20px;

        }
    </style>


</head>
<body>

    <!-- span{行内元素}*20 -->
     <span>行内元素</span>
     <span>行内元素</span>
    
</body>
```

### 行内间隔的解决:

```html
<style>
        span{
            /* 
            解决间隔问题
            1.代码不换行
            2.设置父元素font-size:0
              设置子元素font-size:12px;
             */
            background-color: red;
            font-size: 16px;
        }
        .box{
            font-size: 0;
        }
    </style>


</head>
<body>
    <div class="box">
        <span>行内元素</span><span>行内元素</span>
        <span>行内元素</span>
    </div>
</body>
```

### 其他行内元素:

```html
<body>
<!-- 其他行内元素 -->
    <label for="">label</label>
    <input type="text">
    <a href=""></a>
    <img src="" alt="">
    <!-- 有语义的 标签 -->
    <strong>重要内容</strong>
    <em>强调语气词 emphasis</em>
    <i>专业名词 italic</i>
    <!-- i标签和font-style:italic区别 
    font-style:italic 是设置的斜体样式
    i标签可以被抓取数据 抓取
    -->
    <b>产品名称 关键字 bold</b>

</body>
```

### 示例:

```html
<style>
    .box{
        width: 900px;
        height: 50px;
        border: 1px solid black;

        /* div居中 */
        margin: 0 auto;
         
        /* 水平居中 */
        text-align: center;
        /* 垂直居中 */
        line-height: 50px;
    }
    /* 2.改变字体颜色 去掉下划线 */
    .box a{
        color: black;
        text-decoration: none;
    }

    /* 3.设置左右的间隔 */
    .box span{
        margin: 0 10px;
        font-size: 12px;
        color: lightgray;

    }
    /* 4.鼠标悬浮 改变颜色 */
    .box a:hover{
        color: gold;
    }
    </style>
</head>
<body>
    <!-- 1.搭建界面 -->
    <div class="box">
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>
        <span>|</span>
        <a href="">首页</a>        

    </div>
```

### 行内块元素:

display{

 none:元素隐藏 不占位置

 block 元素以块元素显示

 inline 元素以内联元素显示

 inline-block 元素以内联块元素显示

 特点:

 支持全部样式

 盒子并在一起

 代码换行 盒子会产生间隔

 }

```html
<style>
        
        div{
            /* 1.将块元素 转换成 行内元素 */
            display: inline;
            /* 2块元素 转换成 行内块元素 */
            display: inline-block;
            
        }
        .box{
            width: 200px;
            height: 200px;
            background-color: red;
        }

        .box1{
            width: 200px;
            height: 200px;
            background-color: green;
        }

        a{
            background-color: gold;

            /* 1.行内转换 块元素 */
            display: block;
            width: 100px;
            height: 100px;

            /* 2.行内转换 行内块元素 */
            display: inline-block;
        }

        span{

            /* 3.隐藏元素 不占位置 */
            display: none;
        }
    </style>
</head>
<body>
    <div class="box">块元素</div>
    <div class="box1">块元素</div>

    <a href="">行内元素</a>
    <a href="">行内元素</a>

    <span>span标签</span>
    <span>span标签</span>
</body>
```



