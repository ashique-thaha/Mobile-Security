
Basic commands:

`
=> First we should get a shell to the emulator for that type: 
```shell
adb shell 
```

=> Now you can install APKs with this command: 
```shell
adb install PATH_TO_APK
```

=>You can also download files from your device to your laptop by running
the following: 

```shell
adb pull REMOTE_PATH LOCAL_PATH
```

=>Or copy files on your laptop to your mobile device: `adb push LOCAL_PATH REMOTE_PATH`

=> To list all package / application that is installed on the device type : `pm list packages` 

=> To find a specific package: `pm list packages | grep {keyword}` 

=> To find the path of the app installed: `pm path {package name}` 

=> To pull apk from emulator to host: `adb pull {path of the file to be pulled} {name to save in host}` 

=> To decompile an application using apktool : `apktool d {app name}` 

=>To start an exported  activity: `am start -n {package_name/.activityname}` 

=> if you encounter something like `R.string.{something}` then you can find string at `string.xml` and the variable corresponding to it.

=> on enumerating firebase don't relay on automatic tools, so instead go manually and use the json trick for unauthenticated access eg: `https://something.firebaseio.com/{directory(optional)}/.json` 

=> check **android:allowBackup** is set to true or not, if its true it allows the data stored in the app to be backed up via adb eventhough the device is not rooted. : `<application> android:allowBackup=”false” </application>``
`
=> look for `sendBroadcast` without class , package etc

=> check Intents coming from `getExtras()` 

=>  look for  `loadUrl` or `evaluatejavascript` methods.

=> To start objection : `objection --gadget "package name"  explore` 

=> To find running apps : `frida-ps -Uai`  

=> To start frida : `frida -U -n "process name"`

=> To generate key:
```shell
 ﻿﻿keytool -genkey -v -keystore [nameofkeystore] -alias [your_keyalias] -keyalg RSA -keysize 2048 -validity [numberofdays]
```


=> To  check if the application is signed or not :
```shell
jarsigner -verify-verbose something.apk
```

=> signing app:
```shell
jarsigner -verbose -sigalg MD5withRSA -digestalg  SHA1 - keystore [name of your keystore] [your .apk filel [your key alias]
```