# iOS - Background player for AVPlayer

Replace `APPNAME` with your own app name!

Add `UIBackgroundModes` in the `APPNAME-Info.plist`, with the selection `App plays audio`

Then add the `AudioToolBox framework` to the folder **frameworks**.

In the `APPNAMEAppDelegate.h` add:

```Obj-c
#import <AVFoundation/AVFoundation.h>
#import <AudioToolbox/AudioToolbox.h>
```

so it look like this:
```Obj-c
...
#import <UIKit/UIKit.h>
#import <AVFoundation/AVFoundation.h>
#import <AudioToolbox/AudioToolbox.h>
...
```

In the `APPNAMEAppDelegate.m` add the following:

```Obj-c
// Set AudioSession`
NSError *sessionError = nil;
[[AVAudioSession sharedInstance] setDelegate:self];
[[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayAndRecord error:&sessionError];

/* Pick any one of them */
// 1. Overriding the output audio route
//UInt32 audioRouteOverride = kAudioSessionOverrideAudioRoute_Speaker;
//AudioSessionSetProperty(kAudioSessionProperty_OverrideAudioRoute, sizeof(audioRouteOverride), &audioRouteOverride);

// 2. Changing the default output audio route
UInt32 doChangeDefaultRoute = 1;
AudioSessionSetProperty(kAudioSessionProperty_OverrideCategoryDefaultToSpeaker, sizeof(doChangeDefaultRoute), &doChangeDefaultRoute);
```

into the

```Obj-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
```

but before the two lines:

```Obj-c
[self.window addSubview:viewController.view];
[self.window makeKeyAndVisible];
```

Build your project and see if theres any error, If not, try debug on Device insted of the Simulator, the simulator can bug.

Hope this helps