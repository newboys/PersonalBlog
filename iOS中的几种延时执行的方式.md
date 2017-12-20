
### iOS 中几种延时执行的几种方式

在做项目的时候，总会时不时碰到延时执行某个方法的需求，所以在这里总结一下iOS中所有的延时方法。

#### 方法1：performSelector

在Apple的文档中。我们可以看到performSelector相关的方法一共有四个:

```
- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay inModes:(NSArray<NSRunLoopMode> *)modes;
- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;
+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget selector:(SEL)aSelector object:(nullable id)anArgument;
+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget;
```

* `- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;`

该方法可以执行延时方法，该方法不会阻塞主线程，可以通过`cancelPreviousPerformRequestsWithTarget`方法取消。

示例:

```
//aSelector：需要延时执行的方法
//anArgument：需要传递的参数，如无需参数则写nil
//delay：延时几秒
//无参数
[self performSelector:@selector(yourselfDelayMethod) withObject:nil afterDelay:2.0];
//有参数
[self performSelector:@selector(yourselfDelayMethod:) withObject:@"object" afterDelay:2.0];
```

* `+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget;`

该方法是取消当前target的所有当前通过`- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay`所注册的方法。

示例：

```
[self performSelector:@selector(yourselfDelayMethod:) withObject:@"object" afterDelay:2.0];
[self performSelector:@selector(secondDelayMethod:) withObject:@"second" afterDelay:4.0];
//上面两个延时方法都不会执行
[NSObject cancelPreviousPerformRequestsWithTarget:self];
```
