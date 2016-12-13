# LearniOS

## Swift

### Initialization

1、初始化的两种方式

1)这种方式有参数，在每次声明新的实例的时候，你可以在定义的同时给它的temperature赋一个不同的值。

```
struct Fahrenheit {
    var temperature: Double
    init(temperature: Double) {
        self.temperature = temperature
    }
}
var f = Fahrenheit(temperature: 20)
print("The default temperature is \(f.temperature)° Fahrenheit")
```

2)该方式每个生成的实例的temperature都有一个默认值。

```
struct Fahrenheit {
    var temperature = 32.0
}
```

2、带有参数的构造器，调用的时候必须带有参数列表。

```
struct Color {
    let red, green, blue: Double
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
    init(white: Double) {
        red   = white
        green = white
        blue  = white
    }
}

let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
let halfGray = Color(white: 0.5)
//该句会报错
let veryGreen = Color(0.0, 1.0, 0.0)
```
3、你可以用`_`代替参数名

```
struct Celsius {
    var temperatureInCelsius: Double
    init(_ celsius: Double) {
        temperatureInCelsius = celsius
    }
}

let gelsius = Celsius(30)
print(gelsius.temperatureInCelsius)
```

4、你可以将在构造期间值不确定的属性声明为optional

```
class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        print(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// Prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."
```

5、构造器代理

1)值类型(struct,enumeration)相对简单，它们不支持继承，只能调用自己的相关的构造器。

2)类的比较复杂，它们支持继承。

```
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
    init() {}
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}

let basicRect = Rect()
let originRect = Rect(origin: Point(x: 2.0, y: 2.0),size: Size(width: 5.0, height: 5.0))
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),size: Size(width: 3.0, height: 3.0))
```

6、Swift提供类的两种构造器，指定构造器(designated initializers)和便利构造器(convenience initializers)
我们首要的应该使用designated initializers，每个类应至少有一个designated initializers，如果没有必要的话，你可以不写convenience initializers。
1)声明designated initializers的语法

```
init(`parameters`) {
    `statements`
}
```

2)声明convenience initializers的语法

```
convenience init(`parameters`) {
    `statements`
}
```


Tips:
1、与Object-C中的构造器不同，Swift的构造器不需要有返回值。

2、类和结构体在创建实例时，必须为所有存储型属性设置合适的初始值。存储型属性的值不能处于一个未知的状态。

3、对于类的实例，一个常量属性只能在当前类的构造阶段修改，不能由它的子类修改。

4、构造器可以调用其他的构造器来执行实例的初始化，这个过程叫做构造器代理。

5、如果你为某个值类型定义了一个自定义的构造器，你将无法访问到默认构造器(如果是结构体，还将无法访问逐 一成员构造器)。这种限制可以防止你为值类型增加了一个额外的且十分复杂的构造器之后,仍然有人错误的使用 自动生成的构造器。如果你想自定义的构造器和原始的都能使用，你可以将其写在Extensions中。
