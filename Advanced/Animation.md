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

4、图层几何学

* zPosition

我们希望在真实的应用中也能显示出绘图的顺序，同样地，如果我们提高绿色视图的zPosition（清单3.3），我们会发现顺序就反了（图3.9）。其实并不需要增加太多，视图都非常地薄，所以给zPosition提高一个像素就可以让绿色视图前置，当然0.1或者0.0001也能够做到，但是最好不要这样，因为浮点类型四舍五入的计算可能会造成一些不便的麻烦

* CALayer并不关心任何响应链事件，所以不能直接处理触摸事件或者手势。但是它有一系列的方法帮你处理事件：`-containsPoint:`和`-hitTest:`
* `borderWidth/borderColor`

---shadow --- shadow---shadow


5、视觉效果

Tips:

* 如果你不需要寄宿图，那就不要创建这个方法了，这会造成CPU资源和内存的浪费，这也是为什么苹果建议：如果没有自定义绘制的任务就不要在子类中写一个空的-drawRect:方法.
* 当使用寄宿了视图的图层的时候，你也不必实现-displayLayer:和-drawLayer:inContext:方法来绘制你的寄宿图。通常做法是实现UIView的-drawRect:方法，UIView就会帮你做完剩下的工作，包括在需要重绘的时候调用-display方法.

