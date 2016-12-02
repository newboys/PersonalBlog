# LearniOS

## Swift

### Properties

1、When an instance of a value type is marked as a constant, so are all of its properties，If you assign an instance of a reference type to a constant, you can still change that instance’s variable properties

[stackoverflow](http://stackoverflow.com/questions/38010936/why-constant-constraints-the-property-from-a-structure-instance-but-not-the-clas)

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
2、You must always declare a lazy property as a variable (with the var keyword), because its initial value might not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore cannot be declared as lazy
