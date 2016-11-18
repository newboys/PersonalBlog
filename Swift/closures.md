# LearniOS

## Swift

### Strings and Characters
1、你不能对一个已存在的字符(Character)变量进行字符或者字符串的拼接(Example1)，因为字符变量只能包含一个字符。

Example1 :

```
var str = "hello"
str += " world"
var character: Character = "!"
//你不能写character.append(str)
str.append(character)
```

2、在Example2中的输出语句中，不能包含'\'和换行符。

Example2 :

```
let num = 123
print("the number is \(num)")
```

3、字符串索引的相关操作

Example3 :
```
let greeting = "Guten Tag!"
//greeting[greeting.endIndex]会越界
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
```

4、你可以对遵守`Collection protocol`的任何类型，使用`startIndex`、`endIndex`属性和`index(before:)`、`index(after:)`、`index(_:offsetBy:)`方法。
这些类型包括String/Array/Dictionary/Set。你可以对遵守`RangeReplaceableCollection protocol`的任何类型，使用`insert(_:at:)`/`insert(contentsOf:at:)`/`remove(at:)`/`removeSubrange(_:) `方法。这些类型包括String/Array/Dictionary/Set。

5、`hasPrefix(_:)`和`hasSuffix(_:)`方法会每个字符去匹配你提供的字符串(Example4)。

Example4 :

```
let str = "abcdeeeeee"
if str.hasPrefix("ab") {
    print("yes")
}
```

