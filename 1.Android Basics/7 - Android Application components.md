---

---
___

## 1. Activity: 
   - Represent each single UI screen of the application 
   - These  are processes that lasts a short amount of time.
   - Every single screen on the application makes up the activity file of the app. `forexample:`

**scenario1:** imagine you are on the login screen, this may be represented as: `loginActivity.java` in Manifest file 
    
**scenario2:** now you are on the cart of the same app, the screen  will be represented as `cartActivity.java` 


## 2.Services
- More long running processes compared to activities.
- Don't need UI to perform.
- Services can run on background even if the user switches to another application eg: `spotify` playing music.
- The code for the Service will be defined on the java file  `{servicename}.java`.

## 3.Broadcast Receivers
- messages that applications can send and receive from each other.
- an example of android system sending broadcast to an application  is when the device is plugged to the charger where we can see a notification. another example is when an ongoing download is complete.
- it is declared within the receiver tag on manifest file.

## 4.Content Providers 
- Provide an interface for the app to manage its stored data which can be  cloud, file  storage or database.
- The advantage of using these content providers is that it will help another apps to access the shared data 
- The content providers use `content resolvers`.
- content resolvers are present in every apps, they accept request from the client and they are directed towards the content providers using URI. 
   
## 5.Intents
- Intents are the things that helps all these components to interact with each other.
- Think of intent like a command that can send message from one component to another and describes exactly what you need to get done.
- example: Let's take  e-commerce application as example, 
    - imagine you are at `cartActivity.java` (Activity1) now you completed the order and for that you must click the place-order button.
    - The place-order button contains an intent which  sends the message to open `orderstatusActivity.java` (Activity2), ie changing  from  Activity1  to  Activity2.
    -  so the intent helped in communicating b/w activity1 and activity2.
-  The source code of the intent will be on the java file of the component that it originates from, so in `cartActivity.java` we can find the intent declared.


`There are two type of intents:-`

###### 1.explicit intent:
- while declaring the intent if we specifically mention the component where the intent should be send, then android will directly resolve the intent to that component. These are called explicit intents.
- example:
```java
 Intent downloadIntent = new Intent;
 downloadIntent.setComponent(DownloadService.class);     
 downloadIntent.setType("video/mpeg");
```
- Here we can see that using the set component method we set the intent specifically to `downloadService.class` 

###### 2. Implicit Intent:
- The components is not mentioned here, alike the other one.
- But here it contains some other attributes which help to lead android to the correct component.
- `example:`
```java
Intent sendIntent = new Intent;
sendIntent.setAction(Intent.ACTION_CALL); sendIntent.setData(Uri.parse("tel:+15555555555")); sendIntent.addCategory(Intent.CATEGORY_HOME);
```

###### Intent Resolution:
- in-order to figure out where the implicit intents should be send android uses a process called `intent resolution`.
-  Android takes a look at `action, data , category` components for this specific purpose 
- The above given example is used for calling a phone number
- `setAction`: the action that needed to be performed, here `ACTION_CALL` helps in calling a phone number.
- `setData`: refers specific location or data type can be expressed as a `uri` or a `mime type`  or both, here the data will be the phone number. 
- `addCategory`:  its used for additional informations, for example here `CATEGORY_HOME` attribute is used for home screen activities.
- but for to work these attributes need to match the `intent filters` of a component in the [[Android Manifest File|Android Manifest File]] file.

###### Intent Filters:
- Intent filters are sub elements for any components on [[Android Manifest File|Android Manifest File]]
- Intent filters basically tells the android system, what kind of intent that component is capable of handling
- So back to intent Resolution, the process uses `action,data,category` attribute of an intent  to map it with intent filters.![[../images/Screenshot 2024-07-03 at 12.06.06 AM.png|Screenshot 2024-07-03 at 12.06.06 AM.png]]
- here we can see that the attributes of intent matches with intent filters, therefore intents can be sent
- But if you look here you can see a mismatch:![[../images/Screenshot 2024-07-03 at 12.08.16 AM.png|Screenshot 2024-07-03 at 12.08.16 AM.png]]
- therefore intent cannot be sent to this component.
- what if there are one or more components with exact same match required for the intent?![[../images/Screenshot 2024-07-03 at 12.10.46 AM.png|Screenshot 2024-07-03 at 12.10.46 AM.png]]
- That is exactly where options like this happens
- note: when intent filters are mentioned in manifest file for a component, that component automatically becomes `exported` unless the developer explicitly mentions `exported="False"`  in the components attribute.
- so using `implicit intents` can be potentially `dangerous`, as if the intent contains something sensitive, then that data can be leaked to third party application from the device which have matching intent filters to handle that intent.

###### AIDL (Android interface definition language)

- Specific interface definition language for android
- This enables interprocess communication
- This is an API offered by a service to external applications.
- This enables interprocess communication by allowing client to understand what the service is expecting.
- The client app can rely on the underlying OS to deliver them to service in another app
- Services that use AIDL is referred to as bound services.
- When looking for potential vulnerabilities, you will want to begin with the onBind method and follow the application's logic to determine what actions are invoked as a result of the requests from client apps and where the data passed in from these requests are used

###### Messenger
- It is another type of IPC to share a service with other apps.
- the client invoking a Messenger receives an /Binder that can be used t o send data to the service.
- Since a Messenger is also a "Bound Service", the data passed in from the client app is also processed through the onBind method .


