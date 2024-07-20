___

- let's consider a situation where the application that is installed on our device needs an update, so we are headed to `playstore` and we update the application there
- so how can we verify its the real app, and not some hacker's trick?
- for `playstore` this might not happen, suppose you are downloading the application from a third party website, then what?

- The process of signing an application comes handy here
- The developer is singing the app with his private key which is only available to the developer himself
- The whole process relays on public private key infrastructure

- Apart from that the data can be shared with other apps easily
- imagine there is applications from same developer which needs to share information
- This signing process will make it easier for them to interact as both are from same developer.
___
# Older Approach

1. Suppose there is an application called `game.apk` 
2. we can use `apktool` to decompile the app and make modifications as we like 
3. now lets rebuild the app using `apktool` itself 
4. then we sign the application with `jarsigner`
5. this would have worked before android 11.
___
# New Approach

1.  everything is exactly same as before using `jarsigner` (step 4)
2.  now we use tools called `zipalign` and `apksigner` 
3. This will work in android 11 and 12.
___
# Execution

1.  our certificates needs to be stored in a `keystore` which is a kind of safe.
2.  we can create a new `keystore` by opening the terminal and using the `keytool`, provide the following command:
```bash
 keytool -genkey -v -keystore ~/keystore_name.keystore -alias cert_name -keyalg RSA -keysize 2048 -validity
```

 ###### Breaking down the command:  
- `-genkey` : this simply generate a private key
- `-v` : print the certificate in a human readable form (normally this will be stored in binary)
- `-keystore` : we have to provide a new file here, this is the `keystore`, here we are creating a new `keystore` because this file doesn't exist
- `-alias` : reference to the certificate.
- `-keyalg RSA` : the key algorithm here its RSA
- `-keysize` : defines the `keysize`
- `-validity` : no of days of validity

3. the next step is to use the certificate within the `keystore` to sign the application, (this is where `jarsigner` has been used in the past, after that `zipalign` could be used, but that wasn't a necessity and only used in rare cases. But  after android 11 things have changed, so we take newer approach).

4. after the `keytool` command, use `zipalign` with the following command:
```shell
zipalign -v 4 base.apk out. apk
```

5. now use `apksigner` to sign the application:
```bash
apksigner sign -ks ~/keystore_name.keystore base.apk
```

6. To list all certificates on `keystore`:
```bash
keytool -list -keystore keystore_name.keystore
```


7. if you have multiple certificates make sure you give alias parameter:
```bash
apksigner sign --ks-key-alias cert_name -ks ~/keystore_name.keystore out. apk
```


___
