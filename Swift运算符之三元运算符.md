## Swift运算符之三元运算符


```
question ? answer1 : answer2
```

### Demo
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
