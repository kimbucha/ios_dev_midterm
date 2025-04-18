# iOS Development Midterm Review: Sample Questions

This document contains sample questions covering all topics from weeks 1-7 of the iOS development course. Use these questions to test your understanding and prepare for the midterm exam.

## 1. Xcode and Development Environment

1. **Multiple Choice**: What happens when you try to open a project created with a newer version of Xcode in an older version?
   - A) It works without any issues
   - B) It opens but with limited functionality
   - C) It automatically downgrades the project format
   - D) It cannot open the project

2. **Short Answer**: Explain the purpose of the Organization Identifier when creating a new Xcode project.

3. **True/False**: When working in a team, it's recommended that all team members use different versions of Xcode to ensure compatibility across all Apple devices.

4. **Multiple Choice**: Which of the following project templates allows you to target multiple Apple platforms with a single codebase?
   - A) iOS App
   - B) Multiplatform App
   - C) Universal App
   - D) Cross-Platform App

5. **Short Answer**: What is the difference between the simulator and running your app on a physical device? List at least two differences.

---

## 2. Swift UI vs UI Kit

6. **Multiple Choice**: Which framework uses a declarative syntax for building user interfaces?
   - A) UI Kit
   - B) Swift UI
   - C) Both
   - D) Neither

7. **Short Answer**: Compare and contrast the basic structure of a UI Kit view controller and a Swift UI view.

8. **True/False**: Swift UI requires iOS 13 or later, while UI Kit works on earlier iOS versions.

9. **Multiple Choice**: In UI Kit, how do you connect UI elements from Interface Builder to your code?
   - A) Using outlets and actions
   - B) Using binding variables
   - C) Using the @State property wrapper
   - D) Using the Canvas preview

10. **Short Answer**: Explain how you would implement a button that toggles the visibility of a text label in both Swift UI and UI Kit.

---

## 3. Swift Language Basics

11. **Multiple Choice**: What is the difference between `let` and `var` in Swift?
    - A) `let` is for global variables, `var` is for local variables
    - B) `let` is for declaring classes, `var` is for declaring structs
    - C) `let` declares constants, `var` declares variables
    - D) `let` is for numeric values, `var` is for strings and collections

12. **Short Answer**: Explain what optional values are in Swift and why they are useful.

13. **True/False**: In Swift, arrays and dictionaries are value types, not reference types.

14. **Multiple Choice**: What does the following code do? `let displayName = name ?? "Anonymous"`
    - A) Assigns "Anonymous" to displayName if name contains "Anonymous"
    - B) Assigns the value of name to displayName, or "Anonymous" if name is nil
    - C) Checks if name is equal to "Anonymous"
    - D) Creates a tuple with name and "Anonymous"

15. **Short Answer**: Write Swift code to safely unwrap an optional value using both if-let binding and guard-let statements.

---

## 4. App Architecture

16. **Multiple Choice**: Which architectural pattern is built into UI Kit by default?
    - A) MVVM (Model-View-ViewModel)
    - B) MVC (Model-View-Controller) 
    - C) MVP (Model-View-Presenter)
    - D) VIPER

17. **Short Answer**: Explain why the Model and View components should not communicate directly in the MVC pattern.

18. **True/False**: Swift UI naturally encourages an MVVM architecture pattern due to its reactive and declarative nature.

19. **Multiple Choice**: In MVVM, which component is responsible for transforming Model data into a format that can be displayed by the View?
    - A) Model
    - B) View
    - C) Controller
    - D) ViewModel

20. **Short Answer**: Compare how data binding works in MVVM implementations for UI Kit versus Swift UI.

---

## 5. UI Components and Layout

21. **Multiple Choice**: In Swift UI, which stack arranges its children horizontally?
    - A) VStack
    - B) HStack
    - C) ZStack
    - D) WStack

22. **Short Answer**: Explain how Auto Layout works in UI Kit and how it differs from the layout system in Swift UI.

23. **True/False**: In Swift UI, a List component is roughly equivalent to a UITableView in UI Kit.

24. **Multiple Choice**: What property wrapper is used to create two-way bindings in Swift UI text fields?
    - A) @State
    - B) @Binding
    - C) @ObservedObject
    - D) @Environment

25. **Short Answer**: Describe how you would create a form with multiple input fields and a submit button in Swift UI.

---

## 6. Delegation Pattern

26. **Multiple Choice**: What is a key reason for using the weak reference for delegates?
    - A) To improve performance
    - B) To avoid retain cycles and memory leaks
    - C) To allow multiple delegates
    - D) To enable optional delegate methods

27. **Short Answer**: Explain the three key components of the delegation pattern and their roles.

28. **True/False**: In Swift, delegate protocols must always inherit from AnyObject.

29. **Multiple Choice**: Which of the following UI Kit components does NOT use delegation?
    - A) UITableView
    - B) UITextField
    - C) UIButton
    - D) UIPickerView

30. **Short Answer**: Write code to define a custom delegation pattern for passing data back from a child view controller to its parent.

---

## 7. Enumerations

31. **Multiple Choice**: Which statement about Swift enums is false?
    - A) Enums can have methods
    - B) Enums can have computed properties
    - C) Enums can have stored properties
    - D) Enums can have associated values

32. **Short Answer**: Explain the difference between raw values and associated values in Swift enumerations.

33. **True/False**: Swift enums with associated values can automatically conform to the CaseIterable protocol.

34. **Multiple Choice**: What does the `indirect` keyword allow in Swift enumerations?
    - A) Makes the enum cases mutable
    - B) Allows enums to have static methods
    - C) Enables recursive enumeration definitions
    - D) Creates type aliases for enum cases

35. **Short Answer**: Write a Swift enum to represent different payment methods (cash, credit card with number, and bank transfer with account details).

---

## 8. Functions and Closures

36. **Multiple Choice**: What makes a closure "escaping" in Swift?
    - A) It captures values from its surrounding context
    - B) It's stored for execution after the function returns
    - C) It uses shorthand argument names like $0
    - D) It's passed as an argument to another function

37. **Short Answer**: Explain how capturing values works in closures and potential memory considerations.

38. **True/False**: In Swift, functions are first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions.

39. **Multiple Choice**: What is the purpose of the `[weak self]` syntax in a closure?
    - A) To create a strong reference to self
    - B) To break potential retain cycles
    - C) To make self optional in the closure
    - D) To prevent access to self's properties

40. **Short Answer**: Rewrite the following anonymous function with the most concise Swift syntax: 
    
    ```swift
    array.filter({ (number: Int) -> Bool in
        return number % 2 == 0
    })
    ```

---

## 9. Example Projects

41. **Multiple Choice**: In the Tip Calculator example, which UI component would you use to let users select from predefined tip percentages in UI Kit?
    - A) UISegmentedControl
    - B) UIPickerView
    - C) UISlider
    - D) UIStepper

42. **Short Answer**: Describe how you would implement the To-Do List app's item completion toggling functionality in both Swift UI and UI Kit.

43. **True/False**: In the Swift UI To-Do List app implementation, each view directly updates the data model when a change occurs.

44. **Multiple Choice**: Which feature of Swift UI makes it easier to update the UI when a task is marked as completed in the To-Do app?
    - A) @State property wrapper
    - B) ObservableObject and @Published properties
    - C) Automatic view reloading
    - D) Imperative UI updates

45. **Short Answer**: Describe how the MVC architecture manifests in the UI Kit tip calculator project, identifying each component's responsibility.

---

## 10. Swift Features and Best Practices

46. **Multiple Choice**: What is the primary purpose of using a guard statement in Swift?
    - A) To protect variables from being changed
    - B) To implement the delegation pattern
    - C) To handle early returns and improve code readability
    - D) To create thread-safe access to variables

47. **Short Answer**: Explain what property wrappers are in Swift and give at least two examples of built-in property wrappers used in Swift UI.

48. **True/False**: In Swift, it's generally preferred to use `let` (constants) over `var` (variables) when the value doesn't need to change.

49. **Multiple Choice**: Which higher-order function would you use to convert an array of strings to an array of integers, removing any values that couldn't be converted?
    - A) map
    - B) filter
    - C) compactMap
    - D) reduce

50. **Short Answer**: Describe the concept of type inference in Swift and how it helps write more concise code.

---

## Answer Key

### Xcode and Development Environment
**1. What happens when you try to open a project created with a newer version of Xcode in an older version?**  
    D) It cannot open the project

**2. Explain the purpose of the Organization Identifier when creating a new Xcode project.**  
    The Organization Identifier is a unique string (typically a reverse domain name) that identifies you or your organization. Combined with the product name, it creates a unique bundle identifier for your app.

**3. When working in a team, it's recommended that all team members use different versions of Xcode to ensure compatibility across all Apple devices.**  
    False

**4. Which of the following project templates allows you to target multiple Apple platforms with a single codebase?**  
    B) Multiplatform App

**5. What is the difference between the simulator and running your app on a physical device?**  
    Simulators run on your Mac, are faster to deploy to, but can't test hardware-specific features like camera or accelerometer. Physical devices provide real-world testing but require developer accounts and provisioning.

### Swift UI vs UI Kit
**6. Which framework uses a declarative syntax for building user interfaces?**  
    B) Swift UI

**7. Compare and contrast the basic structure of a UI Kit view controller and a Swift UI view.**  
    UI Kit uses a class-based approach with UIViewController where UI is separate and connected with outlets/actions. Swift UI uses structs conforming to View protocol with a body property that defines the UI declaratively.

**8. Swift UI requires iOS 13 or later, while UI Kit works on earlier iOS versions.**  
    True

**9. In UI Kit, how do you connect UI elements from Interface Builder to your code?**  
    A) Using outlets and actions

**10. Explain how you would implement a button that toggles the visibility of a text label in both Swift UI and UI Kit.**  
    In Swift UI: Use @State variable and conditional view rendering. In UI Kit: Create IBOutlet to the label and IBAction for the button, toggle isHidden property.

### Swift Language Basics
**11. What is the difference between `let` and `var` in Swift?**  
    C) `let` declares constants, `var` declares variables

**12. Explain what optional values are in Swift and why they are useful.**  
    Optionals represent values that might be absent (nil). They prevent crashes by forcing explicit unwrapping or safe handling of potentially missing values.

**13. In Swift, arrays and dictionaries are value types, not reference types.**  
    True

**14. What does the following code do? `let displayName = name ?? "Anonymous"`**  
    B) Assigns the value of name to displayName, or "Anonymous" if name is nil

**15. Write Swift code to safely unwrap an optional value using both if-let binding and guard-let statements.**  
```swift
// Using if-let binding
if let unwrapped = optional { 
    // Use unwrapped value
} else { 
    // Handle nil case 
}

// Using guard-let statement
guard let unwrapped = optional else { 
    // Handle nil case
    return 
}
// Use unwrapped value
```

### App Architecture
**16. Which architectural pattern is built into UI Kit by default?**  
    B) MVC (Model-View-Controller)

**17. Explain why the Model and View components should not communicate directly in the MVC pattern.**  
    Keeping Model and View separate creates better separation of concerns, improves testability, allows components to evolve independently, and enables reuse across different interfaces.

**18. Swift UI naturally encourages an MVVM architecture pattern due to its reactive and declarative nature.**  
    True

**19. In MVVM, which component is responsible for transforming Model data into a format that can be displayed by the View?**  
    D) ViewModel

**20. Compare how data binding works in MVVM implementations for UI Kit versus Swift UI.**  
    In UI Kit: Manually implemented using closures, delegation, or KVO.  
    In Swift UI: Automatic with ObservableObject, @Published properties, and property wrappers like @ObservedObject.

### UI Components and Layout
**21. In Swift UI, which stack arranges its children horizontally?**  
    B) HStack

**22. Explain how Auto Layout works in UI Kit and how it differs from the layout system in Swift UI.**  
    Auto Layout in UI Kit uses constraints to define relationships between views. Swift UI uses a declarative approach with stacks (VStack, HStack, ZStack) and modifiers.

**23. In Swift UI, a List component is roughly equivalent to a UITableView in UI Kit.**  
    True

**24. What property wrapper is used to create two-way bindings in Swift UI text fields?**  
    B) @Binding

**25. Describe how you would create a form with multiple input fields and a submit button in Swift UI.**  
    Create a Form container with Sections for organization. Use TextField for text input, Toggle for boolean values, and add a Button for submission, all connected to @State variables.

### Delegation Pattern
**26. What is a key reason for using the weak reference for delegates?**  
    B) To avoid retain cycles and memory leaks

**27. Explain the three key components of the delegation pattern and their roles.**  
    1) Protocol: defines methods the delegate must implement.  
    2) Delegator: object that sends messages to its delegate.  
    3) Delegate: object that implements the protocol and receives messages.

**28. In Swift, delegate protocols must always inherit from AnyObject.**  
    False (only if they have optional methods that require @objc)

**29. Which of the following UI Kit components does NOT use delegation?**  
    C) UIButton

**30. Write code to define a custom delegation pattern for passing data back from a child view controller to its parent.**  
```swift
// 1. Define the protocol
protocol ColorSelectedDelegate: AnyObject {
    func didSelectColor(_ color: UIColor)
}

// 2. Create the child view controller with a delegate property
class ColorPickerViewController: UIViewController {
    weak var delegate: ColorSelectedDelegate?
    
    func colorButtonTapped(_ sender: UIButton) {
        // When a color is selected, notify the delegate
        delegate?.didSelectColor(sender.backgroundColor ?? .white)
        dismiss(animated: true)
    }
}

// 3. Implement the protocol in the parent view controller
class ParentViewController: UIViewController, ColorSelectedDelegate {
    func didSelectColor(_ color: UIColor) {
        // Handle the selected color
        view.backgroundColor = color
    }
    
    func showColorPicker() {
        let colorPicker = ColorPickerViewController()
        colorPicker.delegate = self
        present(colorPicker, animated: true)
    }
}
```

### Enumerations
**31. Which statement about Swift enums is false?**  
    C) Enums can have stored properties

**32. Explain the difference between raw values and associated values in Swift enumerations.**  
    Raw values are fixed values of the same type for all cases, defined at compile time.  
    Associated values are dynamic values of potentially different types attached to individual cases at runtime.

**33. Swift enums with associated values can automatically conform to the CaseIterable protocol.**  
    False

**34. What does the `indirect` keyword allow in Swift enumerations?**  
    C) Enables recursive enumeration definitions

**35. Write a Swift enum to represent different payment methods (cash, credit card with number, and bank transfer with account details).**  
```swift
enum PaymentMethod {
    case cash
    case creditCard(number: String)
    case bankTransfer(accountNumber: String, routingNumber: String)
}
```

### Functions and Closures
**36. What makes a closure "escaping" in Swift?**  
    B) It's stored for execution after the function returns

**37. Explain how capturing values works in closures and potential memory considerations.**  
    Closures capture and store references to variables from surrounding context. This can create strong reference cycles if self is captured strongly in a closure that's also held by self.

**38. In Swift, functions are first-class citizens, meaning they can be assigned to variables, passed as arguments, and returned from other functions.**  
    True

**39. What is the purpose of the `[weak self]` syntax in a closure?**  
    B) To break potential retain cycles

**40. Rewrite the following anonymous function with the most concise Swift syntax:**  
```swift
array.filter { $0 % 2 == 0 }
```

### Example Projects
**41. In the Tip Calculator example, which UI component would you use to let users select from predefined tip percentages in UI Kit?**  
    A) UISegmentedControl

**42. Describe how you would implement the To-Do List app's item completion toggling functionality in both Swift UI and UI Kit.**  
    In Swift UI: Update a @State or @Published boolean property on the task model and use that in conditional styling.  
    In UI Kit: Update a property in the data model when a cell is tapped, then reload that cell to reflect the new state.

**43. In the Swift UI To-Do List app implementation, each view directly updates the data model when a change occurs.**  
    False

**44. Which feature of Swift UI makes it easier to update the UI when a task is marked as completed in the To-Do app?**  
    B) ObservableObject and @Published properties

**45. Describe how the MVC architecture manifests in the UI Kit tip calculator project, identifying each component's responsibility.**  
    Model: TipCalculator struct with business logic.  
    View: Storyboard UI elements (labels, text field, etc.).  
Controller: TipCalculatorViewController connecting user input to model calculations and updating the view.

### Swift Features and Best Practices
**46. What is the primary purpose of using a guard statement in Swift?**  
    C) To handle early returns and improve code readability

**47. Explain what property wrappers are in Swift and give at least two examples of built-in property wrappers used in Swift UI.**  
    Property wrappers add behavior to properties. Examples:  
        - @State (manages mutable state in views)  
        - @Binding (creates two-way connection)  
        - @ObservedObject (observes external objects)  
        - @Environment (accesses shared values)

**48. In Swift, it's generally preferred to use `let` (constants) over `var` (variables) when the value doesn't need to change.**  
    True

**49. Which higher-order function would you use to convert an array of strings to an array of integers, removing any values that couldn't be converted?**  
    C) compactMap

**50. Describe the concept of type inference in Swift and how it helps write more concise code.**  
    Type inference allows Swift to automatically determine variable types from their initialization values, reducing explicit type annotations and making code more concise while maintaining type safety. 