
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

* `- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay inModes:(NSArray<NSRunLoopMode> *)modes;`



* `- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;`

该方法可以执行延时方法，该方法不会阻塞线程但是只能在主线程执行，可以通过`cancelPreviousPerformRequestsWithTarget`方法取消。但该方法需要为延时执行的代码创建单独的方法。
？？？？为什么在子线程不调用
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

* `+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget selector:(SEL)aSelector object:(nullable id)anArgument;`

该方法是取消当前target，通过`- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay`注册的某个特定的方法。

示例：

```
[self performSelector:@selector(yourselfDelayMethod:) withObject:@"object" afterDelay:2.0];
[self performSelector:@selector(secondDelayMethod:) withObject:@"second" afterDelay:4.0];
//yourselfDelayMethod方法不会执行
[NSObject cancelPreviousPerformRequestsWithTarget:self selector:@selector(yourselfDelayMethod:) object:@"object"];
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

#### 方法2 GCD（推荐）

使用GCD的延时方法，无论在主线程子线程都会调用，而且不用为延时代码单独创建一个方法。

[取消GCD的延时方法](https://github.com/Spaceman-Labs/Dispatch-Cancel)

示例：

```
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    NSLog(@"gcd delay");
});
```

#### 方法3 NSTimer

该方法不会阻塞线程，但一般用于定时或倒计时操作，不用于延时。

示例：

```
NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0 target:self selector:@selector(yourselfDelayMethod:) userInfo:nil repeats:NO];
//释放timer
[timer invalidate];
timer = nil;
```

#### 参考

* [iOS 高效开发-----延时执行用GCD](https://www.cnblogs.com/tianlin106/p/4517483.html)
* [NSTimer研究+一点点NSInvocation](http://www.jianshu.com/p/ba91373f7997)
* [performselector-Apple Document](https://developer.apple.com/documentation/objectivec/nsobject/1416176-performselector)
