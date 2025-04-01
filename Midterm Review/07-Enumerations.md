# Enumerations

Swift enumerations (enums) are a powerful type that allow you to define a group of related values and work with those values in a type-safe way.

## Basic Enumerations

At their simplest, enums provide a way to work with a predefined set of values:

```swift
enum Direction {
    case north
    case east
    case south
    case west
}

// Alternate syntax with all cases on one line
enum Direction {
    case north, east, south, west
}

// Usage
let currentDirection = Direction.north

// Type inference allows for shorter syntax after the type is known
var windDirection = Direction.east
windDirection = .south  // Swift knows the type is Direction
```

### Using Enums in Switch Statements

Enums are particularly powerful when used with switch statements, as Swift ensures all cases are handled:

```swift
func getDirectionInstruction(for direction: Direction) -> String {
    switch direction {
    case .north:
        return "Go north"
    case .east:
        return "Go east"
    case .south:
        return "Go south"
    case .west:
        return "Go west"
    }
}

let instruction = getDirectionInstruction(for: .east)  // "Go east"
```

If you don't handle all cases, you need to include a `default` case:

```swift
func getSimpleInstruction(for direction: Direction) -> String {
    switch direction {
    case .north:
        return "Go up"
    case .south:
        return "Go down"
    default:
        return "Go sideways"
    }
}
```

## Raw Values

Enums can have raw values, which are values of the same type assigned to each case:

```swift
enum Planet: Int {
    case mercury = 1
    case venus
    case earth
    case mars
    case jupiter
    case saturn
    case uranus
    case neptune
}

// Access the raw value
let earthNumber = Planet.earth.rawValue  // 3 (auto-incremented from 1)
```

Common raw value types include:
- Int: Often for numerical representation or order
- String: Often when you want a string representation that matches the case name
- Double: For numerical values with decimal points
- Character: For single characters

```swift
enum CompassDirection: String {
    case north = "N"
    case east = "E"
    case south = "S"
    case west = "W"
}

let westSymbol = CompassDirection.west.rawValue  // "W"
```

With String raw values, if you don't specify a value, Swift uses the case name as the raw value:

```swift
enum Day: String {
    case monday, tuesday, wednesday, thursday, friday, saturday, sunday
}

let mondayString = Day.monday.rawValue  // "monday"
```

### Initializing from Raw Values

You can create an enum instance from a raw value, but this returns an optional since the raw value might not correspond to any case:

```swift
let possiblePlanet = Planet(rawValue: 3)  // Returns Planet.earth
let unknownPlanet = Planet(rawValue: 11)  // Returns nil (no planet with raw value 11)

// Safe usage with optional binding
if let planet = Planet(rawValue: 3) {
    print("Found planet: \(planet)")
} else {
    print("No planet found with that number")
}
```

## Associated Values

One of Swift's most powerful enum features is the ability to store associated values with each case:

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

// Create enum instances with associated values
let productBarcode = Barcode.upc(8, 85909, 51226, 3)
let websiteQRCode = Barcode.qrCode("https://www.example.com")
```

### Extracting Associated Values

You can extract associated values using pattern matching in a switch statement:

```swift
func scanBarcode(_ barcode: Barcode) {
    switch barcode {
    case .upc(let numberSystem, let manufacturer, let product, let check):
        print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
    case .qrCode(let productCode):
        print("QR code: \(productCode)")
    }
}

scanBarcode(productBarcode)  // "UPC: 8, 85909, 51226, 3"
```

You can also use a shorter syntax when all values should be constants or variables:

```swift
func scanBarcode(_ barcode: Barcode) {
    switch barcode {
    case let .upc(numberSystem, manufacturer, product, check):
        print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
    case let .qrCode(productCode):
        print("QR code: \(productCode)")
    }
}
```

## Enums with Methods and Properties

Swift enums can also have methods and computed properties:

```swift
enum Temperature {
    case celsius(Double)
    case fahrenheit(Double)
    
    var celsius: Double {
        switch self {
        case .celsius(let value):
            return value
        case .fahrenheit(let value):
            return (value - 32) * 5/9
        }
    }
    
    var fahrenheit: Double {
        switch self {
        case .celsius(let value):
            return value * 9/5 + 32
        case .fahrenheit(let value):
            return value
        }
    }
    
    func toString() -> String {
        switch self {
        case .celsius(let value):
            return "\(value)°C"
        case .fahrenheit(let value):
            return "\(value)°F"
        }
    }
}

let roomTemp = Temperature.celsius(22.5)
print(roomTemp.fahrenheit)  // 72.5
print(roomTemp.toString())  // "22.5°C"

let bodyTemp = Temperature.fahrenheit(98.6)
print(bodyTemp.celsius)     // 37.0
print(bodyTemp.toString())  // "98.6°F"
```

## Recursive Enumerations

Enums can reference themselves in associated values by using the `indirect` keyword:

```swift
// An arithmetic expression that can contain other expressions
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}

// Create an expression for (5 + 4) * 2
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let two = ArithmeticExpression.number(2)
let product = ArithmeticExpression.multiplication(sum, two)

// Evaluate the expression recursively
func evaluate(_ expression: ArithmeticExpression) -> Int {
    switch expression {
    case let .number(value):
        return value
    case let .addition(left, right):
        return evaluate(left) + evaluate(right)
    case let .multiplication(left, right):
        return evaluate(left) * evaluate(right)
    }
}

let result = evaluate(product)  // 18 ((5 + 4) * 2)
```

## CaseIterable Protocol

For enums that should be iterable, you can conform to the `CaseIterable` protocol:

```swift
enum Weekday: CaseIterable {
    case monday, tuesday, wednesday, thursday, friday, saturday, sunday
}

// Access all cases
let allWeekdays = Weekday.allCases
print("There are \(allWeekdays.count) days in a week")

// Iterate through all cases
for day in Weekday.allCases {
    print(day)
}
```

Note: Enums with associated values cannot conform to CaseIterable automatically.

## Common Use Cases for Enums

1. **State Management**
```swift
enum ConnectionState {
    case disconnected
    case connecting
    case connected
    case disconnecting
}
```

2. **Result Types**
```swift
enum Result<Success, Failure: Error> {
    case success(Success)
    case failure(Failure)
}
```

3. **Configuration Options**
```swift
enum MapViewType {
    case standard
    case satellite
    case hybrid
}
```

4. **API Endpoints**
```swift
enum APIEndpoint {
    case login
    case fetchUserProfile(userId: String)
    case updateUserSettings(userId: String, settings: [String: Any])
}
```

5. **Error Types**
```swift
enum NetworkError: Error {
    case invalidURL
    case serverError(statusCode: Int)
    case noData
    case decodingError(description: String)
}
```

## Review Questions

1. What is the difference between a raw value and an associated value in an enum?
2. How would you create an enum to represent different payment methods like cash, credit card (with card number), and bank transfer (with account number)?
3. Why might you use an enum with associated values instead of separate classes or structs?
4. How would you add a method to an enum that calculates a value based on the current case?
5. What does the `CaseIterable` protocol provide, and when would you use it? 