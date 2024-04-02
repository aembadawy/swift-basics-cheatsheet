# swift-basics-cheatsheet

### Variable & Constants declaraation 

Variables declaared using *var*, constants using *let*

```
var num: Int = 10
let pi: Float = 3.14159
let name: String = "Aem"
var isRight: Bool = true
```
or using swift's type-inferance
```
var num = 10
let name = "Aem"
var isTrue = !false //infix or unary operator, true
var isAppleMoreThanMango = "Apple" > "Mango" //false, compares alphabet
```

### Optionals
Represent the value or the absance of a value which is *nil*.
We can not know if the optional has a value or not untill it's unwrapped.
Type-inferance doesn't work with optionals.

*Ways to unwrap optionals*
1- Force Unwrap
The easiest way to unwrap optionals.
```
var catName: String?
catName = "Zoe"

var unwrappedCatName = catName!
```
But if the optional had no value it will crash. Use force unwrap only when it's certian it has value.

2- Optional binding
Similar to an *if-else-statment*
```
if let catName = catName {
    print(catName)
} else {
    print("Cat has no name")
}
```
In optional bining, we can add more than one optional like *&& operation*.
```
var otherPetName: String? = nil

if let catName = catName,
    let otherPetName = otherPetName {
    print(catName, otherPetName)
} else {
    print("Cat has no name, other pet has no name either.")
}
```
> output: Cat has no name, other pet has no name either.

3- Guard Statment
Guard is used to gaurd aganist something really bad that should rarly happen. 

```
func print(PetName otherName: String?) {
    
    guard let otherName = otherPetName else {
        print("No other name")
        return
    }
    print(otherName)
}

print(PetName: otherPetName)
```
> output: no otherName

4- Nil Coalesing
Sets a default value for the optional in case it's nil.

```
var num: Int? = 10

var defaultNum = num ?? 0
```

5- Optional Chaining 
When we have optional *structs, or classes* we use optional chaining to access calss or struct properties and methods in a safe way.
```
struct Car {
    var color = "Red"
    
    func move() {
        print(color, "car drives forward.")
    }
}

var myCar: Car? = Car()

myCar?.color
myCar?.move()
```
> output: Red car drives forward.

if the struct or calss instance is nil, it won't continue down the chain.

### Tuples
Wrap more that one small related peices of the same-type or different-type data together.
```
let coordinates: (Int, Int) = (2,3)
let namedCoordinatesTuple: (Int, Int) = (x: 2, y:3)
let coordinates3D: (Int, Int, Int) = (x:2, y:3, z: 1)
let firstOperandWithOperation: (Int, String) = (5, "+")
```
or using swift's type-inferance 
```
let coordinates = (2,3)
```

### Arrays
Ordered list of values of the same data-type with indexes assigned to each element starting at `0`.
Arrays are Objects so they have both data and functions.

```
let array: [Int] = [1,2,3,4,5]
let arrayx10: Array<Int> = [10,20,30,40,50]
```
or using type-inferance

```
var strArray = ["val1", "val2", "val3"]
var anotherStrArray = ["key1", "key2", "key3"]
```
- Using Array Methods
  - Append
    ```strArray.append("val4")```
  - Append ContentsOf Another Array
    ```strArray.append(contentsOf: anotherStrArray)```
    or
    ```strArray += anotherStrArray```
  - Remove At index
    ```strArray.remove(at: 0)```
  - RemoveFirst: Removes first element and returns removed element
    ```let str = strArray.removeFirst()```
  - RemoveLast: Removes last element and returns removed element
    ```let str = strArray.removeLast()```
  - RemoveAll
    ```strArray.removeAll()```
  - isEmpty
    ```strArray.isEmpty```
  - Count
    ```strArray.count```
  - First: retruns first element of array if existed (returns optional)
    ```strArray.first```
  - Last: retruns last element of array if existed (returns optional)
    ```strArray.last```
  - Min: retruns minimum element of array if existed (returns optional)
    ```strArray.min()```
  - Max: retruns maximum element of array if existed (returns optional)
    ```strArray.max()```
  - Contains: check if array contains an element, returns bool
    ```strArray.contains("val1")```
  - Insert: inserts new element value at specified index
    ```strArray.insert("val8", at: 0)```
  - Insert Contents of: intserts contets of another collection at a specidied index
    ```strArray.insert(contentsOf: anotherStrArray, at: 0)```
  - Swap at: extchanges the values of 2 elements at specified indexes
    ```strArray.swapAt(1, 2)```
  - Enumerated: Returns a sequence of pairs (n, x), where n represents index and x represents value.
    ```strArray.enumerated()```
  - Subscripting: getting the element at a spcific index, if element doesn't exist the app will crash.
    ```let element = array[3]```
  - Array Slicing: stores a ref to a part of the array
    ```let arraySlice = strArray[1...3]```

### Loops
- While loop: as long as the condition is true, the code excutes
```
var i = 110
while i > 99 {
    print("Above 100")
    i -= 1
}
```
loop can also be broken out of by using *break*.
```
while i > 99 {
    print("Above 100")
    i -= 1
    if i == 105 {
        break
    }
}
```
- Repeat while: makes sure the code is excuted at least once before checking the condition
```
repeat {
    print("Above 90")
    i -= 1
} while i > 90
```
- For Loop: runs a specified number of times with an increasing countable range
**Example using a closed range**
```
for i in 0...9 {
   print(i)
}
```
**Example using halp-open range**
```
for i in 0..<5 {
    print(i)
}
```
**Example when value of i is not needed**
```
for _ in 0...10 {
    print("Repetetion...")
}
```
**Example using *where* to add condition on a loop**
```
for i in 1...100 where i%2 == 0 {
    print(i, "is odd")
}
```
**Example using *Loop Labeled Statment*, *Nested Loops*, and *continue***
Continue key word stops current iteration and continues 
```
floors: for floor in 12...14 {
rooms: for room in 11...16 {
    if room == 13 {
        continue floors
    }
    print("Available room", room, "in floor", floor)
}
}
```
>output:
>Available room 11 in floor 12
>Available room 12 in floor 12
>Available room 11 in floor 13
>Available room 12 in floor 13
>Available room 11 in floor 14
>Available room 12 in floor 14

**Example using *break***
Break stops the loop intierly, breaks out of it
```
floors: for floor in 12...14 {
rooms: for room in 11...16 {
    if room == 13 {
        break floors
    }
    print("Available room", room, "in floor", floor)
}
}
```
>output:
>Available room 11 in floor 12
>Available room 12 in floor 12

### Dictionary
Dictionaries are unordered collection of *(key, value)* pairs, of the same data type.
Keys must be unique, but values can be redundant.
Used when we need to store and retrive values based on a value of an identifier.
```
var dictionary: [String: Int] = [:]
dictionary = ["1": 1, "2": 2, "3": 3]
```
or using type-inferance
```
var dictionary = ["1": 1, "2": 2, "3": 3]
```
updating value of key
```
dictionary["1"] = 10 // changes if key exists
dictionary["4"] = 4 // adds new if key doesn't exist
```
or 
```
dictionary.updateValue(1, forKey: "1")
```
removing value
```
dictionary.removeValue(forKey: "3")
```
or
```
dictionary["2"] = nil
```

### Set
Unordered sequance of unique elements of the same data type, ensures no duplication.
```
var set: Set<Int> = [1,2,3,4]
var anotherSet: Set<Int> = [5,6,4,3,8,9]
```
- Using set methods
  - Insert: inserts element with no index needed, as it's an unordered list.
    ```
    set.insert(11)
    ```
  - Containts: checks if the set contains an elements and return bool.
    ```
    set.contains(11)
    ```
  - Remove: removes element if exists, and returns either the removed element or nil if element does not exist.
    ```
    set.remove(9)
    ```
  - Intersection: returns a set of only the elements that exist in both sets
    ```
    let intersectionSet = set.intersection(anotherSet)
    ```
  - Form intersection: like *intersection* but mutates the set it's called on in place.
    ```
    set.formUnion(anotherSet)
    ```
  - SymmetricDifference: retruns elements that do not exists in either set, *opposit of intersection*.
    ```
    let diffSet = set.symmetricDifference(anotherSet)
    ```
  - Form Symmetric Difference: like *symmetric difference* but mutates the set it's called on in place
    ```
    set.formUnion(anotherSet)
    ```
  - Union: returns a set containing elements of both sets
    ```
    let unionSet = set.union(anotherSet)
    ```
  - Form Union: like *union* but mutates the set it's called on in place.
    

