
# App Lifecyle

## Application States

### active
The app is foregrounded (has focus) and is executing and the UI can be interacted with.

### inactive
The app is foregrounded (has focus) executing but cannot be interacted with. This can often be the result of an interruption from iOS such as a phone call or prompt for Location Services access.

### background
Another App (or iOS/Springboard itself) has focus.  Eventually iOS will `suspend` the app to save on resources. 

### Suspended 
The app is **not** executing. It has been frozen in memory. It can be hard to test suspension because Xcode’s debugger prevents the system from suspending your app: https://developer.apple.com/forums/thread/14855

### Not Running
The app's process has been killed. Launching the app will call `willFinishLaunchingWithOptions`/`didFinishLaunchingWithOptions`.

Note: `active`, `inactive` and `background` are the only states included in UIApplication.State as `Suspended` and `Not Running` cannot be encountered during code execution.


## UIApplication Lifecycle Events

### willFinishLaunchingWithOptions/didFinishLaunchingWithOptions
State is `inactive`. Called when the app is first launched.

### applicationDidBecomeActive
State is `active`. Called when app finishes launching and then becomes active. Also called after dismissing a UI interruption from Springboard like a Location Services auth alertView. UIKit posts a didBecomeActiveNotification *before* calling this method. 

### applicationWillResignActive
State is `active` and becomes `inactive` after exiting the function. Called when the UI interrupted by iOS/Springboard 

### applicationDidEnterBackground
State is `background`.

### applicationWillEnterForeground 
State is `background` and will become `active` after exiting the function. UIKit posts a `willEnterForegroundNotification` shortly *before* calling this method. Invariably followed by `applicationDidBecomeActive`.

### applicationWillTerminate
State is `background` or `inactive`.


## Common Transitions

### Installing & Launching App:
didFinishLaunchingWithOptions: inactive
applicationDidBecomeActive: active
Note that it skips `applicationWillEnterForeground` because it's already foregrounded, it's just not *active*.

### Swipe Up From Bottom:
applicationWillResignActive: active
Note that this doesn't call applicationDidEnterBackground because the application is still foregrounded. 

### Swipe Up From Bottom followed by selecting another app:
applicationWillResignActive: active
applicationDidEnterBackground: background


### TODO: Prompt for location access:

Question: when does 





