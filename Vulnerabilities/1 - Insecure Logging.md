
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

