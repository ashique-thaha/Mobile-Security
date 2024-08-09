
##### Cross App Scripting 
This is just like an XSS on a traditional web app, here inputs ends up on web view.
Finding these instances can be tricky, but looking for instances of the `loadUrl` or `evaluatejavascript` methods would be a good start. Trace backwards from these calls to determine if the parameters come from an insecure source. 

##### Intent Redirection
- When an intent comes into an app, it is used to trigger an activity to start. if not validated correctly, malicious app can trick victim app into kick starting malicious activity.
- Intents coming from `getExtras()` will be a good start. Developers should validate incoming intents to the app and never directly send them to `startActivity()` .
- Whenever possible, construct brand new Intents and add relevant parameters and permissions as needed, keeping the influence of the incoming intent  to a minimum. 
- If you need to use them directly, make sure to check both the class and package names of the target activity, to make sure it's going somewhere safe.

##### Intent Broadcasting
- Applications can broadcast intents to the system, to be handled by any capable application.
- For example it allows system to make apps aware of changes on the mobile, for instance phone going into and out of airplane mode.
- Unless the receiver is specified any apps on the system can intercept the broadcast.
- If you see a `sendBroadcast`  call for an intent without a specified class or component, you may be able to intercept any data that is sent out.

##### Unprotected Activities
- There will be applications where in its manifest file, exported="true" attribute is found 
- This can be intentional or unintentional
- These publicly exported apps can be accessed by another apps resulting in malicious apps to cause un intended activities to be triggered.

`Scenario:` App named `victim.apk` have its activities publicly exported. now the user unintentionally installed `malware.apk` now this app can trigger the `victim.apk`  into executing things that they like for example deleting the user account.


##### Custom Permission typos
- This is actually a bug caused due to typing errors
- Usually android apps can provide custom permissions, which allow access to certain activities from authorised apps.
- But if the name of the defined permission and the permission actually used differ, all apps are authorised.

##### Path Traversal
- Applications often download files to their private directory 
- if not controlled properly or sanitised as in web attackers can even conduct RCE

##### Zip Path Traversal
- For this we need to know how a zip file works: zip file contains a table which contains sort of a directory tree and a well formatted zip file will only contains paths like something/directory/filename.txt. when the file is unzipped, it takes a destination directory and then adds on each of the zip file entries to figure out where to write a final file 
- But it is possible to construct some zip file with a path like ../../../../file.txt
- `evilarc` is a tool that makes this kind of zip file possible.


##### Embedded secrets
- sometimes when you decompile an app you can see crypto secrets embedded on that for example symmetric crypto keys, private keys, HMAC etc.
- also third party keys or secrets can be found on here, if so then see documentations and all for third parties and see how far you can go.

##### OAuth issues
- implicit grants is one such vulnerability, with this the application will request an access token from the OAuth provider which will be  send back as the part of the  url this can lead to token leak issues 
- if you see a response type=token in an OAuth url, that is an implicit grant and is always considered to be a bad idea.
- Instead, use the standard Auth authorisation flow, via response_type=code.