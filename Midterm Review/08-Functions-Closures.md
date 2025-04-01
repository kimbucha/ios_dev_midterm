# Functions and Closures

Functions and closures are essential components in Swift for organizing code and enabling powerful patterns like asynchronous programming and functional programming.

## Functions as First-Class Citizens

In Swift, functions are first-class citizens, which means they can be:
- Assigned to variables and constants
- Passed as arguments to other functions
- Returned from other functions

This flexibility enables powerful programming patterns that are essential for iOS development.

## Function Types

Every function has a specific type consisting of the function's parameter types and return type:

```swift
// A function that takes an Int and returns a String
func convertToString(_ number: Int) -> String {
    return String(number)
}

// The type of this function is: (Int) -> String
let stringConverter: (Int) -> String = convertToString

// Using the function through the variable
let result = stringConverter(42)  // "42"
```

## Functions as Arguments

Functions can be passed as arguments to other functions:

```swift
func applyOperation(_ a: Int, _ b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func multiply(_ a: Int, _ b: Int) -> Int {
    return a * b
}

// Passing named functions as arguments
let sum = applyOperation(5, 3, operation: add)        // 8
let product = applyOperation(5, 3, operation: multiply)  // 15
```

## Closures

Closures are self-contained blocks of functionality that can be passed around and used in your code. They are essentially unnamed functions.

### Basic Closure Syntax

```swift
// Function version
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

// Equivalent closure expression
let addClosure = { (a: Int, b: Int) -> Int in
    return a + b
}

// Usage
let sum = addClosure(5, 3)  // 8
```

### Shorthand Syntax

Swift provides several ways to write closures more concisely:

```swift
// Full syntax
let numbers = [1, 2, 3, 4, 5]
let doubled = numbers.map({ (number: Int) -> Int in
    return number * 2
})

// Inferring parameter and return types
let doubled = numbers.map({ number in
    return number * 2
})

// Implicit return for single-expression closures
let doubled = numbers.map({ number in number * 2 })

// Shorthand argument names ($0, $1, etc.)
let doubled = numbers.map({ $0 * 2 })

// Trailing closure syntax when closure is the last argument
let doubled = numbers.map { $0 * 2 }
```

### Capturing Values

Closures can capture and store references to variables and constants from the surrounding context:

```swift
func makeIncrementer(incrementAmount: Int) -> () -> Int {
    var total = 0
    
    // This closure captures both total and incrementAmount
    let incrementer = {
        total += incrementAmount
        return total
    }
    
    return incrementer
}

let incrementByTen = makeIncrementer(incrementAmount: 10)
print(incrementByTen())  // 10
print(incrementByTen())  // 20
print(incrementByTen())  // 30

// Each closure has its own captured variables
let incrementByFive = makeIncrementer(incrementAmount: 5)
print(incrementByFive())  // 5
print(incrementByFive())  // 10
```

### Escaping Closures

When a closure is passed as an argument to a function and is stored for later execution (after the function returns), it needs to be marked as `@escaping`:

```swift
// This closure might be called after the function returns
func fetchData(completion: @escaping (Data) -> Void) {
    // Simulate network request
    DispatchQueue.global().async {
        let data = Data()  // Pretend this is real data
        
        // Call the closure after the function has returned
        DispatchQueue.main.async {
            completion(data)
        }
    }
}

// Usage
fetchData { data in
    print("Received data: \(data)")
}
```

Non-escaping closures (the default) are guaranteed to be called before the function returns, which allows the compiler to apply certain optimizations.

## Functions and Closures for Asynchronous Code

### Callback Pattern

The traditional way to handle asynchronous operations in Swift uses completion handler closures:

```swift
func fetchUserData(userId: String, completion: @escaping (Result<User, Error>) -> Void) {
    // Simulate network request
    DispatchQueue.global().async {
        if userId.isEmpty {
            let error = NSError(domain: "com.example", code: 1, userInfo: [NSLocalizedDescriptionKey: "Invalid user ID"])
            completion(.failure(error))
            return
        }
        
        // Simulate successful response
        let user = User(id: userId, name: "John Doe", email: "john@example.com")
        completion(.success(user))
    }
}

// Usage
fetchUserData(userId: "123") { result in
    switch result {
    case .success(let user):
        print("Fetched user: \(user.name)")
    case .failure(let error):
        print("Error: \(error.localizedDescription)")
    }
}
```

### Callback Chains

Before modern async/await, handling sequences of asynchronous operations led to nested callbacks:

```swift
func fetchUserProfile(userId: String, completion: @escaping (Result<User, Error>) -> Void) {
    // First fetch the user
    fetchUserData(userId: userId) { result in
        switch result {
        case .success(let user):
            // Then fetch their posts
            fetchUserPosts(userId: userId) { postsResult in
                switch postsResult {
                case .success(let posts):
                    // Combine the data
                    var user = user
                    user.posts = posts
                    completion(.success(user))
                case .failure(let error):
                    completion(.failure(error))
                }
            }
        case .failure(let error):
            completion(.failure(error))
        }
    }
}
```

This pattern can lead to "callback hell" or the "pyramid of doom" as nesting deepens.

## Functional Programming with Functions and Closures

Swift's standard library includes several higher-order functions that take closures as arguments:

### Map

Transform each element in a collection:

```swift
let numbers = [1, 2, 3, 4, 5]
let squared = numbers.map { $0 * $0 }  // [1, 4, 9, 16, 25]
```

### Filter

Select elements that satisfy a condition:

```swift
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let evenNumbers = numbers.filter { $0 % 2 == 0 }  // [2, 4, 6, 8, 10]
```

### Reduce

Combine all elements to produce a single value:

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0) { $0 + $1 }  // 15
let product = numbers.reduce(1) { $0 * $1 }  // 120
```

### CompactMap

Transform elements and remove nil results:

```swift
let strings = ["1", "2", "three", "4", "five"]
let numbers = strings.compactMap { Int($0) }  // [1, 2, 4]
```

### FlatMap

Transform each element into a sequence and flatten the results:

```swift
let nestedArrays = [[1, 2], [3, 4], [5, 6]]
let flattened = nestedArrays.flatMap { $0 }  // [1, 2, 3, 4, 5, 6]
```

## Closures in Swift UI

Swift UI extensively uses closures for event handling and view updates:

```swift
struct ContentView: View {
    @State private var count = 0
    
    var body: some View {
        VStack {
            Text("Count: \(count)")
                .padding()
            
            Button("Increment") {
                // This is a closure
                count += 1
            }
            
            // Closure in a modifier
            .onChange(of: count) { newValue in
                print("Count changed to \(newValue)")
            }
        }
    }
}
```

## Type Aliases for Function Types

For complex function types, you can create type aliases to improve readability:

```swift
// Without type alias
func performNetworkRequest(completion: @escaping (Result<[String: Any], Error>) -> Void) {
    // Implementation
}

// With type alias
typealias NetworkCompletion = (Result<[String: Any], Error>) -> Void

func performNetworkRequest(completion: @escaping NetworkCompletion) {
    // Implementation
}
```

## Review Questions

1. What is the difference between a function and a closure in Swift?
2. Why would you mark a closure parameter with `@escaping`, and what does it indicate?
3. How would you use a closure to implement a custom sorting function for an array of custom objects?
4. Explain the capture list in closures and why you might use `[weak self]` in a closure.
5. How do higher-order functions like `map`, `filter`, and `reduce` simplify common programming tasks? 