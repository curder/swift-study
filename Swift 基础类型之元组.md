## Swift 基础类型之元组
　　元组（`tuples`）把多个值组合成一个复合值。元组内的值可以是任意类型，并不要求是相同类型。

### 记录一个点的坐标位置
```
var point = ( 2 , 1 )
```

### 记录Http的相应头信息
```
let http404Error = ( httpStatus: 404 , httpMessage: "The Page Not Found!" )
```

### 显式的指定元组的数据类型
```
var point2:( Int ,  Int , Int ) = ( 10 , 20 , 30 )
let httpResponse:( httpStatus: Int , httpMessage: String ) = ( 200 , "OK" )
```

### 元组的解包
　　将一个元组的内容分解（`decompose`）成单独的常量和变量。
```
let ( x , y ) = point // 分别得到 x 的值为 2 , y 的值为 1 .
```
　　也可以使用如下的方式使用 point 分量，但这种方式获取不直观。
```
point.0
point.1
```

```
var ( statusCode , statusMessage ) = httpResponse // 分别得到 statusCode 的值为 200 , statusMessage 的值为 OK
```

