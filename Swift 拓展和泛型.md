# Swift 拓展和泛型

## Swift 拓展 Extension

### 扩展计算型属性和便利构造函数
```
struct Point{
    var x = 0.0
    var y = 0.0
}

struct Size{
    var width = 0.0
    var height = 0.0
}


class Rectangle{
    var origin  = Point()
    var size = Size()
    
    init (origin: Point, size: Size){
        self.origin = origin
        self.size = size
    }
}

// 拓展 Rectangle
extension Rectangle{
    func translate(x: Double,y: Double){
        self.origin.x += x
        self.origin.y += y
    }
}

let rect = Rectangle(origin: Point(), size: Size(width: 4, height: 5))
rect.translate(x: 10, y: 10)

rect

// 扩展计算型属性和扩展便利构造函数
extension Rectangle{
//    var center: Point = Point() // 不允许扩展存储型属性
    var center: Point {
        get{
            let centerX = origin.x + size.width/2
            let centerY = origin.y + size.height/2
            return Point(x: centerX, y: centerY)
        }
        set{
            origin.x = newValue.x - size.width/2
            origin.y = newValue.y - size.height/2
        }
    }

    // 扩展构造函数 - 扩展中加入构造函数必须是一个便利的 convenience 构造函数，使用 self.init() 的方式引用指定的构造函数
    convenience init(center: Point, size: Size){
        let originX = center.x - size.width/2
        let originY = center.y - size.height/2
        
        self.init(origin: Point(x: originX, y: originY),size: size)
    }
}
```
### 扩展嵌套枚举
```
class UI{
    
    enum Theme{
        case DayMode
        case NightMode
    }
    
    var fontColor: UIColor!
    var backgroundColor: UIColor!
    var themeMode: Theme = .DayMode{
        didSet{
            self.changeTheme(themeMode: self.themeMode)
        }
    }
    
    init(){
        self.themeMode = .DayMode
        self.changeTheme(themeMode: self.themeMode)
        
    }
    
    
    init(themeMode: Theme){
        self.themeMode = themeMode
        self.changeTheme(themeMode: themeMode)
    }
    
    func changeTheme( themeMode: Theme ){
        switch(themeMode){
        case .DayMode:
            fontColor = UIColor.black
            backgroundColor = UIColor.white
        case .NightMode:
            fontColor = UIColor.white
            backgroundColor = UIColor.black
        }
    }
}


let ui = UI()
ui.themeMode
ui.fontColor
ui.backgroundColor

ui.themeMode = UI.Theme.NightMode
ui.themeMode
ui.fontColor
ui.backgroundColor
```

### 使用 extension 扩展系统类库

```
extension Int{
    // 计算平方
    var square: Int{
        return self * self
    }
    
    // 计算立方
    var cube: Int{
        return self * self * self
    }
    
    // 扩展方法 判断整型是否在前闭后开的范围内
    func inRange(closedLeft left: Int, opendRight right: Int) -> Bool {
        return self >= left && self < right
    }
    
    // 扩展方法
    func repetitions( task: () -> Void ){
        for _ in 0 ..< self {
            task()
        }
    }
    
}

let num = 8
num.square // 64
num.cube // 512

let index = 10
index.inRange(closedLeft: 0, opendRight: 20) // 判断 index 是否在 0 ..< 20
```

## Swift 泛型 Generic

泛型：是指有一套通用的逻辑，不与类型相关。例如交换两个参数的值。
```
func swapTwoInt( _ a: inout Int , _ b: inout Int){
    (a,b) = (b,a)
}

var a: Int = 0
var b: Int = 6
swapTwoInt(&a, &b)
a
b

func swapTwoDouble(_ a: inout Double , _ b: inout Double){
    (a,b) = (b,a)
}
```
> 以上函数不管是交换整型还是交换浮点型，都是给两个遍历交换相互的值。那我们可以通过泛型对这种需求做改进。

```
// generic function
func swapTwoThings<T>(_ a: inout T , _ b: inout T){
    (a,b) = (b,a)
}

var hello = "Hello"
var bye = "Bye"
swapTwoThings(&hello, &bye)
hello
bye

swapTwoThings(&a, &b)
a
b

swap(&a, &b) // Swift 中的一个泛型函数
```
> 使用 泛型 可以创建更加通用的函数。


### 泛型类型
















