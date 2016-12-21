# UIImage View 图片控件
在 IOS 中，使用 UIImageView 控件创建图片视图，也可以使用它进行帧动画。

```
 // 初始化一个 ImageView 常量
 let imageView: UIImageView = UIImageView(frame: CGRect(x: 100, y: 100, width: 100, height: 100) )

// 设置图片
imageView.image = UIImage(named: "0.png")
// 设置 ImageView 背景颜色
imageView.backgroundColor = UIColor.black

// 设置 ImageView 动画效果
var imageArr: Array<UIImage?> = []
for i in 0 ... 11{
	let image: UIImage? = UIImage(named: String(i))
	if let image = image{
		imageArr.append(image)
	}
}

// 设置 ImageView 动画数组
imageView.animationImages = imageArr as? [UIImage]
// 设置 ImageView 播放次数
imageView.animationRepeatCount = 0
// 设置播放一轮的时间
imageView.animationDuration = 12
// 开始播放动画
imageView.startAnimating()

self.view.addSubview(imageView)
```