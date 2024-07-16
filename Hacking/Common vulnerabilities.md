
 ## Insecure Logging

- Android maintains a centralised `logcat`.
- Typically used by android developers for debugging purposes. it is accessible via adb or other apps.
- This may lead to some vulnerabilities.

`example:`

- To get the logs of a specific app via `adb` : ﻿
```
 adb shell ps | grep -i 'application's name' 
```


- This command will give a result with its process id, like this:
```shell
u0_a87   3515  1447  14029480 131692 do_epoll_wait  0 S jakhar.aseem.diva
```


- `3515` is the process id here. now we give a command using the process id  to  adb to see the log:
```shell
adb  logcat | grep -i `3515`
```


- we can see the sensitive data of the application using  this way. Here in this example i am accessing sensitive information of an application using logcat: 
```shell
- 07-08 07:23:09.871  3515  3515 E diva-log: Error while processing transaction with credit card: 12345566
```


- We can see the credit card details on the log.


## Hard coding issues
-  This vulnerability arises due to hard coded strings or keys leaking sensitive information.
- For to analyse it reverse the app using `jadx-gui`
- Find any thing useful like password usernames, api keys etc.

## Insecure Data strorage
`scenario1:` 
-  ﻿/data/data/[package-name]/shared_prefs is a place where many developers store sensitive data, we can just access it using adb.
- The adb command for this is:
```shell
adb shell
cd /data/data/pakage-name/shared_prefs
cat something.xml
```
`scenario2:` 
- here the data is stored in database but we can access it using sqlite3
- by following these commands
- adb shell `/data/data/packagename/databases` 
- use sqlite3 and access the database in which the sensitive data is stored.


`scenario3:`
- Here the data is stored in the temp file
- now cat the temp file and just get the password 
- example: 

```shell 
adb shell 
cd /data/data/packagename/
cat tmp_file 
```


`scenario4:` 
- here it uses external storage  to store data 
- usually developers hide it in `/mnt/sdcard`
- here file will be something like - `.uinfo.txt` 

## Input validation isuues

`Sql injection:`
- Look for sql queries in source code if visible, then try usual trial and error method based on the query

`URL tampering:`
- here in this specific scenario i am attempting to access local file using `file://`  uri
- here i am giving a sample exploitation: `file:///data/data/jakhar.aseem.diva/uinfo9043715121375703512tmp`
- file on sdcard will also be accessible here.