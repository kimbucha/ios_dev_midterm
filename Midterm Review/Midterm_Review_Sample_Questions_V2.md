# iOS Development Midterm Review: Sample Questions (Version 2)

This document contains a new set of sample questions covering topics from weeks 1-7 of the iOS development course, based on the lecture transcripts. Use these questions to further test your understanding and prepare for the midterm exam.

## 1. Xcode and Development Environment

1. **Short Answer**: Why is it generally recommended for team members working on the same Xcode project to use the *same* version of Xcode?

2. **Multiple Choice**: When creating a new project targeting iOS only, which "Interface" option corresponds to using the UI Kit framework?
   - A) Swift UI
   - B) Storyboard
   - C) XIB
   - D) Programmatic

3. **True/False**: The Multiplatform App template in Xcode allows you to use UI Kit for the macOS target.

4. **Short Answer**: What is the purpose of the Xcode Simulator, and name one limitation it has compared to a physical device?

5. **Multiple Choice**: Which file format does Interface Builder (Storyboard/XIB) primarily use under the hood to store UI layouts?
   - A) JSON
   - B) Swift Code
   - C) XML
   - D) Binary Plist

---

## 2. Swift UI vs UI Kit

6. **Short Answer**: Explain the core difference between imperative and declarative UI programming paradigms, giving an example related to hiding a label.

7. **True/False**: In Swift UI, the Canvas preview directly modifies the underlying Storyboard file.

8. **Multiple Choice**: What is the Swift UI equivalent of a `UIViewController` in UI Kit for managing a screen's content?
   - A) `UIView`
   - B) A struct conforming to the `View` protocol
   - C) `UIWindow`
   - D) `UIApplicationDelegate`

9. **Short Answer**: How does Swift UI handle UI updates when a state variable changes, and how does this differ fundamentally from typical UI Kit updates? (Hint: Analogy discussed in lectures).

10. **Multiple Choice**: Which property wrapper is commonly used in Swift UI to represent mutable state owned by a specific view?
    - A) `@Binding`
    - B) `@State`
    - C) `@ObservedObject`
    - D) `@EnvironmentObject`

---

## 3. Swift Language Basics

11. **Short Answer**: What is an optional in Swift, and what problem does it solve, particularly regarding type conversions (e.g., `String` to `Double`)?

12. **Multiple Choice**: Which of the following safely unwraps an optional `Double?` named `optionalValue` and assigns it to `unwrappedValue` if it's not `nil`?
    - A) `let unwrappedValue = optionalValue!`
    - B) `guard let unwrappedValue = optionalValue else { return }`
    - C) `let unwrappedValue: Double = optionalValue`
    - D) `let unwrappedValue = optionalValue ?? defaultDouble`

13. **True/False**: Classes in Swift are value types, meaning they are copied when assigned or passed to functions.

14. **Short Answer**: Explain type inference in Swift. Give an example.

15. **Multiple Choice**: What is the difference between initializing a class property inline (`var name: String = "Default"`) versus initializing it within an `init()` method?
    - A) There is no difference
    - B) Inline initialization happens for all instances; init() can vary based on parameters
    - C) Inline initialization is only for constants; init() is for variables
    - D) Inline initialization only works for built-in types; init() is needed for custom types

---

## 4. App Architecture

16. **Short Answer**: What are the three main components of the MVC (Model-View-Controller) pattern, and what is the primary responsibility of each?

17. **True/False**: In a strict MVC implementation, the Model should directly update the View when its data changes.

18. **Multiple Choice**: Which architectural pattern does Swift UI's state management system naturally lend itself to?
    - A) MVC
    - B) VIPER
    - C) MVVM
    - D) MVP

19. **Short Answer**: Why is separating components (like Model, View, Controller/ViewModel) beneficial in software architecture? Name two benefits.

20. **Multiple Choice**: In the context of MVC for UI Kit, where does the `UIViewController` subclass typically fit?
    - A) Model
    - B) View
    - C) Controller
    - D) ViewModel

---

## 5. UI Components and Layout

21. **Short Answer**: What is the purpose of `VStack`, `HStack`, and `ZStack` in Swift UI?

22. **Multiple Choice**: In UI Kit, how are relationships and positioning between UI elements typically defined when using Auto Layout?
    - A) Frame-based coordinates
    - B) Constraints
    - C) Stack Views only
    - D) Size classes only

23. **True/False**: A `UITextField` in UI Kit and a `TextField` in Swift UI both require a `@Binding` to manage their text content.

24. **Short Answer**: What is the purpose of the `Spacer` view in Swift UI layout?

25. **Multiple Choice**: Which UI Kit component is functionally similar to Swift UI's `Picker` for selecting from a list of options?
    - A) `UISegmentedControl`
    - B) `UIPickerView`
    - C) `UISlider`
    - D) `UIStepper`

---

## 6. Delegation Pattern

26. **Short Answer**: What is the main purpose of the Delegation pattern?

27. **Multiple Choice**: In the delegation pattern, which component defines the "contract" or set of methods that the delegate must (or can) implement?
    - A) The Delegator
    - B) The Delegate
    - C) The Protocol
    - D) The View Controller

28. **True/False**: A delegate property should typically be declared as `strong` to ensure it doesn't get deallocated prematurely.

29. **Short Answer**: Name two common UI Kit classes that heavily rely on the delegation pattern.

30. **Multiple Choice**: When passing data back from a presented `UIViewController` (Child) to the presenting `UIViewController` (Parent) using delegation, where is the delegate typically set?
    - A) In the Child's `viewDidLoad`
    - B) In the Parent's `prepare(for:sender:)` method
    - C) In the App Delegate
    - D) In the Scene Delegate

---

## 7. Enumerations

31. **Short Answer**: Besides providing a restricted set of named values, what is a key feature of Swift enums that distinguishes them from enums in many other languages (hint: related to Optionals)?

32. **Multiple Choice**: Which keyword allows an enum case to store additional information of a specific type?
    - A) `rawvalue`
    - B) `indirect`
    - C) Associated Value (syntax like `case success(Data)`)
    - D) `static`

33. **True/False**: An enum can have both raw values (e.g., `enum MyEnum: String`) and associated values within the same definition.

34. **Short Answer**: How can you iterate over all cases of an enum, and what protocol conformance is required?

35. **Multiple Choice**: If `Optional<T>` is implemented as an enum, what would the two cases likely represent?
    - A) `case value(T)`, `case error(Error)`
    - B) `case some(T)`, `case none`
    - C) `case valid(T)`, `case invalid`
    - D) `case present(T)`, `case absent`

---

## 8. Functions and Closures

36. **Short Answer**: What does it mean for functions to be "first-class citizens" in Swift?

37. **Multiple Choice**: What is the type signature of a function that takes an Int and a String and returns a Bool?
    - A) `(Int, String) -> Bool`
    - B) `Function<Int, String, Bool>`
    - C) `[Int, String]: Bool`
    - D) `func(Int, String) -> Bool`

38. **True/False**: A closure is essentially a named function that can be passed around.

39. **Short Answer**: Explain what an "escaping" closure is and why it might be marked with `@escaping`.

40. **Multiple Choice**: In the context of closures, what potential memory management issue does `[weak self]` help prevent?
    - A) Stack overflow
    - B) Nil pointer exceptions
    - C) Retain cycles
    - D) Dangling pointers

---

## 9. Example Projects

41. **Short Answer**: In the simple UI Kit toggle app, what was the role of the `IBAction` and the `IBOutlet`?

42. **Multiple Choice**: In the Swift UI Tip Calculator, how was the `TextField`'s input connected to a variable in the view?
    - A) Using an `IBOutlet`
    - B) Using `@State` and `@Binding` (implicitly via `TextField(value: $amount, ...)` syntax)
    - C) Using Delegation
    - D) Using `NotificationCenter`

43. **True/False**: The UI Kit Tip Calculator used Auto Layout constraints defined in the Storyboard.

44. **Short Answer**: Describe how the `Picker` was populated with tip percentage options in the Swift UI Tip Calculator.

45. **Multiple Choice**: Which pattern was used in the UI Kit Tip Calculator to send the selected tip percentage back from the `TipViewController` to the `CalculationViewController`?
    - A) `@Binding`
    - B) `NotificationCenter`
    - C) KVO (Key-Value Observing)
    - D) Delegation

---

## 10. Swift Features and Best Practices

46. **Short Answer**: What is the benefit of using formatters (like `NumberFormatter` or `.formatted()`) for displaying currency or percentages?

47. **True/False**: Swift's type safety features, like optionals, primarily aim to catch errors at runtime rather than compile time.

48. **Multiple Choice**: When should you generally prefer using `let` over `var`?
    - A) When the value might be `nil`
    - B) When the value will not change after initialization
    - C) When working with classes
    - D) When working with collections

49. **Short Answer**: What is the purpose of the `guard let` statement compared to `if let`?

50. **True/False**: Swift arrays (`[Type]`) can hold elements of different types without any special considerations.

---

## Answer Key (Version 2)

### Xcode and Development Environment
**1. Why is it generally recommended for team members working on the same Xcode project to use the *same* version of Xcode?**  
Newer Xcode versions might introduce project format changes or rely on newer SDK features, making the project unable to be opened or built correctly in older Xcode versions.

**2. When creating a new project targeting iOS only, which "Interface" option corresponds to using the UI Kit framework?**  
B) Storyboard

**3. The Multiplatform App template in Xcode allows you to use UI Kit for the macOS target.**  
False (*Multiplatform uses Swift UI across all targets*)

**4. What is the purpose of the Xcode Simulator, and name one limitation it has compared to a physical device?**  
The Simulator allows developers to run and test their iOS/iPadOS/etc. apps on their Mac without needing a physical device. A limitation is that it cannot simulate hardware-specific features like the camera, accelerometer, GPS (accurately), or cellular connectivity.

**5. Which file format does Interface Builder (Storyboard/XIB) primarily use under the hood to store UI layouts?**  
C) XML

### Swift UI vs UI Kit
**6. Explain the core difference between imperative and declarative UI programming paradigms, giving an example related to hiding a label.**  
Imperative: You command the UI step-by-step (e.g., "label, set your isHidden property to true"). Declarative: You declare the desired state, and the framework updates the UI to match (e.g., "if showLabel is false, the label isn't part of the view").

**7. In Swift UI, the Canvas preview directly modifies the underlying Storyboard file.**  
False (*The Canvas renders Swift UI code; Storyboards are separate XML files edited via Interface Builder for UI Kit.*)

**8. What is the Swift UI equivalent of a `UIViewController` in UI Kit for managing a screen's content?**  
B) A struct conforming to the `View` protocol

**9. How does Swift UI handle UI updates when a state variable changes, and how does this differ fundamentally from typical UI Kit updates?**  
When state changes, Swift UI conceptually tears down the affected part of the view hierarchy and rebuilds it based on the new state. UI Kit typically involves finding the specific UI element and directly modifying its properties.

**10. Which property wrapper is commonly used in Swift UI to represent mutable state owned by a specific view?**  
B) `@State`

### Swift Language Basics
**11. What is an optional in Swift, and what problem does it solve, particularly regarding type conversions?**  
An optional represents a value that might be present or absent (`nil`). It solves the problem of representing failure or absence in a type-safe way, e.g., when converting a `String` to `Double`, the result is `Double?` because the conversion might fail if the string isn't a valid number.

**12. Which of the following safely unwraps an optional `Double?` named `optionalValue` and assigns it to `unwrappedValue` if it's not `nil`?**  
B) `guard let unwrappedValue = optionalValue else { return }`

**13. Classes in Swift are value types, meaning they are copied when assigned or passed to functions.**  
False (*Classes are reference types; structs are value types.*)

**14. Explain type inference in Swift. Give an example.**  
Type inference allows Swift to deduce the type of a variable or constant from its initial value, so you don't always have to explicitly declare the type. Example: `let message = "Hello"` infers `message` is a `String`.

**15. What is the difference between initializing a class property inline versus initializing it within an `init()` method?**  
B) Inline initialization happens for all instances; init() can vary based on parameters

### App Architecture
**16. What are the three main components of the MVC (Model-View-Controller) pattern, and what is the primary responsibility of each?**  
Model: Holds the application data and business logic. View: Displays the data to the user and presents the UI. Controller: Mediates between Model and View, handling user input and updating the Model/View.

**17. In a strict MVC implementation, the Model should directly update the View when its data changes.**  
False (*Communication should go through the Controller.*)

**18. Which architectural pattern does Swift UI's state management system naturally lend itself to?**  
C) MVVM

**19. Why is separating components (like Model, View, Controller/ViewModel) beneficial in software architecture? Name two benefits.**  
1) Improved Maintainability/Readability: Code is organized logically. 2) Increased Reusability: Components (especially Model, sometimes View) can be reused elsewhere. 3) Easier Testability: Components can be tested in isolation.

**20. In the context of MVC for UI Kit, where does the `UIViewController` subclass typically fit?**  
C) Controller

### UI Components and Layout
**21. What is the purpose of `VStack`, `HStack`, and `ZStack` in Swift UI?**  
They are layout containers. `VStack` arranges children vertically, `HStack` arranges them horizontally, and `ZStack` overlays children on top of each other (back-to-front).

**22. In UI Kit, how are relationships and positioning between UI elements typically defined when using Auto Layout?**  
B) Constraints

**23. A `UITextField` in UI Kit and a `TextField` in Swift UI both require a `@Binding` to manage their text content.**  
False (*`UITextField` often uses the delegate pattern or target-action; `TextField` in Swift UI uses `@Binding`.*)

**24. What is the purpose of the `Spacer` view in Swift UI layout?**  
`Spacer` expands to take up available space within a stack (`VStack` or `HStack`), pushing other content.

**25. Which UI Kit component is functionally similar to Swift UI's `Picker` for selecting from a list of options?**  
B) `UIPickerView`

### Delegation Pattern
**26. What is the main purpose of the Delegation pattern?**  
To allow one object (the delegator) to customize its behavior or be notified of events by another object (the delegate) without needing to know the specific class of the delegate, promoting loose coupling.

**27. In the delegation pattern, which component defines the "contract" or set of methods that the delegate must (or can) implement?**  
C) The Protocol

**28. A delegate property should typically be declared as `strong` to ensure it doesn't get deallocated prematurely.**  
False (*Delegate properties should be `weak` to prevent retain cycles.*)

**29. Name two common UI Kit classes that heavily rely on the delegation pattern.**  
`UITableView`, `UITextField`, `UIPickerView`, `UIScrollView` (many others).

**30. When passing data back from a presented `UIViewController` (Child) to the presenting `UIViewController` (Parent) using delegation, where is the delegate typically set?**  
B) In the Parent's `prepare(for:sender:)` method

### Enumerations
**31. Besides providing a restricted set of named values, what is a key feature of Swift enums that distinguishes them from enums in many other languages?**  
Associated Values: Swift enum cases can store values of other types, which vary per case (e.g., `Optional.some(value)` stores the actual value).

**32. Which keyword allows an enum case to store additional information of a specific type?**  
C) Associated Value (syntax like `case success(Data)`)

**33. An enum can have both raw values (e.g., `enum MyEnum: String`) and associated values within the same definition.**  
False (*An enum can have EITHER raw values OR associated values, not both directly in the main definition.*)

**34. How can you iterate over all cases of an enum, and what protocol conformance is required?**  
Conform the enum to the `CaseIterable` protocol, then access the static `allCases` property (which returns an array of all cases).

**35. If `Optional<T>` is implemented as an enum, what would the two cases likely represent?**  
B) `case some(T)`, `case none`

### Functions and Closures
**36. What does it mean for functions to be "first-class citizens" in Swift?**  
Functions can be treated like any other value: assigned to variables/constants, passed as arguments to other functions, and returned from functions.

**37. What is the type signature of a function that takes an Int and a String and returns a Bool?**  
A) `(Int, String) -> Bool`

**38. A closure is essentially a named function that can be passed around.**  
False (*A closure is typically an unnamed block of code that can capture values from its surrounding context. Named functions can be assigned to variables or passed, but the term closure usually refers to the anonymous form.*)

**39. Explain what an "escaping" closure is and why it might be marked with `@escaping`.**  
An escaping closure is one that is called *after* the function it was passed into returns (e.g., stored for later execution, used in an async callback). It must be marked `@escaping` so the compiler knows it needs to manage memory potentially beyond the function's scope.

**40. In the context of closures, what potential memory management issue does `[weak self]` help prevent?**  
C) Retain cycles

### Example Projects
**41. In the simple UI Kit toggle app, what was the role of the `IBAction` and the `IBOutlet`?**  
`IBAction`: A method linked to a UI event (like a button tap) triggered from Interface Builder. `IBOutlet`: A property linked to a UI element in Interface Builder, allowing the code to reference and modify that element.

**42. In the Swift UI Tip Calculator, how was the `TextField`'s input connected to a variable in the view?**  
B) Using `@State` and `@Binding` (implicitly via `TextField(value: $amount, ...)` syntax)

**43. The UI Kit Tip Calculator used Auto Layout constraints defined in the Storyboard.**  
True

**44. Describe how the `Picker` was populated with tip percentage options in the Swift UI Tip Calculator.**  
Using a `ForEach` loop within the `Picker`'s content view, iterating over an array of `Double` percentage values. Each value was displayed as `Text`, formatted using `.formatted(.percent)`.

**45. Which pattern was used in the UI Kit Tip Calculator to send the selected tip percentage back from the `TipViewController` to the `CalculationViewController`?**  
D) Delegation

### Swift Features and Best Practices
**46. What is the benefit of using formatters (like `NumberFormatter` or `.formatted()`) for displaying currency or percentages?**  
They handle localization automatically, displaying currency symbols, decimal separators, grouping separators, and percentage signs according to the user's device region settings.

**47. Swift's type safety features, like optionals, primarily aim to catch errors at runtime rather than compile time.**  
False (*Swift's type safety aims to catch many errors, especially those related to type mismatches and `nil` handling, at compile time.*)

**48. When should you generally prefer using `let` over `var`?**  
B) When the value will not change after initialization

**49. What is the purpose of the `guard let` statement compared to `if let`?**  
`guard let` is used for early exits. If the optional contains a value, it's unwrapped and made available for the rest of the scope; if it's `nil`, the `else` block (which must exit the current scope, e.g., with `return`, `break`, `throw`) is executed. `if let` unwraps the optional only for the scope of the `if` block.

**50. Swift arrays (`[Type]`) can hold elements of different types without any special considerations.**  
False (*Swift arrays are strongly typed; a standard `[Type]` array can only hold elements of that specific `Type`.*) 