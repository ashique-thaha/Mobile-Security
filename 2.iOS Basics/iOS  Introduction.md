
#### IPA Container
- Just like APK this is also a format which is basically a zip file. 
- This an be unzipped just by renaming them .zip and using a standard tool to unzip.
- The interesting parts of the package like the application binary  will be on `payload/appname.app`  directory. 
- if a small change is made on the zip file the app cannot be installed.

#### Encryption
If the IPA is from app store then it will be encrypted for to prevent anyone from tampering it. but there is a way to get past that. This is called FairPlay. All the executable files are encrypted here.

#### .app Directory (Bundle directory)
- During installation the contents of this directory is directly copied to the device.
- The bundle is signed to prevent tampering at runtime.
- This also contains the primary application executable and and any dependencies or resources requires by the application.

#### Entitlements
- During the signing of the bundle a directory is created in the process. it is called `_codeSignature` .
- This code signature directory contains what apple calls entitlements.
- This is used to request for capabilities like push notifications or integrate with user's iCloud storage.
- some entitlements may require authorisation from apple.

#### Info.plist
The Info.plist file inside the app package is used to indicate a number of properties about the application. It's typically in a binary form, but can be edited via Xcode or converted to/from an XML form using the plutil utility. This is sort of like iOs version of `androidmanifest.xml`.


#### Native Code
- Android apps are typically complied to dalvik bytecode, this one is pretty easy to decompile
- in iOS the apps are compiled to native machine code, which is much harder to decompile.

#### Memory Corruption Bugs
 - Due to most iOS apps are built in Objective-C, it is possible to induce memory corruption bugs like buffer overflows. 
 - This can lead from information disclosure to remote code execution.
 - Look for the uses of memcpy, strcpy, sprintf etc you may be able to find bug there.

#### Custom Url Schemes
- The Info. plist file contains information on URL schemes registered by the application, under the CFBundleURLTypes key.
- Here in this functionality applications can register to be launched by a specific URL scheme via browser or other apps.
- This can lead to an XSS on web view or a memory corruption.

