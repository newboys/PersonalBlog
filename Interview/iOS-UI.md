## UIView和CALayer是什么关系?
UIView包含CALayer，每个UIView都有一个自己的主Layer，UIView负责处理交互，CALayer负责内容渲染和显示

### 区别
* UIView可以接受并处理事件，CALayer则不可以
* UIView的父类是UIResponder，CALayer的父类是NSObject
* 每个 UIView 内部都有一个 CALayer 在背后提供内容的绘制和显示，并且 UIView 的尺寸样式都由内部的 Layer 所提供


### 参考
* [详解CALayer 和 UIView的区别和联系](https://www.jianshu.com/p/079e5cf0f014)

### 扩展
* UIResponder

## LoadView的作用

## UITableViewCell使用cell和cell.contentView的区别