- Applications can broadcast intents to the system, to be handled by any capable application.
- For example it allows system to make apps aware of changes on the mobile, for instance phone going into and out of airplane mode.
- Unless the receiver is specified any apps on the system can intercept the broadcast.
- If you see a `sendBroadcast`  call for an intent without a specified class or component, you may be able to intercept any data that is sent out.
- don't forget `onreceive()` method 
- to trigger a specific broadcast using activity manager.pa
eg:
```shell
am broadcast -a android.intent.action.BOOT_COMPLETED
```

- trigger broadcasts with key values as extra:
eg:
```
am broadcast -a com.packagename --es "key" "value"
```
