## Category 和 Extension 的区别
### Category
* 源码:
```
Category
Category 是表示一个指向分类的结构体的指针，其定义如下：
typedef struct objc_category *Category;
struct objc_category {
  char *category_name                          OBJC2_UNAVAILABLE; // 分类名
  char *class_name                             OBJC2_UNAVAILABLE; // 分类所属的类名
  struct objc_method_list *instance_methods    OBJC2_UNAVAILABLE; // 实例方法列表
  struct objc_method_list *class_methods       OBJC2_UNAVAILABLE; // 类方法列表
  struct objc_protocol_list *protocols         OBJC2_UNAVAILABLE; // 分类所实现的协议列表
}
Tip:并没有存放属性的地方
```
* 如果分类中有和原有类同名的方法,会优先调用分类中的方法,就是说会忽略原有类的方法。所以同名方法调用的优先级为 分类 > 本类 > 父类。因此在开发中尽量不要覆盖原有类
* 原则上Category只是扩展本类的方法，不能添加成员变量(可以通过runtime添加上set/get方法，但并没有声明实例变量)

### Extension
* 相当于在.m文件中实现的属性和方法
* 用来实现私有方法和属性
* Extension 没有独立的.m文件，具体实现要依靠对应类的.m文件

### 区别
* Category只能扩展方法(可以通过runtime添加上set/get方法，但并没有声明实例变量)，Extension可以添加属性和方法(只能在本类里面用，相当于private)
* Extension 并没有implementation部分，它要依靠对应类的implementation来实现

### 参考
* [iOS分类(category),类扩展(extension)—史上最全攻略](https://www.jianshu.com/p/9e827a1708c6)

## define 和 const常量有什么区别?
* define在预处理阶段进行替换，const常量在编译阶段使用
* define仅仅进行替换不会进行数据类型检查，const有数据类型
* define可以定义简单的函数，const则不能，只能定义常量
* define定义的常量在替换后运行过程中会不断地占用内存，而const定义的常量存储在数据段只有一份copy，效率更高，所以定义常量的时候尽量使用const

### 参考
* [iOS 宏(define)与常量(const)的正确使用](https://www.jianshu.com/p/f83335e036b5)

## __block 和 __weak的区别
* __block可以修饰基本类型和对象，该修饰符修饰的变量可以在Block中修改
* __weak只能修饰对象类型，不能修饰基本类型
* __weak主要用来解决reference circle

### 参考
* [iOS开发-由浅至深学习block](https://www.jianshu.com/p/29d70274374b)

## static关键词的作用
* static修饰的变量，是一个私有的全局变量

## 栈和堆的区别
* 从管理上：对栈来讲，由编译器自动管理，无需我们手工控制；对于堆来讲，释放工作由程序员控制，可能产生内存泄漏
* 从申请大小上：栈空间比较小；堆空间比较大
* 数据存储方面：栈一般存储基础类型，对象地址；堆空间一般存放对象本身，Block的copy

## Objective-C使用什么机制管理对象内存？
* 使用ARC，通过 retainCount 的机制来决定对象是否需要释放。 每次 runloop 的时候，都会检查对象的retainCount，如果retainCount为0，说明该对象没有地方需要继续使用了，可以释放掉了
