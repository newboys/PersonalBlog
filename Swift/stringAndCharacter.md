# LearniOS

## Swift

### Strings and Characters
1、You can’t append a String or Character to an existing Character variable, because a Character value must contain a single character only

```
var str = "hello"
str += " world"
var character: Character = "!"
//你不能写character.append(str)
str.append(character)
```
2/The expressions you write inside parentheses within an interpolated string cannot contain an unescaped backslash (\), a carriage return, or a line feed. However, they can contain other string literals.

3/string index 
endIndex not valid
```
let greeting = "Guten Tag!"
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
4/ You can use the startIndex and endIndex properties and the index(before:), index(after:), and index(_:offsetBy:) methods on any type that conforms to the Collection protocol. This includes String, as shown here, as well as collection types such as Array, Dictionary, and Set.
You can use the the insert(_:at:), insert(contentsOf:at:), remove(at:), and removeSubrange(_:) methods on any type that conforms to the RangeReplaceableCollection protocol. This includes String, as shown here, as well as collection types such as Array, Dictionary, and Set.

5/The hasPrefix(_:) and hasSuffix(_:) methods perform a character-by-character canonical equivalence comparison between the extended grapheme clusters in each string



