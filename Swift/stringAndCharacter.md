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
