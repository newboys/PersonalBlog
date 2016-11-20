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

Prefixes are an important part of names in programmatic interfaces. They differentiate functional areas of software. Usually this software comes packaged in a framework or (as is the case of Foundation and Application Kit) in closely related frameworks. Prefixes protect against collisions between symbols defined by third-party developers and those defined by Apple (as well as between symbols in Apple’s own frameworks).

* A prefix has a prescribed format. It consists of two or three uppercase letters and does not use underscores or “sub prefixes.” Here are some examples:
前缀 | Framework|
----|------|
NS | Foundation| 
NS | Application Kit|
AB | Address Book|
IB | Interface Builder|



