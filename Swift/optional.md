# LearniOS

## Swift

### Optional

1、什么是Optional？

如果在Object-C中创建的对象的值为nil，你可以通过`obj != nil`来判断该对象是否为空，但是在Object-C中基本类型(eg:Int/Double)是不能用nil的。而在Swift中optional机制可以修饰任意可能出现nil的类型(包括基本类型)。

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
