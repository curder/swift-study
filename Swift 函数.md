## Swift 函数

### 函数语法
```
func  函数名 ( 参数变量: 类型 , 参数变量: 类型 ... ) -> 函数返回值 {

}
```
> 说明: 
> 1: func 是定义函数的关键字
> 2：`{}` 函数体
> 3: 参数变量是默认常量类型，不能在函数函数体里面直接修改。即： `func A (value:String)`  与 `func A (let value:String)` 写法是相同的，即 `value` 是常量。


### 使用元组返回多个值

```

func findMaxAndMin( numbers: [Int])->( max: Int, min: Int )? {
    
    guard numbers.count > 0 else {
        return nil
    }
    
    var minValue = numbers[0]
    var maxValue = numbers[0]
    for number in numbers{
        minValue = minValue < number ? minValue : number
        maxValue = maxValue > number ? maxValue : number
    }
    return ( maxValue, minValue )
}

var scores: [Int]? = [202,1232,4321,33,432,666]

scores = scores ?? []

if let resault = findMaxAndMin(numbers: scores!){
    print("The max score is \(resault.max)")
    print("The min score is \(resault.min)")
}
```



























