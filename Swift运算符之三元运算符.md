## Swift运算符之三元运算符


```
question ? answer1 : answer2
```

### Demo
场景：当手机点亮小于 20 的时候，显示 红色，当大于 20 的时候显示绿色
```
import UIKit

var battery = 18
var batterColor: UIColor
if battery <= 20 {
    batterColor = UIColor.red
} else {
    batterColor = UIColor.green
}

batterColor


var batterColor2 = ( battery <= 20 ) ? UIColor.red : UIColor.green
```
