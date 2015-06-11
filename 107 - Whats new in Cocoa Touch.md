# What’s new in cocoa touch (107)

# What’s new in iOS 9

## UILayoutGuide
1. layoutMarginsGuide - *these supersede layout margins in 8 (suck it), should replace a lot of “container” invisible views*
2. readableContentGuide

## UIStackView
Adjust spacing and alignment of collection of views that can be laid out horizontally or vertically

## Shortcuts bar
Can be customized by `UITextInput` returning `UITextInputAssistantItem`

## Storyboards
Organize/link storyboards, and unwind (?) segues

## RTL support

- Better layout for right-to-left support `semanticContentAttribute` on `UIView`/`UIViewController` (defines how content should be flipped in right-to-left locales)

- `imageFlippedForRightToLeft` on `UIImage`

## Accessibility

Changes to `AVSpeechSynthesis`, more access

## Text editing gestures

Just make sure you don’t conflict with it. (This surely breaks in gifjam/mrn)

## Keyboard commands

Can add shortcuts, and if you set a discoverability title on them it will show up

## Touch events

Lag between finger and where drawing is on screen, touch-to-display latency. Since touch refresh rates can be higher than the screen refresh ratios there are additional APIs to grab the intermediate points, and there is a new touch prediction API

## UIKit Dynamics

Supporting non-rectangular collision bounds, field behaviors, new attachment types

## Visual Effects

Animate blur radius (like spotlight interactive transitions)

## Swift niceness

- Audited/marked up for nullability
- Generics for collections

## Text input in notifications
- `UIUserNotificationAction` `behavior` will allow you to emulate the iMessage quick reply notification

## SFSafariViewController

Safari as a modal view controller

## New extension points

### VPN

- VPN packet tunnel provider
- App proxy provider
- Filter control provider/filter data provider (* ping fred s. about this!)

### Safari

- Shared Links
- Content blocking

### Spotlight

- Indexing of application data
- Index maintenance

### Audio Units

- Can now write your own audio units

## Contacts

- Swift/objectice-c API replacement for adress book

## Wallet / PassKit

- Card provisioning, suppress Apple Pay

## CoreLocation

- Updates to background location tracking
- New API for fetching current location from CLLocationManager

## MapKit

- Flyover, Show traffic, compass/scale, custom callouts

## HealthKit

- Realtime access to sensor data, new data types

## ResearchKit

- iPad support and active tasks

## HomeKit

- Detailed change notifications: Identifies the specific accessory change. Defined action sets for going to bed/waking up/etc… Remote access via wifi

## CloudKit

Web services to hit CloudKit from non iOS/mac devices

## UIDocument

Open in place (?)

## On Demand Resources

Content loaded dynamically by app and cached, hosted by app store

## App Slicing

- Deliver just the resources and binaries for the architecture/device.
- New `NSDataAsset` which helps fetch appropriate data for device

## Game Center 

Guest players

## ReplayKit

Easily record audio/visuals and share with other users

## SpriteKit

Backed by Metal where supported, new action editor in Xcode, works with on demand resources

## SceneKit

New scene editor in Xcode 7, transitions, audio, model i/o, light maps, …

## GamePlayKit

- Entities/components
- Agents
- Path Finding
- AI
- Rule Systems
- State Machines

## watchOS 2

- Connectivity
- Direct access
- ClockKit