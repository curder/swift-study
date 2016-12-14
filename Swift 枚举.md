## Swift 枚举

### 枚举定义

定义枚举型 Month 时，我们可以使用如下方式：

```
emun 枚举名称{
	case 枚举值
    case 枚举值
    ...
}
```
具体如下：
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
var currMonth: Month = Month.September

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

// 枚举月份
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
enum Month: Int{
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

// 使用 Month 的构造函数进行数据处理
let input = 2
if let month = Month( rawValue: input){
    monthsBeforeNewYear(month)
}
```
### 使用枚举行默认的原始值

```
enum Grade: Int{
    case F,E,D,C,B,A
}
let grade: Grade = .A
print("Your score is \(grade.rawValue)") // Your score is 5
```
### 枚举其他类型原始值

```
enum ProgrammingLanguage: String{
    case Swift // 不填写 使用 ProgrammingLanguage.rawValue 的值为：Swift，即默认原始值为 Swift
    case ObjectiveC = "Objective-C"
    case C
    case Java
}

var myFavoriteLanguage: ProgrammingLanguage = .ObjectiveC

print("\(myFavoriteLanguage.rawValue) is my favorite language.") // Objective-C is my favorite language.

myFavoriteLanguage = ProgrammingLanguage.Swift
print("\(myFavoriteLanguage.rawValue) is my favorite language.")
```
































