# Swift 结构体

## 声明语法
```
struct 结构体名称 {

}
```
## 声明结构体
```
struct Location { // Location 为数据类型，首字母大写
    var latitude: Double // 纬度
    let longitude: Double // 经度
}

let appleHeadQarterLocation = Location( latitude: 37.3230, longitude: -122.0322)
var googleHeadQarterLocation: Location = Location(latitude: 37.4220, longitude: -122.0841)
```
## 获取属性值
```
appleHeadQarterLocation.latitude
googleHeadQarterLocation.longitude
```

## 结构体的嵌套使用
```
struct Place{
    let location: Location
    var name: String
}

var googleHeadQarter = Place( location: googleHeadQarterLocation , name: "google" )

googleHeadQarter.location.latitude // 37.422
```


## 结构体之构造函数
```
struct Location {
    var latitude: Double = 0
    var longitude: Double = 0
}

Location()
let appleHeadQarterLocation = Location( latitude: 37.3230,longitude: -122.0322)
```
>  结构体的初始化时默认将结构体内所有的属性值补齐;
> 结构体默认初始化函数内传递的属性值不是任意的，根据定义的时候的顺序传递
> 对于结构体的属性可以在定义结构体的时候赋初始值，并将其设置为变量，也就是使用 var 关键字声明属性


### 自定义构造函数
```
struct Location {
    let latitude: Double
    let longitude: Double

    // 自定义构造函数
    init (coordinateString: String){
        let commaIndex = coordinateString.range(of: ",")!.lowerBound

        let firstElement = coordinateString.substring(to: commaIndex)
        let secondElement = coordinateString.substring(from: coordinateString.index(after: commaIndex))
        
        self.latitude = Double(firstElement)!
        self.longitude = Double(secondElement)!
    }
}

let location = Location(coordinateString: "37.3230,-122.0322")
```

如上代码中自定义了结构体的构造函数，则不再允许以下面这种方式初始化结构体。

```
let location2 = Location(latitude: 37.3230, longitude:-122.0322)
```

这时我们可以再定义一个构造函数进行结构体的初始化。**同时也建议这样做。**

```
struct Location {
    let latitude: Double
    let longitude: Double
    
    // 自定义构造函数，同时省略参数名,但是为了程序的可读性不建议这么做。
    init (_ coordinateString: String){
        let commaIndex = coordinateString.range(of: ",")!.lowerBound
        
        let firstElement = coordinateString.substring(to: commaIndex)
        let secondElement = coordinateString.substring(from: coordinateString.index(after: commaIndex))
        
        self.latitude = Double(firstElement)!
        self.longitude = Double(secondElement)!
    }
    
    // 自定义构造函数2
    init(latitude: Double, longitude: Double) {
        self.latitude = latitude
        self.longitude = longitude
    }
}


let location = Location("37.3230,-122.0322")
let location2 = Location(latitude: 37.3230, longitude:-122.0322)
```

> 上面的结构体构造函数中使用了可选型的强制解包，这将导致程序的不可预料的错误，这时我们可以使用 guard 关键词进行判定。

### 可失败的构造函数

```
struct Location {
    let latitude: Double
    let longitude: Double
    
    init(){
        self.latitude = 0.0
        self.longitude = 0.0
    }
    
    // 自定义构造函数
    // 可失败的构造函数
    init?(coordinateString: String){
        // 使用 guard 进行程序保卫性判定,防止 nil 值.
        guard let commaIndex = coordinateString.range(of: ",")?.lowerBound,
            let firstElement = Double(coordinateString.substring(to: commaIndex)),
            let secondElement = Double( coordinateString.substring(from: coordinateString.index(after: commaIndex)) )
        else{
            return nil
        }
        
        self.latitude = firstElement
        self.longitude = secondElement
    }
    
    // 自定义构造函数2
    init(latitude: Double, longitude: Double) {
        self.latitude = latitude
        self.longitude = longitude
    }
}


// 所以大多数情况下建议将构造函数的参数与结构体的属性保持一致
let location = Location(coordinateString: "37.3230,-122.0322")
let location2 = Location(coordinateString: "37.3230,-122.0322")!

let location3 = Location(coordinateString: "37.3230&-122.0322")
let location4 = Location(coordinateString: "apple,-122.0322")
let location5 = Location(coordinateString: "37.3230,apple")
let location6 = Location(coordinateString: "Hello, World!")
```


[TOC]
## 在结构体中写方法








