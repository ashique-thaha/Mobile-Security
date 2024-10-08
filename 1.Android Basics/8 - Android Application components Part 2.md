

___

#### Android Manifest.XML 

- ﻿﻿Declares the Android API that the application is going to use
- ﻿﻿Permissions that an application needs
- ﻿﻿Lists  all the Activities, Services, Broadcast Receivers and Content  Providers etc.
- Defines the UID the app will run on .
- Naming scheme: if an attribute begins with a dot then it is treated as relative to the packages name. eg: `com.example.appname` is the package name then the attribute will be treated as `com.example.appname.attributename`


___

***`<uses-sdk>` `element`***
It has one or more of the following attributes:
 - minSdkVersion,
 - targetSDKVersion
 - and/or maxSdkVersion.

- The `minSdkVersion` specifies the earliest version of Android the app will run on. Failing to specify a value results in a default of 1, which would allow the app to run on any version of Android, back to the very first.

- The `targetSdkVersion` specifies which version of Android the application has been tested to be compatible with.
- If not set, it will fall back to the same value as minSDKVersion. 

- neither the `targetSdkVersion` nor `maxSdkVersion` have any significant security impact
___
#### Intents
- The means by which android apps communicate b/w their components or other apps
- These message objects can carry data b/w apps or components similar to the usage of GET POST verbs in HTTP communication.
- used to invoke an action or set of actions in the receiving component or application
- these can be directed to specific components or applications.
- also can be sent out without a specific recipient designated.

___
#### Implicit Intents

- These intents do not specify particularly an application's component.
- They specify an action to be taken instead of component eg: `Action.X`
- The `X` described here will be view, send etc.
- The action of intent will be declared via setAction() method.

- Intents are programatically constructed like this:
```java
Intent email = new Intent (Intent.ACTION_SEND,
Uri.parse("mailto: ")) ;
```

- in the above example, the Intent's name is `email`, the `Action` is `ACTION_SEND` and it includes an `Extra` of `mailto`, whose `type` is `Uri`

- This is used for sending a `mailto` link to an application which is capable of generating an email.

- `Extra` is the term for the portion of the Intent which carries data

- In the intent receiving app's manifest, it would be necessary to have  an intent-filter element, which matches our action.

- In addition to a matching `action`, an intent and its corresponding intent-filter in the receiving component, are paired with their `data` and `category`.

- In order to receive any implicit intent, the app also needs to specify the default category, eg: `android.intent.category.DEFAULT`

```xml
<activity android:name="ShareActivity">
  <intent-filter>
   <action android:name="android.intent.action.SEND" />
   <category android:name="android.intent.category.DEFAULT" />
  <intent-filter>
</activity>
```

- Implicit intents brings up the risk of data being stolen by a malicious application.
___
#### Intent Resolution

-  The intent resolution is something that queries the system manager  process and determine which apps are capable of handling the intent based on if they match the action, category and type.

- If there are multiple application capable of handling the intent, then the priority attribute can be specified on the intent filter for a component, this will select the app with the highest priority value. SYSTEM_HIGH_PRIORITY is the maximum value for this.

- Or a chooser window will appear if there are multiple apps and there is not a priority attribute set.

- A vulnerability related to this happened on google's play store related to in-app purchases in 2013, the hackers built a malicious app which matched the google play's intent filter, and given the malicious app equal or higher priority. now when the chooser window appears they will simply select the malicious app. At last  to resolve the payment intent, they will simply send a response which which emulated a successful payment.

___
#### Explicit Intent 
- This sort of intents will specify the class name it is targeting in the intent constructor. like this: 
```java
  Intent downloadIntent = new Intent ( this ,
  DownloadService.class) ;
```

- This will make sure that the application that receive the intent will be the one that we set up and forbids intercepting or eavesdropping on the intent contents.
- we may use `setComponent` or `setClass` methods for this purpose, eg:
```java
Intent intent = new Intent( ) ;
intent.setClassName ("com.other.app",
"com.other.app.ServiceName"); context.startService (intent) ;
```

___

#### Broadcast Intents

- The previously discussed intents where meant for an app or a component inside the app, but broadcast intents can be received by multiple apps.

- If only there is a need to ensure that only one application needs to receive the broadcast its needed to specify the app, using `Intent.setPackage`.

- Also the receiving app will need to specify the `user-permission` element in the manifest file.

___

#### Normal Broadcast & Ordered Broadcast

- Normal Broadcasts can be processed by multiple applications in any order, simultaneously.

- Ordered Broadcasts are run one at a time. The order is determined by the priority defined within the corresponding receiver element, within the receiving app's Manifest file: 
___
consider a scenario where an OTP has to be passed to a banking application: the system messaging app with highest priority will be the one to receive the Broadcast first and this system app will decide whether to pass the message to the banking application or not. In this case there is only two application but there might be scenarios where there are more applications. The application with higher priority will decide whether to forward the message to lower priority or not.
___

- To ensure the delivery of Broadcast you'll either need to use appropriate permission or a normal Broadcast.

- To send a broadcast intent, with a permission specified, you'd use something like the example below:

```java
sendBroadcast (intent, receiverPermission)
```

- unless the permission you declare is reserved for system level apps, any app could also have declared the same permission

- If the broadcast only need to be  received by components within the same application it is being sent from, then you can use the `sendBroadcast` method from `LocalBroadCastManager` class.

- the `sendBroadcast` method from the `LocalBroadCastManager` ensures that your broadcast never leaves your app

- This also  means that we don't have to export a receiver component. This will significantly reduce the attack surface.

___

#### Sticky Broadcasts

- Difference here is that the system maintains these Broadcasts
- therefore they can be accessed long after they were initially sent
- This was  deprecated in API Level 21.
- also review and see any methods that contains the word "sticky", like `sendStickyBroadcast`, `sendStickyBroadcastAsUser` etc.

___

#### Pending Intents

- allow other applications to take actions on behalf of your application, using your app's identity and permissions.
- constructing a Pending Intent, developers specify an intent and action to perform.
- If this intent is not an Explicit Intent, a malicious application could receive it and perform the action on behalf of the victim app.

___

#### Deep Links
- allows to load a remote url and display web pages \
- allows to trigger an intent via url
- In order to receive the Intent, we need to configure the manifest file  to confirm the action, category and data, in the Deep Link's URL, match up with the intent-filter element for the receiving component.
- The intent filter should also have the category with the value: `android.intent.category.BROWSABLE`

___

#### Activity

- Defined inside the application tag, represents the UI screen. 
- it looks like: 
```xml
 <activity android:name=".MainActivity">
```
- The code of activity is defined on another file called ManiActivity.java


`Exploitation:`
- The most direct situations where an improperly protected Activity could be exploited would be those where it returns data to a caller.
- In order to locate situations where this could occur, you'll need to examine the Activity code for the `setResult` method
- here, evaluate what data is passed into the `setResult` method's `Intent` parameter.
- If this data is sensitive in nature, you would have an information leakage vulnerability. This is exploitable by all applications capable of communicating with the Activity.

___

#### Service:
- Declared inside the application element.
- more long running process than activity.
- don't need a UI screen.
- continues to work on background even if the user switch to another app.
- This is what it looks like:
```xml
 < service android:name=".ExampleService" />
```

- The main code of the service will be defined in another java file in the apk called ExampleService.java

- If the client calls a service using the `startService` method, it will run indefinitely, until the `stopService` method is invoked.
- If the service is active as long as the client (Third party) is connected, the client should "bind" to it using the `bindService` method. when they disconnects it gets shut down.

`exploitaiton:`
- the first place to look for vulnerabilities would be from the Intent, passed into the `onStartCommand` method for "started" services
- look for any sensitive functionality invoked because of this Intent
- For a `"bound"` service,  start with the Intent passed to the `onBind` method, looking for the same types of issues
___

#### Broadcast receivers
- listens to broadcasted intents, this is the way that applications send and receive messages.
- declared using the  receiver tag like this: 
```xml
<receiver android:name=".MyBroadcastReceiver" android:exported="true">
```
- declared on java file using `onReceive()` method

___

#### Content Providers
-  the means by which Android apps share structured data, such as relational databases 
- Unlike other elements, Content Providers also have a second layer of permissions which, when present, takes over the permission attribute
- The `readPermission` and `writePermission` attributes specify which permissions an app must have, in order to query the database or make changes to the data.
- Content Providers also provide the ability to allow for temporary exceptions to these two layers of permissions.
- Setting the `grantUriPermission` attribute value to true, Then configuring the appropriate parameters in the `grant-uri-permission` element, within the provider element, of the app's AndroidManifest.xml file will do it.
- We can interact with them via content URI like this one: 
```
- content://com.android.contacts/contacts/2 - 
content:// => prefix 
com.android.contacts => authority(usually pacakage name)
contacts => table name
/2 => row
```

___

#### Content-Resolver
- let's take the scenario of contacts here,
- Content-Resolver will ask the content provider to provide the content to us
- if we have permissions and if the part is being exported equals true, then we can access this 
- if so then the content provider sends back a cursor which is a pointer to the database selection or entry.
- custom content providers will store data on `/data/data/package-name/db` directory.

___


#### Permissions
- when average user thinks of Android permissions, they think of the prompts they receive when they install applications, such as access to your Contacts, GPS location etc.
- These prompts are a direct result of the configuration of the `uses-permission` elements in the AndroidManifest.xml file.
- The uses-permission element has two attributes, `name` and `maxSdkVersion` 


`Classes.dex`
   • It contains Java byte code in DEX (Dalvik Exchange) format

`res`
   • Contains device configuration, Bitmaps and Layouts

`resources.arsc`
- ﻿﻿Contains compiled resources in a binary format
- ﻿﻿May also include images, strings, or other data used by an app

`META-INF`


- This one sort of does the integrity checks for the app, like for example verifying the hash and all....
-  ==MANIFEST.MF== : It contains various information used by the JRT when loading the jar file, such as which is the main class to be run from the jar file, version of package, build number, creator of the package, security policies/permissions of java applets and the list of file names in the jar along with their SHA1 digests, etc.
-  ==CERT.SF==: This contains the list of all files along with their SHA-1 digest.
-  ==CERT.RSA== : This contains the signed contents of the CERT.SF file along with the certificate chain of the public key used for signing the contents.





