# Go语言学习笔记

### 1. Go语言简介

**Go语言特色**

- 简洁、快速、安全
- 并行、有趣、开源
- 内存管理、数组安全、编译迅速

**Go语言用途**

- Go语言被设计成一门应用于搭载Web服务器，存储集群或类似用途的巨型中央服务器的系统编程语言
- 对于高性能分布式系统领域而言，Go语言比大多数其他语言有更高开发效率
- 提供了海量并行的支持，对于游戏服务端的开发很好

**Go语言开发工具**

GoLand、LiteIDE、Eclipse



### 2. Go语言结构

**Hello World实例**

```go
package main
import "fmt"

func main() {
	/* 这是我的第一个简单的程序 */
	fmt.Println("Hello, World!")
}
```

Go语言基础组成：

①包声明：package main表示一个可独立执行的程序，每个Go应用程序都包含一个名为main的包

②引入包：fmt包实现了格式化IO的函数

③函数：main函数是每一个可执行程序所必须包含的，一般是在启动后第一个执行的函数（如有 `init()`函数则先执行该函数）

④注释：单行注释用 `//`开头，多行注释以 `/*`开头，以 `*/`结尾

⑤语句&表达式

⑥变量：当标识符以一个大写字母开头，那么使用这种形式的标识符的对象就可以被外部包的代码所使用，称为导出（类似面向对象中的public）；当标识符以小写字母开头，则对包外不可见，但在整个包内部是可见并且可用的（类似面向对象中的protected）

**执行Go程序**

- 在命令行中输入 `go run filename.go`
- 在命令行使用 `go build filename.go`命令生成二进制文件

⭐注意 `{` 不可以单独放在一行



### 3. Go基础语法

**Go标记**

Go程序可由多个标记组成，可以是关键字，标识符，常量，字符串，符号

**行分隔符**

一行代表一个语句结束，无需添加分号结尾，因为这些工作将由Go编译器自动完成

**标识符**

一个标识符是由一个或多个字母、数字、下划线组成的序列，但第一个字符必须是字母或下划线而不能是数字

**字符串连接**

类似Java，以 `+`实现

**关键字**

25个关键字或保留字：

| break        | default         | func       | interface   | select     |
| ------------ | --------------- | ---------- | ----------- | ---------- |
| **case**     | **defer**       | **go**     | **map**     | **struct** |
| **chan**     | **else**        | **goto**   | **package** | **switch** |
| **const**    | **fallthrough** | **if**     | **range**   | **type**   |
| **continue** | **for**         | **import** | **return**  | **var**    |

**空格**

变量的声明必须使用空格隔开



### 4. Go语言数据类型

按类别分为：

①布尔型：true、false。 `var b bool = true`

②数字类型：int、float32、float64、复数。位的运算使用补码

③字符串类型：Go的字符串是由单个字节连接起来，使用UTF-8编码标识Unicode文本

④派生类型：指针类型（Pointer）、数组类型、结构化类型（Struct）、Channel类型、函数类型、切片类型、接口类型（interface）、Map类型

**数字类型**

| **unit8**  | **无符号8位整型(0-255)** | **int8**  | **有符号8位整型(-128到127）** |
| ---------- | ------------------------ | --------- | ----------------------------- |
| **uint16** | **无符号16位整型**       | **int16** | **有符号16位整型**            |
| **unit32** | **无符号32位整型**       | **int32** | **有符号32位整型**            |
| **unit64** | **无符号64位整型**       | **int64** | **有符号64位整型**            |

浮点型

| **float32** | **IEEE-754 32位浮点型数** | **complex64**  | **32位实数和虚数** |
| ----------- | ------------------------- | -------------- | ------------------ |
| **float64** | **IEEE-754 64位浮点型数** | **complex128** | **64位实数和虚数** |

其他数字类型

| **byte**    | **类似uint8**                    |
| ----------- | -------------------------------- |
| **rune**    | **类似int32**                    |
| **uint**    | **32位或64位**                   |
| **int**     | **与uint一样大小**               |
| **uintptr** | **无符号整型，用于存放一个指针** |



### 5. Go语言变量

声明变量的一般形式： `var identifier type`

一次声明多个变量形式：`var identifier1,identifier2 type`

```go
package main
import "fmt"

func main() {
	var a int = 2
	var b string = "Test"
	fmt.Println(a,b)
}
```

**变量声明的三种方式**

①指定变量类型，如没有初始化，则默认为零值

```go
package main
import "fmt"

func main() {
	var a int
	a = 2
	var b int
	var c bool
	var d string
	var e *int
	fmt.Println(a,b,c,d,e)
}
```

"零值"

- 数值类型（包括complex64/128）为0
- 布尔类型为false
- 字符串为“”(空字符串)

- 以下几种类型为nil：

  ```go
  var a *int
  var a []int
  var a map[string] int
  var a chan int
  var a func(string) int
  var a error // error 是接口
  ```

②根据值自行判断变量类型

```go
package main
import "fmt"

func main() {
	var a = "str"
	fmt.Println(a)
}
```

③省略var，注意 `:=`左侧如果没有声明新的变量就会产生编译错误

```go
package main
import "fmt"

func main() {
	a := "str"
	var b int
	// b := 2（编译错误）
	b,c := 2,3 //有声明新的变量，ok
	fmt.Println(a,b,c)
}
```

**多变量声明**

```go
//类型相同多个变量，非全局变量
var vname1,vname2,vname3 type
vname1,vname2,vname3 = v1,v2,v3
//和python很像，不需要显式声明类型
var vname1,vname2,vname3 = v1,v2,v3
//:=左侧变量不应该是已经被声明过的
vname1,vname2,vname3 := v1,v2,v3
//这种因式分解关键字写法一般用于声明全局变量
var(
	vname1 v_type1
    vname2 v_type2
)
```

实例

```go
package main
import "fmt"

var x,y int
var(
	a int
	b bool
)
var c,d int = 1, 5
var e,f = 123,"str"
// g,h := 123,"str"（这种不带声明格式的只能在函数体内出现）
func main() {
	g,h := 123,"str"
	fmt.Println(x,y,a,b,c,d,e,f,g,h)
}
```

**值类型和引用类型**

①值类型

- 所有像int、float、bool和string这些基本类型都属于值类型，使用这些类型的变量直接指向内存中的值。
- 当使用等号进行赋值时，如 b = a ，实际上是在内存中将a的值进行了拷贝

②引用类型

- 更复杂的数据通常需要使用多个字，这些数据使用引用类型保存
- 一个引用类型的变量r1存储r1的值所在的内存地址，或内存地址中第一个字所在的位置。这个内存地址称为指针，这个指针实际上也被存在了另外的某一个字中
- 当使用等号进行赋值时，只有引用（地址）被复制，如 r2 = r1，如果r1值被改变，那么这个值的所有引用都会指向被修改后的内容，r2也受到影响

**使用 := 赋值操作符**

- :=为变量赋值只能被用于函数体内，不可以用于全局变量的声明与赋值。使用操作符 := 高效创建一个新的变量，称之为初始化声明。
- 声明了一个局部变量却没有在相同的代码块中使用它，也会有编译错误
- 全局变量允许声明但不使用。同一类型的多个变量可声明在同一行
- 多变量可在同一行赋值
- 如果想要交换两个变量的值，可以用 `a,b=b,a`，两变量类型必须相同

**空白标识符 _**

用于抛弃值。如 `_,b = 5,7`中，值5被抛弃

_ 实际上是一个只写变量，不能得到它的值。因为Go语言中必须使用所有被声明的变量。但有时并不需要使用从一个函数得到的所有返回值。



### 6. Go语言常量

常量中的数据类型只可以是布尔型、数字型（整型、浮点型和复数）和字符串型

常量定义格式：`const identifier [type] = value`

- 显式类型定义：`const b string = "str"`
- 隐式类型定义：`const b = "str"`
- 多个相同类型声明：`const c_name1,c_name2 = value1,value2`

常量还可以用于枚举：

```go
const(
	Unknown = 0
	Female = 1
	Male = 2
)
```

常量可用len()、cap()、unsafe.Sizeof()函数计算表达式的值。常量表达式中，函数必须是内置函数：

```go
package main
import "unsafe"

const(
	a = "str"
	b = len(a)
	c = unsafe.Sizeof(a)
)
func main() {
	println(a,b,c)
}
/*
输出 str 3 16
*/
```

🔺字符串类型在go里是个结构，包含指向底层数组的指针和长度，这两部分每部分都是8个字节，所以字符串类型大小为16个字节

**iota**

特殊常量，可认为是一个可被编译器修改的常量

iota在const关键字出现时将被重置为0(const内部的第一行之前)，const中每新增一行常量声明将使iota计数一次（iota可理解为const语句块中行索引）

iota可被用作枚举值：

```go
const(
	a = iota
	b = iota
	c = iota
)
```

iota用法：

```go
package main
import "fmt"

func main() {
	const(
		a = iota
		b
		c
		d = 50
		e
		f = iota
		g
	)
	fmt.Println(a,b,c,d,e,f,g)
}
/*
输出 0 1 2 50 50 5 6
*/
```

🔺在定义常量组时，如不提供初始值，则表示使用上行的表达式

另一个iota实例：

```go
package main
import "fmt"

func main() {
	const(
		a = 1<<iota
		b = 3<<iota
		c
		d
	)
	fmt.Println(a,b,c,d)
}
/*
输出 1 6 12 24
*/
```

a = 1<<0，b=3<<1，c=3<<2，d=3<<3



### 7. Go语言运算符

| 分类       | 运算符                                       |
| ---------- | -------------------------------------------- |
| 算术运算符 | +、-、*、/（整数除法）、%、++、--            |
| 关系运算符 | ==、!=、>、<、>=、<=                         |
| 逻辑运算符 | &&、\|\|、!                                  |
| 位运算符   | &、\|、^（异或）、<<、>>                     |
| 赋值运算符 | =、+=、-=、*=、/=、%=、<<=、>>=、&=、\|=、^= |
| 其他运算符 | &（返回变量存储地址）、*（指针变量）         |

**运算符优先级**

由高到低：

| 优先级 | 运算符                 |
| ------ | ---------------------- |
| 5      | *、/、%、<<、>>、&、&^ |
| 4      | +、-、\|、^            |
| 3      | ==、!=、<、<=、>、>=   |
| 2      | &&                     |
| 1      | \|\|                   |

二元运算符运算方向从左至右

***和&的使用区别**

```go
package main
import "fmt"

func main() {
	var a int = 3
	var ptr *int
	ptr = &a
	fmt.Println(a,*ptr,ptr)
}
/*
输出 3 3 0xc0000a0090
*/
```

🔺指针变量保存的是一个地址值，会分配独立的内存来分配一个整型数字。当变量前面有*号标识时，才等同于&用法，否则会直接输出一个整型数字。



### 8. Go条件语句

①if语句

②if...else语句

③if嵌套语句

④switch语句

- switch语句执行过程从上到下，直到找到匹配项，匹配项后面不需要加break
- 默认case最后自带break语句，匹配成功后不会执行其他case，要使用后面的case可使用fallthrough

```go
switch var1{
	case val1:
	case val2:
	...
	default:
}
```

var1可以是任何类型。val1和val2可以是同类型任意值。类型不局限于常量或整数，但必须是相同类型；或者最终结果为相同类型表达式

可以同时测试多个可能值，使用逗号分隔，如case val1,val2,val3

```go
package main

import "fmt"

func main() {
	var grade string = "B"
	var marks int = 90

	switch marks{
	case 90:grade = "A"
	case 80:grade = "B"
	case 60,70:grade = "C"
	default:grade = "D"
	}

	switch{
	case grade == "A":
		fmt.Println("优秀")
	case grade == "B":
		fmt.Println("良好")
	case grade == "C":
		fmt.Println("及格")
	case grade == "D":
		fmt.Println("不及格")
	}
	fmt.Printf("等级为 %s\n",grade)
}
```

**Type Switch**

判断某个interface变量中实际存储的变量类型

```go
switch x.(type){
	case type:
		stmts;
	case type:
		stmts;
	default:
		stmts;
}
```

实例：

```go
package main
import "fmt"

func main() {
	var x interface{}

	switch i:=x.(type){
	case nil:
		fmt.Println("x的类型为",i)
	case int:
		fmt.Println("x是int型")
	default:
		fmt.Println("未知")
	}
}
```

**fallthrough用法**

```go
package main
import "fmt"

func main() {
	switch{
	case false:
		fmt.Println("false")
		fallthrough
	case true:
		fmt.Println("true")
		fallthrough
	case false:
		fmt.Println("false")
		fallthrough
	case true:
		fmt.Println("true")
	case false:
		fmt.Println("false")
		fallthrough
	default:
		fmt.Println("default")
	}
}
/*
true
false
true
*/
```

switch从第一个判断表达式为true的case开始执行，如果case带有fallthrough，程序继续执行下一条case，不会判断下一个case表达式是否为true

⑤select语句

- 类似于用于通信的switch语句，每个case必须是一个通信操作，要么是发送要么是接收。
- select随机执行一个可运行的case，如果没有case可运行，它将阻塞，直到有case可运行，一个默认子句应该总是可运行的。

```go
select{
	case communication clause:
		stmts;
	case communication clause:
		stmts;
	default:
		stmts;
}
```

所有channel表达式都会被求值，所有被发送的表达式都会被求值

实例：

```go
package main
import "fmt"

func main() {
	var c1, c2, c3 chan int
	var i1, i2 int
	select {
	case i1 = <-c1:
		fmt.Printf("received ", i1, " from c1\n")
	case c2 <- i2:
		fmt.Printf("sent ", i2, " to c2\n")
	case i3, ok := (<-c3):  // same as: i3, ok := <-c3
		if ok {
			fmt.Printf("received ", i3, " from c3\n")
		} else {
			fmt.Printf("c3 is closed\n")
		}
	default:
		fmt.Printf("no communication\n")
	}
}
/*
no communication
*/
```

select会循环检测条件，如果有满足则执行并退出，否则一直循环检测



### 9. Go循环语句

①for语句

三种使用方式：

- 和C语言的for一样： `for init;condition;post{}`
- 和C语言的while一样：`for condition{}`
- 和C语言的for(;;)一样：`for {}`

for循环的range格式可对slice、map、数组、字符串等进行迭代循环：

```go
for key,value := range oldMap{
	newMap[key] = value
}
```

实例：

```go
package main
import "fmt"

func main() {
	sum := 0
	for i:=0;i<=10;i++{
		sum+=i
	}
	fmt.Println(sum)
}
```

**For-each range循环**

对字符串、数组、切片等进行迭代输出元素

```go
package main
import "fmt"

func main() {
	strings := []string{"google", "runoob"}
	for i, s := range strings {
		fmt.Println(i, s)
	}
	
	numbers := [6]int{1, 2, 3, 5}
	for i,x:= range numbers {
		fmt.Printf("第 %d 位 x 的值 = %d\n", i,x)
	}
}
/*
0 google
1 runoob
第 0 位 x 的值 = 1
第 1 位 x 的值 = 2
第 2 位 x 的值 = 3
第 3 位 x 的值 = 5
第 4 位 x 的值 = 0
第 5 位 x 的值 = 0
*/
```

②循环嵌套

```go
for [condition|(init;condition;increment)|Range]
{
	for [condition|(init;condition;increment)|Range]
	{
		stmts;
	}
	stmts;
}
```

输出2到100之间素数实例：

```go
package main
import "fmt"

func main() {
	var i, j int
	for i=2; i < 100; i++ {
		for j=2; j <= (i/j); j++ {
			if i%j==0 {
				break // 如果发现因子，则不是素数
			}
		}
		if j > (i/j) {
			fmt.Printf("%d  是素数\n", i);
		}
	}
}
```

③break语句

- 用于跳出循环，并开始执行循环之后语句
- 在多重循环中，可使用标记label标记出想break的循环

多重循环break实例：

```go
package main
import "fmt"

func main() {
	fmt.Println("---- break ----")
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)
		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			break
		}
	}
	
	fmt.Println("---- break label ----")
re:
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)
		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			break re
		}
	}
}
/*
---- break ----
i: 1
i2: 11
i: 2
i2: 11
i: 3
i2: 11
---- break label ----
i: 1
i2: 11
*/
```

④continue语句

- 用于跳过当前循环执行下一次循环语句
- 多重循环中，可用标记label标记出想continue的循环

```go
package main
import "fmt"

func main() {
	fmt.Println("---- continue ---- ")
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)
		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			continue
		}
	}

	fmt.Println("---- continue label ----")
re:
	for i := 1; i <= 3; i++ {
		fmt.Printf("i: %d\n", i)
		for i2 := 11; i2 <= 13; i2++ {
			fmt.Printf("i2: %d\n", i2)
			continue re
		}
	}
}
/*
---- continue ---- 
i: 1
i2: 11
i2: 12
i2: 13
i: 2
i2: 11
i2: 12
i2: 13
i: 3
i2: 11
i2: 12
i2: 13
---- continue label ----
i: 1
i2: 11
i: 2
i2: 11
i: 3
i2: 11
*/
```

⑤goto语句

无条件转移到过程中指定的行

goto语句通常与条件语句配合使用，用来实现循环，跳出循环体等功能

```go
goto label;
..
.
label:stmt;
```



### 10. Go函数

Go语言最少有个main()函数

```go
func function_name ([parameter list]) [return_types]{
	函数体
}
```

函数由func开始声明，函数名和参数列表一起构成了函数签名

**函数调用**

求两个数最大值实例：

```go
package main
import "fmt"

func main() {
	var a int = 50
	var b int = 100
	res := max(a,b)
	fmt.Println(res)
}

func max(num1,num2 int)int{
	var result int
	if num1>num2 {
		result = num1
	} else{
		result = num2
	}
	return result
}
```

**函数返回多个值**

交换两个元素实例：

```go
package main
import "fmt"

func main() {
	a,b := swap("str1","str2")
	fmt.Println(a,b)
}

func swap(x,y string)(string,string){
	return y,x
}
```

**函数参数**

🔺Go语言默认使用值传递，即调用过程中不会影响到实际参数

| 传递类型 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| 值传递   | 在调用函数时将实际参数复制一份传递到函数中；在函数中如果对参数进行修改将不会影响到实际参数 |
| 引用传递 | 在调用函数时将实际参数的地址传递到函数中；在函数中对参数的修改将影响到实际参数 |

值传递实例：

```go
package main
import "fmt"

func main() {
	var a int = 100
	var b int = 200

	fmt.Printf("交换前 a 的值为 : %d\n", a )
	fmt.Printf("交换前 b 的值为 : %d\n", b )

	swap(a, b)

	fmt.Printf("交换后 a 的值 : %d\n", a )
	fmt.Printf("交换后 b 的值 : %d\n", b )
}

func swap(x, y int) int {
	var temp int

	temp = x /* 保存 x 的值 */
	x = y    /* 将 y 值赋给 x */
	y = temp /* 将 temp 值赋给 y*/

	return temp
}
/*
交换前 a 的值为 : 100
交换前 b 的值为 : 200
交换后 a 的值 : 100
交换后 b 的值 : 200
*/
```

引用传递实例：

```go
package main
import "fmt"

func main() {
	var a int = 100
	var b int= 200

	fmt.Printf("交换前，a 的值 : %d\n", a )
	fmt.Printf("交换前，b 的值 : %d\n", b )

	/* 调用 swap() 函数
	 * &a 指向 a 指针，a 变量的地址
	 * &b 指向 b 指针，b 变量的地址
	 */
	swap(&a, &b)

	fmt.Printf("交换后，a 的值 : %d\n", a )
	fmt.Printf("交换后，b 的值 : %d\n", b )
}

func swap(x *int, y *int) {
	var temp int
	temp = *x    /* 保存 x 地址上的值 */
	*x = *y      /* 将 y 值赋给 x */
	*y = temp    /* 将 temp 值赋给 y */
}
/*
交换前，a 的值 : 100
交换前，b 的值 : 200
交换后，a 的值 : 200
交换后，b 的值 : 100
*/
```

**Go语言函数作为实参**

```go
package main
import(
	"fmt"
	"math"
)

func main(){
	getSquareRoot := func(x float64) float64{
		return math.Sqrt(x)
	}
	fmt.Println(getSquareRoot(9))
}
```

**函数作为参数传递，实现回调**

```go
package main
import "fmt"

// 声明一个函数类型
type cb func(int) int

func main() {
	testCallBack(1, callBack)
	testCallBack(2, func(x int) int {
		fmt.Printf("我是回调，x：%d\n", x)
		return x
	})
}

func testCallBack(x int, f cb) {
	f(x)
}

func callBack(x int) int {
	fmt.Printf("我是回调，x：%d\n", x)
	return x
}
/*
我是回调，x：1
我是回调，x：2
*/
```

**Go函数闭包**

Go语言支持匿名函数，可作为闭包。匿名函数是一个“内联”语句或表达式。匿名函数优越性在于可直接使用函数内的变量，不必声明。

实例：创建函数getSequence()，返回另外一个函数

```go
package main
import "fmt"

func getSequence() func() int {
	i:=0
	return func() int {
		i+=1
		return i
	}
}

func main(){
	/* nextNumber 为一个函数，函数 i 为 0 */
	nextNumber := getSequence()

	/* 调用 nextNumber 函数，i 变量自增 1 并返回 */
	fmt.Println(nextNumber())
	fmt.Println(nextNumber())
	fmt.Println(nextNumber())

	/* 创建新的函数 nextNumber1，并查看结果 */
	nextNumber1 := getSequence()
	fmt.Println(nextNumber1())
	fmt.Println(nextNumber1())
}
/*
1
2
3
1
2
*/
```

闭包带参数：

```go
package main
import "fmt"

func main() {
	add_func := add(1,2)
	fmt.Println(add_func())
	fmt.Println(add_func())
	fmt.Println(add_func())
}

// 闭包使用方法
func add(x1, x2 int) func()(int,int)  {
	i := 0
	return func() (int,int){
		i++
		return i,x1+x2
	}
}
/*
1 3
2 3
3 3
*/
```

```go
package main
import "fmt"
func main() {
	add_func := add(1,2)
	fmt.Println(add_func(1,1))
	fmt.Println(add_func(0,0))
	fmt.Println(add_func(2,2))
}
// 闭包使用方法
func add(x1, x2 int) func(x3 int,x4 int)(int,int,int)  {
	i := 0
	return func(x3 int,x4 int) (int,int,int){
		i++
		return i,x1+x2,x3+x4
	}
}
/*
1 3 2
2 3 0
3 3 4
*/
```

**Go语言函数方法**

Go语言同时有函数和方法。一个方法就是一个包含了接受者的参数，接受者可以是命名类型或者是结构体类型的一个值或者是一个指针。所有给定类型的方法属于该类型的方法集。

```go
func(variable_name variable_data_type) function_name()[return_type]{
	/* 函数体 */
}
```

实例：

```go
package main

import (
	"fmt"
)

/* 定义结构体 */
type Circle struct {
	radius float64
}

func main() {
	var c1 Circle
	c1.radius = 10.00
	fmt.Println("圆的面积 = ", c1.getArea())
}

//该 method 属于 Circle 类型对象中的方法
func (c Circle) getArea() float64 {
	//c.radius 即为 Circle 类型对象中的属性
	return 3.14 * c.radius * c.radius
}
```



### 11. Go语言变量作用域

作用域为已声明标识符所表示的常量、类型、变量、函数或包在源代码中的作用范围

- 函数内定义的变量称为局部变量
- 函数外定义的变量称为全局变量
- 函数定义中的变量称为形式参数

**局部变量**

作用域只在函数体内，参数和返回值变量也是局部变量

**全局变量**

全局变量可在整个包甚至外部包（被导出后）使用

全局变量可在任何函数使用

🔺全局变量与局部变量名称可以相同，但函数内的局部变量会被优先考虑

**形式参数**

作为函数局部变量使用

**初始化局部和全局变量**

| 数据类型 | 初始化默认值 |
| -------- | ------------ |
| int      | 0            |
| float32  | 0            |
| pointer  | nil          |



### 12. Go数组

数组是具有相同唯一类型的一组已编号且长度固定的数据项序列，这种类型可以是任意的原始类型如整型、字符串或自定义类型。

**声明数组**

```go
var balance [10] float32
```

如上定义了数组名为balance，长度为10，类型为float32

**初始化数组**

```go
var balance = [5]float32{100.0,2.0,3.6,7.0,24.0}
```

如果忽略[]中数字不设置数组大小，Go语言会根据元素的个数来设置数组大小：

```go
var balance = [...]float32{100.0,2.0,3.6,7.0,24.0}
```

**访问数组元素**

```go
package main
import "fmt"

func main(){
	var n = [4]int{1,3,4}
	n[3] = 7
	for i:=0;i<len(n);i++{
		fmt.Printf("n[%d] = %d\n", i,n[i])
	}
}
```

**多维数组**

```go
var arrayName [x][y] variable_type
```

初始化二维数组

```go
a = [2][3] int{
	{0,1,2},
	{3,4,5},
}
```

访问二维数组元素

```go
package main
import "fmt"

func main(){
	var a = [2][3]int{
		{1,2,3},
		{4,5,6},
	}
	for i:=0;i<len(a);i++{
		for j:=0;j<len(a[0]);j++{
			fmt.Printf("a[%d][%d] = %d\n",i,j,a[i][j])
		}
	}
}
```

**向函数传递数组**

- 形参设定数组大小：

  ```go
  void myFunction(param [10]int)
  {
  	...
  }
  ```

- 形参未设定数组大小：

  ```go
  void myFunction(param []int)
  {
  	...
  }
  ```

实例：

```go
package main
import "fmt"

func main(){
	var n = [4]int{1,2,3,4}
	fmt.Println(getSum(n))
}

func getSum(arr[4]int) int {
	var sum int
	for i:=0;i<len(arr);i++{
		sum+=arr[i]
	}
	return sum
}
```



### 13. Go切片（Slice）

Go切片是对数组的抽象。Go数组长度不可变，而切片长度不固定，可以追加元素，在追加时可使切片容量增大

**定义切片**

```go
var identifier []type

var slice1 []type = make([]type,len)

var slice1 []type = make([]T,length,capacity)
```

len是数组长度也是切片初始长度，容量capacity为可选参数

**切片初始化**

```go
s :=[] int{1,2,3}	//cap=len=3
s := arr[:]	//s是对arr的引用
s := arr[start:end]
s := arr[start:]
s := arr[:end]
s1 := s[start:end]	//用切片s初始化切片s1
s := make([]int,len,cap)
```

**len()和cap()**

```go
package main
import "fmt"

func main(){
	var slice1 = make([]int,2,6)
	printSlice(slice1)
}

func printSlice(x []int){
	fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
}

/*
len=2 cap=6 slice=[0 0]
*/
```

切片是可索引的，由 `len()`获取长度，由 `cap()`测量切片最长可达到多少

**空（nil）切片**

一个切片在未初始化之前默认为nil，长度为0

**切片截取**

```go
package main
import "fmt"

func main(){
	var slice1 =make([]int,2,6)
	slice1 = []int{1,3,4,5,6}
	fmt.Println(slice1[2:5])
	fmt.Println(slice1[:])
	fmt.Println(slice1[:2])
	fmt.Println(slice1[3:])
    
	nums1 := make([]int,1,5)
	printSlice(nums1)
	nums2 := slice1[:2]
	printSlice(nums2)
	nums3 := slice1[3:4]
	printSlice(nums3)
}

func printSlice(x []int){
	fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
}
/*
[4 5 6]
[1 3 4 5 6]
[1 3]
[5 6]
len=1 cap=5 slice=[0]
len=2 cap=5 slice=[1 3]
len=1 cap=2 slice=[5]
*/
```

**append()和copy()**

如想增加切片容量，必须创建一个新的更大的切片并把原分片的内容都拷贝过来

```go
package main
import "fmt"

func main(){
	var slice1 []int
	printSlice(slice1)

	slice1 = append(slice1,0)
	printSlice(slice1)

	slice1 = append(slice1,1)
	printSlice(slice1)

	slice1 = append(slice1,2,3,4)
	printSlice(slice1)

	slice2 := make([]int,len(slice1),(cap(slice1))*2)
	copy(slice2,slice1)
	printSlice(slice2)
}

func printSlice(x []int){
	fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
}
/*
len=0 cap=0 slice=[]
len=1 cap=1 slice=[0]
len=2 cap=2 slice=[0 1]
len=5 cap=6 slice=[0 1 2 3 4]
len=5 cap=12 slice=[0 1 2 3 4]
*/
```

⭐对于底层数组容量为k的切片slice[i:j]，长度为 j-i，容量为 k-i

⭐Q：**为什么上面代码中有一步骤cap是变成6？**

`append(list,[params])`

- 当一个一个添加元素时

  len(list)+1<=cap: cap = cap

  len(list)+1>cap: cap = 2*cap

- 当同时添加多个元素时

  len(list)+len([params])为偶数： cap = len(list)+len([params])

  len(list)+len([params])为奇数： cap = len(list)+len([params])+1

⭐函数调用时，slice按引用传递，array按值传递

```go
package main
import "fmt"

func main(){
	changeTest()
}

func changeTest(){
	arr1 := []int{1,2}
	arr2 := [2]int{1,2}
	arr3 := [2]int{1,2}

	fmt.Println("before:arr1",arr1)
	changeSlice(arr1)
	fmt.Println("after:arr1",arr1)
	fmt.Println("before:arr1",arr2)
	changeArray(arr2)
	fmt.Println("after:arr1",arr2)
	fmt.Println("before:arr1",arr3)
	changeArrayByPointer(&arr3)
	fmt.Println("after:arr1",arr3)
}

func changeSlice(arr[]int){
	arr[0] = 50
}

func changeArray(arr [2]int){
	arr[0] = 50
}

func changeArrayByPointer(arr *[2]int){
	arr[0] = 50
}
/*
before:arr1 [1 2]
after:arr1 [50 2]
before:arr1 [1 2]
after:arr1 [1 2]
before:arr1 [1 2]
after:arr1 [50 2]
*/
```



### 14. Go指针

Go语言取地址符是&，放到一个变量前会返回相应变量内存地址

```go
package main
import "fmt"

func main(){
	var a int = 5
	fmt.Printf("变量地址：%x\n",&a)
}
/*
变量地址：c0000a0090
*/
```

**什么是指针**

一个指针变量指向了一个值的内存地址

声明指针：

```go
var var_name *var-type //指向var-type类型
```

**使用指针**

```go
package main
import "fmt"

func main(){
	var a int = 5
	var ip *int
	ip = &a
	fmt.Printf("a 变量地址：%x\n",&a)
	fmt.Printf("ip 变量存储的指针地址：%x\n",ip)
	fmt.Printf("ip变量的值：%d\n",*ip)
}
/*
a 变量地址：c00000c0e8
ip 变量存储的指针地址：c00000c0e8
ip变量的值：5
*/
```

**空指针**

当一个指针被定义后没有分配到任何变量时，它的值为nil

nil指针也称为空指针。

```go
package main
import "fmt"

func main(){
	var ptr *int
	fmt.Printf("ptr值：%x\n",ptr)
	fmt.Println(ptr)
	fmt.Println(&ptr)
}
/*
ptr值：0
<nil>
0xc000006028
*/
```

**指针数组**

在使用数组时，有时可能需要保存数组，就需要用到指针

```go
package main
import "fmt"

func main(){
	arr := [3]int{2,4,6}
	var ptr [3]*int

	for i:=0;i<len(arr);i++{
		ptr[i] = &arr[i]
	}
	for j:=0;j<len(arr);j++{
		fmt.Printf("arr[%d] = %d\n",j,*ptr[j])
	}
}
/*
arr[0] = 2
arr[1] = 4
arr[2] = 6
*/
```

⭐创建指针数组时，不适合用range循环

**指向指针的指针**

如果一个指针变量存放的又是另一个指针变量的地址，则称这个指针变量为指向指针的指针变量

```go
package main
import "fmt"

func main(){
	var a int = 10
	var ptr *int
	var pptr **int

	ptr = &a
	pptr = &ptr

	fmt.Printf("a = %d\n",a)
	fmt.Printf("*ptr = %d\n",*ptr)
	fmt.Printf("**ptr = %d\n",**pptr)
	fmt.Printf("pptr = %x\n",pptr)
	fmt.Printf("ptr = %x\n",ptr)
}
/*
a = 10
*ptr = 10
**ptr = 10
pptr = c000006028
ptr = c00000c0e8
*/
```

**指针作为函数参数**



### 15. Go结构体

数组可存储同一类型数据，结构体中可为不同项定义不同的数据类型。

结构体是由一系列具有相同类型或不同类型的数据构成的数据集合。

**定义结构体**

```go
type struct_variable_type struct{
	member definition
	member definition
	member definition
}
```

接下来可用于变量声明

```go
variable_name := struct_variable_type {value1,value2,...,valuen}
variable_name := struct_variable_type {key1:value1,key2:value2,...,keyn:valuen}
```

**访问结构体成员**

```go
结构体。成员名
```

使用点号操作符

**结构体作为函数参数**

**结构体指针**

```go
var struct_pointer *Books
struct_pointer = &Book1
struct_pointer.title	//访问成员
```

实例：

```go
package main
import "fmt"

type Books struct{
	title string
	id int
	author string
}

func main(){
	fmt.Println(Books{"abc",12,"Anna"})
	fmt.Println(Books{title:"abcd",id:10,author:"Bobby"})

	var book1 Books
	book1.title = "Go语言"
	book1.id = 12345
	book1.author = "Louis"

	printBook(book1)
	printBook2(&book1)

	changeBook(book1)
	fmt.Println(book1.id)

	changeBook2(&book1)
	fmt.Println(book1.id)
}

func printBook(book Books){
	fmt.Printf("Book author : %s\n",book.author)
}

func printBook2(book *Books){
	fmt.Printf("Book id : %d\n",book.id)
}

func changeBook(book Books){
	book.id = 123
}

func changeBook2(book *Books){
	book.id = 123456
}
/*
{abc 12 Anna}
{abcd 10 Bobby}
Book author : Louis
Book id : 12345
12345
123456
*/
```

⭐结构体是作为参数的值传递，想要在函数里面改变结构体数据内容需要传入指针



### 16. Go范围（Range）

range关键字用于for循环中迭代数组、切片、通道或集合的元素。在数组和切片中它返回元素的索引和索引对应的值，在集合中返回key-value对

```go
package main
import "fmt"

func main(){
	nums := [3]int{1,2,3}
	sum := 0
	length := 0

	for range nums{
		length++
	}
	fmt.Println(length)

	for _,num:=range nums{
		sum+=num
	}
	fmt.Println(sum)

	kvs := map[string]string{"a":"apple","b":"banana"}
	for k,v := range kvs{
		fmt.Printf("%s -> %s\n",k,v)
	}
	// 枚举Unicode字符串
	for i,c := range "go"{
		fmt.Println(i,c)
	}
}
/*
3
6
a -> apple
b -> banana
0 103
1 111
*/
```



### 17. Go的Map（集合）

Map是一种无序的键值对集合，通过key快速检索数据，key类似索引，指向数据值。

可以像迭代数组和切片那样迭代它，但无法决定它的返回顺序，因为Map是以hash表实现的。

**定义Map**

```go
var map_variable map[key_data_type]value_data_type
map_variable := make(map[key_data_type]value_data_type)
```

如果不初始化map，就会创建一个nil map。nil map不能用来存放键值对。

**delete()**

delete()函数用于删除集合元素，参数为map和其对应的key

```go
package main
import "fmt"

func main(){
	var myMap map[string]int
	myMap = make(map[string]int)

	myMap["a"] = 1
	myMap["b"] = 2
	myMap["e"] = 5

	for k,v:=range myMap{
		fmt.Printf("%s -> %d\n",k,v)
	}

	character,ok := myMap["d"]
	if(ok){
		fmt.Println(character)
	}else{
		fmt.Println("not exist")
	}

	delete(myMap,"a")
	fmt.Println(myMap)
}
/*
e -> 5
a -> 1
b -> 2
not exist
map[b:2 e:5]
*/
```



### 18. Go递归函数

使用递归时，开发者需要设置退出条件，否则递归将陷入无限循环。

**斐波那契数列**

```go
package main
import "fmt"

func main(){
	a:=6
	fmt.Println(fib(a))
}

func fib(n int)int{
	if(n<2){
		return n
	}
	return fib(n-1)+fib(n-2)
}
```

🔺一种更好的斐波那契数列的实现

```go
package main
import "fmt"

func main(){
	a:=6
	fmt.Println(fib(a))
}

func fib(n int)int{
	_,b:=fib2(n)
	return b
}

func fib2(n int)(int,int){
	if n<2{
		return 0,n
	}
	a,b:=fib2(n-1)
	return b,a+b
}
```



### 19. Go类型转换

基本格式：

```go
type_name(expression)
```

实例：

```go
package main
import "fmt"

func main(){
	var a int = 17
	var b int = 5
	var mean float32
	mean = float32(a)/float32(b)
	meanint := a/b
	fmt.Println(mean)
	fmt.Println(meanint)
}
/*
3.4
3
*/
```



### 20. Go接口

把所有具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口

```go
type interface_name interface{
	method_name1 [return_type]
	...
	method_namen [return_type]
}
type struct_name struct{
}
func (struct_name_variable struct_name) method_name1() [return_type]{
}
func (struct_name_variable struct_name) method_namen()	[return_type]{
}
```

**普通实例**

```go
package main
import "fmt"

type Animal interface {
	run()
}

type Dog struct{
}

type Cat struct{
}

func (dog Dog) run(){
	fmt.Println("Dog run")
}

func (cat Cat) run(){
	fmt.Println("Cat run")
}

func main(){
	var animal Animal
	animal = new(Dog)
	animal.run()
	animal = new(Cat)
	animal.run()
}
/*
Dog run
Cat run
*/
```

**接口增加参数**

```go
package main
import "fmt"

type Animal interface {
	name() string
}

type Dog struct{
}

func (dog Dog) name() string{
	return "Bobby"
}

func main(){
	var animal Animal
	animal = new(Dog)
	fmt.Println(animal.name())
}
/*
Bobby
*/
```

**接口方法传参和返回结果**

```go
package main
import "fmt"

type Animal interface {
	run(s int)
}

type Dog struct{
}

func (dog Dog) run(s int){
	fmt.Printf("A dog runs %d s",s)
}

func main(){
	var animal Animal
	animal = new(Dog)
	animal.run(15)
}
/*
A dog runs 15 s
*/
```

**将接口作为参数**

```go
package main
import "fmt"

type Phone interface {
	call() string
}

type Android struct{
	brand string
}

type IPhone struct{
	ver string
}

func (android Android) call() string{
	return "Android "+ android.brand
}

func (iPhone IPhone) call() string{
	return "IPhone "+iPhone.ver
}

func print(p Phone){
	fmt.Println(p.call()+", I can call you.")
}

func main(){
	huawei := Android{"HuaWei"}
	i7 := IPhone{"7"}

	print(huawei)
	print(i7)
}
/*
Android HuaWei, I can call you.
IPhone 7, I can call you.
*/
```

**通过接口方法修改属性，在传入指针的结构体**

```go
package main
import "fmt"

type Animal interface {
	getName() string
	setName(name string)
}

type Dog struct{
	name string
}

func (dog *Dog) getName() string{
	return dog.name
}

func (dog *Dog) setName(name string){
	dog.name = name
}

func main(){
	var animal Animal
	animal = new(Dog)
	animal.setName("Bob")
	fmt.Println(animal.getName())
	animal.setName("Kot")
	fmt.Println(animal.getName())
}
/*
Bob
Kot
*/
```



### 21. Go错误处理

error类型是一个接口类型：

```go
type Error interface{
	Error() string
}
```

🔺通过实现error接口类型生成错误信息

函数通常在最后的返回值中返回错误信息。使用errors.New可返回一个错误信息：

```go
func Sqrt(f float64) (float64,error){
	if f<0{
		return 0,errors.New("math:square root of negative number")
	}
}
```

调用Sqrt传递一个负数，得到non-nil的error对象，将此对象与nil比较，fmt包在处理error时会调用Error方法：

```go
result,err := Sqrt(-1)
if err != nil{
	fmt.Println(err)
}
```

**除零错误实例**

```go
package main
import "fmt"

type DIV_ERR struct{
	etype int
	v1 int
	v2 int
}

func (div_err DIV_ERR) Error() string{
	if 0==div_err.etype {
		return "除零错误"
	}else{
		return "其他未知错误"
	}
}

func div(a int,b int)(int,*DIV_ERR){
	if b==0{
		return 0,&DIV_ERR{0,a,b}
	}else{
		return a/b,nil
	}
}

func main(){
	_,r := div(50,5)
	if nil != r{
		fmt.Println("fail")
	}else{
		fmt.Println("succeed")
	}

	_,r = div(50,0)
	if nil!=r{
		fmt.Println("fail")
	}else{
		fmt.Println("succeed")
	}
}
```

**panic、recover、defer**

panic和recover是内置函数，用于处理Go运行时的错误。

panic主动抛出错误，recover捕获panic抛出的错误

🔺引发panic两种情况：①程序主动调用、②程序产生运行时错误，由运行时检测并退出

🔺发生panic后，程序从调用panic的函数位置或发生panic的地方立即返回，逐层向上执行函数defer语句，然后逐层打印函数调用堆栈，直到被recover捕获或运行到最外层函数

🔺panic不但可在函数正常流程中抛出，在defer逻辑里也可以再次调用panic或抛出panic。defer里面的panic能够被后续执行的defer捕获。

🔺recover用来捕获panic，阻止panic继续向上传递。recover()和defer一起使用，但是defer只有后面的函数体内直接被调用才能捕获panic来终止异常，否则返回nil，异常继续向外传递

实例1：

```go
package main
import "fmt"

func main(){
	defer func(){
		if err := recover() ; err != nil {
			fmt.Println(err)
		}
	}()
	defer func(){
		panic("three")
	}()
	defer func(){
		panic("two")
	}()
	panic("one")
}
/*
three
*/
```

多个panic只会捕捉最后一个

🔺panic在没有用recover前以及在recover捕获那一级函数栈，panic之后的代码均不会执行；一旦被recover捕获后，外层的函数栈代码恢复正常，所有代码均会得到执行

🔺panic后，不再执行后面的代码，立即按照逆序执行defer，并逐级往外层函数栈扩散；defer类似finally

🔺利用recover捕获panic时，defer需要在panic之前声明，否则由于panic之后的代码得不到执行，因此也无法recover

实例2：

```go
package main
import "fmt"

func main() {
	fmt.Println("外层开始")
	defer func() {
		fmt.Println("外层准备recover")
		if err := recover(); err != nil {
			fmt.Printf("%#v-%#v\n", "外层", err) // err已经在上一级的函数中捕获了，这里没有异常，只是例行先执行defer，然后执行后面的代码
		} else {
			fmt.Println("外层没做啥事")
		}
		fmt.Println("外层完成recover")
	}()
	fmt.Println("外层即将异常")
	f()
	fmt.Println("外层异常后")
	defer func() {
		fmt.Println("外层异常后defer")
	}()
}

func f() {
	fmt.Println("内层开始")
	defer func() {
		fmt.Println("内层recover前的defer")
	}()

	defer func() {
		fmt.Println("内层准备recover")
		if err := recover(); err != nil {
			fmt.Printf("%#v-%#v\n", "内层", err) // 这里err就是panic传入的内容
		}

		fmt.Println("内层完成recover")
	}()

	defer func() {
		fmt.Println("内层异常前recover后的defer")
	}()

	panic("异常信息")

	defer func() {
		fmt.Println("内层异常后的defer")
	}()

	fmt.Println("内层异常后语句") //recover捕获的一级或者完全不捕获这里开始下面代码不会再执行
}
/*
外层开始
外层即将异常
内层开始
内层异常前recover后的defer
内层准备recover
"内层"-"异常信息"
内层完成recover
内层recover前的defer
外层异常后
外层异常后defer
外层准备recover
外层没做啥事
外层完成recover
*/
```



### 22. Go并发

通过go关键字开启goroutine。

goroutine是轻量级线程，goroutine的调度是由Golang运行时进行管理的。

goroutine语法格式：

```go
go 函数名(参数列表)
```

Go允许使用go语句开启一个新的运行期线程，即goroutine，以一个不同的、新创建的goroutine来执行一个函数。

同一个程序中所有goroutine共享同一个地址空间。

```go
package main
import (
	"fmt"
	"time"
)

func print(s string){
	for i:=0;i<5;i++{
		time.Sleep(100*time.Millisecond)
		fmt.Println(s)
	}
}

func main(){
	go print("a")
	print("b")
}
/*
a
b
b
a
a
b
a
b
b
a
*/
```

输出没有固定顺序

**通道（Channel）**

通道是用来传递数据的一个数据结构。

通道可用于两个goroutine之间通过传递一个指定类型的值来同步运行和通讯。

操作符 `<-`用于指定通道方向，发送或接收。如果未指定方向，则为双向通道。

```go
ch <- v //把v发送到通道ch
v := <- ch	//从ch接收数据并把值赋给v
```

声明一个通道：

```go
ch := make(chan int)
```

⭐默认通道不带缓冲区。发送端发送数据，同时必须有接收端相应的接收数据

实例：

```go
package main
import "fmt"

func sum(arr[]int,c chan int){
	sum := 0
	for _,v := range(arr){
		sum+=v
	}
	c <- sum
}

func main(){
	arr:=[]int{1,4,2,3,2,7}
	c:=make(chan int)
	go sum(arr[:len(arr)/2],c)
	go sum(arr[len(arr)/2:],c)
	a,b:=<-c,<-c
	fmt.Println(a,b)
}
/*
12 7
*/
```

**通道缓冲区**

通过make的第二个参数指定缓冲区大小：

```go
ch := make(chan int,100)
```

带缓冲区的通道允许发送端的数据发送和接收端的数据获取处于异步状态，即发送端发送的数据可以放在缓冲区里，等待接收端获取数据，而不是立刻需要接收端获取数据。

但缓冲区大小有限，还是必须有接收端接收数据，否则缓冲区一满数据发送端就无法再发送数据了。

⭐如果通道不带缓冲，发送方会阻塞直到接收方从通道中接收了值。如果通道带缓冲，发送方则会阻塞直到发送的值被拷贝到缓冲区内；如果缓冲区已满，意味着需要等待直到某个接收方获取到一个值。接收方在有值可以接收之前会一直阻塞。

```go
package main
import "fmt"

func main(){
	ch := make(chan int,10)
	ch <- 1
	ch <- 3
	ch <- 4
	fmt.Println(<-ch)
	fmt.Println(<-ch)
	fmt.Println(<-ch)
}
/*
1
3
4
*/
```

**遍历通道与关闭通道**

```go
package main
import (
	"fmt"
	"time"
)

func main(){
	ch := make(chan int,10)
	go fib(cap(ch),ch)
    /*
    如果ch通道不关闭，那么range函数就不会结束，从而在接收第11个数据时会阻塞
    */
	for i:=range ch{
		fmt.Println(i)
	}
}

func fib(n int,c chan int){
	x,y:=0,1
	for i:=0;i<n;i++{
		c <- x
		x, y =  y,x+y
		time.Sleep(1000*time.Millisecond)
	}
	close(c)
}
```

🔺关闭通道并不会丢失里面的数据，只是让读取通道数据的时候不会读完之后一直阻塞等待新数据写入

🔺Channel可以控制读写权限

```go
go func(c chan int)	// 读写均可的channel
go func(c <- chan int)	//只读的channel
go func(c chan <- int)	//只写的channel
```

⭐通道遵循先进先出原则：

```go
package main
import "fmt"

func main(){
	ch := make(chan int,2)
	ch <- 1
	a:= <- ch
	ch <- 2
	ch <- 3
	fmt.Println(<-ch)
	fmt.Println(<-ch)
	fmt.Println(a)
}
/*
2
3
1
*/
```

🔺一个实例：

```go
package main
import (
    "fmt"
    "time"
)
func say(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s, (i+1)*100)
    }
}
func say2(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(150 * time.Millisecond)
        fmt.Println(s, (i+1)*150)
    }
}
func main() {
    go say2("world")
    say("hello")
}
/*
hello 100
world 150
hello 200
world 300
hello 300
hello 400
world 450
hello 500
*/
```

say2只执行了3次，而不是5次，是因为goroutine还没来得及跑完5次主函数已经退出了。

下面想办法阻止主函数结束，要等待goroutine执行完成后，再退出主函数。

```go
package main
import (
	"fmt"
	"time"
)

func say(s string) {
	for i := 0; i < 5; i++ {
		time.Sleep(100 * time.Millisecond)
		fmt.Println(s, (i+1)*100)
	}
}
func say2(s string, ch chan int) {
	for i := 0; i < 5; i++ {
		time.Sleep(150 * time.Millisecond)
		fmt.Println(s, (i+1)*150)
	}
	ch <- 0
	close(ch)
}

func main() {
	ch := make(chan int)
	go say2("world", ch)
	say("hello")
	fmt.Println(<-ch)
}
```

引入一个默认信道，信道的存消息和取消息都是阻塞的，goroutine执行完后给信道一个值0，则主函数会一直等待信道中的值，一旦信道有值主函数才会结束。