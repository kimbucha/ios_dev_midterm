# Development Environment and Tools

## Xcode Overview

Xcode is Apple's integrated development environment (IDE) for creating applications for all Apple platforms.

### Key Features of Xcode

- **Single integrated environment** for UI design, coding, testing, debugging, and submitting to App Store
- **Built-in Interface Builder** for visual UI design with both Storyboard (UI Kit) and Canvas (Swift UI)
- **Real-time preview** of Swift UI designs using Canvas
- **Simulator integration** for running and testing apps on virtual devices
- **Version control integration** for working with Git repositories
- **Comprehensive debugging tools** to identify and fix issues

### Xcode Versions and Compatibility

- Current version (as of the course): Xcode 16.x
- Backward compatibility: Older Xcode versions can open older projects, but newer projects cannot be opened in older versions
- When working with teams, keeping consistent Xcode versions is important to avoid conflicts

## Project Setup

### Creating a New Project

1. Open Xcode and select "Create a new Xcode project"
2. Choose a template:
   - **iOS** - For iPhone/iPad specific apps
   - **Multiplatform** - For apps targeting multiple Apple platforms (iOS, macOS, etc.)
3. Select the App template for most standard applications
4. Configure project options:
   - **Product Name** - The name of your app
   - **Organization Identifier** - Typically a reverse domain name (e.g., edu.sfsu.username)
   - **Interface** - Choose between:
     - **Swift UI** - Modern declarative UI framework
     - **Storyboard** - Traditional UI Kit interface builder
   - **Language** - Swift (Objective-C also available but not covered in the course)
   - **Storage** - Options include:
     - None - No persistent storage framework
     - Core Data - Traditional database framework
     - Swift Data - Modern Swift-friendly storage (newer option)
   - **Include Tests** - Option to include unit/UI test templates (not covered early in the course)

### Project Structure

- **Info.plist** - Configuration settings for your app
- **Assets.xcassets** - Image and color resources
- **AppDelegate.swift** - Application lifecycle management
- **SceneDelegate.swift** - Scene lifecycle management (UI Kit)
- **ContentView.swift** - Main view (Swift UI)
- **ViewController.swift** - Main controller (UI Kit)
- **Main.storyboard** - Visual UI design file (UI Kit)
- **LaunchScreen.storyboard** - App launch screen

## Simulators and Device Deployment

### Using the iOS Simulator

- Access through Xcode's run button or target selection menu
- Multiple device types available (iPhone, iPad models with different screen sizes)
- Can simulate different iOS versions
- Features include:
  - Hardware menu for simulating device orientation, location, and other physical features
  - Debug menu for performance testing
  - File menu for accessing app sandbox

### Running on Physical Devices

- Requires Apple Developer account
- Device must be registered in your developer account
- Connected via USB or configured for wireless development
- Trust relationship must be established between device and computer

## Interface Builder Basics

### Storyboard (UI Kit)

- Drag and drop interface for creating user interfaces
- Object library contains UI components to add to your design
- Inspector pane for configuring properties
- Connections inspector for connecting UI elements to code (outlets and actions)
- Size classes and constraints for responsive design

### Canvas (Swift UI)

- Live preview of Swift UI code
- Interactive design mode with real-time code generation
- Inspector pane for modifying component properties
- Changes in code automatically reflect in the preview
- Device selection for previewing on different screen sizes

## Review Questions

1. What are the two main UI frameworks available in Xcode, and how do you select between them when creating a new project?
2. What is the purpose of the Organization Identifier when setting up a new project?
3. Explain the difference between running an app in the simulator versus on a physical device.
4. What are the main components of an Xcode project structure and what role does each play?
5. How do Interface Builder and Canvas differ in their approach to UI design? 