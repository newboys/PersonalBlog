# LearniOS
iOS Knowledge

## 一、Category

### 1、category的作用
#### 1）给已经存在的类添加方法
#### 2）将类的实现分开写在几个分类里面
这样做的好处:

* 可以减少单个文件的体积 
* 可以把不同的功能组织到不同的category里
* 可以由多个开发者共同完成一个类 
* 可以按需加载想要的category

#### 3）声明私有的方法

### 2、category的缺点
#### 1)不能给相应的类添加`instance variable`
![classStruct](https://github.com/fengzhihao123/LearniOS/blob/master/Basic/classStruct.png)
原因：`在上面的objc_class结构体中，ivars是objc_ivar_list（成员变量列表）指针；methodLists是指向objc_method_list指针的指针。在Runtime中，objc_class结构体大小是固定的，不可能往这个结构体中添加数据，只能修改。所以ivars指向的是一个固定区域，只能修改成员变量值，不能增加成员变量个数。methodList是是一个二维数组，所以可以修改*methodLists的值来增加成员方法，虽没办法扩展methodLists指向的内存区域，却可以改变这个内存区域的值（存储的是指针）。因此，可以动态添加方法，不能添加成员变量`

由此问题引申出一个问题，为什么category能添加一个`property`，不能添加`instance variable`?这个我们要从category的结构体开始分析。

```
typedef struct category_t {
    const char *name;
    classref_t cls;
    struct method_list_t *instanceMethods;
    struct method_list_t *classMethods;
    struct protocol_list_t *protocols;
    struct property_list_t *instanceProperties;
} category_t;
```

* 类的名字（name）
* 类（cls）
* category中所有给类添加的实例方法的列表（instanceMethods）
* category中所有添加的类方法的列表（classMethods）
* category实现的所有协议的列表（protocols）
* category中添加的所有属性（instanceProperties）

从category的定义也可以看出category的可为（可以添加实例方法，类方法，甚至可以实现协议，添加属性）和不可为（无法添加实例变量）.

#### 2）如果特殊情况必须添加？如何解决？
解决办法:`我们可以Runtime的objc_getAssociatedObject和objc_setAssociatedObject方法来模拟属性的get和set方法，用关联对象来模拟实例变量，这样就有了@property的三要素，只是跟@property的实现机制是完全不一样的。`

##### 添加property的两种方法
* 第一种
```
//.h文件：
@property (nonatomic, copy) NSString *str;
//.m文件，要#import <objc/runtime.h>
-(void)setStr:(NSString *)str{
    objc_setAssociatedObject(self, @selector(str), str, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}

-(NSString *)str{
    return objc_getAssociatedObject(self, @selector(str));
}

```

* 第二种
```
static void *UIViewPoint =@"UIViewPoint";
@implementation UIView (Point)

@dynamic pointView;

- (void)setPointView:(UIView *)pointView {
    objc_setAssociatedObject(self, UIViewPoint, pointView,OBJC_ASSOCIATION_RETAIN);
}

- (UIView *)pointView {
   return objc_getAssociatedObject(self, UIViewPoint);
}
```


### 3、成员变量的创建方式
### 4、


### 参考链接
* [Category深度解析](http://www.jianshu.com/p/a263e53bf4ef)
* [iOS 开发中的争议（一）](http://blog.devtang.com/2015/03/15/ios-dev-controversy-1/)
* [深入理解Objective-C：Category](http://tech.meituan.com/DiveIntoCategory.html)
* [类别(Category)与类扩展 (Extension)的区别](http://www.jianshu.com/p/57d7f1910ef4)
* [Is there a difference between an “instance variable” and a “property” in Objective-c?](http://stackoverflow.com/questions/843632/is-there-a-difference-between-an-instance-variable-and-a-property-in-objecti)
