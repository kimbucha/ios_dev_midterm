# Swift Language Basics

Swift is Apple's modern programming language designed for safety, performance, and expressiveness. This section covers the fundamental Swift concepts needed for iOS development.

## Variables and Constants

### Variables (var)

Variables are used when the value needs to change over time:

```swift
var score = 0
score = 10 // Can be changed
```

### Constants (let)

Constants are used when the value won't change once set (preferred when possible):

```swift
let maximumScore = 100
// maximumScore = 200 // This would cause a compile error
```

## Basic Data Types

Swift has type inference, but you can also explicitly declare types:

### Numeric Types

```swift
let integer: Int = 42
let float: Float = 3.14159
let double: Double = 3.14159265359 // Default for floating-point numbers
```

### Text Types

```swift
let character: Character = "A"
let string: String = "Hello, Swift!"

// String interpolation
let name = "John"
let greeting = "Hello, \(name)!"
```

### Boolean Type

```swift
let isEnabled: Bool = true
let isDisabled = false
```

### Collections

**Arrays** - Ordered collections of values:
```swift
let fruits: [String] = ["Apple", "Banana", "Orange"]
var dynamicArray = [1, 2, 3]
dynamicArray.append(4)
let firstFruit = fruits[0] // Accessing by index
```

**Dictionaries** - Key-value collections:
```swift
let heights: [String: Double] = ["Taylor": 1.78, "John": 1.82]
var settings = ["theme": "dark", "notifications": "enabled"]
settings["sound"] = "on" // Adding a new key-value pair
let johnsHeight = heights["John"] // Accessing by key
```

**Sets** - Unordered collections of unique values:
```swift
let primaryColors: Set<String> = ["Red", "Blue", "Yellow"]
var numbers: Set = [1, 2, 3, 4]
numbers.insert(5)
```

## Type Inference and Type Safety

Swift can infer the type from the initial value:

```swift
let name = "Swift" // Inferred as String
let version = 5.5 // Inferred as Double
let isAwesome = true // Inferred as Bool
```

Swift is type-safe, meaning you can't accidentally use a value of the wrong type:

```swift
let text = "42"
// let number = text + 10 // Error: Cannot add String and Int
let number = Int(text)! + 10 // Correct: Convert then add
```

## Control Flow

### Conditionals

**if-else statements**:
```swift
let temperature = 25

if temperature > 30 {
    print("It's hot outside")
} else if temperature > 20 {
    print("It's nice outside")
} else {
    print("It's cold outside")
}
```

**switch statements**:
```swift
let weatherCondition = "rain"

switch weatherCondition {
case "sun":
    print("Bring sunglasses")
case "rain":
    print("Bring an umbrella")
case "snow":
    print("Bring a coat")
default:
    print("Check the weather forecast")
}
```

### Loops

**for-in loops**:
```swift
// Looping through ranges
for i in 1...5 {
    print(i) // Prints 1, 2, 3, 4, 5
}

// Looping through collections
let animals = ["dog", "cat", "bird"]
for animal in animals {
    print("I have a \(animal)")
}

// Looping through dictionaries
let weights = ["apple": 0.1, "banana": 0.2]
for (fruit, weight) in weights {
    print("\(fruit) weighs \(weight)kg")
}
```

**while loops**:
```swift
var count = 3
while count > 0 {
    print("\(count)...")
    count -= 1
}
print("Go!")
```

**repeat-while loops** (execute at least once):
```swift
var number = 1
repeat {
    print(number)
    number *= 2
} while number < 100
```

## Functions

### Basic Function Declaration

```swift
func greet(person: String) -> String {
    return "Hello, \(person)!"
}

let greeting = greet(person: "Taylor")
```

### Parameters and Return Values

```swift
// Multiple parameters
func calculateArea(width: Double, height: Double) -> Double {
    return width * height
}
let area = calculateArea(width: 5.0, height: 3.0)

// No return value
func printDetails(name: String, age: Int) {
    print("\(name) is \(age) years old")
}
printDetails(name: "Alice", age: 25)

// Multiple return values using tuples
func getMinMax(array: [Int]) -> (min: Int, max: Int) {
    return (array.min() ?? 0, array.max() ?? 0)
}
let bounds = getMinMax(array: [8, 3, 9, 4])
print("Min: \(bounds.min), Max: \(bounds.max)")
```

### Parameter Labels and Default Values

```swift
// External and internal parameter names
func greet(to person: String, with message: String) -> String {
    return "\(message), \(person)!"
}
let customGreeting = greet(to: "Bob", with: "Good morning")

// Default parameter values
func greet(person: String, formally: Bool = false) -> String {
    if formally {
        return "Hello, \(person), how do you do?"
    } else {
        return "Hi, \(person)!"
    }
}
greet(person: "Tim") // Uses default value for formally
greet(person: "Sir Tim", formally: true) // Overrides default
```

## Optionals

Optionals are a core Swift feature for handling the absence of a value.

### Basic Optional Syntax

```swift
// Declaring optionals
var name: String? = "John"
var age: Int? = nil

// Accessing optional values
if name != nil {
    print("Name is \(name!)") // Force unwrapping with !
}
```

### Optional Binding

```swift
// if-let binding
if let unwrappedName = name {
    print("Name is \(unwrappedName)")
} else {
    print("Name is nil")
}

// guard-let binding (early exit pattern)
func greet(person: String?) {
    guard let unwrappedPerson = person else {
        print("No name provided")
        return
    }
    
    print("Hello, \(unwrappedPerson)!")
}
```

### Nil Coalescing Operator

```swift
// Provide a default value if the optional is nil
let displayName = name ?? "Anonymous"
```

### Optional Chaining

```swift
// Safely access properties and methods on optionals
struct Person {
    var name: String
    var address: Address?
}

struct Address {
    var street: String
    var city: String
}

let person: Person? = Person(name: "Jane", address: nil)
let street = person?.address?.street // Result is nil, no crash
```

### Implicitly Unwrapped Optionals

```swift
// Used when a value starts as nil but will definitely have a value before use
var requiredName: String! = nil
// Later in code:
requiredName = "Required Name"
let count = requiredName.count // No need for unwrapping
```

## Type Casting

```swift
// Checking types
let items: [Any] = [1, "Hello", true, 4.5]

for item in items {
    if item is Int {
        print("Found an integer: \(item)")
    } else if item is String {
        print("Found a string: \(item)")
    }
}

// Downcasting
for item in items {
    if let number = item as? Int {
        print("Integer: \(number)")
    } else if let text = item as? String {
        print("String: \(text)")
    }
}
```

## Review Questions

1. What is the difference between `var` and `let` in Swift, and when should you use each?
2. How does optional binding work, and why is it safer than force unwrapping?
3. Explain the difference between an Array, a Dictionary, and a Set in Swift.
4. What is type inference, and how does it make Swift code more concise?
5. How do you safely handle optional values in Swift? Describe at least three different approaches. 