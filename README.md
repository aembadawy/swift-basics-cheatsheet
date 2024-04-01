# swift-basics-cheatsheet

### Variable & Constants declaraation 

Variables declaared using *var*, constants using *let*

```
var num: Int = 10
let pi: Float = 3.14159
let name: String = "Aem"
var isRight: Bool = true
```
or using swift type-inferance
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

