# Swift 协议 Protocol

```
protocol Pet{
    
    // 对于属性，不能有初始值
    var name: String{ get set }// = "My Pet"
    // 统一使用var关键字
    var birthPlace: String{ get }
    // 对于属性，get,set隐藏了实现细节，可以使用let实现只读，也可以使用只有get的计算型属性
    
    
    // 对于方法，不能有实现
    func playWith()
    
    // 对于方法，不能有默认参数（默认参数就是一种实现）
    //func fed(food: String = "leftover")
    func fed()
    func fed(food: String)
    
    // 可以使用mutating关键字，强调这个方法应该修改其内容
    mutating func changeName(newName:String)
    
    // 不可以设置访问控制
    // 协议就是协议，如果开发者可以看见协议，就可以看见协议里的任何内容
}

// 不能实例化Pet
//var pet = Pet()

// 协议的继承
protocol PetBird: Pet{
    
    var flySpeed: Double{ get }
    var flyHeight: Double{ get }
}


// 协议的实现，实现协议规定的所有属性和方法即可
struct Dog: Pet{
    
    // 可以使用计算型属性
    //    private var myDoggyName = "Puppy"
    //    var name: String{
    //        get{
    //            return myDoggyName
    //        }
    //        set{
    //            myDoggyName = newValue
    //        }
    //    }
    var name: String
    
    // protocol的read-only，对一个具体类的实现，不一定只读，但是作为Pet是只读的！
    //let birthPlace: String
    var birthPlace: String
    
    
    func playWith() {
        print("Wong!")
    }
    
    func fed(){
        print("I want a bone.")
    }
    
    // 在具体实现上可以加默认参数
    func fed(food: String = "Bone"){
        
        if food == "Bone"{
            print("Happy")
        }
        else{
            print("I want a bone")
        }
    }
    
    // 对于class，不需要mutating关键字
    mutating func changeName(newName: String) {
        name = newName
    }
}


let myDog:Dog = Dog(name: "summer", birthPlace: "beijing")

// 从 Pet 的角度看，myDog 的 birthPlace 是只读的！
let aPet: Pet = myDog
//aPet.birthPlace = "shanghai"
```

```
protocol Pet{
    var name: String{ get set }

    init(name: String)

    func playWith()
    func fed()
}

class Animal{
    var type: String = "mammal"
}


// 如果一个类有继承的类，则父类必须放在前面
class Dog: Animal, Pet{
    
    // 如果protocol没有init(name)的要求，name有默认名字就够了
    var name: String = "Puppy"
    
    // 如果 protocol 有 init ，则在 class 中必须注明 required
    required init(name: String){
        self.name = name
    }
    
    func playWith() {
        print("Wong")
    }
    
    func fed(){
        print("I love bones")
    }
}


final class Cat: Animal, Pet{
    
    var name: String = "Kitten"
    
    // 如果是final class, init 可以没有 required , 因为也不会再被继承了
    init(name: String){
        self.name = name
    }
    
    func playWith() {
        print("Meow")
    }
    
    func fed(){
        print("I love fish")
    }
}


class Bird: Animal{
    
    var name: String = "Little Little Bird"
    
    init(name: String){
        self.name = name
    }
}


// 如果只是继承 Bird ，Bird 的 init 为 required ，则 override 可以省略
// 否则，必须有 override , 可以没有 required
// 因为有 Pet ，则 required 也不能省
class Parrot: Bird, Pet{
    
    required override init(name: String){
        super.init( name: name + " " + name )
    }
    
    func playWith() {
        print("Hello")
    }
    
    func fed(){
        print("Thank you!")
    }
}
```


















