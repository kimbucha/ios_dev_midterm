# Delegation Pattern

The delegation pattern is a fundamental design pattern in iOS development, especially when working with UI Kit. It allows one object to communicate with another without them being tightly coupled.

## Understanding Delegation

### Conceptual Overview

Delegation is a design pattern that enables an object to "delegate" or "hand off" some of its responsibilities to another object.

Imagine a real-world scenario:
1. A manager (delegator) assigns a task to an employee (delegate)
2. The employee performs the task
3. The employee reports back to the manager when the task is complete

In this scenario:
- The manager doesn't need to know how the task is performed
- The employee doesn't need to know why the task is needed
- They can work together without being tightly coupled

### Key Components

1. **Protocol (contract)**: Defines the methods the delegate must implement
2. **Delegator (source)**: The object that sends messages to its delegate
3. **Delegate (receiver)**: The object that implements the protocol and receives messages

## Delegation in UI Kit

UI Kit uses delegation extensively for event handling and customization.

### Built-in UI Kit Delegates

Many UI Kit components use delegation for configuration and event handling:

```swift
// UITableView uses two delegate patterns:
// 1. UITableViewDataSource - Provides data
// 2. UITableViewDelegate - Handles events

class MyTableViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
    
    let tableView = UITableView()
    let items = ["Item 1", "Item 2", "Item 3"]
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Set the controller as both the data source and delegate
        tableView.dataSource = self
        tableView.delegate = self
        
        // Setup table view
        view.addSubview(tableView)
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Cell")
    }
    
    // MARK: - UITableViewDataSource
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return items.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath)
        cell.textLabel?.text = items[indexPath.row]
        return cell
    }
    
    // MARK: - UITableViewDelegate
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        print("Selected \(items[indexPath.row])")
        tableView.deselectRow(at: indexPath, animated: true)
    }
}
```

Other common UI Kit delegate examples:
- UITextField uses UITextFieldDelegate for handling text changes and keyboard events
- UIScrollView uses UIScrollViewDelegate for monitoring scroll behavior
- UIPickerView uses UIPickerViewDelegate and UIPickerViewDataSource for content and selection

## Creating Custom Delegates

### Step 1: Define a Protocol

First, define a protocol that outlines the methods your delegate should implement:

```swift
protocol TaskDelegate: AnyObject {
    func taskCompleted(result: String)
    func taskFailed(error: Error)
    
    // Optional method using @objc optional
    @objc optional func taskProgress(percent: Float)
}
```

Note: To make methods optional, the protocol must be marked with `@objc` and inherit from `AnyObject`.

### Step 2: Create the Delegator (Source)

Next, create the class that will send messages to its delegate:

```swift
class TaskManager {
    // Use weak reference to avoid retain cycles
    weak var delegate: TaskDelegate?
    
    func performTask() {
        // Simulate work
        print("Starting task...")
        
        // Notify progress (optional method)
        delegate?.taskProgress?(percent: 0.5)
        
        // Simulate successful completion
        if Bool.random() {
            delegate?.taskCompleted(result: "Task completed successfully")
        } else {
            let error = NSError(domain: "TaskError", code: 1, userInfo: [NSLocalizedDescriptionKey: "Failed to complete task"])
            delegate?.taskFailed(error: error)
        }
    }
}
```

### Step 3: Implement the Delegate (Receiver)

Finally, create a class that implements the delegate protocol:

```swift
class TaskViewController: UIViewController, TaskDelegate {
    
    let taskManager = TaskManager()
    let statusLabel = UILabel()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Set up UI
        statusLabel.text = "Ready to start"
        view.addSubview(statusLabel)
        
        // Set self as the delegate
        taskManager.delegate = self
        
        // Start the task
        taskManager.performTask()
    }
    
    // MARK: - TaskDelegate
    
    func taskCompleted(result: String) {
        statusLabel.text = result
        statusLabel.textColor = .green
    }
    
    func taskFailed(error: Error) {
        statusLabel.text = error.localizedDescription
        statusLabel.textColor = .red
    }
    
    func taskProgress(percent: Float) {
        print("Task is \(percent * 100)% complete")
    }
}
```

## Communication Between View Controllers

Delegation is particularly useful for communication between view controllers.

### Passing Data Back from a Child View Controller

```swift
// STEP 1: Define the protocol
protocol ColorSelectionDelegate: AnyObject {
    func colorSelected(_ color: UIColor)
}

// STEP 2: Create the child view controller (delegator)
class ColorPickerViewController: UIViewController {
    
    weak var delegate: ColorSelectionDelegate?
    
    private let colors: [UIColor] = [.red, .green, .blue, .yellow, .purple]
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupColorButtons()
    }
    
    private func setupColorButtons() {
        let stackView = UIStackView()
        stackView.axis = .vertical
        stackView.spacing = 10
        stackView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(stackView)
        
        NSLayoutConstraint.activate([
            stackView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            stackView.centerYAnchor.constraint(equalTo: view.centerYAnchor),
            stackView.widthAnchor.constraint(equalToConstant: 200)
        ])
        
        for color in colors {
            let button = UIButton(type: .system)
            button.backgroundColor = color
            button.setTitle(color.accessibilityName, for: .normal)
            button.setTitleColor(.white, for: .normal)
            button.heightAnchor.constraint(equalToConstant: 44).isActive = true
            button.layer.cornerRadius = 8
            button.addTarget(self, action: #selector(colorButtonTapped(_:)), for: .touchUpInside)
            stackView.addArrangedSubview(button)
        }
    }
    
    @objc private func colorButtonTapped(_ sender: UIButton) {
        guard let color = sender.backgroundColor else { return }
        
        // Notify the delegate
        delegate?.colorSelected(color)
        
        // Dismiss this view controller
        dismiss(animated: true)
    }
}

// STEP 3: Implement the delegate in the parent view controller
class MainViewController: UIViewController, ColorSelectionDelegate {
    
    private let colorView = UIView()
    private let selectColorButton = UIButton(type: .system)
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
    }
    
    private func setupUI() {
        // Set up color view
        colorView.backgroundColor = .gray
        colorView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(colorView)
        
        // Set up button
        selectColorButton.setTitle("Select Color", for: .normal)
        selectColorButton.addTarget(self, action: #selector(selectColorTapped), for: .touchUpInside)
        selectColorButton.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(selectColorButton)
        
        NSLayoutConstraint.activate([
            colorView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            colorView.centerYAnchor.constraint(equalTo: view.centerYAnchor, constant: -50),
            colorView.widthAnchor.constraint(equalToConstant: 200),
            colorView.heightAnchor.constraint(equalToConstant: 200),
            
            selectColorButton.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            selectColorButton.topAnchor.constraint(equalTo: colorView.bottomAnchor, constant: 20)
        ])
    }
    
    @objc private func selectColorTapped() {
        let colorPicker = ColorPickerViewController()
        colorPicker.delegate = self
        present(colorPicker, animated: true)
    }
    
    // MARK: - ColorSelectionDelegate
    
    func colorSelected(_ color: UIColor) {
        // Update the color view with the selected color
        colorView.backgroundColor = color
    }
}
```

## Best Practices for Delegation

1. **Use weak references for delegates**
   - To avoid retain cycles (memory leaks), always declare delegate properties as `weak`
   - This requires delegates to be reference types (classes), not value types (structs or enums)

2. **Make protocols descriptive**
   - Name protocols clearly: `[Class]Delegate` or `[Feature]Delegate`
   - Method names should clearly indicate what happened: `didSelect`, `willAppear`, etc.

3. **Consider optional methods when appropriate**
   - Required methods: Core functionality that must be implemented
   - Optional methods: Additional customization that can be ignored

4. **Keep delegate methods focused**
   - Each method should handle a specific event or responsibility
   - Avoid passing the delegator as a parameter unless needed

5. **Separate delegate protocols when responsibilities differ**
   - UITableView uses separate protocols for data (UITableViewDataSource) and events (UITableViewDelegate)

## Alternatives to Delegation

While delegation is powerful, other communication patterns may be better suited for certain scenarios:

- **Closures/Callbacks**: For simple, one-off communication
- **Notification Center**: For broadcasting events to multiple listeners
- **KVO (Key-Value Observing)**: For observing property changes on objects
- **Combine (iOS 13+)**: For reactive programming with publishers and subscribers

## Review Questions

1. What are the three key components in the delegation pattern, and what is the role of each?
2. Why do we typically declare delegate properties as `weak`? What problem does this solve?
3. What is the difference between a required and an optional delegate method? How do you define each?
4. In what scenarios is delegation particularly useful compared to direct method calls?
5. How would you implement a delegate pattern to enable a child view controller to pass data back to its parent? 