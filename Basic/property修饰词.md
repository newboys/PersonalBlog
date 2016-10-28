# property

* strong
* assign
* copy
* retain
* weak
* synthesize
自动合成set/get方法，此方法配合property。如果你直接用`.`语法来访问这个p属性的话，你是没必要写synthesize的，因为点语法实质上就是实现了set/get方法。
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

* dynamic


