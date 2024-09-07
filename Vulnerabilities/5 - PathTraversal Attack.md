
- first of all look for the provider tag on manifest file
-  see if its enabled exported= 'true'
- let's take a scenario:
	- There is an application that creates a secret file on `/data/data/packagename/secretfile`
	- only the owner or root can access it
	- analysing the source code we found that the app uses an overridden method for content provider for file access
	- usually we will be on the `/cache` directory according to the app.
	- so we cannot access the `secretfile` which is in another directory
	- we use `../` just like in web attack here for to bypass the restriction of context. 
	- for that use maximum `../../` as we don't know the exact path.
	- we may go as far as root directory.

	- on `adb` shell we can test it by this command :
 ```shell
content read --uri content://packagename/../../../../../../../../../../../../../../../../data/data/packagename/files/mySecretFile
 ```
	  
	  - not: you can put as much ../ as you want 

