## Swift 函数

[TOC]

### 函数语法
```
func  函数名 ( 参数变量: 类型 , 参数变量: 类型 ... ) -> 函数返回值 {

}
```
> 说明: 
> 1: func 是定义函数的关键字
> 2：`{}` 函数体
> 3: 参数变量是默认常量类型，不能在函数函数体里面直接修改。即： `func A (value:String)`  与 `func A (let value:String)` 写法是相同的，即 `value` 是常量。


### 函数中使用元组返回多个值

```
func findMaxAndMin( numbers: [Int])->( max: Int, min: Int )? {
    
    guard numbers.count > 0 else {
        return nil
    }
    
    var minValue = numbers[0]
    var maxValue = numbers[0]
    for number in numbers{
        minValue = minValue < number ? minValue : number
        maxValue = maxValue > number ? maxValue : number
    }
    return ( maxValue, minValue )
}

var scores: [Int]? = [202,1232,4321,33,432,666]

scores = scores ?? []

if let resault = findMaxAndMin(numbers: scores!){
    print("The max score is \(resault.max)")
    print("The min score is \(resault.min)")
}
```

### 函数的多个参数处理
#### 函数内部参数与外部参数
```
func sayHello( to name: String , message greeting: String ) -> String {
    return "\(name),\(greeting)"
}
sayHello(to: "Curder", message: "Hello!!!")
```

> 内部参数有 `to` 与 `message`
> 外部参数有 `name` 与 `greeting`



#### 函数省略外部参数名
```
func mutiply( _ num1: Int, _ num2: Int ) -> Int{
    return num1 * num2
}

mutiply(1, 2)
```

### 函数默认参数与可变参数
```
func sayHello(to name: String, message greeting: String = "Hello",punctuation: String = "!")->String{
    return "\(greeting),\(name)\(punctuation)"
}

// 调用省略可选参数
sayHello(to: "Luo") // "Hello,Luo!"
sayHello(to: "Luo",message: "Hi") // "Hi,Luo!"
sayHello(to: "Curder",punctuation: "!!!") // "Hello,Curder!!!"

sayHello(to: "Curder",message: "Hi",punctuation:"!!!") // "Hi,Curder!!!"
```

### 函数变长参数
　　在声明函数的形参的时候 后面加上 `...`，即可。在函数中，将该变长参数的值作为数组看待即可。

```
func mean( numbers: Double ... )->Double{
    var sum: Double = 0
    for number in numbers{
        sum += number
    }
    return sum / Double(numbers.count)
}

mean(numbers: 2)
mean(numbers: 2,3,4)
```
> 对于一个函数而言，只能有一个变长的参数。

### inout参数
// 参数的地址引用
```
func swapTwoInts( _ a: inout Int, _ b:inout Int){
    let t:Int = a
    a = b
    b = t
}
var x: Int = 1
var y: Int = 2

swapTwoInts(&x, &y)

x // 2
y // 1
```

### 声明函数型变量
如果函数存在返回值的情况
```
func add(_ a: Int,_ b: Int)-> Int{
    return a + b
}

let anotherAdd: (Int, Int) -> Int = add

anotherAdd(1,2)
```

如果函数不存在返回值的清空
```
func sayHello(to name: String) -> Void{
    print("Hello \(name)")
}

let anotherSayHello: (String)->Void = sayHello
// 或者这样声明函数常量
let anotherSayHello: (String)->() = sayHello
```











