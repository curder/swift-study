## Swift 属性和方法

在Swift中，构建结构体或者类属性和方法中，它们分为：存储型属性、计算型属性和静态属性。

### 计算型属性

```
struct Point {
    var x = 0.0 // 存储型属性
    var y = 0.0
}

struct Size {
    var width = 0.0 // 存储型属性
    var height = 0.0
}


class Rectangle {
    var origin = Point() // 存储型属性
    var size = Size()

    // 计算性属性,必须声明称变量，因为它的值是根据其他属性的值计算得出。
    // 另外，计算型属性必须声明数据类型，否则将会报错 (error: computed property must have an explicit type)
    var center: Point {
        // getter
        get {
            let centerX = origin.x + size.width / 2
            let centerY = origin.y + size.height / 2
            return Point(x: centerX , y: centerY)
        }
        // setter
        set {
            origin.x = newValue.x - size.width / 2 // newValue 是要传递给center计算性属性的新值
            origin.y = newValue.y - size.height / 2
        }
    }
    
    // 计算性属性，只有 getter 即只读属性（无setter）。
    var area: Double {
        return size.width * size.height
    }
    
    init (origin: Point , size: Size){
        self.origin = origin
        self.size = size
    }
}


var rect = Rectangle( origin: Point(), size: Size(width: 10 , height: 5) )

rect.center

rect.origin = Point(x: 10 , y: 10)

print( rect.center ) // 改变计算型属性值

rect.center = Point()
rect
```

### 静态属性

使用 `static` 关键字声明静态属性，该属性定义在类型属性上的Type Property。

```
class Player {
    var name: String // 存储型属性
    var score: UInt32 = 0
    static var highestScore: UInt32 = 0 // 使用关键字static声明静态属性，存储最高分
    
    init(name: String) { // 构造函数中给存储型属性赋值
        self.name = name
    }
    
    func play() {
        
        let score = arc4random() % 100
        print("\(self.name) played and got \(score) scores.")
        
        self.score += score
        
        print("Total score of \(self.name) is \(self.score)")
        
        if self.score > Player.highestScore { // 使用类自身调用静态变量，而不是使用self调用自己的静态属性并且也不能省略Player的书写
            Player.highestScore = self.score
        }
        print("Highest scores is \(Player.highestScore)")
    }
}

let player1 = Player(name: "Player1")
let player2 = Player(name: "Player2")

player1.play() // 玩一局得分
player1.play() // 玩第二局得分

player2.play()
player2.play()
player2.play()
```

### 类型方法 静态方法
```
// 类型方法
struct Matrix{
    var m: [[Int]]
    var row: Int
    var col: Int
    
    init?(_ arr2d: [[Int]]){
        guard arr2d.count > 0 else{
            return nil
        }
        let row = arr2d.count
        let col = arr2d[0].count
        for i in 1..<row{
            if arr2d[i].count != col{
                return nil
            }
        }
        self.m = arr2d
        self.row = row
        self.col = col
    }
    
    func printMatrix() {
        for i in 0 ..< row {
            for j in 0 ..< col {
                print(m[i][j],terminator:"\t")
            }
            print()
        }
    }
    
    static func identityMatrix(n: Int) -> Matrix? { // 静态方法
        if n <= 0 {
            return nil
        }
        
        var arr2d:[[Int]] = []
        for i in 0 ..< n {
            var row = [Int](repeating: 0, count: n)
            row[i] = 1
            arr2d.append(row)
        }
        return Matrix(arr2d)!
    }
}

if let m = Matrix([[1,2,],[3,4]]){
    m.printMatrix()
}

if let e = Matrix.identityMatrix(n: 8) {
    e.printMatrix()
}
```

### 属性观察器

如果外部修改了类中的成员属性操作类的 static 静态属性大小，可以通过关键字限制。可以通过关键字 `didSet`、`willSet` 进行逻辑判断。

```
class LightBulb{
    static let macCurrent = 30
    var current = 0 {
        willSet { // 在对象中赋值 current 之前，{} 中的逻辑代码将执行
            print("Current value changed. The Change is \(abs(current - newValue))")
        }
        
        didSet{ // 在对象中赋值 current 完成，{} 中的逻辑代码将执行
            
            if self.current == LightBulb.macCurrent {
                print("Pay attention, the current value get to the maximum point.")
            }else if self.current > LightBulb.macCurrent{
                print("Current too height , falling back to previous setting.")
                self.current = oldValue
            }
            
            
            print("The current is \(self.current)")
        }
    }
    
}

let bulb = LightBulb()
bulb.current = 20
bulb.current = 30
bulb.current = 40
```

> 注意： `didSet` 和 `willSet` 不会在初始化阶段调用。

如下Demo：

```
enum Theme {
    case DayMode
    case NightMode
}

class UI{
    var fontColor: UIColor!
    var backgroundColor: UIColor!
    var themeMode: Theme = .DayMode {
        didSet{
            switch themeMode {
            case .DayMode:
                fontColor = UIColor.black
                backgroundColor = UIColor.white
            case.NightMode:
                fontColor = UIColor.white
                backgroundColor = UIColor.black
            }
        }
    }
    
    init(themeMode: Theme) {
        self.themeMode = themeMode
    }
    
}

let ui = UI(themeMode: Theme.DayMode)

ui.themeMode
ui.fontColor // nil
ui.backgroundColor // nil
```

我们查看到 `ui.fontColor` 和 `ui.backgroundColor` 的值为 `nil` 。说明在执行初始化的时候并没有调用 `didSet` ，应该进行如下代码改进。


```
enum Theme {
    case DayMode
    case NightMode
}

class UI{
    var fontColor: UIColor!
    var backgroundColor: UIColor!
    var themeMode: Theme = .DayMode {
        didSet{
            self.chengeTheme(themeMode: themeMode)
        }
    }
    
    init(themeMode: Theme) {
        self.themeMode = themeMode
        self.chengeTheme(themeMode: themeMode)
    }
    
    func chengeTheme(themeMode: Theme) {
        switch themeMode {
        case .DayMode:
            fontColor = UIColor.black
            backgroundColor = UIColor.white
        case.NightMode:
            fontColor = UIColor.white
            backgroundColor = UIColor.black
        }
    }
}

let ui = UI(themeMode: Theme.DayMode)

ui.themeMode
ui.fontColor // nil
ui.backgroundColor // nil
```

### 惰性加载（延迟加载）

```
class ClosedRange{
    let start: Int
    let end: Int

    var width: Int{
        return end - start + 1
    }
    
    lazy var sum: Int = { // 延迟性属性
        var res = 0
        for i in self.start ... self.end{
            res += i
        }
        return res
    }()
    
    
    init?( start: Int , end: Int ) {
        if start > end {
            return nil
        }
        
        self.start = start
        self.end = end
    }
}

if let range = ClosedRange(start: 0, end: 10_000){
    range.width
    range.sum
    range.sum
    range.sum
    
}
```

> `lazy` 关键字不允许使用在常量属性上。

#### 惰性加载的一些其他场景

```
// 根据经纬度计算地理位置
class Location{
    let latitude: Double
    let longitude: Double
    lazy var address: String? = {
        return nil
    }()
    
    init(latitude: Double , longitude: Double){
        self.latitude = latitude
        self.longitude = longitude
    }
}

// 图书、电影、音乐相关App
class Book{
    let name: String
    lazy var content: String? = {
        // 从本地读取书的内容
        return nil
    }()
    init(name: String){
        self.name = name
    }
}

// Web请求
class Web{
    let url: String
    lazy var html: String? = {
        // 从网络读取url对应的html
        return nil
    }()
    
    init(url: String){
        self.url = url
    }
}
```

### 访问控制

Swift 的访问控制是通过**文件**为单位控制的。其中：

 * public 可以被模块外访问
 
 * internal 可以被本模块访问
 
 * private 可以被本文件访问，当我们不显式指定的时候，所有的类、属性或者方法的访问权限都是 **internal** 。

例如：`Sources` 目录下  `ui.swift` 文件内容如下：

```
enum Theme {
    case DayMode
    case NightMode
}

class UI{
    private var fontColor: UIColor!
    private var backgroundColor: UIColor!
    var themeMode: Theme = .DayMode {
        didSet{
            self.chengeTheme(themeMode: themeMode)
        }
    }
    
    init(){
        self.themeMode = .DayMode
        self.chengeTheme(themeMode: self.themeMode)
    }
    
    init(themeMode: Theme) {
        self.themeMode = themeMode
        self.chengeTheme(themeMode: themeMode)
    }
    
    private func chengeTheme(themeMode: Theme) {
        switch themeMode {
        case .DayMode:
            fontColor = UIColor.black
            backgroundColor = UIColor.white
        case .NightMode:
            fontColor = UIColor.white
            backgroundColor = UIColor.black
        }
    }
    
    func show() {
        print("The font color is \(self.fontColor == UIColor.white ? "BLACK" : "WHITE")")
        print("The background color is \(self.backgroundColor == UIColor.black ? "WHITE" : "BLACK")")
    }
}
```

`Sources` 目录下 `app.swift` 文件 内容如下：

```
import Foundation

public class App{
    private let ui = UI()
    public var name: String
    
    public init(name: String){
        self.name = name
    }
    
    public func switchMode(){
        switch ui.themeMode {
        case Theme.DayMode:
            ui.themeMode = Theme.NightMode
        case Theme.NightMode:
            ui.themeMode = Theme.DayMode
        }
    }
    
    public func show() {
        print("The App name is \(self.name)")
        ui.show()
    }
}
```


### 单例模式

有两个文件，`gameManager.swift` 是一个单利类。

```
import Foundation
public class GameManager{
    public var score = 0
    public static let defaltGameManager = GameManager()
    
    private init(){
        
    }
    
    public func addScore(){
        self.score += 10
    }
}
```

> 注意： 初始化函数设置为 `private` ，`defaultGameManager` 设置为静态常量。

```
import UIKit

let gameManager = GameManager.defaltGameManager

gameManager.addScore()
gameManager.score // 10

let gm = GameManager.defaltGameManager

gm.addScore()

gm.score // 20
```