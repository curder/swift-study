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

// 字典的解包
if let value = dict["swift"] {
    print("swift 的意思是 \(value)") // swift 的意思是 雨燕,快速
}
```

> 字典的无序的。
> 在同一个字典中不允许声明同一个key作为字典的键。

### 字典值的获取
由于字典是无序的数据集合，可以通过字典的`key`去获取值。
```
dict["swift"] // 返回一个可选型 Optional("雨燕,快速")
dict["php"] // nil
```

### 数组的基本查询
```
dict.count // 判断字典的元素个数

dict.isEmpty // 判断字段是否为空

Array(dict.keys) // 返回字典中所有的键，并存储在数组中
Array(dict.values) // 返回字典中所有的值，并存储在数组中
```

### 字典的遍历
```
// 遍历字典的键
for key in dict.keys {
    print(key)
}

// 遍历字典中的值
for value in dict.values {
    print(value)
}

// 遍历字典中的所有键值
for (key, value) in dict {
    print("\(key) : \(value)")
}
```


### 字典是值类型
```
var dir1 = ["key1":"val","key2":"val2"]
var dir2 = dir1

dir2["key1"] = "value1"

dir1 // ["key2": "val2", "key1": "val"]
dir2 // ["key2": "val2", "key1": "value1"]
```



