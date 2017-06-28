## Swift 枚举

### 枚举定义

定义语法：

```
emun 枚举名称 {
	case 枚举值
    case 枚举值
    ...
}
```

例如：定义枚举型 Month 时，我们可以使用如下方式：

```
enum Month{
    case January
    case February
    case March
    case April
    case May
    case June
    case July
    case August
    case September
    case October
    case November
    case December
}
```
### 枚举型的取值

```
var currMonth = Month.September

// 当确定了变量是枚举类型也可以直接使用 .枚举名 获取。
var currMonth: Month = .September
```

### 使用枚举类型

```
// 枚举月份
enum Month{
    case January
    case February
    case March
    case April
    case May
    case June
    case July
    case August
    case September
    case October
    case November
    case December
}

// 枚举月份 可以将case省略而将定义放在一行
enum Season{
    case Spring, Summer, Autumn, Winter
}


func season(month: Month) -> Season{
    switch month {
        case .March, .April, .May:
            return .Spring
        case .June, .July, .August:
            return .Summer
        case .September, .October, .November:
            return .Autumn
        case .December, .January, .February:
            return .Winter
    }
}


print( season(month: .April ) ) // Spring
```

### 枚举之原始值

```
enum Month: Int { // 定义原始值是整形类型
    case January = 1
    case February = 2
    case March = 3
    case April = 4
    case May = 5
    case June = 6
    case July = 7
    case August = 8
    case September = 9
    case October = 10
    case November = 11
    case December = 12
}

// 查找当前月份距离新年还剩多少个月
func monthsBeforeNewYear( _ month: Month ) -> Int{
    return 12 - month.rawValue
}

let month: Month = .October
monthsBeforeNewYear(month) // 距离新年还有 2 个月

// 使用枚举型的构造函数进行数据处理
let input = 2
if let month = Month( rawValue: input) {
    monthsBeforeNewYear(month)
}
```
### 使用枚举型默认的原始值

```
enum Grade: Int{
    case F, E, D, C, B, A
}
let grade: Grade = .A
print("Your score is \(grade.rawValue)") // Your score is 5
```
> 枚举型的原始值默认从0开始计算，逐步+1。


自定义枚举型的原始值
```
enum Coin: Int{
    case Penny = 1
    case Nickel = 5
    case Dime = 10
    case Quarter = 25
}
let coin: Coin = .Quarter
print("It's \(coin.rawValue) cents") // It's 25 cents
```

### 枚举其他类型原始值

枚举型的rawValue为String定义

```
enum ProgrammingLanguage: String { // 枚举型的rawValue为String
    case Swift // 不填写 使用 ProgrammingLanguage.rawValue 的值为：Swift，即默认原始值为 Swift
    case ObjectiveC = "Objective-C"
    case C
    case Java
}

var myFavoriteLanguage: ProgrammingLanguage = .ObjectiveC

print("\(myFavoriteLanguage.rawValue) is my favorite language.") // Objective-C is my favorite language.

myFavoriteLanguage = ProgrammingLanguage.Swift
print("\(myFavoriteLanguage.rawValue) is my favorite language.") // Swift is my favorite language.
```

### 枚举之关联值

在Swift中，枚举型支持枚举的可能性可以和一个变量相关联（Associat Value），并且他们之间的值类型可以不同。

#### 关联一个值
下列是一个用户在 ATM 取款的场景，判断用户取的钱是否小于账户余额。
```
enum AtmStatus {
    case Success(Int) // 枚举的值关联一个整型值
    case Error(String) // 枚举的值关联一个字符串
    case Waiting
}

var balance = 1000 // 账户与余额

func withDraw( amount: Int) -> AtmStatus { // 返回值为枚举型
    if balance >= amount{
        balance -= amount
        return .Success(balance)
    }else{
        return .Error("Not enough money")
    }
}

let result = withDraw(amount: 100)
switch result { // 在判断语句中使用 let 解包
case let .Success(newBanacle):
    print("\(newBanacle) Yuan left in your account.")
case let .Error(errorMessage):
    print("Error: \(errorMessage)")
case .Waiting:
	print("Waiting")    
}
```

> 枚举型中关联值不是必须的，可以有的存在，有的不存在。


#### 关联多个值

关联多个值时，参数相当于元组
```
enum Shape{
    case Square( side: Double )
    case Rectangle( width: Double, height: Double )
    case Circle(centerx: Double , centery: Double , radius: Double)
    case Point
}

let square = Shape.Square(side: 10)
let rectangle = Shape.Rectangle(width: 20, height: 30)
let circle = Shape.Circle(centerx: 40, centery: 50, radius: 60)
let point = Shape.Point


func area(shape: Shape) -> Double{
    switch shape {
    case let .Square( side ):
        return side * side
    case let .Rectangle( width , height ):
        return width * height
    case let .Circle( _ , _ , r ):
        return M_PI * r * r
    case .Point:
        return 0
    }
}

area(shape: square) // 正方形
area(shape: rectangle) // 长方形
area(shape: circle) // 圆形
area(shape: point) // 点
```

### 可选型的实质是枚举
```
var website: Optional<String> = Optional.some("webfsd.com")

// website = .none

// 可选型的解包
switch website {
case .none:
    print("No website")
case let .some(website):
    print("The website is \(website)")
}

if let website = website {
    print("The website is \(website)")
}else{
    print("No website")
}
```


### 枚举类型定义方法
```
// 枚举类型定义方法
enum Shape{
    case Square(side: Double) // 正方形
    case Rectangle(width: Double , height: Double) // 长方形
    case Circle(centerx: Double , centery: Double , radius: Double) // 圆形
    case Point // 点
    
    // 计算面积的方式
    func area() -> Double {
        switch self {
        case let .Square( side ):
            return side * side
        case let .Rectangle( width , height ):
            return width * height
        case let .Circle( _ , _ , r ):
            return M_PI * r * r
        case .Point:
            return 0
        }
    }
}


let shape = Shape.Square(side: 10)
let rectangle = Shape.Rectangle(width: 10, height: 5)
let circle = Shape.Circle(centerx: 10, centery: 20, radius: 8)
let point = Shape.Point

shape.area()
rectangle.area()
circle.area()
point.area()
```


### 枚举类型是值类型
```
enum Direction{
    case North
    case South
    case East
    case West
}

var d1 = Direction.East
var d2 = d1

d2 = Direction.West

d1 // East
d2 // West
```