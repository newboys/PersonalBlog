# LearniOS

## Swift

### Optional机制

1、什么是Optional机制？

optional机制:就是当你声明optional类型的变量值为空的时候，编译器会自动返回nil。

我们来通过一个例子来理解这一句话，字符串类型转整型。我们知道通过调用函数我们是可以把字符串中的数字转换为整型，但是不是所有的字符串都能转换为整型，比如:`Dota`,那我们应该怎么解决这一问题呢？这就用到了optional机制。例如下面Example1的代码。我们通过编译器发现`convertedNumber`并不是`Int`类型，而是`Int?(等同于optional Int)`类型。我们可以通过判断convertedNumber中的值来知道转换是否成功(如果声明的类型不是optional类型，那么它一定不会为nil)。通过optional机制我们就可以避免程序发生因类型转换而导致的一些计算错误。

注:在C和Object-C中并没有optional这种机制，和它比较相似的是

The concept of optionals doesn’t exist in C or Objective-C. The nearest thing in Objective-C is the ability to return nil from a method that would otherwise return an object, with nil meaning “the absence of a valid object.” However, this only works for objects—it doesn’t work for structures, basic C types, or enumeration values. For these types, Objective-C methods typically return a special value (such as NSNotFound) to indicate the absence of a value. This approach assumes that the method’s caller knows there is a special value to test against and remembers to check for it. Swift’s optionals let you indicate the absence of a value for any type at all, without the need for special constants.

Example1 :
```
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
```

Example2 :

```
if convertedNumber != nil {
    // success
}else{
    //fail
}
```

2、在什么情况下使用

当可能发生值缺失(value may be absent)的情况时，你应该使用optional机制。比如Example1的情况。

optional类型的变量会发生两种情况:

* 该变量有值，你可以通过解包(unwarp)的方式来访问该值
* 该变量木有值

3、关于optional返回的`nil`

* 非可选(nonoptional)常量或者变量是不能赋值为nile的，如果你代码中的常量或者变量可能发生值缺失的情况，你应该将它声明为合适的可选(optional)类型
* Swift中的nil和Object-C中的nil是不同的。在OC中，nil是一个指向一个不存在的对象的指针。而在swift中nil并不是一个指针，它是代表值缺失的一种类型。声明为optional的任何类型都能设置为nil，而不仅仅是对象类型(注:在OC中只能把对象类型设置为nil，结构体、枚举和C的基本类型是不能设置为nil的)。






2、Optional的用法

代码示例：
```
//str 为可能为nil的字符串
let str: String?
//num 为可能为nil的整型
let num: Int? 
```

使用optional可以使我们摆脱很多不必要的判断和取值。在OC中如果我们传参的值为nil在编译的阶段是不会报错的，这样会导致不必要的crash，如果我们引入optional机制就不会出现这种问题。

1)OC 代码示例：

```
- (void)viewDidLoad {
    [super viewDidLoad];
    NSArray *array;
    //此时array为nil，但是编译器不会报错
    [self setup:array];
}

- (void)setup:(NSArray *)array{
    //do something
}
```

2)Swift代码示例：

```
override func viewDidLoad() {
        super.viewDidLoad()
        let array: NSArray
        //如果注释此句，编译器会报错。因为array是不允许nil的
        array = []
        doSomething(array: array)
    }

    func doSomething(array: NSArray) -> Void {
        print(array)
    }

```

其实了解一下 optional 的实现机制，就可以更深刻地理解 A 与 A？是两种完全不同的类型。

optional 在 Swift 中可以这样实现：
```
enum Optional<T> {
    case Nil
    case Some( value:T )
} 
```

// 把 T 放在外面更好理解一点吧， 没有用 case Some<T> (value:T)
所以 Bool？，除去语法糖，就是 Optional<Bool> 。它是一个 enum ，而不再是 Bool。而 nil 就是 Optional.Nil。unwrap 做的事情 （ a! ）就是提取 .Some 中的 value 变量。

强制解析/解包 (forced unwrapping)

当确定可选类型确实包含值之后,可以在可选的名字后面加一个感叹号(!)来获取值.当Option == nil时,使用 ! 来获取会导致运行时错误。所以使用 ! 来强制解析值之前,一定要确定Option类型不是nil的.

3、Optional的进阶

1)optaional chaining

```
class Toy{
    let name: String
    init(name: String) {
        self.name = name
    }
}

extension Toy{
    func play()  {
        print("extension")
    }
}

class Pet{
    var toy: Toy?
}

class Child{
    var pet: Pet?
}

let xiaoming = Child()
let petInstance = Pet()
let toyInstance = Toy.init(name: "aaa")

xiaoming.pet = petInstance
xiaoming.pet?.toy = toyInstance

if let tonyName = xiaoming.pet?.toy?.name {
    print("yes")
}else{
    print("no")
}
```

4、Optional的注意事项

参考：

* [Swift 的 Optional 机制有什么用](https://www.zhihu.com/question/28026214)

* [[iOS笔记]Swift中的Optional类型 (可选类型)](http://www.jianshu.com/p/0e3712b0c044)

* Swift Tips

