- There will be applications where in its manifest file, exported="true" attribute is found 
- This can be intentional or unintentional
- These publicly exported apps can be accessed by another apps resulting in malicious apps to cause un intended activities to be triggered.

`Scenario:` App named `victim.apk` have its activities publicly exported. now the user unintentionally installed `malware.apk` now this app can trigger the `victim.apk`  into executing things that they like for example deleting the user account.

