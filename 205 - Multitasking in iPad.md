Getting started with Multitasking in iPad (205)

# Modes
## Slide Over
Sliding map on top of Safari
## Split View
Can promote from Slide over to split view by dragging/tapping slider, can be resized interactively by user and doesn’t trigger size class update
## PIP Video
mini player for video
# Adaptivity
## Horizontal size class
iPhone (portrait/landscape) -> Compact
iPhone 6+ (portrait) -> Compact
iPhone 6+ (landscape) -> Regular
iPad (portrait) -> Regular
iPad (landscape) -> 
	Slide over: Compact
	Full screen: Regular
## Why
Need to adopt it in order to show up in the app picker
## Requirements
- Build against 9
- Support all orientations
- Use launch storyboard
- Opt out with UIRequiresFullscreen key in info.plist
# UIKit changes
## Bounds
`UIScreen` `-bounds` still returns screen bounds, and `UIWindow` `-bounds` now returns the bounds of your window (origin always `{0, 0}`)
## Transitions
- You won’t always get size class changes for window resizes
- Use autolayout
## Legibility Improvements
- Position views with consideration to readableContentGuide, which will increase/decrease margins depending on the size in order to ensure legibility
- `UITableView` `cellLayoutMarginsFollowReadableWidth` adds margins to cell to accomplish the same
## Orientation
Remove explicit handling for orientations, instead represent different orientation layouts as size change and rotation
### Transition
Same between rotation and multitasking resizing
`willTransitionToTraitCollection`/`viewWillTransitionToSize`
1. Setup
	`willTransitionToTraitCollection`
	`viewWillTransitionToSize`
	`traitCollectionDidChange`
	*time limit with watchdog*
2. Create animations
	`animateAlongsideTransition`
3. Run animations
4. Cleanup
	`completion` block of `animateAlongsideTransition`
If theres no change in trait collection
`viewWillTransitionToSize` -> `animateAlongsideTransition`
If theres no change in size
`viewWillTransitionToTraitCollection`, `traitCollectionDidChange` -> `animateAlongsideTransition`
### UIWindow
Custom created UIWindows that are not the same size as your keyWindow will be translated but not scaled as window size changes. Use default init to get correct “full screen” behavior: `UIWindow()`
### Presentation Controller
`UIAdaptivePresentationControllerDelegate`
	`adaptivePresentationStyleForPresentationController`
	`willChangePresentationStyle`
Hooks to change the app UI in response to a change in the presentation style (can now go from regular to compact)
### Keyboard
Respond to notifications from the UIKeyboard…Notification, to ensure that the important UI is visible even when another app is the one that caused the keyboard to be presented
## Best Practices
### Design
- Make app universal
- Design for size classes rather than devices
### Strategies
- Be flexible, don’t hardcode sizes
### Guidelines
- Maintain same appearance when deactivated
	- Save size / state on deactivation and onSizeChange don’t change unless active or is the persisted size
- Do as little as possible 
