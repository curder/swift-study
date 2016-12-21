## UILable 文本显示控件

**UILabel 控件**是最基础的显示控件。常见的 label 文本属性控制有： `text` 、`font` 、`textColor`、`backgroundColor` 、`textAlignment` 、`shadowOffset` 、`shadowColor` 、`numberOfLines` 等。使用如下：

```
// 初始化定义 Label 常量，并设置这个label的x、y坐标以及长宽等参数值
let label: UILabel = UILabel(frame: CGRect(x: 20, y: 100, width: 300, height: 100 ))

// 设置 Label 上的文字
label.text = "Hello Swift, This is a Label Study Lession"

// 设置字体大小 （加粗到 20 ）
label.font = UIFont.boldSystemFont(ofSize: 20)

// 设置字体颜色 （红色）
label.textColor = UIColor.red

// 设置背景色
label.backgroundColor = UIColor.gray

// 设置文字对齐方式 （left , center , right）
label.textAlignment = NSTextAlignment.center

// 设置阴影
label.shadowOffset = CGSize(width: 2, height: 3) // 阴影的偏移默认为 1px
label.shadowColor = UIColor.orange

// 设置label 的显示行数 0 为无限行
label.numberOfLines = 0

// 将 Label 放置到视图
self.view.addSubview(label)
```