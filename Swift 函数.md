## Swift 函数
Swift 中函数是引用类型。

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

if let resault = findMaxAndMin(numbers:scores!){
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

### 函数默认参数
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

### 函数可变参数

在声明函数的形参的时候 后面加上 `...`，在函数中，将该变长参数的值作为数组看待即可。

```
func mean( numbers: Double ... )->Double{
    var sum: Double = 0
    
    // 将变长的参数的值作为数组看待
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

函数的参数默认是 `let` 常量类型，我们不能在函数内部对传入的参数进行修改，在Swift3.0中，可以在函数内部使用 `var` 声明函数参数为变量进行修改。
```
func toBinary(num: Int) -> String {
    var num = num // 需要将传入的变量定义为 `var` 变量
    var res = ""
    repeat {
        res = String(num%2) + res
        num /= 2
    } while num != 0
    
    return res
}

toBinary(num: 100)
```

参数的地址引用，使用`inout`关键字

```
func swapTwoInts( _ a: inout Int, _ b:inout Int) {
    let t:Int = a
    a = b
    b = t
}
var x: Int = 1
var y: Int = 2

swapTwoInts(&x, &y) // 使用 & 按引用传递

x // 2
y // 1
```

上面的函数也可以使用Swift中的元组实现。

```
func swapTwoInts2( _ a:inout Int, _ b:inout Int){
    (a, b) = (b, a)
}

var x: Int = 1
var y: Int = 2

swapTwoInts2(&x, &y)

x // 2
y // 1
```

按值传递的数组
```
func initArray(arr: inout [Int], by value: Int) {
    for i in 0..<arr.count {
        arr[i] = value
    }
}

var arr = [1, 2, 3, 4, 5]

initArray(arr: &arr, by: 0) // 需要使用 & 取地址符传递数据，改变原数组的值 [0, 0, 0, 0, 0]
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
> 上面的操作将 `add()` 函数直接赋值给 `anotherAdd()`，那么 `anotherAdd` 也是一个函数。

如果函数不存在返回值的清空
```
func sayHello(to name: String) -> Void{
    print("Hello \(name)")
}

let anotherSayHello: (String)->Void = sayHello
// 或者这样声明函数常量
let anotherSayHello: (String)->() = sayHello
```

如果函数返回值和参数都不存在的情况，可以显式的定义 `->Void`的方式定义。

```
func say(){
    print("Hello!")
}

let anotherSay: ()->() = say
let anotherSay2: (Void)->Void = say
let anotherSay3: ()->Void = say
let anotherSay4: (Void)->() = say
```
> 就是 `Void` 和`()` 都可以表示返回值为空的情况。


#### 函数型变量的应用

使用系统函数`sorted()` 传入函数型变量，对数组中的元素进行从大到小的排序

```
var arr: [Int] = []
for _ in 0..<100 {
    arr.append(Int(arc4random() % 1000))
}



arr.sorted() // 不改变原有数组的值进行从小到大排序
arr.sort() // 改变有数组的值进行从小到大排序


// 那么我们想数组从大到小排序要怎么做呢？

arr.sorted(by: biggerNumberFirst) // 使用函数型变量传值给参数

func biggerNumberFirst (a: Int, _ b: Int) -> Bool {
//    if a > b {
//        return true
//    } else {
//        return false
//    }
    return a > b // 可以直接使用运算符简化上面的写法
}
```

根据字符串排序

```
func cmpByNumberString(a: Int, _ b: Int) -> Bool {
    return String(a) < String(b)
}

arr.sorted(by: cmpByNumberString) // [101, 105, 116, 129, 131, 142, 142, 146, 182, 183, 184, 187, 189, 197, 206, 207, 207, 229, 23, 240, 252, 253, 255, 262, 291, 295, 295, 32, 33, 377, 38, 395, 398, 422, 439, 450, 458, 464, 470, 475, 485, 488, 488, 494, 503, 505, 509, 518, 572, 573, 58, 584, 598, 6, 605, 615, 616, 619, 622, 624, 625, 633, 638, 647, 649, 655, 674, 680, 685, 713, 746, 746, 756, 757, 771, 771, 787, 789, 790, 791, 792, 792, 794, 806, 818, 836, 844, 864, 868, 880, 880, 888, 898, 902, 922, 944, 947, 960, 962, 99]
```

#### 返回函数类型和函数嵌套
```
// 计费方式1
func tierMailFeeByWeight(weight: Int) -> Int {
    return 1 * weight
}

// 计费方式2
func tier2MailFeeByWeight(weight: Int) -> Int {
    return 3 * weight
}

// 函数嵌套的应用
func feeByUnitPrice(price: Int, weight: Int) -> Int {
    // 判断计费方式 将函数作为返回值的用法
    func chooseMailFeeCalculationByWeight(weight: Int) -> (Int) -> Int {
        return weight <= 10 ? tierMailFeeByWeight : tier2MailFeeByWeight
    }

    let mailFeeByWeight = chooseMailFeeCalculationByWeight(weight: weight)
    return mailFeeByWeight(weight) + price * weight
}
```