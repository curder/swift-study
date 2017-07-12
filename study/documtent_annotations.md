## Swift文档注释

Swift文档注释的使用Markdown的语法，具体可以参考这里 [LearnShare/Learning-Markdown](https://github.com/LearnShare/Learning-Markdown/blob/master/README.md)

### 文档注释语法

Swif中文档注释分为多行注释和单行注释。
* 多行注释的语法是：
```
/**
 这里是文档注释的内容区域
 */
```
也就是普通的多行注释多一个`*`号

* 单行文档注释的语法是：
```
///
```
也就是普通的单行注释多一个 `/`

### 文档注释的查看

按住键盘`Option`键，鼠标左击目标变量、常量、类名、方法名、属性值等就可以查看。


### 基本注释

```
/**
这里是文档注释的内容区域0

这是文档注释区域1
 - 无序列表0
 - 无序列表1
 - 无序列表2
 
 1. 有序列表0
 2. 有序列表1
 3. 有序列表2
 \```
 let a = "Hello"
 let b = "Swift"
 \```
 */
class SomeClass {
    
}
/// # Headline 标题1
/// ## Headline 标题2
/// ### Heading 标题3
/// #### Heading 标题4
/// ##### Heading 标题5
/// ###### Heading 标题5
/// Hello,Swift 下面的一行效果是分行
///
/// Hello,IOS App
///
/// 斜体：*this* and _this_.
///
/// 粗体：**Strong font**
///
/// 超链接： [Swift.org](https://swift.org)
///
/// 图片引入： ![Swift Logo](https://camo.githubusercontent.com/de32b354687f1cd9b05a89e4aa03c7f2d311f294/68747470733a2f2f73776966742e6f72672f6173736574732f696d616765732f73776966742e737667)
///
///
func funcName() -> String {
    return ""
}
```

> 以上注释都是放在Swift注释中的Desription中。

### Parameters、Returns和Throws

在基础的文档注释语法中，我们只是将注释写在了Description注释里，但是当我们定义一个函数，它包括响应的参数、返回值等内容。

#### Parameters 参数

对于函数的参数，使用关键字`Parameters`，又会有两种不同的书写方式，它们分别如下：

```
/// - Parameters:
///   - item1: 参数1的注释
///   - item2: 参数2的注释
func funcName(item1: AnyObject?, item2: AnyObject?)-> String{
    return ""
}

/// - Parameter item1: 参数1的注释
/// - Parameter item2: 参数2的注释
func funcName2(item1: AnyObject?, item2: AnyObject?)-> String{
    return ""
}
```

#### Returns 返回值

函数返回值的说明，使用关键字`Returns`

```
/// - Parameter item1: 参数1的注释
/// - Parameter item2: 参数2的注释
/// - Returns: 返回值的说明
func funcName3(item1: AnyObject?, item2: AnyObject?)-> String{
    return ""
}
```

#### Throws 异常

函数在使用的时候可能抛出的异常，使用关键字`Throws`

```
/// - Throws: `异常抛出`的内容
func funcName3(item1: AnyObject?, item2: AnyObject?)-> String{
    retunr ""
}
```

### 算法注释

这些内容是在Description中

*   - Precondition: 前置条件
*   - Postcondition: 后置条件
*   - Requires: 需求条件
*   - Invariant: 循环不变量
*   - Complexity: 复杂度
*   - Important: 重要提示
*   - Warning: 警告信息
*   - Attention: 同Warning
*   - Note: 备注
*   - Remark: 同Note

### 元信息注释

这些内容还是在Description中的

*   - Author: 作者
*   - Authors: 团队
*   - Copyright: 版权
*   - Date: 时间
*   - Since: 起始适配版本
*   - Version: 版本



### Mark

> 注意是两个反斜杠

~~~
// MARK: - 说明
属性

// MARK: - Methods
方法
~~~

### TODO

~~~
// TODO: 说明
~~~

### FIXME

 这个一般用在方法内

~~~
// FIXME: 说明
~~~