## Swift 字典之初始化

**存储键、值，数据对的无序数据集。**

## 创建字典

### 创建空字典
声明不同类型的空字典
```
var emptyDict1: Dictionary<String,Int> = [:] // 键是String类型，值是Int类型的空字典
var emptyDict2: [Int:String] = [:] // 键是Int类型，值是String类型的空字典
var emptyDict3 = [String:String]() // 键是String类型，值是String类型的空字典
var emptyDict4 = Dictionary<Int,Int>() // 键和值都是Int类型的空字典
```

### 创建一般字典
```
var dict: Dictionary<String,String> = ["swift":"雨燕,快速","python":"大蟒","java":"爪洼岛","groovy":"绝妙的，时髦的"] // var dict: [String:String] = .. 或者 var dict: Dictionary = .. 
```


### 字典值的获取
由于字典是无序的数据集合，可以通过字典的`key`去获取值。
```
dict["swift"] // 返回一个可选型 Optional("雨燕,快速")
dict["php"] // nil
```






