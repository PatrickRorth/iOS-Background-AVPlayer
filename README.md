# iOS - Background player for AVPlayer

Replace `APPNAME` with your own app name!

Im on iOS 4.2.1

EDIT: Working with iOS5 + 6 + 7 beta so far

Add UIBackgroundModes in the APPNAME-Info.plist, with the selection App plays audio

Then add the AudioToolBox framework to the folder frameworks.

In the APPNAMEAppDelegate.h add:

#import <AVFoundation/AVFoundation.h>
#import <AudioToolbox/AudioToolbox.h>

so it look like this:

...
#import <UIKit/UIKit.h>
#import <AVFoundation/AVFoundation.h>
#import <AudioToolbox/AudioToolbox.h>
...

In the APPNAMEAppDelegate.m add the following:

// Set AudioSession
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

into the

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

but before the two lines:

[self.window addSubview:viewController.view];
[self.window makeKeyAndVisible];

Build your project and see if theres any error, If not, try debug on Device insted of the Simulator, it CAN bug on simulator.

Hope this helps others with same problem..