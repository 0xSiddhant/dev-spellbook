# Guide: Creating and Linking an Xcode Framework in a Workspace

This guide provides a complete walkthrough for creating a reusable framework and linking it to an application within a single Xcode workspace. This is the standard and recommended approach for managing multi-project iOS or macOS applications.

---

## Part 1: Setting Up the Workspace

First, we need a workspace to contain both our main application project and our new framework project.

1.  **Create a New Workspace**:
    * In Xcode, go to **File > New > Workspace...**.
    * Name it (e.g., `MyAwesomeApp_Workspace`) and save it in a root folder that will also contain your project folders.

2.  **Add Your Projects to the Workspace**:
    * Open the new, empty workspace.
    * Drag and drop your main application's `.xcproject` file (e.g., `AppProject.xcproject`) from Finder into the Xcode Project Navigator (the left-hand pane).
    * Do the same for the project that will become your framework (e.g., `LibraryProject.xcproject`).

Your Project Navigator should now look like this:
```
    MyAwesomeApp_Workspace
    ├── AppProject
    └── LibraryProject
```

---

## Part 2: Creating the Framework Target

Now, we'll turn the `LibraryProject` into a framework that can be shared.

1.  **Select the Library Project**: In the Project Navigator, click on `LibraryProject`.

2.  **Add a New Target**:
    * With the project selected, go to **File > New > Target...**.
    * In the template window that appears, select the **Framework** template.
    * Click **Next**.

3.  **Name Your Framework**:
    * Give it a clear name, like `MyLibraryFramework`.
    * Ensure the "Project" is set to `LibraryProject` and "Embed in Application" is set to "None".
    * Click **Finish**.

4.  **Add Code to the Framework Target**:
    * Add your Swift source files to the `LibraryProject`.
    * For each file you want to include in the framework, select the file and open the **File Inspector** on the right.
    * In the **Target Membership** section, make sure the checkbox next to your new `MyLibraryFramework` target is **checked**.

5.  **Make Your Code Public**:
    * For any class, struct, function, or variable in your framework that you want to access from your main app, you **must** mark it as `public`.

    ```swift
    // In a file within MyLibraryFramework
    
    import Foundation
    
    public class MyAwesomeManager {
        public init() {} // The initializer must also be public
    
        public func doSomethingCool() {
            print("Framework is doing something cool!")
        }
    }
    ```

---

## Part 3: Linking the Framework to Your App

This is the final step where we connect the framework to the main application.

1.  **Share the Framework's Scheme**:
    * At the top of the Xcode window, click on the scheme selection dropdown and choose **Manage Schemes...**.
    * Find the scheme for `MyLibraryFramework` and check the **Shared** box. This makes it visible to other projects in the workspace. Click **Close**.

2.  **Select Your App's Target**:
    * In the Project Navigator, click on your `AppProject` and then select its main application target.

3.  **Add the Framework Dependency**:
    * Go to the **General** tab.
    * Scroll down to the **"Frameworks, Libraries, and Embedded Content"** section.
    * Click the **+** button.

4.  **Choose the Framework from the Workspace**:
    * A dialog will appear. You will see `MyLibraryFramework.framework` listed under the "Workspace" group.
    * Select it and click **Add**.

Xcode automatically handles the necessary build phase settings for you. You have now successfully linked the framework.

---

## Part 4: Using the Framework in Your App

Now you can import and use your framework's code in your main application.

1.  **Open a source file** in your `AppProject`.

2.  **Import your framework** at the top of the file.

3.  **Use the public code** you created.

```swift
// In a ViewController.swift file inside AppProject

import UIKit
import MyLibraryFramework // 1. Import the framework

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        // 2. Use the public class from the framework
        let manager = MyAwesomeManager()
        manager.doSomethingCool() // This will print the message from the framework
    }
}
```
**Final Step:** Build and run your main app scheme (AppProject). Xcode will first build the framework and then build and run the app, resolving the dependency automatically.
