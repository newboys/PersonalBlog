# LearniOS

## Swift

### Enumerations

1、语法

```
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

2、Unlike C and Objective-C, Swift enumeration cases are not assigned a default integer value when they are created. In the CompassPoint example above, north, south, east and west do not implicitly equal 0, 1, 2 and 3. Instead, the different enumeration cases are fully-fledged values in their own right, with an explicitly-defined type of CompassPoint.

3The type of directionToHead is inferred when it is initialized with one of the possible values of CompassPoint. Once directionToHead is declared as a CompassPoint,.The type of directionToHead is already known, and so you can drop the type when setting its valueyou can set it to a different CompassPoint value using a shorter dot syntax:

```
var directionToHead = CompassPoint.west
directionToHead = .east
```

