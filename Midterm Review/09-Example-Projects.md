# Example Projects

This section examines key example projects covered in the course, explaining their architecture, implementation details, and the concepts they demonstrate.

## Basic UI Kit vs Swift UI Project

The first project demonstrated the differences between UI Kit and Swift UI by building a simple app that showed and hid a label when a button was pressed.

### UI Kit Implementation

```swift
import UIKit

class ViewController: UIViewController {
    
    // MARK: - Outlets
    @IBOutlet weak var helloLabel: UILabel!
    
    // MARK: - Actions
    @IBAction func buttonPressed(_ sender: UIButton) {
        // Toggle visibility of the label
        helloLabel.isHidden = !helloLabel.isHidden
        
        // Update button text based on label visibility
        if helloLabel.isHidden {
            sender.setTitle("Show", for: .normal)
        } else {
            sender.setTitle("Hide", for: .normal)
        }
    }
    
    // MARK: - Lifecycle Methods
    override func viewDidLoad() {
        super.viewDidLoad()
        // Initial setup
        helloLabel.text = "Hello, World!"
    }
}
```

Key UI Kit concepts:
- Using Interface Builder (Storyboard) for layout
- Connecting UI elements to code with IBOutlet and IBAction
- Manipulating UI elements imperatively
- View controller lifecycle methods

### Swift UI Implementation

```swift
import SwiftUI

struct ContentView: View {
    @State private var isLabelVisible = true
    
    var body: some View {
        VStack {
            if isLabelVisible {
                Text("Hello, World!")
                    .padding()
            }
            
            Button(action: {
                // Toggle visibility
                isLabelVisible.toggle()
            }) {
                Text(isLabelVisible ? "Hide" : "Show")
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(10)
            }
        }
    }
}
```

Key Swift UI concepts:
- Declarative UI syntax
- State management with @State
- Conditional view rendering
- Implicit animations and transitions
- No need for outlets or explicit connections

## Tip Calculator Project

This project demonstrates more advanced UI components, user input handling, and separation of concerns through architecture patterns.

### Model

```swift
struct TipCalculator {
    // Business logic for calculating tips
    func calculateTip(amount: Double, percentage: Double) -> Double {
        return amount * percentage / 100.0
    }
    
    func calculateTotal(amount: Double, tip: Double) -> Double {
        return amount + tip
    }
}
```

### Swift UI Implementation 

```swift
import SwiftUI

struct TipCalculatorView: View {
    // State variables for user input
    @State private var billAmount = ""
    @State private var tipPercentage = 15.0
    @State private var tipAmount = 0.0
    @State private var totalAmount = 0.0
    
    // Available tip percentages
    let tipPercentages = [10.0, 15.0, 18.0, 20.0, 25.0]
    
    // Calculator model
    let calculator = TipCalculator()
    
    var body: some View {
        Form {
            Section(header: Text("Bill Details")) {
                TextField("Bill Amount", text: $billAmount)
                    .keyboardType(.decimalPad)
                
                Picker("Tip Percentage", selection: $tipPercentage) {
                    ForEach(tipPercentages, id: \.self) { percentage in
                        Text("\(Int(percentage))%")
                    }
                }
                .pickerStyle(SegmentedPickerStyle())
            }
            
            Section(header: Text("Result")) {
                Button("Calculate") {
                    calculateTip()
                }
                
                HStack {
                    Text("Tip:")
                    Spacer()
                    Text("$\(tipAmount, specifier: "%.2f")")
                }
                
                HStack {
                    Text("Total:")
                    Spacer()
                    Text("$\(totalAmount, specifier: "%.2f")")
                }
            }
        }
        .navigationTitle("Tip Calculator")
    }
    
    func calculateTip() {
        // Convert string input to Double
        guard let amount = Double(billAmount) else { return }
        
        // Use model to perform calculations
        tipAmount = calculator.calculateTip(amount: amount, percentage: tipPercentage)
        totalAmount = calculator.calculateTotal(amount: amount, tip: tipAmount)
    }
}
```

### UI Kit Implementation with MVC

#### Model

Same as above.

#### View Controller

```swift
import UIKit

class TipCalculatorViewController: UIViewController {
    
    // MARK: - Outlets
    @IBOutlet weak var amountTextField: UITextField!
    @IBOutlet weak var tipPercentageSegmentedControl: UISegmentedControl!
    @IBOutlet weak var tipAmountLabel: UILabel!
    @IBOutlet weak var totalAmountLabel: UILabel!
    
    // MARK: - Properties
    let tipPercentages = [10.0, 15.0, 18.0, 20.0, 25.0]
    let calculator = TipCalculator()
    
    // MARK: - Lifecycle Methods
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Setup UI
        title = "Tip Calculator"
        amountTextField.keyboardType = .decimalPad
        
        // Configure segmented control
        tipPercentageSegmentedControl.removeAllSegments()
        for (index, percentage) in tipPercentages.enumerated() {
            tipPercentageSegmentedControl.insertSegment(withTitle: "\(Int(percentage))%", at: index, animated: false)
        }
        tipPercentageSegmentedControl.selectedSegmentIndex = 1 // Default to 15%
        
        // Initial labels
        tipAmountLabel.text = "$0.00"
        totalAmountLabel.text = "$0.00"
    }
    
    // MARK: - Actions
    @IBAction func calculateButtonTapped(_ sender: UIButton) {
        calculateTip()
    }
    
    @IBAction func tipPercentageChanged(_ sender: UISegmentedControl) {
        calculateTip()
    }
    
    // MARK: - Helper Methods
    func calculateTip() {
        // Dismiss keyboard
        amountTextField.resignFirstResponder()
        
        // Get bill amount
        guard let amountText = amountTextField.text, 
              let amount = Double(amountText) else { return }
        
        // Get selected percentage
        let selectedIndex = tipPercentageSegmentedControl.selectedSegmentIndex
        let percentage = tipPercentages[selectedIndex]
        
        // Calculate
        let tip = calculator.calculateTip(amount: amount, percentage: percentage)
        let total = calculator.calculateTotal(amount: amount, tip: tip)
        
        // Update UI
        tipAmountLabel.text = String(format: "$%.2f", tip)
        totalAmountLabel.text = String(format: "$%.2f", total)
    }
}
```

### Key Architectural Concepts

#### MVC in the UI Kit Implementation

1. **Model**: The `TipCalculator` struct contains the business logic for calculating tips and totals
2. **View**: The storyboard elements (text field, segmented control, labels, button)
3. **Controller**: The `TipCalculatorViewController` class that connects the model and view, handling user input and updating the UI

#### MVVM in the Swift UI Implementation

While not explicitly using MVVM classes, Swift UI naturally encourages an MVVM-like separation:

1. **Model**: The `TipCalculator` struct with business logic
2. **View**: The `TipCalculatorView` struct defining the UI
3. **ViewModel**: The state variables and calculation methods in the view struct function as a rudimentary view model

## To-Do List App

This project demonstrates table views, delegation, and basic data management.

### Swift UI Implementation

```swift
import SwiftUI

// Model
struct TodoItem: Identifiable {
    let id = UUID()
    var title: String
    var isCompleted: Bool = false
}

// ViewModel
class TodoListViewModel: ObservableObject {
    @Published var items: [TodoItem] = []
    @Published var newItemTitle = ""
    
    func addItem() {
        guard !newItemTitle.isEmpty else { return }
        items.append(TodoItem(title: newItemTitle))
        newItemTitle = ""
    }
    
    func toggleItemCompletion(at index: Int) {
        items[index].isCompleted.toggle()
    }
    
    func deleteItem(at offsets: IndexSet) {
        items.remove(atOffsets: offsets)
    }
}

// View
struct TodoListView: View {
    @StateObject private var viewModel = TodoListViewModel()
    
    var body: some View {
        NavigationView {
            VStack {
                // New item input
                HStack {
                    TextField("New task", text: $viewModel.newItemTitle)
                        .textFieldStyle(RoundedBorderTextFieldStyle())
                    
                    Button(action: viewModel.addItem) {
                        Image(systemName: "plus.circle.fill")
                            .foregroundColor(.blue)
                            .font(.title)
                    }
                }
                .padding()
                
                // Todo list
                List {
                    ForEach(viewModel.items.indices, id: \.self) { index in
                        let item = viewModel.items[index]
                        HStack {
                            Image(systemName: item.isCompleted ? "checkmark.circle.fill" : "circle")
                                .foregroundColor(item.isCompleted ? .green : .gray)
                            
                            Text(item.title)
                                .strikethrough(item.isCompleted)
                                .foregroundColor(item.isCompleted ? .gray : .primary)
                            
                            Spacer()
                        }
                        .contentShape(Rectangle())
                        .onTapGesture {
                            viewModel.toggleItemCompletion(at: index)
                        }
                    }
                    .onDelete(perform: viewModel.deleteItem)
                }
            }
            .navigationTitle("To-Do List")
        }
    }
}
```

### UI Kit Implementation with Delegation

```swift
import UIKit

// MARK: - Model
struct TodoItem {
    var title: String
    var isCompleted: Bool = false
}

// MARK: - Controller
class TodoListViewController: UIViewController {
    
    // MARK: - Outlets
    @IBOutlet weak var tableView: UITableView!
    @IBOutlet weak var newItemTextField: UITextField!
    
    // MARK: - Properties
    var items: [TodoItem] = []
    
    // MARK: - Lifecycle Methods
    override func viewDidLoad() {
        super.viewDidLoad()
        
        title = "To-Do List"
        
        // Configure table view
        tableView.delegate = self
        tableView.dataSource = self
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "TodoCell")
    }
    
    // MARK: - Actions
    @IBAction func addButtonTapped(_ sender: UIButton) {
        guard let title = newItemTextField.text, !title.isEmpty else { return }
        
        // Add new item
        items.append(TodoItem(title: title))
        
        // Clear text field
        newItemTextField.text = ""
        
        // Update table view
        tableView.reloadData()
    }
}

// MARK: - UITableViewDataSource
extension TodoListViewController: UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return items.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "TodoCell", for: indexPath)
        let item = items[indexPath.row]
        
        // Configure cell
        var content = cell.defaultContentConfiguration()
        content.text = item.title
        
        if item.isCompleted {
            content.textProperties.strikethroughStyle = .single
            content.textProperties.color = .gray
            cell.accessoryType = .checkmark
        } else {
            content.textProperties.strikethroughStyle = .none
            content.textProperties.color = .label
            cell.accessoryType = .none
        }
        
        cell.contentConfiguration = content
        return cell
    }
    
    func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        if editingStyle == .delete {
            items.remove(at: indexPath.row)
            tableView.deleteRows(at: [indexPath], with: .automatic)
        }
    }
}

// MARK: - UITableViewDelegate
extension TodoListViewController: UITableViewDelegate {
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)
        
        // Toggle completion status
        items[indexPath.row].isCompleted.toggle()
        
        // Update cell
        tableView.reloadRows(at: [indexPath], with: .automatic)
    }
}
```

### Key Concepts Demonstrated

1. **UI Kit Table View and Delegation**
   - UITableViewDataSource for providing data to the table
   - UITableViewDelegate for handling user interactions
   - Cell reuse for efficient scrolling performance
   - Editing capabilities (deletion of items)

2. **Swift UI List and State Management**
   - ObservableObject for reactive data updates
   - @Published for automatically notifying views of changes
   - List component with ForEach and onDelete modifiers
   - Built-in handling of user interactions

3. **MVVM in Swift UI**
   - Clear separation of View (TodoListView) and ViewModel (TodoListViewModel)
   - State management through the ViewModel
   - ViewModel handles business logic while View handles presentation

## Review Questions

1. What are the key differences in how the Tip Calculator is implemented in Swift UI versus UI Kit?
2. How does the delegation pattern work in the UI Kit To-Do List app? Identify the delegator and delegate objects.
3. How does Swift UI's declarative approach to UI creation differ from UI Kit's imperative approach in the example projects?
4. In the Swift UI To-Do List app, how is data updated and reflected in the UI when a task is marked as completed?
5. How does the MVC architecture manifest in the UI Kit implementation of the Tip Calculator project? 