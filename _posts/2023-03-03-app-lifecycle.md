
resignActive and becomeActive happen with iOS generated AlertViews like prompts for FaceID, Location Access, etc.

applicationDidEnterBackground and applicationWillEnterForeground 


UIApplication.shared.applicationState:
active, inactive and background


Common Transitions

Installing & Launching App:
didFinishLaunchingWithOptions: inactive
applicationDidBecomeActive: active
Note that it skips applicationWillEnterForeground because it's already foregrounded, it's just not *active*.

Swipe Up From Bottom:
applicationWillResignActive: active
Note that this doesn't call applicationDidEnterBackground because the application is still foregrounded. 

Swipe Up From Bottom FOLLOWED BY selecting another app:
applicationWillResignActive: active
applicationDidEnterBackground: background


Prompt for location access:

It can be hard to test suspension because Xcode’s debugger prevents the system from suspending your app [https://developer.apple.com/forums/thread/14855]

