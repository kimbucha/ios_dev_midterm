# UI Components

This section covers the essential UI components that you'll use to build iOS applications using both Swift UI and UI Kit.

## Common UI Elements

### Text Display

#### Swift UI
```swift
// Simple text
Text("Hello, World!")
    .font(.title)
    .foregroundColor(.blue)
    .padding()
    
// Styled text
Text("Important").bold() + Text(" information").italic()

// Multiline text
Text("This is a long text that will automatically wrap to multiple lines when it reaches the edge of its container.")
    .lineLimit(3)
    .truncationMode(.tail)
```

#### UI Kit
```swift
// UILabel
let label = UILabel()
label.text = "Hello, World!"
label.font = UIFont.systemFont(ofSize: 24, weight: .bold)
label.textColor = .blue
label.numberOfLines = 0 // Multiline
view.addSubview(label)
```

### Buttons

#### Swift UI
```swift
Button(action: {
    print("Button tapped!")
}) {
    Text("Tap Me")
        .padding()
        .background(Color.blue)
        .foregroundColor(.white)
        .cornerRadius(10)
}

// Icon button
Button(action: { print("Saved!") }) {
    Image(systemName: "heart.fill")
        .foregroundColor(.red)
}
```

#### UI Kit
```swift
// UIButton
let button = UIButton(type: .system)
button.setTitle("Tap Me", for: .normal)
button.backgroundColor = .blue
button.setTitleColor(.white, for: .normal)
button.layer.cornerRadius = 10
button.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)
view.addSubview(button)

@objc func buttonTapped() {
    print("Button tapped!")
}
```

### Text Input

#### Swift UI
```swift
@State private var text = ""

TextField("Enter your name", text: $text)
    .padding()
    .textFieldStyle(RoundedBorderTextFieldStyle())
    
// Secure field for passwords
@State private var password = ""
SecureField("Password", text: $password)
    .padding()
    .textFieldStyle(RoundedBorderTextFieldStyle())
```

#### UI Kit
```swift
// UITextField
let textField = UITextField()
textField.placeholder = "Enter your name"
textField.borderStyle = .roundedRect
textField.delegate = self // Implement UITextFieldDelegate
view.addSubview(textField)

// For passwords
let passwordField = UITextField()
passwordField.placeholder = "Password"
passwordField.borderStyle = .roundedRect
passwordField.isSecureTextEntry = true
view.addSubview(passwordField)
```

### Images

#### Swift UI
```swift
// From asset catalog
Image("profile_picture")
    .resizable()
    .aspectRatio(contentMode: .fit)
    .frame(width: 100, height: 100)
    .clipShape(Circle())
    
// SF Symbols
Image(systemName: "star.fill")
    .foregroundColor(.yellow)
    .font(.system(size: 30))
```

#### UI Kit
```swift
// UIImageView
let imageView = UIImageView(image: UIImage(named: "profile_picture"))
imageView.contentMode = .scaleAspectFit
imageView.frame = CGRect(x: 0, y: 0, width: 100, height: 100)
imageView.layer.cornerRadius = 50
imageView.clipsToBounds = true
view.addSubview(imageView)

// SF Symbols
let symbolConfig = UIImage.SymbolConfiguration(pointSize: 30)
let starImage = UIImage(systemName: "star.fill", withConfiguration: symbolConfig)
let symbolView = UIImageView(image: starImage)
symbolView.tintColor = .yellow
view.addSubview(symbolView)
```

### Selection Controls

#### Swift UI
```swift
// Toggle (Switch)
@State private var isToggled = false
Toggle("Notifications", isOn: $isToggled)
    .padding()

// Picker (Dropdown)
@State private var selectedOption = "Option 1"
let options = ["Option 1", "Option 2", "Option 3"]

Picker("Select an option", selection: $selectedOption) {
    ForEach(options, id: \.self) {
        Text($0)
    }
}
.pickerStyle(MenuPickerStyle())
.padding()

// Slider
@State private var sliderValue = 50.0
Slider(value: $sliderValue, in: 0...100, step: 1) {
    Text("Adjust value")
}
.padding()
Text("Value: \(Int(sliderValue))")
```

#### UI Kit
```swift
// UISwitch
let toggle = UISwitch()
toggle.isOn = false
toggle.addTarget(self, action: #selector(switchChanged), for: .valueChanged)
view.addSubview(toggle)

@objc func switchChanged(_ sender: UISwitch) {
    print("Switch is now: \(sender.isOn)")
}

// UIPickerView
// Requires implementing UIPickerViewDataSource and UIPickerViewDelegate

// UISlider
let slider = UISlider()
slider.minimumValue = 0
slider.maximumValue = 100
slider.value = 50
slider.addTarget(self, action: #selector(sliderValueChanged), for: .valueChanged)
view.addSubview(slider)

@objc func sliderValueChanged(_ sender: UISlider) {
    print("Slider value: \(Int(sender.value))")
}
```

## Layout and Containers

### Swift UI Layout

#### VStack, HStack, and ZStack
```swift
VStack(alignment: .leading, spacing: 10) {
    Text("Title")
        .font(.title)
    Text("Subtitle")
        .font(.subheadline)
}

HStack(spacing: 15) {
    Image(systemName: "person.fill")
    Text("Profile")
    Spacer()
}

ZStack {
    Rectangle()
        .fill(Color.blue)
        .frame(width: 100, height: 100)
    
    Text("Overlay")
        .foregroundColor(.white)
}
```

#### Spacer and Divider
```swift
VStack {
    Text("Top")
    Spacer() // Pushes content to edges
    Text("Bottom")
}

HStack {
    Text("Left")
    Divider() // Adds a vertical line
    Text("Right")
}
```

#### ScrollView
```swift
ScrollView {
    VStack(spacing: 20) {
        ForEach(1..<20) { item in
            Text("Item \(item)")
                .frame(height: 50)
                .frame(maxWidth: .infinity)
                .background(Color.gray.opacity(0.2))
        }
    }
    .padding()
}
```

#### Lists
```swift
struct Item: Identifiable {
    let id = UUID()
    let name: String
}

let items = [
    Item(name: "Apple"),
    Item(name: "Banana"),
    Item(name: "Cherry")
]

List {
    ForEach(items) { item in
        Text(item.name)
    }
}
```

### UI Kit Layout

#### Auto Layout with NSLayoutConstraint
```swift
let label = UILabel()
label.text = "Hello, Auto Layout!"
label.translatesAutoresizingMaskIntoConstraints = false
view.addSubview(label)

NSLayoutConstraint.activate([
    label.centerXAnchor.constraint(equalTo: view.centerXAnchor),
    label.centerYAnchor.constraint(equalTo: view.centerYAnchor),
    label.widthAnchor.constraint(lessThanOrEqualTo: view.widthAnchor, multiplier: 0.8)
])
```

#### Stack Views
```swift
let stackView = UIStackView()
stackView.axis = .vertical
stackView.spacing = 10
stackView.alignment = .leading
stackView.translatesAutoresizingMaskIntoConstraints = false
view.addSubview(stackView)

let titleLabel = UILabel()
titleLabel.text = "Title"
titleLabel.font = UIFont.systemFont(ofSize: 24, weight: .bold)

let subtitleLabel = UILabel()
subtitleLabel.text = "Subtitle"
subtitleLabel.font = UIFont.systemFont(ofSize: 16)

stackView.addArrangedSubview(titleLabel)
stackView.addArrangedSubview(subtitleLabel)

NSLayoutConstraint.activate([
    stackView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 20),
    stackView.leadingAnchor.constraint(equalTo: view.leadingAnchor, constant: 20),
    stackView.trailingAnchor.constraint(equalTo: view.trailingAnchor, constant: -20)
])
```

#### Scroll Views
```swift
let scrollView = UIScrollView()
scrollView.translatesAutoresizingMaskIntoConstraints = false
view.addSubview(scrollView)

let contentView = UIView()
contentView.translatesAutoresizingMaskIntoConstraints = false
scrollView.addSubview(contentView)

NSLayoutConstraint.activate([
    scrollView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor),
    scrollView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
    scrollView.trailingAnchor.constraint(equalTo: view.trailingAnchor),
    scrollView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor),
    
    contentView.topAnchor.constraint(equalTo: scrollView.topAnchor),
    contentView.leadingAnchor.constraint(equalTo: scrollView.leadingAnchor),
    contentView.trailingAnchor.constraint(equalTo: scrollView.trailingAnchor),
    contentView.bottomAnchor.constraint(equalTo: scrollView.bottomAnchor),
    contentView.widthAnchor.constraint(equalTo: scrollView.widthAnchor)
    // Height will depend on content
])

// Add content to contentView
```

#### Table Views
```swift
class MyTableViewController: UITableViewController {
    
    let items = ["Apple", "Banana", "Cherry"]
    
    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Cell")
    }
    
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return items.count
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath)
        cell.textLabel?.text = items[indexPath.row]
        return cell
    }
}
```

## Form Elements and User Input

### Swift UI Forms

```swift
struct ProfileForm: View {
    @State private var name = ""
    @State private var email = ""
    @State private var age = 25
    @State private var notifications = true
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Personal Information")) {
                    TextField("Name", text: $name)
                    TextField("Email", text: $email)
                        .keyboardType(.emailAddress)
                        .autocapitalization(.none)
                    
                    Stepper("Age: \(age)", value: $age, in: 18...100)
                }
                
                Section(header: Text("Preferences")) {
                    Toggle("Receive Notifications", isOn: $notifications)
                }
                
                Section {
                    Button("Save") {
                        saveProfile()
                    }
                }
            }
            .navigationTitle("Profile")
        }
    }
    
    func saveProfile() {
        print("Saving profile...")
    }
}
```

### UI Kit Forms

Typically implemented using UITableView:

```swift
class ProfileFormViewController: UITableViewController {
    
    let nameCell = TextFieldCell(label: "Name")
    let emailCell = TextFieldCell(label: "Email")
    let notificationsCell = SwitchCell(label: "Receive Notifications")
    
    override func viewDidLoad() {
        super.viewDidLoad()
        title = "Profile"
        tableView.tableFooterView = UIView()
        
        // Configure cells
        emailCell.textField.keyboardType = .emailAddress
        emailCell.textField.autocapitalizationType = .none
        notificationsCell.switchControl.isOn = true
    }
    
    override func numberOfSections(in tableView: UITableView) -> Int {
        return 3
    }
    
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        switch section {
        case 0: return 2 // Personal info
        case 1: return 1 // Preferences
        case 2: return 1 // Save button
        default: return 0
        }
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        switch indexPath.section {
        case 0:
            if indexPath.row == 0 { return nameCell }
            else { return emailCell }
        case 1:
            return notificationsCell
        case 2:
            let cell = UITableViewCell(style: .default, reuseIdentifier: nil)
            cell.textLabel?.text = "Save"
            cell.textLabel?.textAlignment = .center
            cell.textLabel?.textColor = .systemBlue
            return cell
        default:
            return UITableViewCell()
        }
    }
    
    override func tableView(_ tableView: UITableView, titleForHeaderInSection section: Int) -> String? {
        switch section {
        case 0: return "Personal Information"
        case 1: return "Preferences"
        default: return nil
        }
    }
    
    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)
        
        if indexPath.section == 2 {
            saveProfile()
        }
    }
    
    func saveProfile() {
        print("Saving profile...")
    }
}

// Custom cells would be defined separately
```

## Review Questions

1. What are the equivalent UI components for displaying text in Swift UI and UI Kit?
2. How do layout systems differ between Swift UI (stacks) and UI Kit (Auto Layout)?
3. How would you create a form with text input fields, toggles, and a submit button in both frameworks?
4. What's the difference between a List in Swift UI and a UITableView in UI Kit?
5. How do you handle user input events (like button taps) in both Swift UI and UI Kit? 