## Swift 基础类型之元组

[TOC]

元组（`tuples`）把多个值组合成一个复合值。
  * **元组内的值可以是任意类型**
  * **并不强制要求是相同类型**。

### 元组的声明

```
// 记录一个点的坐标位置
var point = ( 2 , 1 )

// 记录Http的相应头信息
let http404Error = ( httpStatus: 404 , httpMessage: "The Page Not Found!" )
```

### 显式的指定元组的数据类型

在声明元组时，可以定义好分量的名称和数据类型，方便后期解包使用分量名称对数据的获取。

```
var point2:( Int ,  Int , Int ) = ( 10 , 20 , 30 )
let httpResponse:( httpStatus: Int , httpMessage: String ) = ( 200 , "OK" )
```

### 元组的解包

将一个元组的内容分解（ `decompose` ）成单独的常量和变量。

```
var point = ( 2 , 1 )
let ( x , y ) = point // 分别得到 x 的值为 2 , y 的值为 1 .

let httpResponse:( httpStatus: Int , httpMessage: String ) = ( 200 , "OK" )
var ( statusCode , statusMessage ) = httpResponse // 分别得到 statusCode 的值为 200 , statusMessage 的值为 OK
```

也可以使用如下的方式使用 `point` 分量，但这种方式获取不直观。如下：

```
point.0
point.1
```

### 获取元组中部分单元的值

对于元组中我们不关心的值，使用 `_` 跳过不关心的值。

```
let loginResult: ( isLoginSuccess: Bool , userName: String , loginTime: Int ) = ( true , "curder" , 1481101192 )

let ( _ , userName , _ ) = loginResult // 常量 userName 的值为 `curder`
```

### 可变元组和不可变元组

使用 `let` 声明的元组是**不可变元组**，使用 `var` 声明的元组是**可变元组**。

```
var userInfo = (name: "Stive", true, age: 22)
let user = (name: "Stive" , true , age: 50)

userInfo.name = "Stive Jobs" // 修改成功

user.name = "Stive Jobs" // 无法修改 error: cannot assign to property: 'user' is a 'let' constant
```

需要注意的是，可变元组虽然**可以修改数据**，**但却不能改变其数据的数据类型**：

```
var userInfo = (name: "Stive", true, age: 22)

userInfo.name = 22 // 修改了数据类型报错 error: cannot assign value of type 'Int' to type 'String'
```