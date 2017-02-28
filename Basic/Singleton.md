### Singleton

#### Intro
一个单例的类，无论你创建多少次它都只返回一个实例。它提供了对其类的资源的全局访问


#### Code
* Objective-C

```
+ (instancetype)shareInstance {
    static TestClass *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[TestClass alloc]init];
    });
    return sharedInstance;
}

```

* Swift

```
class TheOneAndOnlyKraken {
    static let sharedInstance = TheOneAndOnlyKraken()
    private init() {}
}
```

Apple中的singleton: NSNotificationCenter, UIApplication, and NSUserDefaults

#### 参考资料
* [apple document](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/Singleton.html)
* [print memory address in swift](http://stackoverflow.com/questions/24058906/printing-a-variable-memory-address-in-swift)
