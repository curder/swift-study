## Swift 类

### 定义类

类是自定义的数据类型，所以类名首字母需要大写
类属性必须赋初始值，或者使用构造函数中赋初始值

```
class 类名称{
    var 属性: 属性变量类型
    let 属性：属性常量类型
    
    // 构造函数
    init(){
        
    }
    
    // 类方法
    func funcName(<#parameters#>) -> <#return type#> {
        <#function body#>
    }
}
```
定义一个类
```
class Person {
    var firstName: String
    var lastName: String
    init(firstName: String , lastName: String) {
        self.firstName = firstName
        self.lastName = lastName
    }
    
    // 可失败的构造函数 排除 nil 的情况
    init?( fullName: String ){
        guard let spaceIndex = fullName.range(of: " ")?.lowerBound else {
            return nil
        }
        
        self.firstName = fullName.substring(to: spaceIndex)
        self.lastName = fullName.substring(from: fullName.index(after: spaceIndex))
    }
    
    // 定义方法
    func fullName() -> String{
        return self.firstName + " " + self.lastName
    }
}

let person1 = Person(firstName: "Steve", lastName: "Jobs")
let person2 = Person(fullName: "Steve Jobs")
person1.fullName() // Steve Jobs
```


### 类的比较
使用 `===` 判断两个类的实例话对象是否相等，即比较它们是否是指向同一内存地址。

```
class Person {
    let firstName: String
    let lastName: String
    var career: String?
    
    init(firstName: String , lastName: String , career: String){
        self.firstName = firstName
        self.lastName = lastName
        self.career = career
    }
    
    init(firstName: String , lastName: String) {
        self.firstName = firstName
        self.lastName = lastName
    }
    
    // 定义方法
    func fullName() -> String{
        return self.firstName + " " + self.lastName
    }
    
    func changeCareer(newCareer: String) {
        self.career = newCareer
    }
}


let person1 = Person(firstName: "Steve", lastName: "Jobs")
let person2 = person1
person1 === person2 // true

let person3 = Person(firstName: "Steve", lastName: "Jobs")
person1 === person3 // false
```
> 判定两个不同的实例可以使用 `!==` 进行判断。


### 类的继承
```
// 角色类
class Avater{
    var name: String
    var life: Int = 100
    var isAlive: Bool = true
    
    init(name: String){
        self.name = name
    }
    
    func beAttacked(attack: Int) {
        self.life -= attack
        if life <= 0{
            isAlive = false
        }
    }
}

// 用户类 继承自角色类
class User: Avater{
    var score: Int = 0
    var level: Int = 0
    
    func getScore(score: Int) {
        self.score += score
        if self.score > level * 100{
            level += 1
        }
    }
}


let user1 = User(name: "Stive")
user1.name
user1.score
user1.life
user1.isAlive

user1.beAttacked(attack: 10)
user1.life

user1.getScore(score: 10)
user1.getScore(score: 100)
user1.score
user1.level
```
> 如果类不允许子类继承，可以使用 `final` 关键字修饰类。





















### 类是引用类型 Reference Type

　　类不是值类型，而是一个**引用类型**
```
class Person {
    var firstName: String
    var lastName: String
    var career: String?
    
    init(firstName: String , lastName: String , career: String){
        self.firstName = firstName
        self.lastName = lastName
        self.career = career
    }
    
    init(firstName: String , lastName: String) {
        self.firstName = firstName
        self.lastName = lastName
    }
    
    // 定义方法
    func fullName() -> String{
        return self.firstName + " " + self.lastName
    }
}

let person1 = Person(firstName: "Steve", lastName: "Jobs",career: "Developer")

let person2 = person1 // person2 是 person1 的别名，共用内存地址空间

person2.career = "CEO"

person1
person2
```


### Swift 引用类型的特点 Reference Type
```
class Person {
    let firstName: String
    let lastName: String
    var career: String?
    
    init(firstName: String , lastName: String , career: String){
        self.firstName = firstName
        self.lastName = lastName
        self.career = career
    }
    
    init(firstName: String , lastName: String) {
        self.firstName = firstName
        self.lastName = lastName
    }
    
    // 定义方法
    func fullName() -> String{
        return self.firstName + " " + self.lastName
    }
    
    func changeCareer(newCareer: String) {
        self.career = newCareer
    }
}


let person = Person(firstName: "Steve", lastName: "Jobs")

person.career // nil
person.career = "CEO" // 赋值修改类的变量属性
person.career // CEO

// 对于一个类的变量属性，如果他的实例对象是常量，依然可以在外界对它的值做修改。

person.changeCareer(newCareer: "winner")
person.career // winner
```

#### 在结构体中方法改变自身属性的举例
```
struct Location{
    var x = 0
    var y = 0
    
    mutating func goEast(){
        self.x += 1
    }
}
```

#### 在枚举方法中改变自身属性
```
var location = Location()
location.goEast()

enum Swith{
    case On
    case Off
    
    mutating func click() {
        switch self {
        case .On:
            self = .Off
        case .Off:
            self = .On
        }
    }
}

var swith = Swith.On
swith.click() // Off
swith.click() // On
```

