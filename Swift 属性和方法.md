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

print( rect.center )

rect.center = Point()
```


