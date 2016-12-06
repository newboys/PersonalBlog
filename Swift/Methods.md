# LearniOS

## Swift

### Methods
1、定义方法:Swift和Object-C最大的不同是，Swift中类、枚举、结构体都可以定义方法，而在Object-C中，只有类可以定义方法。
2、一般情况下，在Swift中不需要显性的调用self，但是当名字重复时必须写self

Example: 

```
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOf(x: 1.0) {
    print("This point is to the right of the line where x == 1.0")
}
```
3、结构体和枚举是值类型，默认情况下，值类型的属性是不能在它的实例方法中修改的，但是如果你想修改的话，你可以在方法前加上`mutating`关键字。

Example:

```
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
print("The point is now at (\(somePoint.x), \(somePoint.y))")
```
注意:你不能用结构体类型的常量来调用mutating方法，因为常量的属性是不变的(值类型的实例，一旦你声明为常量，则它的属性都默认为常量，即使该属性声明为变量)。

Example:

```
let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveBy(x: 2.0, y: 3.0)
// this will report an error

```
