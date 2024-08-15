- **`AndroidManifest.xml`**: the manifest file in binary XML format.

- **`classes.dex:`** application code compiled in the `dex` format. 

- **`resources.arsc`:** file containing precompiled application resources, in binary XML. 

- **`res/`:** folder containing resources not compiled into `resources.arsc`

- **`assets/`:** optional folder containing applications assets, which can be retrieved by AssetManager. 

- **`lib/`:** optional folder containing compiled code - i.e. native code libraries.

- **`META-INF/`:** folder containing the MANIFEST.MF file, which stores meta data about the contents of the JAR. which sometimes will be store in a folder named original.The signature of the APK is also stored in this folder.
