

# Golang学习

## 一、基础语法

1.导包 import

2.声明 var

```
:=声明后要使用，不然会报错
```

3.匿名变量 _

```
匿名结构体  赋值  struct  初始化
```

4.常量const 不能用:=

```
iota是一个特殊常量，可以认为是一个可以被编译器修改的常量，默认为0，被调用时自动+1
```

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


切片创建
s:=[]int{1,2,3}
make([]int,3)

切片操作是左闭右开的
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

16.接收器

```
值接收器 func(p Person)
指针接收器func(P * Preson)

修改接收器的值：如果需要在方法中修改接收器的值，必须使用指针接收器。
避免值拷贝：对于大的结构体，使用指针接收器可以避免值拷贝，提高性能。
一致性：对于一些类型，最好对所有的方法都使用指针接收器，以保持一致性。

值接收器和指针接收器的赋值一样
```

17、go和c++的new的区别

```
返回值：
Go 的 new 返回的是指向零值对象的指针，不会初始化对象。
C++ 的 new 返回的是指向动态分配的对象的指针，并会调用构造函数来初始化对象。
内存管理：
Go 的 new 会自动管理内存，不需要手动释放。
C++ 的 new 分配的内存需要手动释放，使用 delete 操作符。
```

18、GMP

线程调度器

19、文件结构

20、结构体

```
结构体
type name struct{}
结构体 Student
Strudent和&Student区别
复制体和返回一个指针的区别


go语言编译器有一定自动识别
```

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
range 用于迭代数据结构(array,slice,map,channel)中的元素(类似for与auto这种增强for循环)

 for i := range c
 (i作为c中的元素进行迭代)
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

3、[Golang 入门 : 理解并发与并行](https://www.cnblogs.com/sparkdev/p/10930120.html)

4、[Golang 入门 : 等待 goroutine 完成任务](https://www.cnblogs.com/sparkdev/p/10917536.html)

```
不等待的话，goroutine 以非阻塞的方式执行，它们会随着程序(主线程)的结束而消亡

```

```go
func main() {
    done := make(chan bool)
    go func() {
        for i := 0; i < 3; i++ {
            time.Sleep(100 * time.Millisecond)
            fmt.Println("hello world")
        }
        done <- true
    }()

    <-done
    fmt.Println("over!")
}

done通道收到数据后协程停止阻塞，


2.WaitGroup 用来等待单个或多个 goroutines 执行结束

runtime.GOMAXPROCS(1)分配逻辑处理器
```

<img src="Golang学习.assets/image-20240912175733033.png" alt="image-20240912175733033" style="zoom:33%;" />

协程需要切换

```
进程、线程、协程

线程
```

Linux线程实现

```
Go 调度器最多可以创建 10000 个线程  创建线程数量跟cpu核数有关
```

#### Context

```
上下文 Context
简单说 就是
 快速退出协程
 协程直接传递信息
 
 todo 返回一个空的context
 
 WithTimeout  设置任务超时时间
 Background   创建一个空的上下文
 
 找个资料分析源码好一点
```

```
使用Context传递traceId<重点>
```

#### Channel

```
1、Channel类型
chan T          // 可以接收和发送类型为 T 的数据
chan<- float64  // 只可以用来发送 float64 类型的数据
<-chan int      // 只可以用来接收 int 类型的数据

2、blocking 
make(chan int)
make(chan int，1)

3、select选择
4、close
```

#### sync

synchronize (同步)



Mutex

```
mutexLocked — 表示互斥锁的锁定状态；
mutexWoken — 表示从正常模式被从唤醒；
mutexStarving — 当前的互斥锁进入饥饿状态；
waitersCount — 当前互斥锁上等待的 Goroutine 个数

sync.Mutex 正常模式  饥饿模式  （先进先出）
饥饿模式避免goroutine等待时间过长

自旋状态：线程在没有抢到锁之后不会立刻进入休眠状态
```

```
计算新的互斥状态用
CAS 函数


互斥锁和读写锁
未完待续
```



## 五、框架

### 1、gin框架

web开发框架

分为几个模块

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

路由组

中间件





#### 2.golang中的orm

```
相似性

各orm支持的数据库都基本相同（主流数据库都支持）
支持事务性、链式查询等
差异

xorm、gorose支持批量查询处理
xorm支持主从式读写分离
gorm支持热加载
gorose便于在多个数据库切换
文档全面性gorm>xorm>gorose
```

3、go redis



## 六、数据结构

1、数组array

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

3、map源码解析

```
get流程
确定有多少（b）桶，确定key的hash值，有b桶，取hash值后b为，得到二进制数，得到所在桶，对比桶里的tophash跟hash值前8位做对比，没有找溢出桶

put流程
跟get流程类似，每个桶有8个ky,发生哈希冲突使用链表法
```

```
扩容方式，相同容量扩容(桶数据从新排列)，二倍扩容(增加桶，从新排)
装载因子

map扩容后，地址发生变化
```

map线程不安全，需要用到互斥锁 

4、stack

```
type ArrayStack struct {
    array []string   // 底层切片
    size  int        // 栈的元素数量
    lock  sync.Mutex // 为了并发安全使用的锁
}

//链表栈
type LinkStack struct {
    root *LinkNode  // 链表起点
    size int        // 栈的元素数量
    lock sync.Mutex // 为了并发安全使用的锁
}

// 链表节点
type LinkNode struct {
    Next  *LinkNode
    Value string
}
元素和size
```

```
排除栈顶元素
stack.array = stack.array[0 : stack.size-1]

写一个入栈和出栈
```

5、Queue

```
//数组队列
type ArrayQueue struct {
    array []string   // 底层切片
    size  int        // 队列的元素数量
    lock  sync.Mutex // 为了并发安全使用的锁
}


// 链表队列
type LinkQueue struct {
    root *LinkNode  // 链表起点
    size int        // 队列的元素数量
    lock sync.Mutex // 为了并发安全使用的锁
}

// 链表节点
type LinkNode struct {
    Next  *LinkNode
    Value string
}
```



### 深入剖析slice和array

```
未理解完
```



## 七、GO所用到的包

fmt

unsafe

```
unsafe.Pointer
uintptr无符号整数类型
用于将指针转换为整数值或将整数值转换回指针
```

## 八、常用的设计模式

创建型模式

```
单例模式
	饿汉模式 先初始化，再运行
	饱(懒)汉模式 先运行，再初始化


工厂模式
	简单工厂  返回结构体
	
	工厂方法   
	
	抽象工厂  返回接口
	
	
结构性模式

```

![image-20241002024929314](C:\Users\really\AppData\Roaming\Typora\typora-user-images\image-20241002024929314.png)

## 八、进阶语法



## 八、题收集

1、[为什么 Go map 和 slice 是非线程安全的？](https://segmentfault.com/a/1190000040716956)

```
多协程处理会报错和数据不对

配合读写锁

mutex+map初步解决并发问题，但是只有一把锁会出现抢占锁的情况->go支持并发读写map(sync.Map)[空间换时间]


根据需要，map不适合线程安全机制，在协程中效率会产生印象，不适应这种环境
```

```
type Map struct {
 mu Mutex
 read atomic.Value // readOnly
 dirty map[interface{}]*entry
 misses int
}
适合读多写少的场景
```

```
var m sync.Map

func main() {
 //写入
 data := []string{"煎鱼", "咸鱼", "烤鱼", "蒸鱼"}
 for i := 0; i < 4; i++ {
  go func(i int) {
   m.Store(i, data[i])
  }(i)
 }
 time.Sleep(time.Second)

 //读取
 v, ok := m.Load(0)
 fmt.Printf("Load: %v, %v\n", v, ok)

 //删除
 m.Delete(1)

 //读或写
 v, ok = m.LoadOrStore(1, "吸鱼")
 fmt.Printf("LoadOrStore: %v, %v\n", v, ok)

 //遍历
 m.Range(func(key, value interface{}) bool {
  fmt.Printf("Range: %v, %v\n", key, value)
  return true
 })
}
```

## 疑问

在函数里调用有协程的函数，然后再执行有协程的匿名函数

## 学习心得

```
9.18重新规划一下学习思路，现在细究比较吃力
10.3还是需要列个计划
技术美术，摄影透视




```

## 微信摇一摇

sql转struct

```
{"view_prize_list":[{"id":1,"name":"Q币","pic":"http://q.qlogo.cn/g?b=qq\u0026nk=1\u0026s=100\u0026nk2=1\u0026s2=100","link":"http://q.qq.com","type":1,"data":"100Q币","total":20000,"left":20000,"is_use":1,"probability":5000,"probability_max":5000,"probability_min":0},{"id":2,"name":"充电宝","pic":"","link":"","type":3,"data":"","total":100,"left":100,"is_use":1,"probability":100,"probability_max":5100,"probability_min":5000},{"id":3,"name":"iphone14","pic":"","link":"","type":4,"data":"","total":10,"left":10,"is_use":1,"probability":10,"probability_max":5110,"probability_min":5100},{"id":4,"name":"优惠券满100减10元","pic":"","link":"","type":2,"data":"黄焖鸡外卖优惠券","total":5000,"left":5000,"is_use":1,"probability":3000,"probability_max":8110,"probability_min":5110}]}
--- PASS: TestAddPrize (0.00s)
```

