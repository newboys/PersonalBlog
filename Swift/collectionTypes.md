# LearniOS

## Swift

### Collection Types

#### Array

1、It is good practice to create immutable collections in all cases where the collection does not need to change. Doing so makes it easier for you to reason about your code and enables the Swift compiler to optimize the performance of the collections you create.

2/

```
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]

```

3/ + operator
```
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]
 
var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]

```

4/Because all values in the array literal are of the same type

5/You access and modify an array through its methods and properties, or by using subscript syntax.

* To find out the number of items in an array, check its read-only count property:
```
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

* Use the Boolean isEmpty property as a shortcut for checking whether the count property is equal to 0:
```
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// Prints "The shopping list is not empty."
```

* apppend +=
```
shoppingList.append("Flour")
shoppingList += ["Baking Powder"]
```

6/The first item in the array has an index of 0, not 1. Arrays in Swift are always zero-indexed.

7/You can’t use subscript syntax to append a new item to the end of an array.

8/insert(_:at:)/remove(at:)/removeLast()/enumerated()

* the enumerated() method returns a tuple composed of an integer and the item

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





