# INFO449Note

## 3.31

### Today - Project Pitch Day - Project Review Day

### Reaching

- Ted

### HW

Hello, iOS!

## 4.1

### iOS

Variety of useful features

- Touch UI and controls
- Several different screen sizes
- Audio playback
- Video camera
- Telephony
- Networking
- OpenGL

History

- iPod -- Nano
- Click Wheel
- **iTunes**
- iPhone OS
- iPhone OS 2.0
- 3.2 - iOS

iOS Architecture 

- From Mac OS X
- Gone since its inception
- **Layered architecture**
  - Code - user mode code
  - into system called - Darwin
    - UNIX-Core
    - Comprised of kernel, XNU
    - versioned independently
      - OSX 10.x.y Darwin 4.
  - turn into 'kernel'
  - kernel turn talks to hardware
  - **Wont have to worry about drives**

Difference

- iOS - single user, macOS - multi user
- iOS beased on ARM processor line, nor Intel x86/x84
- kernel is closed source while Darwin is open source
- iOS GUI is Spring Board, not Aqua
- memory management: tight than macOS
- swap space: constrain than macOS
- system is jailed -- cannot access to directory/underlying UNIX APIs

Same

- Key element: **Bundles**
- "A standardized hierachical structure that holds executable code and resouces used by that code"
- applications: directory stuctured not a single file
- programmatic access is available

iOS AppStore-packaged applications are ".ipa" files

- Zip-packed bundles

Frameworks are lib bundles

Process: instance of an executing program have many threads

- Executable 

Thread: instance of executable CPU time running code 

### Applications

- Run in a separate process on top of iOS operating system

- Begin by invoking UIApplicationMain()

  - creates the core object of app
  - loads the app UI from storyboard
  - call app custom code to do initial setup

- start the main thread running a "run loop" processing UI events (not need to worry about now)

- **Core objects**

  - UIApplication: one instance per iOS app
    - facilitate app interactions with system
    - typically not subclassed
    - ***Process related***
  - App Delegate: per-app custom delegate
    - responds to incoming events, interaction from system
    - only object guaranteed to be present in every app
    - Where app-wide setup/control lives
    - ***Customize*** 
  - Documents/data model objects
    - App-specific
    - less emphasis in iOS
    - recovery - restore purchasing 
  - UIWindow object
    - one or more views on screen
    - most have only one
  - View object: object that draws content
  - Control object: specialized type of view responsible for implementing interface objects
  - Layer objects: complex animations and other visual effects
  - View controllers - UIViewController subclasses
    - manage presentation of Appa content on screen
    - when presented, make its view visible by installing them in the appa window
  - **Main run loop**
    - processes all user-related events
      - UIApplication gets first crack at them
    - executes in the main thread 
    - process all events serially - in order they generated 
  - **Lifecycle states**
    - App will go through
      - not running
      - Inactive: running foreground but not processing events
      - Active: running in foregroung and processing events
      - Background: running in background and executing code (like BGM)
      - Suspended: running in background and not executing code
    - state changes will be fired through app delegate methods
      - application: willFinishLaunchingWithOptions: first chance to execute at launch
      - application:didFinishLaunchingWithOptions: final chance before displaying the app
      - applicationDidBecomeActive: app is about to go foreground 

  

## 4.6 Swift Basics

- Playground - try things out

  - Click on play automatically/manually 

- Import

  - `import Foundation`

- Comments

  - `/**/`
  - `//`

- No semicolons

- Basic variable types

  - **Automatically assign type**
  - Or `var truth : Boolean = true`
    - in this case if we say it is a int -> error
    - Or Do `var truth : Int = Int(True)`
  - String, Integers: Uint(Unsigned) 
    - String: use **double quote**
    - Uint: cannot be negative 0~max
    - UInt16/32: bit size
  - Array: `[Int]`

- `.negate`

- **let -> constant cannot be reassign**

- Var -> can change

- `"\(variable)"` String interpretations, variable can be any expression

- **Underscore: anonymous variable `var _ = 3`**

- Types: in swift everything are **objects**

- `1...32` from 1 to 32

- wrapper

  - ```swift
    var a : Int? = 42
    print(a) // optional(42)
    a = nil
    print(a) //nil
    ```

  - unwrap

    ```swift
    let intNum = a! // 42
    //cannot use when it is nil
    ```

    

- Control Flow

  - `if consition {`

    `} else {`

    `}`  	

  - guard expression 

    - catch error

  - switch

    - `switch name {`

      `case "": print()`

      `default:`

      `}`

    - switch must be executable 

  - **Pattern matching**

  - Repeat while

    ``` swift
    repeat {
    
    } while
    ```

    

  - For in 

    ```swift
    for x in 1...32 {
    
    }
    ```

    x can be underscore

- Functions

  - ```swift
    func doSomething() {
    	print("1")
    }
    doSomething()
    ```

  - Function can be captured

    ```swift
    let doIt = doSomething // doIt is now a function
    doIt()
    
    let doItt = doSomething // doItt is now a value
    ```

    Function can be pass to another function

  - ```swift
    func add(left ihs: Int,right rhs: Int = 0) -> Int { // declare a return type, left and right make more readable, = 0 is a default
      return ihs + rhs
    } 
    print(add(left: 4, right: 5)) // use here if you declear left/right before
    ```

    - Positional parameter

  - ```swift
    nums: Int... // Ranged int
    ```

  - ``` swift
    _ nums : inout Int // change the input in function
    ```

  - Closures

    ```swift
    let doIt = {
      print("1")
    }
    //add parameter
    let add = { (_ nums: Int...) -> Int in
      print(nums)
    }
    ```

    - When to do closure? function pass into functions, event handle

      ```swift
      let nums = [1, 2, 3, 4, 5, 6]
      nums.sorted(by: { (l : Int, r : Int) -> Bool in // l>r
        return 1>r
      })
      ```

    - Other trick - 

      ```swift
      func mathOp(left : Int, right : Int, op : (Int, Int) -> Int) -> { // takes 2 int and a closure
        return op(left, right)
      }
      let result = mathOp(left: 1, right: 2) {$0 + $1} // 1+2 = 3
      ```

      

