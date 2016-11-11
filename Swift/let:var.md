# LearniOS

## Swift

### let&var

#### 1、let
let is a little bit like a const pointer in C. If you reference an object with a let, you can change the object's properties or call methods on it, but you cannot assign a different object to that identifier.

let also has implications for collections and non-object types. If you reference a struct with a let, you cannot change its properties or call any of its mutating func methods.

Using let/var with collections works much like mutable/immutable Foundation collections: If you assign an array to a let, you can't change its contents. If you reference a dictionary with let, you can't add/remove key/value pairs or assign a new value for a key — it's truly immutable. If you want to assign to subscripts in, append to, or otherwise mutate an array or dictionary, you must declare it with var.


参考：
* [How exactly does the “let” keyword work in Swift?](http://stackoverflow.com/questions/24002999/how-exactly-does-the-let-keyword-work-in-swift)
