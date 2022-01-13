HelloWord

```go
package main

import "fmt"

func main() {
	fmt.Println("helloworld")
}

```

编译运行
====

```sh
# 直接运行
go run xxxx.go
# 编译
go build xxxx.go
# 运行
./xxxx
```

注意:

* min函数和main包必须同时存在
* 定义的变量或引入的包,必须使用,否则无法编译
* 程序入口是main函数
* 严格区别大小写
* 多条语句不能写在一行
* 不需要分号结束
* 括号要成对出现
* 格式化代码gofmt xxx.go fofmt -w xxx.go

转义字符
----

```go
// \t  tab
// \n  换行
// \\  单\
// \"  单引号
// \r  /r后边的字符,替换到字符串,从头开始依次替换
```

### 注释

```go
// 行注释

/*
块注释
*/

```

变量
--

* 指定变量类型,声明后不赋值使用默认值int=0
  * int = 0
  * float = 0
  * str = “”
  * bol = false
* + 数字类型表示相加,字符串类型表示合并字符串

* := 声明变量并且赋值

```go
//package learn_go
package main

import "fmt"

//指定变量类型,声明后不赋值使用默认值int
var a int

// 全局变量
var n1 = 100
var n2 = 200
var name = "henrydu"

// 一次性声明
var (
	n3    = 300
	n4    = 400
	name2 = "peter"
)

func main() {
	println(a)
	fmt.Println(n1, n2, n3, n4, name, name2)
}
```

```go
//package learn_go
package main

import "fmt"



func main() {
   // 在作用域里可以改变变量数值
   var a = 1
   a = 2
   // a = 1.2 error 不能给整形变量定义其他类型
   
   // var a = 6 error 不能重复定义变量名

   fmt.Println(a)
}
```

数据类型
----

### 基本数据类型

* 数值型:
  * 整数类型(int,int8,int16,int32,int64)(无符号:uint,uint8,uint16,uint32,uint64,byte)
  * byte 0~255 无符号 存放字母
  * rune:有符号,与int32等价,表示一个Unicode码
  * 浮点类型(float32,float64)
* 字符型(byte 存单个字母字符)
* 布尔型
* 字符串

* 浮点数:默认为float64声明变量
* 字符:没有专门的字符类型,一般用byte保存
* 字符串:传统字符串是由字符组成,go字符串由字节组成
  * 字符串一旦赋值,就无法改变

### 派生/复杂数据类型

* 指针
* 数组
* 结构体
* 管道
* 函数
* 切片
* 接口
* map

```go
//package learn_go
// 查看变量容量
package main

import (
	"fmt"
	"unsafe"
)

func main() {
	var a int64 = 1

	fmt.Println("a 变量存储容量是%d", unsafe.Sizeof(a))
}

```

```go
//package learn_go
// 字符输出
package main

import (
	"fmt"
)

var s1 byte = 'a'
var s2 byte = 'b'
var s3 int = '北'

func main() {
	// 单个字符
	fmt.Printf("格式化输出:%c, %c", s1, s2)
	// 汉字
	fmt.Printf("格式化输出:%c", s3)

}

```

```go
//package learn_go
package main

import "fmt"

func main() {
	str1 := "我爱北京"
	str2 := `我爱
北京
天安门`
	str3 := "天安门"
	str4 := str1 + str3
	// 字符串
	fmt.Println(str1)
	// 字符段
	fmt.Println(str2)
	// 字符串拼接
	fmt.Printf(str4)

}

```

### 数据类型转换

数据类型转换的是值,原有的变量数据类型并没有改变

大数据类型转到小数据类型,会按照溢出处理(二进制溢出处理)

```go
//package learn_go
package main

import (
	"fmt"
)

func main() {
	n1 := 100
	n2 := int64(n1)
	n3 := float32(n2)
	fmt.Printf("%T", n3)

}

```









