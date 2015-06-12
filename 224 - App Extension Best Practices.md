# App Extension Best Practices (224)

## Action

Allows user to perform action on a piece of content and then return the result in place. Uses custom template icon.

## Share

Share piece of content to your app/web service. Need to allow user to edit/validate content before sharing. Only one per containing app, uses application icon.

## NSItemProvider

Object that encapsulates multiple representations of the same item. Allows you to support multiple types of share/action extensions.

## Today Widget Enhancements

### Sharing data

Use app groups for NSUserDefaults or Files (model data/sqlite/json/etc…). Avoid using the shared container for caches so that they can be purged.

#### Task Assertions

Extensions are suspended when no longer in use. So serialization and disk cleanup tasks need to be protected to avoid corruption.

```
let pi = NSProcessInfo.processInfo()
pi.performExpiringActivityWithReason(“clean-up”) { expired in
    if (!expired) {
        // Perform sensitive work
        // guaranteed to not be on the main queue so dispatch_sync to the main queue if needed
    } else {
        // Abort and cleanup quickly
        // Note if the assertion cannot be acquired this is called back with expired==true immediately
    }
    // once block returns the task assertion is released
}
```

#### Darwin Notification Center
```
// Add Observer
let nc = CFNotificationCenterGetDarwinNotifyCenter()
CFNotificationCenterAddObserver(nc, nil, { _ in self.reloadModen() }, nil, .DeliverImmediately)
```
```
// Fire Notification
let nc = CFNotificationCenterGetDarwinNotifyCenter()
CFNotificationCenterPostNotification(nc, “com.example.example-notification-name”, nil, nil, CFBooleanTrue)
```

Not guaranteed delivery, since observer can be suspended, so don’t use for essential coordination like locks

#### Background Refresh

Conform to `NCWidgetProviding` and `widgetPerformUpdateWithCompletionHandler(…)` and the system will opportunistically call this to refresh data

#### Sharing Secrets

`SecItemUpdate`/`Add`/`Copy` will all search the available app groups so no need to add explicit group identifier.


