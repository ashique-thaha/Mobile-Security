 There is a list of things that we do on static analysis they are:

- Reading the application code and finding vulnerabilities, sort of code review  using manual or automated testing. We can also look for security misconfigurations, hard-coded strings, Api keys, usernames, passwords, emails  etc.

- Additional enumeration or fingerprinting will also be part of static analysis such as: finding a url that we didn't knew about, Finding emails or usernames, Finding a storage buckets etc.


![[../images/Screenshot 2024-04-10 at 10.14.25 AM.png|Screenshot 2024-04-10 at 10.14.25 AM.png]]


#### Hardcoded strings

These hardcoded string is found in `resources/strings.xml`,  hardcoded strings can also be found in activity source code.


Things we look for:
- ﻿﻿Login bypass (username/password, or client credentials)
- ﻿﻿URLs Exposed (http/https)
- ﻿﻿API Keys Exposed
- ﻿﻿Firebase URLs (firebase.io)
- etc

