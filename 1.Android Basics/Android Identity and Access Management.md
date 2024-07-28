
##### Android IAM Basics

- Each application has its own user.
- User is the owner of the application directory.
- UID b/w 10000 and 999999 
- Username similar ie, U0_a188 for UID 10188

- /data/app/com.example.app - generic application data.
- /data/data/com.example.app - runtime storage of data.
- /mnt/sdcard/Android/data/com.example.app - externally stored location for runtime.
- /data/data/com2.example.app - a different app requiring different user.

This will stop applications from interacting with each other, unless explicitly granted permission or else they should use a content provider broadcast receiver. 

- Root user and system level accounts can only access all these different type directories.



##### Profiles
 These are separated app data, like: Work profile, Personal profile, Always-on -vpn for     some apps.

##### Primary User
 This is the first user created when the first time the phone is started, this can only be      
 removed by factory reset.

##### Secondary User 
This is the user created by primary user and can be deleted by primary user.

##### Guest User
Only one Guest user is allowed at a time, This is a fast way to give a guest access to your phone

##### Kid Mode 
This is specifically for kids, to control what they can do on the devices. works only on supported devices.




