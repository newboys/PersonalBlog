# LearniOS

## Code Guide

### 基础命名规范(Code Name Basic)

#### 一般命名规范(General Principles)

1、清晰(Clarity)

* 如果既精简又清晰那是最好的，但是你不应该为了精简而摒弃清晰。

示例代码 | 评价|
----|------|
insertObject:atIndex: | Good  | 
insert:at:            | 不清晰，插入什么？at又是具体指的什么 |
removeObjectAtIndex:  | Good  |
removeObject:         | Good, 因为它指出了删除的为对象类型  |
remove:               | 不清晰; 删除什么?|

* 一般情况下，不要缩写名字，即使它们很长。你可能认为简写是众所周知的，但是它可能不是，尤其是那些和你不同语言和不同文化背景的人。

示例代码 | 评价|
----|------|
destinationSelection  | Good   | 
destSel               | 不清晰  |
setBackgroundColor:   | Good   |
setBkgdColor:         | 不清晰  |

* 然而，少数一部分缩写是非常通用的，也有很长的使用历史。你可以继续使用它们；[可用缩写](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html#//apple_ref/doc/uid/20001285-BCIHCGAE)

* API的名字要避免模棱两可，例如方法名称可以被解读为多个意思。

示例代码 | 评价|
----|------|
sendPort     | 是发送port还是返回port？   | 
displayName  | 它是显示一个名字还是返回用户界面的接受者的title？| 

2、一致性(Consistency)

* 尽量使用和Cocoa 编程风格保持一致。如果你不确定如何命名，你可以浏览本文或者查看API文档。
* 
Consistency is especially important when you have a class whose methods should take advantage of polymorphism. Methods that do the same thing in different classes should have the same name.
示例代码 | 评价|
----|------|
`- (NSInteger)tag` | 在 NSView, NSCell, NSControl中被定义| 
`- (void)setStringValue:(NSString *)`  | 在很多Cocoa的类中被定义| 

3、不要自我重复No Self Reference

* 名称不要自我重复Names shouldn’t be self-referential.

示例代码 | 评价|
----|------|
NSString | Okey| 
NSStringObject  | NSString和Object重复|

* 作为掩码的常量（因此可以按位操作组合）是此规则的例外，还有通知名称的常量。(此句为google，这是原句:`Constants that are masks (and thus can be combined in bitwise operations) are an exception to this rule, as are constants for notification names`)

示例代码 | 评价|
----|------|
NSUnderlineByWordMask | Okey| 
NSTableViewColumnDidMoveNotification  | Okey|

#### 前缀(Prefixes)

前缀是程序设计非常重要的一种命名方式。不同的前缀在软件区域中有不同的功能。

* 每种前缀有各自规定的格式。它由两个或者三个大写字母组成，它不能使用下划线或者下标。下面是一些具体的例子:

前缀 | Framework|
----|------|
NS | Foundation| 
NS | Application Kit|
AB | Address Book|
IB | Interface Builder|

* 当你命名类、协议、函数、常量和定义结构体的时候应该使用前缀。当命名方法的时候不要使用前缀；方法是存在于定义它们的类的命名空间。在命名结构体的字段时也不要使用前缀。

#### 书写约定(Typographic Conventions)

当命名API元素的时候你要准守一些很简单的约定:

* 名字由多个单词组成，不要使用标点符号或者空格(或者下划线等等)当做名字的一部分；另外，每个单词的首字母要大写然后将这些单词拼在一起即可(第一个单词的首字母要小写)。eg:`runTheWordsTogether`。下面还有几条要求:

1)对于方法的名字，第一个字母小写，以后每个单词的首字母大写。不要使用前缀。

eg:
```
fileExistsAtPath:isDirectory:
```
在该规范中对于方法的名字有一个例外，那就是以总所周知的单词缩写开头的，eg:TIFFRepresentation (NSImage)。

2)对于功能和常量的名字，使用与相关类相同的前缀，并大写嵌入字的第一个字母

```
NSRunAlertPanel
NSCellDisabled
```

* Avoid the use of the underscore character as a prefix meaning private in method names (using an underscore character as a prefix for an instance variable name is allowed). Apple reserves the use of this convention. Use by third parties could result in name-space collisions; they might unwittingly override an existing private method with one of their own, with disastrous consequences. See Private Methods for suggestions on conventions to follow for private API.


