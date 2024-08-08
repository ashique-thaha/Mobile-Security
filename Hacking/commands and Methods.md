
## Basic commands:


- First we should get a shell to the `emulator` for that type: 
```shell
adb shell 
```



 - Now you can install APKs with this command: 
```shell
adb install PATH_TO_APK
```



- You can also download files from your device to your laptop by running
the following: 
```shell
adb pull REMOTE_PATH LOCAL_PATH
```



- Or copy files on your laptop to your mobile device: 
```shell
adb push LOCAL_PATH REMOTE_PATH
```



 - To list all package / application that is installed on the device type : 
```shell
pm list packages
```



 - To find a specific package: 
```shell
pm list packages | grep {keyword}
```



 - To find the path of the app installed:
```shell
pm path {package name}
```



 - To pull apk from emulator to host: 
```shell
adb pull {path of the file to be pulled} {name to save in host}
```



 - To decompile an application using apktool :
```shell
apktool d {app name}
```



- To start an exported  activity:
```shell
am start -n {package_name/.activityname}
```



 - if you encounter something like `R.string.{something}` then you can find string at `string.xml` and the variable corresponding to it.



 - on enumerating firebase don't relay on automatic tools, so instead go manually and use the json trick for unauthenticated access eg: 
```shell
https://something.firebaseio.com/{directory(optional)}/.json
```


 - look for `sendBroadcast` without class , package etc

 - check Intents coming from `getExtras()` 

  - look for  `loadUrl` or `evaluatejavascript` methods.


 - To start objection : 
```shell
objection --gadget "package name"  explore
```



 - To find running apps : 
```shell
frida-ps -Uai

```



 - To start frida : 
```shell
frida -U -n "process name"
```



 - To generate key:
```shell
 ﻿﻿keytool -genkey -v -keystore [nameofkeystore] -alias [your_keyalias] -keyalg RSA -keysize 2048 -validity [numberofdays]
```




 - To  check if the application is signed or not :
```shell
jarsigner -verify-verbose something.apk
```



 - signing app:
```shell
jarsigner -verbose -sigalg MD5withRSA -digestalg  SHA1 - keystore [name of your keystore] [your .apk filel [your key alias]
```


- To get backup via adb 
```python
adb backup –apk –shared com.android.insecurebankv2
```

- To extract the data from the .ab file after the backup of the application has been done, use the following command:
```python
dd if=backup.ab bs=1 skip=24 | python -c “import zlib,sys;sys.stdout.write(zlib.decompress(sys.stdin.read()))” | tar -xvf –
```


