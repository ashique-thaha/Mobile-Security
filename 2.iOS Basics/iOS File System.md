iOS application's file system is divided into two paths:
- Bundle Path
- Data Path

#### Bundle Directory
- located under - /var/containers/Bundle/Application/UUID 
- This is signed to prevent tampering.

#### Data Directory
- located at  /var/mobile/Containers/Data/UUID 
- provided to the application for storage of data at runtime
- uuid for the two directories are not the same.

- Applications are provided special purpose directories:
  - ﻿﻿Documents/ - user-generated content
  - ﻿﻿Library/ - files that are not user data
  - ﻿﻿Library/Application Support/ - hidden support files
  - ﻿﻿Library/Caches/ - cache data*
  - ﻿﻿Library/Preferences/ - preference files
  - ﻿﻿tmp/ - temporary data that may be purged*
  - SystemData - OS stores files in this folder that are related to the app but the files are not accessible to the app 

#### File Encryption
- To protect sensitive data stored at runtime, Through the data protection API, apple provides per-file encryption.
- There are four levels of protection provided, also known as data protection classes.

- The lowest protection is none and highest is complete. They are:
  - ﻿﻿NSFileProtectionComplete
  - ﻿﻿NSFileProtectionCompleteUnlessOpen
  - ﻿﻿NSFileProtectionCompleteUntilFirstUserAuthentication
  - ﻿﻿NSFileProtectionNone

- These data protection class determines when the keys to decrypt these files are available
-  `NSFileProtectionNone` :: decryption keys are always available
-  `NSFileProtectionCompleteUntilFirstUserAuthentication` :: keys are available once the device has been booted and unlocked and remain available until the device is rebooted.
-  `NSFileProtectionCompleteUnlessOpen` :: keys are available for files that are open at the time a device is locked but otherwise keys are only accessible when the device is unlocked.
-  `NSFileProtectionComplete` :: keys are unavailable as soon as the device is locked regardless the files are in use.

#### Data Protection API
- For the None and `CompleteUntilFirstUserAuthentication` classes, data can be accessed when the device is locked
- But for the usb connected the user should trust it first.
- also device must be unlocked.