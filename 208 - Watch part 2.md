WatchKit In-Depth Part 2 (208)

# WKInterfacePicker
## Style
List
Stack
Sequence
## Focus
Outline style - Shows currently selected picker with tinted outline
Outline w/ caption - Adds label on top of picker (like complication picker)
## Contextual Indicator
Useful for showing context around where you’re at in the options
## Coordinating Images
Can coordinate another image view to the current value of the picker in order to. Can be a WKInterfaceGroup or WKInterfaceImage.
```
let progressImages = UIImage.animatedImageWithImages([frames], duration: 0)
progressInterfaceGroup.setBackgroundImage(progressImages)
picker.setCoordinatedAnimations([progressInterfaceGroup])
```
## Perf
You should wait until after you haven’t received an update “for some time” before doing anything expensive in response to a picker update

# WKImage
```
// Images included in app bundle
WKImage(imageNamed: “”)
// Image data loadied from network
WKImage(imageData: imageData)
// UIImage drawn in code, less efficient than the previous two
WKImage(image: contentImage)
```
# Media playback
`presentMediaPlayerControllerWithURL(url, options: options)` can pass in a remote URL and the system will load and show progress and then playback when ready
## Recommended format
H.264 (208 x 260 or 320 x 180) 160kbps 30fps
AAC stereo 32kbps
## Location
Place media video/image/audio into the watch extension bundle. Place downloaded media in the app group
# Audio Recording
`WKinterfaceController` `presentAudioRecordingControllerWithOutputURL:preset:…`
# Security
Can lock down keychain access to when device is unlocked, keychain items aren’t synced with iCloud remain local to the device