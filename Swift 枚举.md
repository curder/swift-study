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


































