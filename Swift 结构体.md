# Swift 结构体

声明语法
```
struct 结构体名称 {

}
```
### 声明结构体
```
struct Location { // Location 为数据类型，首字母大写
    var latitude: Double // 纬度
    let longitude: Double // 经度
}

let appleHeadQarterLocation = Location( latitude: 37.3230, longitude: -122.0322)
var googleHeadQarterLocation: Location = Location(latitude: 37.4220, longitude: -122.0841)
```
### 获取属性值
```
appleHeadQarterLocation.latitude
googleHeadQarterLocation.longitude
```

### 结构体的套用
```
struct Place{
    let location: Location
    var name: String
}

var googleHeadQarter = Place( location: googleHeadQarterLocation , name: "google" )

googleHeadQarter.location.latitude // 
```







