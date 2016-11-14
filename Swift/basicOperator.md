# LearniOS

## Swift

### Basic Operators

1、Unlike the assignment operator in C and Objective-C, the assignment operator in Swift does not itself return a value. The following statement is not valid
```
if x = y {
    // This is not valid, because x = y does not return a value.
}
```
This feature prevents the assignment operator (=) from being used by accident when the equal to operator (==) is actually intended. By making if x = y invalid, Swift helps you to avoid these kinds of errors in your code.
2、
The addition operator is also supported for String concatenation
```
"hello, " + "world"  // equals "hello, world"

```
3、Swift also provides two identity operators (=== and !==), which you use to test whether two object references both refer to the same object instance. For more information
```
var label1 = UILabel()
var label2 = UILabel()
var label3 = label1
var label4 = label1
if label3 === label2 {
    print("y")
}else{
    print("n")
}
```
4、The Swift standard library includes tuple comparison operators for tuples with fewer than seven elements. To compare tuples with seven or more elements, you must implement the comparison operators yourself.
```
//tuple数目要小于7个
if (1,2,3,4,5,6) < (1,2,3,4,5,6) {
    
}
```

5、??
```
var defaultColor: String = "red"
var userSetColor: String?
userSetColor = "green"

var currentColor = userSetColor ?? defaultColor
```
