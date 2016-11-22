# LearniOS

## 编码规范

### 方法命名

方法也许是你们程序里面最常见的元素，所以你应该特别注意它们的命名。下面一部分就是讨论方法命名方面的注意事项:

#### 一般规则(General Rules)

当你命名方法的名字时，下面这些规则你应该时刻记在脑中:

* 首字母小写，以后每个单词的首字母大写。不要使用前缀。有两种情况是在该规则之外的。你可以使用众所周知的简写大写当做方法的开头(如TIFF或者PDF)，还有一种就是你可以使用前缀来管理和标识私有方法。

* 对于表示一个对象的相关操作的方法，我们应该以动词当做方法的开头:

```
- (void)invokeWithTarget:(id)target;
- (void)selectTabViewItem:(NSTabViewItem *)tabViewItem
```

方法名字中不应该包含'do'或者'dose'这些词，因为它们太泛泛没有实际的意义。还有，不要在动词之前使用副词或形容词。

* 如果方法返回接受者的属性，那么你应该在方法尾部拼接该属性。一般情况下也不要使用'get'，间接的返回一个或者多个值。

|- (NSSize)cellSize;|Right|
|----|----|
|- (NSSize)calcCellSize;|Wrong|
|- (NSSize)getCellSize;|Wrong|

* 在所有参数前使用关键字。
|- (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag;|Right|
|----|----|
|- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;|wrong|

* 在参数前要描述该参数。
|- (id)viewWithTag:(NSInteger)aTag;|Right|
|----|----|
|- (id)taggedView:(int)aTag;|Wrong|

* 当你创建的方法比继承的方法更加具体时，你应该在现有的方法尾部添加一个新的关键字。Add new keywords to the end of an existing method when you create a method that is more specific than the inherited one.
|- (id)initWithFrame:(CGRect)frameRect;|NSView, UIView.|
|----|----|
|- (id)initWithFrame:(NSRect)frameRect mode:(int)aMode cellClass:(Class)factoryId numberOfRows:(int)rowsHigh numberOfColumns:(int)colsWide;|NSMatrix, a subclass of NSView|

* 不要使用'and'来连接接受者的各属性。

|- (int)runModalForDirectory:(NSString *)path file:(NSString *) name types:(NSArray *)fileTypes;|Right.|
|----|----|
|- (int)runModalForDirectory:(NSString *)path andFile:(NSString *)name andTypes:(NSArray *)fileTypes;|Wrong.|



