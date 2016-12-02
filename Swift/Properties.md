# LearniOS

## Swift

### Properties
1、计算属性(Computed properties)由类、结构体和枚举提供，存储属性(Stored properties)只能由类和结构体提供(存储属性是存储实例的一个常量或者变量的值，而计算属性则是计算一个值，而不是存储)。

2、当一个值类型(value type)的实例被声明为常量时，它的所有属性也会自动变为常量而不可更改。如果你声明一个引用类型(reference type)的实例，你仍然可以修改它的可变属性。

```
struct FixedLengthRange {
    var firstValue = 3
}

class Student {
    var age = 3
}

let john = Student()
john.age = 4
let range = FixedLengthRange()
range.firstValue = 3//这句代码报错
```
3、Lazy Stored Properties

lazy property:当该属性第一次被调用时，才会计算它的初始值。用`lazy`标识。

作用:

* 
* 
注意事项

* 你必须将You must always declare a lazy property as a variable (with the var keyword), because its initial value might not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore cannot be declared as lazy
* If a property marked with the lazy modifier is accessed by multiple threads simultaneously and the property has not yet been initialized, there is no guarantee that the property will be initialized only once.

Example:
```
class DataImporter {
    /*
     DataImporter is a class to import data from an external file.
     The class is assumed to take a non-trivial amount of time to initialize.
     */
    var fileName = "data.txt"
    // the DataImporter class would provide data importing functionality here
}
 
class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // the DataManager class would provide data management functionality here
}
 
let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
```
参考:

* [StackoverFlow](http://stackoverflow.com/questions/38010936/why-constant-constraints-the-property-from-a-structure-instance-but-not-the-clas)
