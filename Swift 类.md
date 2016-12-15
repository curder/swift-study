## Swift 类

### 定义类
/**
* 类是自定义的数据类型，所以类名首字母需要大写
* 类属性必须赋初始值，或者使用构造函数中赋初始值
**/

class 类名称{
    var 属性: 属性变量类型
    let 属性：属性常量类型
    
    init(){
        
    }
    
    func funcName(<#parameters#>) -> <#return type#> {
        <#function body#>
    }
}



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





























