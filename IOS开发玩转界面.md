## IOS开发玩转界面

UI 是 IOS 中 IOS开发的基础功，熟练的掌握UIKit框架的引用，学习 IOS 开发就完成了一半。下面总结 UIKit 框架中所有系统控件，学习自定义控件的封装和搭建。

UILable 文本显示控件

UIButton 简单的交互控件

UIImageView 图片显示控件

UISearch 搜索控件

UISwitch 开关控件

UISegmentControl 分段控制器

UITextField 小巧的输入框

UISider 滑块控件

UIActivityIndicatorView 提示器控件

UIprogressView 进度条控件

UIPageControl 分页控制器

UIStepper 步进控制器

UIAlertController 警告框 / 抽屉

### 设置组建的 layer 属性
```
let imageView: UIImageView = UIImageView(frame: CGRect(x: 100, y: 100, width: 100, height: 100) )

imageView.backgroundColor = UIColor.red

// 设置圆角
imageView.layer.masksToBounds = true

// 设置圆角半径
imageView.layer.cornerRadius = 50

// 设置边框属性
imageView.layer.borderColor = UIColor.green.cgColor
imageView.layer.borderWidth = 2

// 设置阴影
imageView.layer.shadowColor = UIColor.purple.cgColor
imageView.layer.shadowOffset = CGSize(width: 10, height: 10)
imageView.layer.shadowOpacity = 1


self.view.addSubview(imageView)
```
