# Swift 拓展和泛型

## Swift 拓展 Extension
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



## Swift 泛型 






















