Introducing WatchKit for watchOS 2 (105)
Josh Shaffer

- Code can now be moved into the watch kit extension as opposed to openParentApplication:
- Watch can access wifi directly without phone via NSURLSession
- New
# WatchKit
## Digital Crown
WKInterfacePicker, scrolls through set of items with crown and pick one
### Style
	List style
		Like complications configuration on watch faces
		Optional focus outline
	Stack style
		List of images for user to scroll through and pick (3d transition)
	Image sequence
		Scroll through a list of images without a transition (like the crazy emoji thing)
### scroll indicator 
recommended whenever it is unclear how many options exist
### coordinated images
you can coordinate an image to the scroll offset of the WKInterface picker to create a custom UI like the timer filling the ring as you scroll
## IB
Everything that was available in watchOS 1 in IB is now also available at runtime programmatically
## Animations
Allows you to animate any WKInterface changes (Separate session on Layout/animation techniques)
## Taptic Engine
~9 haptic/haptic types of feedback, use one consistent with system rules
## Microphone
Works like the dictation interface controller, presents the modal with recording UI with preview/confirmation and you get an “audio file” back with custom send/confirm button title
## WKInterfaceMovie
Provide poster image and movie file url, movie url can be remote and watchkit will provide the loading feedback before playing back. Designed for short interactions. 
## New api (name?)
Similar audio session in avfoundation, allows for long form audio
## Alerts
Similar to a UIAlertController, title + description and some buttons
## Open system URL on watch
Can take an sms:// url to send a URL, can start a phone call (tel:// url)
## Integration with passkit
Can get access to iOS passes/install new passes
# ClockKit
## Different styles
## Data source
Data is provided to watchOS as a timeline to schedule updates to watch complication ahead of time, also supports time travel
# Networking
Using NSURLSession, the os will choose whether to use phone or just trying the tether-less wifi on watch alone
# Watch Connectivity
Helps watch extensions share data with iOS apps. Allows for bi-directional sharing downloaded/computed data. Two parts:
1. Application context - dictionary of data to always handoff between app instances, behind the scenes watch os transfers when  battery/power efficient
2. File transfer - same as application context but for files
3. Messages - allows watch extension to wake up iPhone app for some work/event
More info in session dedicated to Watch Connectivity
# CoreMotion
Live accelerometer data, and recorded background data provided as batch updates (See session Whats new in Core Motion)
# CoreLocation
Find out current location, subscribe to changes. Permissions for location is shared between iOS and watchOS
# HealthKit
Exposes the same set of APIs on watchOS that were previously available on iOS. Can start workout sessions similar to the workout app, can be used to get higher HR readings frequency. More info in Whats new in HealthKit
# Security
Keychain access, locks based on whether watch is on user’s wrist
# MapKit
Subset of MapKit available on watchOS, particularly MKMapItem which can be used to kick off directions/routing in the map watch app
# Contacts/EventKit
Access to the address book/calendar on apple watch without transferring from phone, similar permissions sharing with CoreLocation