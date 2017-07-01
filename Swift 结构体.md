# Swift 结构体

## 声明语法
```
struct 结构体名称 {

}
```

> 结构体的定义使用 `struct` 关键字开始，由于结构体也是一种新的数据类型，所以首字母需要大写。

## 声明结构体
```
struct Location { // Location 为数据类型，首字母大写
    var latitude: Double // 纬度
    let longitude: Double // 经度
}

let appHeadQuarterLocation: Location = Location(latitude: 37.3230, longitude: -122.0322) // 定义Apple总部的位置
let googleHeadQuarterLocation: Location = Location(latitude: 37.4220, longitude: -122.0841) // 定义Google总部的位置

appHeadQuarterLocation.latitude // 查看Apple的经度属性值
googleHeadQuarterLocation.longitude // 查看Google的纬度属性值


appHeadQuarterLocation.latitude = 0 // 此处会报错，因为结构体Location所定义的latitude为常量
appHeadQuarterLocation = googleHeadQuarterLocation // 此处也会报错，因为appHeadQuarterLocation定义的是一个常量值

```
## 获取属性值
```
appleHeadQarterLocation.latitude
googleHeadQarterLocation.longitude
```

## 结构体的嵌套使用
结构体的使用时非常灵活的，我们不仅仅可以使用之前学习使用的基本数据类型`Int`、`String`、`Doubel` 等等，还可以在结构体内部嵌套结构体。如下
```
struct Place{
    let location: Location // 该结构体是上文中设置的Location的类型
    var name: String // 字符串类型的属性
}

var googleHeadQarter = Place( location: googleHeadQuarterLocation , name: "google" )

googleHeadQarter.location.latitude // 37.422
```


## 结构体之构造函数
```
struct Location {
    var latitude: Double = 0 // 结构体可以赋初始值
    var longitude: Double = 0
}

Location() // 都不填写的话，就使用初始值
let appleHeadQarterLocation = Location( latitude: 37.3230,longitude: -122.0322)
```
>  结构体的初始化时默认将结构体内所有的属性值补齐;
> 结构体默认初始化函数内传递的属性值不是任意的，根据定义的时候的顺序传递
> 对于结构体的属性可以在定义结构体的时候赋初始值，并将其设置为变量，也就是使用 `var` 关键字声明属性


### 自定义构造函数

使用 `init` 定义函数，不需要写 func，也不需要返回值。

```
struct Location {
    let latitude: Double
    let longitude: Double

    // 自定义构造函数，不需要写 func，也不需要返回值。
    init (coordinateString: String) {
        let commaIndex = coordinateString.range(of: ",")!.lowerBound

        let firstElement = coordinateString.substring(to: commaIndex)
        let secondElement = coordinateString.substring(from: coordinateString.index(after: commaIndex))
        
        self.latitude = Double(firstElement)! // 定义的常量可以在这里初始化
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
let location2 = Location(latitude: 37.3230, longitude: -122.0322)
```

> 上面的结构体构造函数中使用了可选型的强制解包，这将导致程序的不可预料的错误，这时我们可以使用 `guard` 关键词进行判定。


对于结构体而言，结构体中的属性可以赋初始值，也可以在`init`函数中赋值，但是可选性却例外，我们可以在结构体外部对可选型的值进行修改

```
struct Location {
    let latitude: Double
    let longitude: Double
    var placeName: String?
    
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
    
 	// 我们可以写一个全参数的初始化init方法，给可选性赋值
 	init(latitude: Double, longitude: Double, placeName: String?) {
        self.latitude = latitude
        self.longitude = longitude
        self.placeName = placeName
    }
}

let location3 = Location(latitude: 37.3230, longitude: -122.0322, placeName: "Apple Head Quarter")
```



### 可失败的构造函数

使用 `init?` 关键字定义可失败的构造函数，叫做Failable-Initializer。在失败的构造函数中，我们可以大胆的返回`nil`值，而不会构造函数内解包出错等问题使程序抛出错误而终止程序。

```
struct Location {
    let latitude: Double
    let longitude: Double
    
    init(){
        self.latitude = 0.0
        self.longitude = 0.0
    }
    
    // 自定义构造函数1
    // 可失败的构造函数
    init?(coordinateString: String){
        // 使用 guard 进行程序保卫性判定,防止 nil 值.
        guard let commaIndex = coordinateString.range(of: ",")?.lowerBound,
            let firstElement = Double(coordinateString.substring(to: commaIndex)),
            let secondElement = Double( coordinateString.substring(from: coordinateString.index(after: commaIndex)) )
        else{
            return nil // `init?` 可是失败的构造函数支持返回nil
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

### 在结构体中创建多个构造函数

对于结构体，没有便利的构造函数和指定的构造函数之分，如果结构体中的函数需要调用自身的其它构造函数，内部逻辑直接使用`self.init(...)`进行调用。

```
struct Point {
    var x = 0.0
    var y = 0.0
}

struct Size {
    var width = 0.0
    var height = 0.0
}

struct Rectangle {
    var origin = Point()
    var size = Size()
    
    var center: Point {
        get {
            let centerX = origin.x + size.width / 2
            let centerY = origin.y + size.height / 2
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - size.width / 2
            origin.y = newValue.y - size.height / 2
        }
    }
    
    // 构造函数0
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    
    // 构造函数1调用其它构造函数，不需要任何关键字进行修饰，内部直接使用 self.init() 进行调用
    init(center: Point, size: Size) {
        let originX = center.x - size.width / 2
        let originY = center.y - size.height / 2
        self.init(origin: Point(x: originX, y: originY), size: size) // 调用自身的指定构造函数
    }
    
    var area: Double {
        return size.width * size.height
    }
}
```


## 在结构体中写方法

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

    // 定义没有参数也没有返回值的方法
    func printLocation() {
        print("The Location is \(self.latitude),\(self.longitude)")
    }

    // 定义有返回值的方法
    func isNorth() -> Bool {
        return self.latitude > 0
    }
    
    // 方法调用结构体中其他方法
    func isSouth()-> Bool {
        return !self.isNorth()
    }
    
    // 方法接收参数
    func distanceTo(location: Location) -> Double {
        return sqrt(pow(self.latitude , location.latitude) + pow(self.longitude, location.longitude))
    }
}


let appleHeadQuarterLocation = Location(latitude: 37.3230 , longitude: -122.0322)

appleHeadQuarterLocation.printLocation() // The Location is 37.323,-122.0322
appleHeadQuarterLocation.isNorth() // true
appleHeadQuarterLocation.isSouth() // false

let googleHeadQuarterLocation = Location(coordinateString: "37.4220,-122.0841")
appleHeadQuarterLocation.distanceTo(location: googleHeadQuarterLocation!) // nan
```

## 结构体是值类型

`Value Type`值类型，赋值即是拷贝。

```
struct Point {
    var x = 0
    var y = 0
}

var p1 = Point()
var p2 = p1 // 赋值 将 p1 的值拷贝了一份赋值给 p2

p2.x += 1

p2.x // 1

p1.x // 0 原始值并没有改变。
```

> `Array` , `Dirctionary` , `Set` 是结构体；
`Int` , `Float` , `Double` , `Bool` , `String` 也都是结构体，所以他们都是值类型的数据结构。