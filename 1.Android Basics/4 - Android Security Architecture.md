
- Android is based on Linux OS, which means it can just take commands like ls, cd etc like how we interact with linux.

- The permissions on android files are also same as that on the linux file permission model. eg: `drwxr-xr-x` , `-rw-r--r--`




## Dalvik  VS Android run time 

### Dalvik

- Every application run in a virtual machine known as android run time.
- Dalvik was the original runtime VM,  and still referenced to the name Dalvik byte-code.
- This is not used in modern Android OS, it has been replaced by ART(Android run time).

### Android Run Time

- This is the modern translation of Application's byte-code to device instructions.
- Every app runs its own sandboxed virtual machine.
- similar to the file system the application is isolated by creating a new user unique for that application.



## Android Application Security

- ﻿﻿Every Android Application can be reverse-engineered, rebuilt, re-signed, and re-run
- ﻿﻿This means an attacker can modify application functionality
- ﻿﻿The source code is available by using a tool like JADX-GUI or APKTOOL

![[../images/Screenshot 2024-04-10 at 2.11.38 PM.png|Screenshot 2024-04-10 at 2.11.38 PM.png]]


## Application Signing

- ﻿﻿Since anyone could modify an application and publish it to the Play Store, how do we ensure it's integrity?
- ﻿﻿Answer: Public-key cryptography!
- ﻿﻿Today there are three methods of verifying signatures:
- ﻿﻿APK Signature scheme v1, v2, and v3
- ﻿﻿In addition, Google implemented Google Play signing which adds unique signatures to the apps
- ﻿﻿`keytool, jarsigner, zipalign` 
