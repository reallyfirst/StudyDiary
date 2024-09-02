# Golang学习

## 一、基础语法

1.导包 import

2.声明 var

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

