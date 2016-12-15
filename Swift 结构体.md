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
        
        latitude = Double(firstElement)!
        longitude = Double(secondElement)!
    }
}

//Location(coordinateString: "1,1")
let location = Location(coordinateString: "37.3230,-122.0322")

// 如上代码中自定义了结构体的构造函数，则不再允许以这种方式初始化结构体
//let location2 = Location(latitude: 37.3230, longitude:-122.0322)
```



