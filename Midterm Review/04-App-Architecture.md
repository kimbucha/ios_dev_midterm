# App Architecture

Architecture patterns provide a structured way to organize code in large applications, allowing teams to work together efficiently and create maintainable software. In iOS development, two primary architectural patterns are commonly used: MVC and MVVM.

## Why Architecture Matters

Architecture provides several key benefits:

1. **Learning from others' mistakes** - Following established patterns helps avoid common pitfalls
2. **Common language** - Teams can discuss code using shared terminology
3. **Modularization** - Breaking large tasks into smaller, manageable components
4. **Separation of concerns** - Each component has a specific responsibility
5. **Testability** - Well-architected code is easier to test
6. **Scalability** - Enables the application to grow without becoming unmanageable

## MVC (Model-View-Controller)

MVC is the traditional architecture pattern for iOS development, especially with UI Kit.

### Components

#### Model
- Represents the app's data and business logic
- Doesn't know about the user interface
- Examples: data structures, networking code, persistence logic

#### View
- The user interface elements (UI Kit views, Swift UI views)
- Displays data to the user and captures user input
- Should be reusable and not tied to specific business logic

#### Controller
- Mediates between Model and View
- Updates the View when Model changes
- Updates the Model when user interacts with the View
- In UI Kit, this is typically a UIViewController

### Communication Patterns in MVC

```
       ┌────────────────────┐
       │                    │
       │     Controller     │
       │                    │
       └─────┬─────────▲────┘
             │         │
      Updates│  Notifies
             │         │
       ┌─────▼─────────┴────┐
       │                    │
       │        View        │
       │                    │
       └────────────────────┘

       ┌────────────────────┐
       │                    │
       │       Model        │
       │                    │
       └────────────────────┘
```

- **Model → Controller**: The Model notifies the Controller of data changes (through callbacks, delegates, or notifications)
- **Controller → View**: The Controller updates the View with data from the Model
- **View → Controller**: The View notifies the Controller of user interactions (through actions, delegates, or callbacks)
- **Controller → Model**: The Controller updates the Model based on user input
- **Model ↔ View**: These two cannot communicate directly (represented by a double solid line in diagrams)

### Implementing MVC in UI Kit

```swift
// Model
struct User {
    var name: String
    var email: String
}

// View
class ProfileView: UIView {
    let nameLabel = UILabel()
    let emailLabel = UILabel()
    
    func configure(with user: User) {
        nameLabel.text = user.name
        emailLabel.text = user.email
    }
}

// Controller
class ProfileViewController: UIViewController {
    private var user: User?
    private let profileView = ProfileView()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.addSubview(profileView)
        
        // Fetch user data
        fetchUser { [weak self] user in
            self?.user = user
            self?.updateView()
        }
    }
    
    private func updateView() {
        if let user = user {
            profileView.configure(with: user)
        }
    }
    
    private func fetchUser(completion: @escaping (User) -> Void) {
        // Network request or database query
        let user = User(name: "John Doe", email: "john@example.com")
        completion(user)
    }
}
```

### Limitations of MVC

- Controllers often become too large ("Massive View Controller")
- Testing can be difficult, especially for controllers
- UI logic often gets mixed with business logic

## MVVM (Model-View-ViewModel)

MVVM addresses some of MVC's limitations by introducing a ViewModel layer.

### Components

#### Model
- Similar to MVC: represents data and business logic
- Independent of the UI

#### View
- The user interface elements
- In UI Kit, often includes the UIViewController
- In Swift UI, this is the View struct

#### ViewModel
- Transforms Model data into a format the View can display
- Contains UI logic but no UI elements
- Provides data bindings that the View can observe

### Communication Patterns in MVVM

```
       ┌────────────────────┐
       │                    │
       │        View        │
       │                    │
       └─────┬─────────▲────┘
             │         │
     Commands│   Bindings
             │         │
       ┌─────▼─────────┴────┐
       │                    │
       │     ViewModel      │
       │                    │
       └─────┬─────────▲────┘
             │         │
      Updates│   Notifies
             │         │
       ┌─────▼─────────┴────┐
       │                    │
       │       Model        │
       │                    │
       └────────────────────┘
```

- **View → ViewModel**: The View sends commands to the ViewModel (user actions)
- **ViewModel → View**: The ViewModel exposes state that the View can bind to
- **ViewModel → Model**: The ViewModel updates the Model based on user actions
- **Model → ViewModel**: The Model notifies the ViewModel of data changes
- **View ↔ Model**: These cannot communicate directly

### Implementing MVVM in Swift UI

Swift UI naturally encourages MVVM with its reactive approach:

```swift
// Model
struct User {
    var name: String
    var email: String
}

// ViewModel
class UserViewModel: ObservableObject {
    @Published var userName: String = ""
    @Published var userEmail: String = ""
    @Published var isLoading: Bool = false
    
    func fetchUser() {
        isLoading = true
        // Simulate network request
        DispatchQueue.main.asyncAfter(deadline: .now() + 1) { [weak self] in
            self?.userName = "John Doe"
            self?.userEmail = "john@example.com"
            self?.isLoading = false
        }
    }
}

// View
struct UserProfileView: View {
    @ObservedObject var viewModel: UserViewModel
    
    var body: some View {
        VStack {
            if viewModel.isLoading {
                ProgressView()
            } else {
                Text(viewModel.userName)
                    .font(.title)
                Text(viewModel.userEmail)
                    .font(.subheadline)
            }
        }
        .onAppear {
            viewModel.fetchUser()
        }
    }
}
```

### Implementing MVVM in UI Kit

```swift
// Model
struct User {
    var name: String
    var email: String
}

// ViewModel
class UserViewModel {
    private var user: User?
    
    // Closures for binding
    var onNameChanged: ((String) -> Void)?
    var onEmailChanged: ((String) -> Void)?
    
    func fetchUser() {
        // Simulate network request
        DispatchQueue.main.asyncAfter(deadline: .now() + 1) { [weak self] in
            let user = User(name: "John Doe", email: "john@example.com")
            self?.user = user
            self?.onNameChanged?(user.name)
            self?.onEmailChanged?(user.email)
        }
    }
}

// View + Controller (in UI Kit, the ViewController often acts as the View in MVVM)
class UserProfileViewController: UIViewController {
    private let nameLabel = UILabel()
    private let emailLabel = UILabel()
    private let viewModel = UserViewModel()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
        setupBindings()
        viewModel.fetchUser()
    }
    
    private func setupUI() {
        // Configure and add UI elements to the view
        view.addSubview(nameLabel)
        view.addSubview(emailLabel)
        // Set up constraints...
    }
    
    private func setupBindings() {
        viewModel.onNameChanged = { [weak self] name in
            self?.nameLabel.text = name
        }
        
        viewModel.onEmailChanged = { [weak self] email in
            self?.emailLabel.text = email
        }
    }
}
```

## Other Architectural Patterns

### Coordinator Pattern

Often used alongside MVC or MVVM to handle navigation flow:

```swift
protocol Coordinator {
    func start()
}

class AppCoordinator: Coordinator {
    let window: UIWindow
    
    init(window: UIWindow) {
        self.window = window
    }
    
    func start() {
        let homeVC = HomeViewController()
        homeVC.onProfileTapped = { [weak self] in
            self?.showProfile()
        }
        window.rootViewController = UINavigationController(rootViewController: homeVC)
    }
    
    func showProfile() {
        let profileVC = ProfileViewController()
        if let navController = window.rootViewController as? UINavigationController {
            navController.pushViewController(profileVC, animated: true)
        }
    }
}
```

### Clean Architecture

Multi-layered approach that separates concerns even further:

- **Entities** (core business models)
- **Use Cases** (application-specific business rules)
- **Interface Adapters** (presenters, controllers, gateways)
- **Frameworks and Drivers** (UI, databases, devices, external services)

## Choosing the Right Architecture

Consider these factors when selecting an architecture:

1. **Project size** - Simple projects might not need complex architecture
2. **Team size** - Larger teams benefit from clearer separation of concerns
3. **Framework** - Swift UI naturally fits with MVVM, while UI Kit was designed for MVC
4. **Testability requirements** - MVVM is generally easier to test than MVC
5. **Long-term maintenance** - More structure helps with long-lived projects

## Review Questions

1. What are the three components of MVC, and what is the responsibility of each?
2. Why can't the Model and View communicate directly in MVC?
3. What problem does MVVM solve that MVC struggles with?
4. How does data binding work in MVVM, and how does it differ between Swift UI and UI Kit?
5. In what scenarios would you choose MVVM over MVC for an iOS application? 