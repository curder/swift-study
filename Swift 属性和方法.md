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

### 类型属性
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

