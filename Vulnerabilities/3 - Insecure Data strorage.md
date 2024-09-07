
`scenario1:` 
-  ﻿***/data/data/[package-name]/shared_prefs*** is a place where many developers store sensitive data, we can just access it using ***ADB*** 
- The ***ADB*** command for this is:
```shell
ADB  shell
cd /data/data/pakage-name/shared_prefs
cat something.xml
```

`scenario2:` 
- here the data is stored in database but we can access it using sqlite3
- by following these commands
- ADB  shell `/data/data/packagename/databases` 
- use sqlite3 and access the database in which the sensitive data is stored.


`scenario3:`
- Here the data is stored in the temp file
- now cat the temp file and just get the password 
- example: 

```shell 
ADB  shell 
cd /data/data/packagename/
cat tmp_file 
```


`scenario4:` 
- here it uses external storage  to store data 
- usually developers hide it in `/mnt/sdcard`
- here file will be something like - `.uinfo.txt` 

