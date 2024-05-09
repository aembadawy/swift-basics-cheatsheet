# swift-basics-cheatsheet

### Variables & Constants declaration 

Variables declared using *var*, constants using *let*

```
var num: Int = 10
let pi: Float = 3.14159
let name: String = "Aem"
var isRight: Bool = true
```
or using swift's type-inference
```
var num = 10
let name = "Aem"
var isTrue = !false //infix or unary operator, true
var isAppleMoreThanMango = "Apple" > "Mango" //false, compares alphabet
```

### Optionals
Represent the value or the absence of a value which is *nil*.
We can not know if the optional has a value or not until it's unwrapped.
Type-inference doesn't work with optionals.

*Ways to unwrap optionals*

1- Force Unwrap
The easiest way to unwrap optionals.
```
var catName: String?
catName = "Zoe"

var unwrappedCatName = catName!
```
But if the optional has no value it will crash. Use force unwrap only when it's certain it has value.

2- Optional binding
Similar to an *if-else-statement*
```
if let catName = catName {
    print(catName)
} else {
    print("Cat has no name")
}
```
In optional binding, we can add more than one optional like *&& operation*.
```
var otherPetName: String? = nil

if let catName = catName,
    let otherPetName = otherPetName {
    print(catName, otherPetName)
} else {
    print("Cat has no name, other pet has no name either.")
}
```
> output: Cat has no name, other pets have no name either.

3- Guard Statement
Guard is used to guard against something really bad that should rarely happen. 

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

4- Nil Coalescing
Sets a default value for the optional in case it's nil.

```
var num: Int? = 10

var defaultNum = num ?? 0
```

5- Optional Chaining 
When we have optional *structs, or classes* we use optional chaining to access class or struct properties and methods in a safe way.
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

if the struct or class instance is nil, it won't continue down the chain.

### Tuples
Wrap more that one small related pieces of the same-type or different-type data together.
```
let coordinates: (Int, Int) = (2,3)
let namedCoordinatesTuple: (Int, Int) = (x: 2, y:3)
let coordinates3D: (Int, Int, Int) = (x:2, y:3, z: 1)
let firstOperandWithOperation: (Int, String) = (5, "+")
```
or using swift's type-inference 
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
or using type-inference

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
  - First: returns first element of array if exists (returns optional)
    ```strArray.first```
  - Last: returns last element of array if exists (returns optional)
    ```strArray.last```
  - Min: returns minimum element of array if exists (returns optional)
    ```strArray.min()```
  - Max: returns maximum element of array if exists (returns optional)
    ```strArray.max()```
  - Contains: check if array contains an element, returns bool
    ```strArray.contains("val1")```
  - Insert: inserts new element value at specified index
    ```strArray.insert("val8", at: 0)```
  - Insert Contents of: insert contents of another collection at a specified index
    ```strArray.insert(contentsOf: anotherStrArray, at: 0)```
  - Swap at: exchanges the values of 2 elements at specific indexes
    ```strArray.swapAt(1, 2)```
  - Enumerated: Returns a sequence of pairs (n, x), where n represents index and x represents value.
    ```strArray.enumerated()```
  - Subscripting: getting the element at a specific index, if the element doesn't exist the app will crash.
    ```let element = array[3]```
  - Array Slicing: stores a ref to a part of the array
    ```let arraySlice = strArray[1...3]```
  - FirstIndex: returns the index of the first element in an array that fulfills a specified condition. If no element satisfies the condition, it returns nil.
    ``` arrayName.firstIndex{ condition }```

### Loops
- While loop: as long as the condition is true, the code executes
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
- Repeat while: makes sure the code is executed at least once before checking the condition
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
**Example using half-open range**
```
for i in 0..<5 {
    print(i)
}
```
**Example when value of i is not needed**
```
for _ in 0...10 {
    print("Repetition...")
}
```
**Example using *where* to add condition on a loop**
```
for i in 1...100 where i%2 == 0 {
    print(i, "is odd")
}
```
**Example using *Loop Labeled Statement*, *Nested Loops*, and *continue***
Continue keyword stops current iteration and continues 
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
Break stops the loop entirely, breaks out of it
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
Used when we need to store and retrieve values based on a value of an identifier.
```
var dictionary: [String: Int] = [:]
dictionary = ["1": 1, "2": 2, "3": 3]
```
or using type-inference
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
Unordered sequence of unique elements of the same data type, ensures no duplication.
```
var set: Set<Int> = [1,2,3,4]
var anotherSet: Set<Int> = [5,6,4,3,8,9]
```
- Using set methods
  - Insert: inserts element with no index needed, as it's an unordered list.
    ```
    set.insert(11)
    ```
  - Contains: checks if the set contains an element and returns a bool.
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
  - SymmetricDifference: returns elements that do not exists in either set, *opposite of intersection*.
    ```
    let diffSet = set.symmetricDifference(anotherSet)
    ```
  - Form Symmetric Difference: like *symmetric difference* but mutates the set it's called on in place
    ```
    set.formSymmetricDifference(anotherSet)
    ```
  - Union: returns a set containing elements of both sets
    ```
    let unionSet = set.union(anotherSet)
    ```
  - Form Union: like *union* but mutates the set it's called on in place.
    ```
    set.formUnion(anotherSet)
    ```


### Functions & Named Types
Named types are types that must have a name when declared, i.e., structs, classes, enums, protocols, and also ints, strings, and arrays, etc.
Compound types on the other hand are defined by a *type-signature*, they are defined by the type they contain, i.e., tuples are compound types they can be *(Int, Int) or (Int, bool)*, etc.
***Functions***, like tuples, are **Compound types**, their type is distinguished by a type-signature instead of a name.

Types can also be ascribed in another important way: 
- Value types: hold value, i.e., structs, tuples
- Reference types: hold only reference to value, i.e., classes, functions.

#### Function overloading 
Overloading is unique to functions, it's creating the functions with the same name but they must be different in either their **param list** in both *param number or param types*, or **return type**, or different **argument labels**. 
NOTE: Difference in param names is not considered overloading.

Overloaded functions must be related, it's also advisable to avoid overloads that differ only in return types.
```
stride(from: 3, through: 0, by: -1)
```
>output: 3,2,1,0
```
stride(from: 3, to: 0, by: -1)
```
>output: 3,2,1
`Stride in overloaded using different argument labels`

Strides are a good example of sequances that is not a collection. Strides also do not conform to the `Equatable` meaning you can't compare them to each other.

#### Variadic params
When the number of values passed in for the params varies.
It's treated as an array, but we can not pass an array.
```
func getHighGrade(for grades: Int...) {
    print(grades.max())
}
getHighGrade(for: 80, 90, 0, 10, 50)
```
>output: 90

#### inout keyword
Normally, when passing a value into a func, it creates a copy of it and that copy is essentially a let constant and immutable in func body, which is the behavior wanted naturally. However, sometimes a func is needed to change a param directly, i.e., *copy-in*, *copy-out*.

Essentially, passing by reference.
```
var count = 10
func printVal(_ val: inout Int) {
    val += 1
}
printVal(&count)
print("Count", count)
```
>output: Count 11

### Closures
Anonymous function, or a function with no name.
Closures also do not have *argument label*, or *default params value*

```
var addClosure: (Int, Int) -> Int = { (a: Int, b: Int) in
    return a + b
}
```
or using type inference
```
var addClosure = { (a: Int, b: Int) in
    return a + b
}
```
and since it's only one statement in the closure body we can remove the *return* keyword
```
var addClosure = { (a: Int, b: Int) in
     a + b
}
```
also we can use short closure syntax, as $0 refers to the first param and $1 refers to param #2 aka **shorthand argument names**
```
var addClosure: (Int, Int) -> Int = { $0 + $1 }
```
a void closure is a closure that takes no param and returns nothing
```
let voidClosure: () -> Void = {
    print("Swift's void closure")
}
```

#### Trailing closure syntax


### Structs vs Classes

#### Structs
Structs are **value types** commonly described as blueprints. i.e. Int, Bool, Array, Double, Dictionary, String types are all structs.
Structs have both properties and methods. 

```
struct Wizard {
    
    var fName: String
    var lName: String
    
    var fullName: String {
        return fName + " " + lName
    }
}
```
we have not actually created a wizard; we've just defined a common way to do so, hinting at a blueprint

```
var newWiz = Wizard(fName: "Harry", lName: "Potter")
newWiz.fullName
```
>output: Harry Potter
structs also automatically generate an initializer known as **memberwise initializer**

```
var wizardFromAnotherHouse = newWiz
```
create a copy, or an entirely new struct with the same values of the original one.
```
wizardFromAnotherHouse.fName = "Helena"
wizardFromAnotherHouse.fullName
newWiz.fullName
```
>output: Helena Potter
>Harry Potter

values are different as structs are **value-types**

```
struct Wizard {
    
    var fName: String
    var lName: String
    var house: String = ""
    
    var fullName: String {
        return fName + " " + lName
    }
    
    mutating func changeWizardHouseTo(_ newHouse: String) {
        house = newHouse
    }
}
```
the **mutating** keyword tells the compiler to create a brand new copy of the struct, since we are changing a variable value inside the struct, we have to mark the function as mutating.
**mutating a struct actually create a new one based upon existing values**
```
wizardFromAnotherHouse.changeWizardHouseTo("Hufflepuff")
```
Structs are *infertile* they cannot inherit or be subclassed. Inheritance is only reserved for classes. 
#### Classes
Classes are reference types meaning classes objects reference the same value. 
As classes objects are stored in the heap, they only carry a reference to that value in the stack, which implies that when we change one of them, all references pointing to that object have the same value.

```
class A {
    var name: String
    var age: Int
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
```
classes do not offer an init by default and if they have stored properties that do not have initial values, they must have an init that initializes these values on object instantiation.

```
let detJake = A(name: "Jake", age: 30)
let detRosa = detJake
detRosa.name = "Rosa"

print(detJake.name)
```
>output: Rosa
both objects have the same value as they are merely a reference to the same object
when we declare ``` let detRosa = detJake``` we only create a new reference to the same thing.
also notice we can change a let object's var stored properties, even when we declared it as a constant, as again it's only a reference. If we want any value to not be changed we have to declare it as a constant in the class declaration itself.

##### Class convenience init
A convenience initializer makes it more convenient to init a class, by offering some default values and delegating the rest of the work to the designated init.
```
class A {
    var name: String
    var age: Int
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    convenience init(name: String) {
        self.init(name: name, age: 30)
    }
}
```
This makes it possible to init a class using only the name property.

##### Class inheritance
aka subclassing. In swift, a class can only inherit from one superclass. But a subclass can have many subclasses.
if a class doesn't inherit from any class it's called **base class**.
**Polymorphism**: A subclass can be treated as its own type or any of its super classes.
In inheritance, we can override a stored property, but we cannot override a computed property.

```
class B: A {
    func printNameAndAge() {
           print(super.name, super.age)
    }
}
```
if the subclass doesn't define it's own init, it automatically inherits all of its superclass's **designated** as well as **convenience** inits.
if we init an object using B class, we have both options for init, with name and age, and only with age (from the convenience init).

```
class B: A {
    
    override init(name: String, age: Int) {
        super.init(name: name, age: age)
    }
}
```
if the subclass overrides the suber class init, it still inherits the convenience init of the superclass.

```
class B: A {
    
    var gender: Character
    
    init(gender: Character) {
        self.gender = gender
        super.init(name: "Aem", age: 30)
    }
}
```
if the subclass chooses to define it's own init, it losses the inherited, both *designated and convenience*.

if we need the convenience init or even the designated init to be implemented in the subclasses regardless of whether they implement their own init or not, we can enforce that by using the **required** keyword.

```
class A {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    required convenience init(name: String) {
        self.init(name: name, age: 30)
    }
}

class B: A {
    
    var gender: Character
    
    init(gender: Character, name: String = "") {
        self.gender = gender
        super.init(name: name, age: 30)
    }
    
    required convenience init(name: String) {
        self.init(gender: "f", name: name)
    }

    func printNameAndAge() {
        print(super.name, super.age)
    }
}

let detAmy = B(name: "Amy")
```
By calling the required convenience init, it then calls the self.init with the name, which calls the super init

| Class    | Struct |
| ---      | ---       |
| Reference type | Value type        |
| Mutable even if declared constant     | immutable if declared constant      |
| Stored in heap    | Stored in stack    |
| Has inheritance, works with objc    | Thread safe, less memory leaks    |

The official apple advice is that we start with a struct when defining a new custom object, and only convert it to class when needed, i.e. it needs inheritance or needs to work with objc. 
