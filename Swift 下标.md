## Swift 下标

　　以结构体为例，使用 `subscript` 关键字申明。如下
```
struct Vector{
    var x: Double = 0.0
    var y: Double = 0.0
    var z: Double = 0.0

    subscript(index: Int) -> Double? {
        get{
            switch index{
            case 0: return x
            case 1: return y
            case 2: return z
            default: return nil
            }
        }

        set{
            guard let newValue = newValue else{
                return
            }

            switch index{
            case 0: x = newValue
            case 1: y = newValue
            case 2: z = newValue
            default: return
            }
            
        }
    }

    subscript (axis: String) -> Double? {
        // 不写 默认是 getter
        switch axis {
        case "x","X" : return x
        case "y","Y": return y
        case "z","Z": return z
        default: return nil
        }
    }
}

var v = Vector(x: 1.1, y: 2.2 , z: 3.3)

v.y // 2.2
v[2] // 3.3

v["x"] // 1.1
v["T"] // nil

// 使用下标对结构体属性赋值
v[1] = 9.09
v.y // 9.09
```
