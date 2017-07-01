## Swift 类

### 定义类

类是自定义的数据类型，所以类名首字母需要大写。
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


#### Swift 引用类型的特点 Reference Type

**类是引用类型（Reference Type）**。下面以引用类型 `Class` 和值类型`Struce`、`Enum`作比较。

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

使用 `mutating` 关键字定义在结构体方法前，说明当前方法需要自己修改自己的属性。

```
struct Location{
    var x = 0
    var y = 0
    
    mutating func goEast(){
        self.x += 1
    }
}
```

#### 在枚举类型方法中改变自身属性

使用 `mutating` 关键字定义在枚举类型的方法前，说明当前方法需要自己修改自己的属性。

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


### 类相等的比较

在Swift中，默认情况下`==`不能直接应用在类的实例化对象相等的比较上（`==`比较的本质是**值的比较**，只可以对两个值类型作比较）。 

使用 `===` 判断两个类（引用类型）的实例话对象是否相等，即比较它们是否是指向同一内存地址。

```
class Person {
    let firstName: String
    let lastName: String
    var career: String? // 职业，字符串的可选性
    
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
person1 === person2 // true 引用同一个内存空间

// 重新实例化一个相同内容的数据后，发现对象不相等
let person3 = Person(firstName: "Steve", lastName: "Jobs")
person1 === person3 // false 两次实例化，计算机分配了两个内存空间存储不同的对象

person1 !== person3 // true
```
> 判定两个不同的实例可以使用 `!==` 进行判断。


### 类的继承

在Swift中，类可以继承，而结构体不可以，当我们发现在业务逻辑中需要使用继承，那么应该选择类这种数据类型。

```
// 游戏角色类
class Avatar{
    var name: String // 角色名
    var life: Int = 100 // 血量
    var isAlive: Bool = true // 是否还活着
    
    init(name: String) {
        self.name = name
    }
    
    // 角色受攻击逻辑
    func beAttacked(attack: Int) {
        self.life -= attack
        if life <= 0 {
            isAlive = false
        }
    }
}

// 玩家继承自角色类
class User: Avatar {
    var score: Int = 0 // 玩家得分
    var level: Int = 0 // 玩家等级
    
    func getScore(score: Int) {
        self.score += score
        if self.score > level * 100{
            level += 1
        }
    }
}


let user1 = User(name: "Stive") // 从父类继承的构造函数
user1.name // 读取父类属性
user1.score
user1.life
user1.isAlive

user1.beAttacked(attack: 10) // 读取父类方法
user1.life

user1.getScore(score: 10)
user1.getScore(score: 100)
user1.score
user1.level


// 魔术师类
class Magician: User {
    var magic: Int = 100
}

let magician = Magician(name: "harry potter") // 调用父类的父类的构造函数

// 调用父类或者父类的父类的属性
magician.name
magician.life
magician.isAlive
magician.score
magician.level
magician.magic
```

类与类的继承不仅仅可以子类继承父类，可以一层层不断的继承下去。

> 如果类不允许子类继承，可以使用 `final` 关键字修饰类。


### 类的多态

举例在游戏中的角色之间的关系，使用多态对角色进行批量操作。

```
// 游戏角色类
class Avatar{
    var name: String // 角色名
    var life: Int = 100 { // 属性观察器
        didSet {
            if self.life <= 0 {
                self.isAlive = false
            }
            if self.life > 100 {
                self.life = 100
            }
        }
    } // 血量

    var isAlive: Bool = true // 是否还活着
    
    init(name: String) {
        self.name = name
    }
    
    // 角色受攻击逻辑
    func beAttacked(attack: Int) {
        self.life -= attack
        if life <= 0 {
            isAlive = false
        }
    }
}

// 玩家继承自角色类
class User: Avatar {
    var score: Int = 0 // 玩家得分
    var level: Int = 0 // 玩家等级
    
    func getScore(score: Int) {
        self.score += score
        if self.score > level * 100{
            level += 1
        }
    }
}

// 魔术师类
final class Magician: User {
    var magic: Int = 100
    
    // 治疗
    func heal(user: User){
        user.life += 10
    }
}

//战士类
final class Warrior: User {
    var weapon: String? // 武器属性
}

// 怪兽
class Monster: Avatar {
    func attack(user: User, amount: Int) {
        user.beAttacked(attack: amount)
    }
}

// 僵尸
final class Zombie: Monster {
    var type: String = "Default"
}

let player1 = Magician(name: "Harry Potter") // 魔法师角色对象
let player2 = Warrior(name: "Stive") // 战士角色对象

let zombie = Zombie(name: "Default Zombie") // 僵尸角色对象
let monster = Monster(name: "Monster") // 怪兽角色对象

func printBasicInfo(avatar: Avatar) { // 打印对象的基本信息
    print("The avatar's name is \(avatar.name)")
    print("The life is \(avatar.life). He is \((avatar.isAlive) ? "still alive" : "dead")")
    print("")
}


printBasicInfo(avatar: player1)
printBasicInfo(avatar: player2)
printBasicInfo(avatar: zombie)
printBasicInfo(avatar: monster)

// 批量操作Avatar对象
let avatarArr: [Avatar] = [player1, player2, zombie, monster]

// 全部受到10攻击
for avatar in avatarArr {
    avatar.beAttacked(attack: 10)
}


printBasicInfo(avatar: player1)
printBasicInfo(avatar: player2)
printBasicInfo(avatar: zombie)
printBasicInfo(avatar: monster)

player1.heal(user: player2) // 魔法师给用户治疗
```

### 类的重载

当继承的过程中，我们想在子类中重写父类的属性或者方法时，需要使用 `override` 关键字重写父类的方法或者属性。

当父类中的属性或者方法是 `final` 时候，那么这时这个方法是不可以覆盖的。

```

// 游戏角色类
class Avatar{
    var name: String // 角色名
    var life: Int = 100 {
        didSet {
            if self.life <= 0 {
                self.isAlive = false
            }
            if self.life > 100 {
                self.life = 100
            }
        }
    }// 血量
    var isAlive: Bool = true // 是否还活着
    var description: String { // 存储型属性
        return "I'm avatar \(name)."
    }
    
    init(name: String) {
        self.name = name
    }
    
    // 角色受攻击逻辑
    func beAttacked(attack: Int) {
        self.life -= attack
        if life <= 0 {
            isAlive = false
        }
    }
}

// 玩家继承自角色类
class User: Avatar {
    var score: Int = 0 // 玩家得分
    var level: Int = 0 // 玩家等级
    override var description: String { // 子类重新定义属性覆盖父类属性
        return "I'm user \(name)."
    }
    
    func getScore(score: Int) {
        self.score += score
        if self.score > level * 100{
            level += 1
        }
    }
}

// 魔术师类
final class Magician: User {
    var magic: Int = 100
    override var description: String { // 子类重新定义属性覆盖父类属性
        return "I'm magician \(name)."
    }
    
    // 治疗
    func heal(user: User){
        user.life += 10
    }
}

//战士类
final class Warrior: User {
    var weapon: String? // 武器属性
    override var description: String { // 子类重新定义属性覆盖父类属性
        return "I'm warrior \(name)."
    }
    
    override func beAttacked(attack: Int) { // 子类重载了父类的方法
        self.life -= attack/2
    }
}

// 怪兽
class Monster: Avatar {
    override var description: String { // 子类重新定义属性覆盖父类属性
        return "I'm monster \(name)."
    }
    func attack(user: User, amount: Int) {
        user.beAttacked(attack: amount)
    }
}

// 僵尸
final class Zombie: Monster {
    var type: String = "Default"
    override var description: String { // 子类重新定义属性覆盖父类属性
        return "I'm zombie \(name)."
    }
}

let player1 = Magician(name: "Harry Potter") // 魔法师角色对象
let player2 = Warrior(name: "Stive") // 战士角色对象

let zombie = Zombie(name: "Default Zombie") // 僵尸角色对象
let monster = Monster(name: "Monster") // 怪兽角色对象

print(player1.description)
print(player2.description)
print(zombie.description)
print(monster.description)

let avatarArr: [Avatar] = [player1, player2, zombie, monster]

for avatar in avatarArr {
    print(avatar.description)
}

// 调用不同类实例化对象的方法
monster.attack(user: player1, amount: 20)
player1.life

monster.attack(user: player2, amount: 20)
player2.life
```


