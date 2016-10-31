# property

代码示例：
```
@property UIButton *btn1;
@property (atomic, readwrite, strong) UIButton *btn1;
```

上面两句话是等价的。

* readwrite(该值为o默认值)
读写：该词修饰的property拥有set和get方法

* readonly
只读：该词修饰的property只拥有get方法

* nonatomic
非原子性：

* atomic(该值为m默认值)
原子性：

* strong(该值为默认值)
强引用：

* weak

* assign

* copy

* retain

* synthesize
自动合成set/get方法，此方法配合property。如果你直接用`.`语法来访问这个属性的话，你是没必要写synthesize的，因为点语法实质上就是实现了set/get方法。
代码示例：
```
#import "ViewController.h"

@interface ViewController ()
@property (nonatomic, copy) NSString *string;
@end

@implementation ViewController
@synthesize string;

- (void)viewDidLoad {
    [super viewDidLoad];
    string = @"synthesize";
    NSLog(@"%@",string);
}

@end
```

* 点语法
代码示例:
```
#import "ViewController.h"

@interface ViewController ()
@property (nonatomic, copy) NSString *string;
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    //此句相当于调用了set方法
    self.string = @"synthesize";
    //此句相当于调用了get方法
    NSLog(@"%@",self.string);
}

@end
```

* dynamic
代码示例:
```
#import "ViewController.h"
#import <objc/runtime.h>
@interface ViewController ()
@property (nonatomic, copy) NSString *string;
@end

@implementation ViewController
@dynamic string;

- (void)viewDidLoad {
    [super viewDidLoad];
    //此句相当于调用set方法
    self.string = @"synthesize";
    //此句相当于调用了get方法
    NSLog(@"%@",self.string);
}

-(void)setString:(NSString *)string{
    objc_setAssociatedObject(self, @selector(string), string, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}

-(NSString *)string{
    return objc_getAssociatedObject(self, @selector(string));
}
```

该词表示对于string系统不会自动生成set/get方法，需要你自己写set/get方法。

`@dynamic 告诉编译器：属性的 setter 与 getter 方法由用户自己实现，不自动生成。（当然对于 readonly 的属性只需提供 getter 即可）。假如一个属性被声明为 @dynamic var，然后你没有提供 @setter方法和 @getter 方法，编译的时候没问题，但是当程序运行到 instance.var = someVar，由于缺 setter 方法会导致程序崩溃；或者当运行到 someVar = var 时，由于缺 getter 方法同样会导致崩溃。编译时没问题，运行时才执行相应的方法，这就是所谓的动态绑定`

参考：
* [《招聘一个靠谱的iOS》面试题参考答案/《招聘一个靠谱的iOS》面试题参考答案（上）.md#11-synthesize和dynamic分别有什么作用](https://github.com/ChenYilong/iOSInterviewQuestions/blob/master/01《招聘一个靠谱的iOS》面试题参考答案/《招聘一个靠谱的iOS》面试题参考答案（上）.md#11-synthesize和dynamic分别有什么作用)
* [What does @dynamic do in Objective-C? [duplicate]](http://stackoverflow.com/questions/4621952/what-does-dynamic-do-in-objective-c)

