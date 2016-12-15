## Swift 属性和方法
### 计算型属性

```
struct Point {
    var x = 0.0
    var y = 0.0
}

struct Size {
    var width = 0.0
    var height = 0.0
}

class Rectangle {
    var origin = Point()
    var size = Size()
    var center: Point{
        // getter
        get{
            let centerX = origin.x + size.width/2
            let centerY = origin.y + size.height/2
            return Point(x: centerX , y: centerY)
        }
        // setter
        set{
            origin.x = newValue.x - size.width / 2
            origin.y = newValue.y - size.height / 2
        }
    }
    
    var area: Double{
        return size.width * size.height
    }
    
    init (origin: Point , size: Size){
        self.origin = origin
        self.size = size
    }
}


var rect = Rectangle( origin: Point(), size: Size(width: 10 , height: 5) )

rect.origin = Point(x: 10 , y: 10)

print( rect.center ) // 改变计算型属性值

rect.center = Point()
```

### 类型属性 静态属性
```
class Player {
    var name: String
    var score: UInt32 = 0
    static var highestScore: UInt32 = 0 // 静态属性
    
    init(name: String){
        self.name = name
    }

    func play() {
        let score = arc4random() % 100
        print("\(self.name) played and got \(score) scores.")
        
        self.score += score
        
        print("Total score of \(self.name) is \(self.score)")
        
        if self.score > Player.highestScore{
            Player.highestScore = self.score
        }
        print("Highest scores is \(Player.highestScore)")
    }
}

let player1 = Player(name: "Player1")
let player2 = Player(name: "Player2")

player1.play()
player1.play()

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








