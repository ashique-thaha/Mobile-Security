
- let's consider a situation where the application that is installed on our device needs an update, so we are headed to `playstore` and we update the application there
- so how can we verify its the real app, and not some hacker's trick?
- for `playstore` this might not happen, suppose you are downloading the application from a third party website, then what?

- The process of signing an application comes handy here
- The developer is singing the app with his private key which is only available to the developer himself
- The whole process relays on public private key infrastructure

- Apart from that the data can be shared with other apps easily
- imagine there is applications from same developer which needs to share information
- This signing process will make it easier for them to interact as both are from same developer.

1. Suppose there is an application called `game.apk` 
2. we can use `apktool` to decompile the app and make modifications as we like 
3. now lets rebuild the app using `apktool` itself 
4. then we sign the application with `jarsigner`
5. this would have worked before android 11.
