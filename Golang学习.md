# Golang学习

## 一、基础语法

1.导包 import

2.声明 var

```
:=声明后要使用，不然会报错
```

3.匿名变量 _

4.常量const 不能用:=

5.判断 不用加（）小括号

6.for循环 不用加（）小括号  

```
 1.根据判断条件数量，可以变成while循环  
 2.无判断条件时 逻辑=while(true)
```

7.函数

func开头  函数名（入参）返回值类型{}

8.defer 推迟 

```
在一个代码块里面最后执行该关键字所修饰的语句（只能修饰函数调用）
多条defer 从下往上依次执行
```

9.指针 与c类似，但没有指针运算

10.数组 var修饰，a[ ] 元素类型

```
数组切片 a[1:3]
```

11.make

```
make(Type, len, cap)
Type：数据类型，必要参数，Type 的值只能是 slice、 map、 channel 这三种数据类型。
len：数据类型实际占用的内存空间长度，map、 channel 是可选参数，slice 是必要参数。
cap：为数据类型提前预留的内存空间长度
example:

make(chan int)和 make(chan int,1 )区别
无缓冲和有缓冲

```

12.结构体struct

```
var  golang会自动分配内存空间	


```

13.func

```
func 函数名(args) 返回类型
func (入参) 函数名(args) 返回类型  值传递和指针传递


```

14.接口

```
type 接口名 interface {
    方法1(参数) 返回类型
    方法2(参数) 返回类型 
    ...
}
接口的赋值形式
```

```
go怎么实现多态：
函数重载
```

```
什么是非侵入式？
该结构体只要能实现接口的所有方法，即视为，该结构体实现该接口
接口的类型不需要显式地声明它们实现了某个接口
```

15.golang是**以首字母大小**写来区分对包外是否可见。

## 二、并发

进程

线程

2.goroutine协程 	(协程如何执行)  **go创建**

```
nil类似null
```

并发的概念，IO多路复用

用go创建

3.channel 管道通信

```
用make创建信道
传数据用channel <- data，取数据用<- channel
```

4.range

```
range 用于迭代数据结构中的元素(类似for与auto这种增强for循环)
```

5.select

```
类似switch case
select 语句只能用于通道操作，每个 case 必须是一个通道操作，要么是发送要么是接收。
```

## 三、创建一个Go项目

vscode配置

vscode部署golang教程

https://blog.csdn.net/m0_71139661/article/details/140274871?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-2-140274871-blog-139811571.235%5Ev43%5Epc_blog_bottom_relevance_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-2-140274871-blog-139811571.235%5Ev43%5Epc_blog_bottom_relevance_base1&utm_relevant_index=5



VSCode配置GO语言环境遇到的问题：go.mod file not found in current directory or any parent directory

https://blog.csdn.net/OrientalGlass/article/details/130791604



```
%+v  用于打印结构体的详细信息
```



c++与go  线程安全

```
c++ 线程不安全
go 线程安全 不需要加锁
```

## 四、协程

1.协程之间数据传输用 管道 channel

2、**有缓冲和无缓冲通道的区别？**

## 五、框架

### 1、gin框架

web开发框架

```
package main

import (
	"log"
	"net/http"

	"github.com/gin-gonic/gin"
)

func SayHello(c *gin.Context) {
	c.String(http.StatusOK, "hello") //以字符串"hello"作为返回包
}

func main() {
	engine := gin.Default() //生成一个默认的gin引擎
	engine.Handle(http.MethodGet, "/say_hello", SayHello)
	err := engine.Run(":8080") //使用8080端口号，开启一个web服务
	if err != nil {
		log.Print("engine run err: ", err.Error())
		return
	}
}
```

## 六、数据结构

1、创建数组

```
var arr1 = [...]int{1,2,3,4}
var arr1 = [10]int{1,2,3,4}默认为0
```

2.slice和array

切片相当于动态数组

```
C 语言的数组变量是指向数组第一个元素的指针  指针传递
Go 语言的数组是一个值					值传递
```

切片扩容name[:5]

切片传递是引用传递

```
切片作为参数传递

```

Golang中的切片追加append()

追加后若超过原数组容量上限地址会发生变化，跟引用区别

```go
fmt.Println(*(*int)(unsafe.Pointer(uintptr(unsafe.Pointer(&arr[0])) + 1*size))：
            
```



## 七、GO所用到的包

fmt

unsafe