
- first of all look for the provider tag on manifest file
-  see if its enabled exported= 'true'
- let's take a scenario:
	- There is an application that creates a secret file on `/data/data/appname/secretfile`
	- only the owner or root can access it
	- analysing the source code we found that the app uses a overridden method for content provider for file access
	- usually we will on the `/cache` directory according to the app.
	- so we cannot access the `secretfile` which is in another directory
	- we use `../` just like in web attack here for to bypass the restriction of context. 
	- for that use maximum `../../` as we don't know the exact path.
	- we may go as far as root directory.
	- - on `abd` shell we can test it by this command :
 ```shell
 	 content read --uri    
 	 content://pacakage_name/../../../../../../../../../../../secretfile
 ```
	  - not: you can put as much ../ as you want 

