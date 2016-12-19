## Swift 下标和运算符重载

[TOC]

　　以结构体为例，使用 `subscript` 关键字申明。如下
```
struct Vector{
    var x: Double = 0.0
    var y: Double = 0.0
    var z: Double = 0.0
	
    // 下标
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

### 运算符重载
假如有如下自定义结构体为例，进行运算符的重载。
```
struct Vector{
    var x: Double = 0.0
    var y: Double = 0.0
    var z: Double = 0.0
    
    // 下标
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
}

var va = Vector(x: 1.0, y: 2.0, z: 3.0)
var vb = Vector(x: 3.0, y: 4.0, z: 5.0)
```

#### 重载 + 运算符
```
func + (left: Vector , right: Vector) -> Vector{
    return Vector(x: left.x+right.x, y: left.y+right.y
, z: left.z+right.z)
}
va + vb // Vector(x: 4.0, y: 6.0, z: 8.0)
```
> 1. 运算符本质是一个函数；
> 2. 参数 left 与 right 有顺序关系。

#### 重载 - 运算符
```
func - (left: Vector, right: Vector) -> Vector{
    return Vector(x: left.x - right.x, y: left.y - right.y, z: left.z - right.z)
}
vb - va // Vector(x: 2.0, y: 2.0, z: 2.0)
```
#### 重载 * 运算符
```
func * (left: Vector, right: Vector) -> Double {
    return left.x * right.x + left.x * right.y + left.z * right.z
}
va * vb // 22.0
```

#### 再重载 * 运算符

```
func * (left: Vector, a: Double) -> Vector {
    return Vector(x: left.x * a, y: left.y * a, z: left.z * a)
}
va * -1.0 // Vector(x: -1.0, y: -2.0, z: -3.0)
```
> 这次运算符接收的参数是不一样的，所以和上面的运算符没有影响.

#### 复用重载的 * 运算符
```
func * (a: Double , right: Vector) -> Vector{
    return right * a
}
-2.0 * va
```

#### 重载 += 运算符
```
func +=( left: inout Vector , right: Vector){
    left = left + right
}

va += vb
va // Vector(x: 4.0, y: 6.0, z: 8.0)
```

#### 重载 -= 运算符
```
func -= (left: inout Vector, right: Vector){
    left = left - right
}
vb -= va
```

> 对于运算符的重载，我们是不可以重载 = 运算符的。

#### 重载运算符 - 表示对值取反
`prefix` 关键字
```
prefix func - (vector: Vector) -> Vector{
    return Vector(x: -vector.x, y: -vector.y, z: -vector.z)
}

-va // Vector(x: -4.0, y: -6.0, z: -8.0)
```

#### 重载逻辑运算符

```
// 重载 == 逻辑运算符
func == (left: Vector, right: Vector) -> Bool {
    return left.x == right.x && left.x == right.y && left.z == right.z
}
va == vb // false

// 重载 == 逻辑运算符
func != (left: Vector, right: Vector) -> Bool{
//    return left.x != right.x || left.y != right.y || left.z != right.z
    return !(left == right) // 复用重载的 == 运算符 逻辑取反
}
va != vb // true

// 重载 < 运算符
func < (left: Vector, right: Vector) -> Bool {
    if left.x != right.x {return left.x < right.x}
    if left.y != right.y {return left.y < right.y}
    if left.z != right.z {return left.z < right.z}
    
    return false
}

// 重载 <= 运算符
func <= (left: Vector, right: Vector) -> Bool {
    return left < right || left == right
}

// 重载 > 运算符
func > (left: Vector, right: Vector)-> Bool{
    return !(left <= right)
}

// 重载 >= 运算符
func >= (left: Vector, right: Vector) -> Bool{
    return !(left > right)
}
```

### 自定义运算符
#### 定义单目运算符
　　Custom operators can begin with one of the ASCII characters `/`, `=` , `-` , `+` , `!` , `*` , `%` , `<` , `>` , `&` , `|` , `^` , or `~` , or with one of the Unicode characters

```
struct Vector{
    var x: Double = 0.0
    var y: Double = 0.0
    var z: Double = 0.0
    
    // 下标
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
}

var va = Vector(x: 1.0, y: 2.0, z: 3.0)
var vb = Vector(x: 3.0, y: 4.0, z: 5.0)

// 重载 + 运算符
func + (left: Vector , right: Vector) -> Vector{
    return Vector(x: left.x+right.x, y: left.y+right.y
        , z: left.z+right.z)
}
// 重载 += 运算符
func += ( left: inout Vector , right: Vector) {
    left = left + right
}

// 后置 +++ 运算符
postfix operator +++ // 声明一个 swift 不存在的运算符
postfix func +++(vector: inout Vector) -> Vector {
    vector += Vector(x: 1.0, y: 1.0, z: 1.0)
    return vector
}
print(va+++) // Vector(x: 2.0, y: 3.0, z: 4.0)

// 前置 +++ 运算符
prefix operator +++ // 声明一个 swift 不存在的运算符
prefix func +++(vector: inout Vector) -> Vector {
    let ret = vector
    vector += Vector(x: 1.0, y: 1.0, z: 1.0)
    return ret
}
+++va
print(va) // Vector(x: 3.0, y: 4.0, z: 5.0)
```

#### 定义双目运算符

```
struct Vector{
    var x: Double = 0.0
    var y: Double = 0.0
    var z: Double = 0.0
    
    // 下标
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
    
    func length() -> Double {
        return sqrt( self.x * self.x + self.y * self.y + self.z * self.z )
    }
}

var va = Vector(x: 1.0, y: 2.0, z: 3.0)
var vb = Vector(x: 3.0, y: 4.0, z: 5.0)

func * (left: Vector, right: Vector) -> Double {
    return left.x * right.x + left.x * right.y + left.z * right.z
}
```

##### 自定义 ^ 运算符
```
infix operator ^
func ^(left: Vector, right: Vector) -> Double{
    return cos( (left * right) / (left.length() * right.length()) )
}

va ^ vb
```

##### 自定义 ** 运算符求幂运算
```
infix operator ** : ATPrecedence
precedencegroup ATPrecedence {
    associativity: left
    higherThan: AdditionPrecedence
    lowerThan: MultiplicationPrecedence
}
func ** (x: Double, p: Double)-> Double{
    return pow(x,p)
}

2**3**3 // 521

1+2**3**3

5*2**3**2
```

> Apple 的一些运算符信息参考这里： https://developer.apple.com/reference/swift/1851035-swift_standard_library_operators#//apple_ref/doc/uid/TP40016054






