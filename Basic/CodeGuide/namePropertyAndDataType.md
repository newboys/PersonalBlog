# LearniOS

## 编码规范

`前言:因为该文档为2013年，很久没有更新，所以有的地方已经过时。过时的地方我回标注出来!`

### 给属性和数据类型命名(Naming Properties and Data Types)

该部分是讨论的如何声明属性，实例变量，常量，通知和异常(properties, instance variables, constants, notifications, and exceptions)

#### 声明属性和实例变量(Declared Properties and Instance Variables)

声明一个属性，实际上就是声明该属性的访问器方法，所以声明属性要遵守的规则和声明访问器方法的规则是一样的。如果实行表示为名词或者动词，它的格式如下:

@property (…) type nounOrVerb;

例如:

```
@property (strong) NSString *title;
@property (assign) BOOL showsAlpha;
```
如果属性表示为形容词的话，属性可以省略'is'的前缀。例如:

```
@property (assign, getter=isEditable) BOOL editable;
```

在大多数情况下，如果你声明了属性，你也要合成一个相关的实例变量(注:现在不需要你手动合成，系统会自动合成)。

Make sure the name of the instance variable concisely describes the attribute stored. Usually, you should not access instance variables directly; instead you should use accessor methods (you do access instance variables directly in init and dealloc methods). To help to signal this, prefix instance variable names with an underscore (_), for example:

```
@implementation MyClass {
    BOOL _showsTitle;
}
```
