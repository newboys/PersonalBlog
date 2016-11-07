# LearniOS

## Animation

### CALayer

 1、不处理用户的交互
 
 2、UIView没有暴露的CALayer的功能
 
* 阴影、圆角、带颜色的边框
* 3D变化
* 非矩形范围
* 透明套罩
* 多级非线性动画

3、寄宿图(图层中包含的图)

* contents
* contentMode(view)
* contentsGravity(layer):内容在图层边界中怎么对齐
* contentsScale
* contentsRect
* contentsCenter

Tips:

* 如果你不需要寄宿图，那就不要创建这个方法了，这会造成CPU资源和内存的浪费，这也是为什么苹果建议：如果没有自定义绘制的任务就不要在子类中写一个空的-drawRect:方法.
* 当使用寄宿了视图的图层的时候，你也不必实现-displayLayer:和-drawLayer:inContext:方法来绘制你的寄宿图。通常做法是实现UIView的-drawRect:方法，UIView就会帮你做完剩下的工作，包括在需要重绘的时候调用-display方法.

