# LearniOS

## Swift

### Collection Types

#### Array

1、当你创建的集合类型不会改变的时候，你应该创建一个不可变的集合(immutable collections)。这样做对你检查代码的错误原因更加容易，并且这样Swift编译器也可以做更好的性能优化。

2、你可以通过`public init(repeating repeatedValue: Element, count: Int)`方法初始化数组(Example1)。

Example1 :

```
var arr = Array(repeating: "ss", count: 3)
//该数组为字符串类型，内容为["ss","ss","ss"]
```

3、'+'可以应用于数组(Example2)。

Example2 :

```
var anotherThreeDoubles = Array(repeating: "2.5", count: 2)
var sixDoubles = anotherThreeDoubles + anotherThreeDoubles
// sixDoubles类型:[String], 包含元素:["2.5", "2.5", "2.5", "2.5"]
```

4、数组中只能存储同一类型的数据。如Example3中，在字符串类型的数组中拼接一个整型元素会报错。

Example3 :

```
var anotherThreeDoubles = Array(repeating: "2.5", count: 2)
//该句会报不能讲Int转换为String的错误
anotherThreeDoubles.append(3)
```

5、你可以通过通过如下方法来访问和修改数组:调用方法、属性、或者使用下标。

* 你可以通过`count`(该属性为只读)属性来查数组的长度(Example4)。

Example4 :

```
var shoppingList = [1,2,3,4]
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 4 items."
```

* 你可以通过访问`isEmpty`(该属性为Boolean类型)属性来查看数组的长度是否为0(Example5)。

Example5 :
```
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// Prints "The shopping list is not empty."
```

* 你可以使用`append`方法或者`+=`(该运算符后面需为数组)运算符来拼接数组。

Example6 :

```
shoppingList.append(5)
shoppingList += [6]
```

6、你不能通过访问下角标的方式给数组的尾部拼接一个新的元素(Example7):

Example7 :

```
var shoppingList = [1,2,3,4]
//该句会报越界的错误
shoppingList[4] = 5
```

7、数组中比较常用的几个方法

* `enumerated()`:该方法返回一个包含索引和对应位置的值的元祖(tuple)数组。
the enumerated() method returns a tuple composed of an integer and the item

```
shoppingList.insert("Maple Syrup", at: 0)
let mapleSyrup = shoppingList.remove(at: 0)
let apples = shoppingList.removeLast()
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
```

9/If you try to access or modify a value for an index that is outside of an array’s existing bounds, you will trigger a runtime error. You can check that an index is valid before using it by comparing it to the array’s count property. Except when count is 0 (meaning the array is empty), the largest valid index in an array will always be count - 1, because arrays are indexed from zero.

#### Set

1/Accessing and Modifying a Set

*  count /isEmpty/insert(_:)/remove(_:)/removeAll()/contains(_:) 
```
print("I have \(favoriteGenres.count) favorite music genres.")

if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}

favoriteGenres.insert("Jazz")
```

* Swift’s Set type does not have a defined ordering. To iterate over the values of a set in a specific order, use the sorted() method, which returns the set’s elements as an array sorted using the < operator.
```
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
```

2/Use the intersection(_:) method to create a new set with only the values common to both sets.
Use the symmetricDifference(_:) method to create a new set with values in either set, but not both.
Use the union(_:) method to create a new set with all of the values in both sets.
Use the subtracting(_:) method to create a new set with values not in the specified set.
```
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]
 
oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]

```

3/Set Membership and Equality
Use the “is equal” operator (==) to determine whether two sets contain all of the same values.
Use the isSubset(of:) method to determine whether all of the values of a set are contained in the specified set.
Use the isSuperset(of:) method to determine whether a set contains all of the values in a specified set.
Use the isStrictSubset(of:) or isStrictSuperset(of:) methods to determine whether a set is a subset or superset, but not equal to, a specified set.
Use the isDisjoint(with:) method to determine whether two sets have any values in common.
```
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]
 
houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true

```

#### Dictionary

1/the updateValue(_:forKey:) method sets a value for a key if none exists, or updates the value if that key already exists. Unlike a subscript, however, the updateValue(_:forKey:) method returns the old value after performing an update. return optional value
```
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```
2/ remove a key-value pair from a dictionary with the removeValue(forKey:) method. This method removes the key-value pair if it exists and returns the removed value, or returns nil if no value existed:
```
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."

```
3/You can also retrieve an iterable collection of a dictionary’s keys or values by accessing its keys and values properties:
```
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR
 
for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
```

4/dictionary -> Array
```
let airportCodes = [String](airports.keys)
// airportCodes is ["YYZ", "LHR"]
 
let airportNames = [String](airports.values)
// airportNames is ["Toronto Pearson", "London Heathrow"]
```
