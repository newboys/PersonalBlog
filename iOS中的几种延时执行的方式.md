
## iOS 中几种延时执行的几种方式

在做项目的时候，总会时不时碰到延时执行某个方法的需求，所以在这里总结一下iOS中所有的延时方法。

### 方法1：performSelector

在Apple的文档中。我们可以看到performSelector相关的方法一共有四个:

```
- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay inModes:(NSArray<NSRunLoopMode> *)modes;
- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;
+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget selector:(SEL)aSelector object:(nullable id)anArgument;
+ (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget;
```

#### performSelector:withObject:afterDelay:

[apple document](https://developer.apple.com/documentation/objectivec/nsobject/1416176-performselector?language=objc)

* 该方法会在使用默认mode的当前线程，延时后调用你指定的selector
* `aSelector`这个参数接受方法类型，该方法应该没有返回值且参数只有一个id类型或者无参数，若方法无参数则第二个参数传nil
* 该方法的本质是在当前线程的run loop中设置一个timer来调用需要延时执行的方法，该timer配置在默认的mode（NSDefaultRunLoopMode）中执行，如果run loop不是default mode则timer会一直等等待直到run loop是default mode（详情可参见官方文档）

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

* 当run loop不是default mode时，你可以使用`performSelector:withObject:afterDelay:inModes: `，如果你不确定当前线程是否为主线程时，你可以使用`performSelectorOnMainThread:withObject:waitUntilDone:`或`performSelectorOnMainThread:withObject:waitUntilDone:modes:`去回到主线程来执行你的延时方法
* 可以通过`cancelPreviousPerformRequestsWithTarget:` 或 `cancelPreviousPerformRequestsWithTarget:selector:object: `来取消未执行`performSelector:withObject:afterDelay:`方法
* 如果你想在dispatch queue中执行延时，你应该使用`dispatch_after`和相关的方法去达到你的预期。因为在dispatch queue中不会自动调用

#### `performSelector:withObject:afterDelay:inModes:`

* `modes`这个参数可接受一个可以联合timer去执行selector的字符串数组，该数组至少包含一个字符串，若传nil或者空数组则不会执行你传入的selector

示例：

```
[self performSelector:@selector(yourselfDelayMethod:) withObject:@"mode" afterDelay:2.0 inModes:@[NSDefaultRunLoopMode]];
```

#### ` cancelPreviousPerformRequestsWithTarget:selector:object: `

* 该方法是取消当前target，通过`- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay`注册的某个特定的方法。
* 该方法只是移除当前run loop的方法，不是所有的run loops

示例：

```
[self performSelector:@selector(yourselfDelayMethod:) withObject:@"object" afterDelay:2.0];
[self performSelector:@selector(secondDelayMethod:) withObject:@"second" afterDelay:4.0];
//yourselfDelayMethod方法不会执行
[NSObject cancelPreviousPerformRequestsWithTarget:self selector:@selector(yourselfDelayMethod:) object:@"object"];
```


#### `cancelPreviousPerformRequestsWithTarget:`

* 该方法是取消当前target的所有通过`- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay`所注册的方法。
* 该方法只是移除当前run loop的方法，不是所有的run loops

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

#### 总结

* 为甚在子线程中`performSelector:withObject:afterDelay:`不起作用？

#### 参考

* [iOS 高效开发-----延时执行用GCD](https://www.cnblogs.com/tianlin106/p/4517483.html)
* [NSTimer研究+一点点NSInvocation](http://www.jianshu.com/p/ba91373f7997)
* [performselector-Apple Document](https://developer.apple.com/documentation/objectivec/nsobject/1416176-performselector)
