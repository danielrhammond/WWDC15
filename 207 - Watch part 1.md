WatchKit In-Depth Part 1 (207)

# Architecture
## iOS Application
### Code
### Resources
## watchOS WatchKit extension
### Code
- Application - WKInterfaceController
- Glance - WKInterfaceController
- Notification - WKUserNotificationInterfaceController
- Complication - CLKComplicationDataSource
WKInterfaceController
	Interface properties
	Menu handling
### Resources
Document folder
	- Non-purgeable
	- Not restored
Caches folder
	- Purgeable
## watchOS Watch App
### Interface
Interface.storyboard, edited in interface builder. Same as watchOS 1 with some new elements 
### Resources
setImageNamed defaults to images in application rather than extension

# Media
Application is responsible for playing media file, recording audio files. Extension is responsible for downloading media and uploading/processing recorded audio files.

You need to use a shared application group to share data betwen extension and app.
# Data
NSURLSession allows for background downloads/uploads to http/https, downloaded files must be copied before the system purges the temporary cache

# WatchConnectivity
- Share data (iOS <> watchOS)
- transfer files (iOS <> watchOS)
- Make requests to iPhone app from extension

# Migration
WatchKit extensions on watchOS 1 targets the iOS Platform/SDK, share code with iPhone application and cache images, respond to openParentApplication() requests which are fast since its phone to phone

In watchOS 2 there is a new platform and SDK dedicated to watchOS. Subset of iOS frameworks are available, can include project frameworks (but will be shipped to watch)

“Same API with some changes and additions”

Create a new watchOS target and pull in code that can be reused.

## Controllers
Same interface/glance/notification controllers, replace WKImageCacheing with UIImage and openParentApplication with WatchConnectivity

# New APIs
## WKExtensionDelegate
watchOS version of UIApplicationDelegate
	Only tracks the 
	`applicationDidFinishLaunching()`
		called once on launch, application is not yet active
	`applicationDidBecomeActive()`
		each time app becomes visually active, activate timers/update state that changed while app was in background/killed
	`applicationWillResignActive()`
		only call before going to background, cancel/pause timers, save state, prepare to be inactive
### User activity
`handleUserActivity()` will be called when glance is used or when a complication is tapped. This will now be called on the WKExtension delegate rather than root interface controller
### Root Interface Controller
Property will be added in future seed, current state:
```
let rootController = WKExtension.sharedExtension.rootInterfaceController
rootController.popToRoot…()
rootController.prepForUserActivity()
```
## WKExtension
`openSystemURL` handles `tel://` `sms://` or other system supplied url schemes
# Notifications
## WKUserNotificationInterfaceController
`didReceiveRemoteNotification()` `didReceiveLocalNotifiaction` need to call completion in timely manner
## Local notifications
Local notifications can only be scheduled on the phone, will follow the normal routing rules (phone in sleep/active, etc…)
## Inline text replies
If you specify notification actions as having a text reply then the watch will display text input interface controller if the user hits reply, can provide suggestions in watchOS app
## When active
`didReceiveRemoteNotification` will be called similar to iOS you need to provide UI when app is active
# Modal Alerts
## Styles
- .Alert
- .SideBySide
- .ActionSheet