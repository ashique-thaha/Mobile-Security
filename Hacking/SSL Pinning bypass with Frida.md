
1.Decompile the application with APK tool
```shell
apktool d myapp.apk -o extractedFolder
```

2 Download Frida gadget with appropriate version of the emulator eg: arm64

3.Now rename the file to `libfrida-gadget` and copy it to `/lib/armeabi`  


4.Modify the `MainActivity.smali` and add this code in a suitable position 
```java
const-string v0, "frida-gadget"
invoke-static {v0}, Ljava/lang/System;>loadLibrary(Ljava/lang/String;)V
```

5.Rebuild the APK with APK tool.


6.Sign the Application: Create a `Keystore`
```bash
keytool -genkey -v -keystore custom.keystore -alias mykeyaliasname -keyalg RSA -keysize 2048 -validity 10000
```


7.Sign the APK
```shell
jarsigner -sigalg SHA1withRSA -digestalg SHA1 -keystore mycustom.keystore -storepass mystorepass repackaged.apk mykeyaliasname
```


8.Verify the signature created 
```shell
jarsigner -verify repackaged.apk
```


9.`Zipalign` the APK
```shell
zipalign 4 repackaged.apk repackaged-final.apk
```

10.Install the modified APK

11.Open the app and run this command on the terminal.
```shell
objection explore
```


12.now disable ssl pinning using objection.
```shell
android-sslpinning-disable
```

