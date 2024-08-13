### Major Layers

The main components of Android architecture are : 
 
- Linux Kernel
- Hardware Abstraction Layer 
- Libraries, ART, Dalvik
- Application framework
- Applications.

![[../images/Screenshot 2024-08-08 at 11.24.41 AM.png|Screenshot 2024-08-08 at 11.24.41 AM.png]]




### 1. Linux Kernel

- Manages all the available drivers such as display drivers, camera drivers, Bluetooth drivers, audio drivers, memory drivers, etc.

- Responsible for management of memory, power, devices etc

### 2. Hardware Abstraction Layer 
- **Hardware Abstraction Layer** just gives Applications direct access to the Hardware resources.

### 3. **Libraries , Android Runtime and Dalvik** 
- Libraries run like Webkit library is used for browsing the web , SQLite library is used for maintaining SQL database and so on
- **Dalvik Virtual Machine** which is specifically designed by Android Open Source Project to execute application written for Android.Each app running in the Android Device has its own Dalvik Virtual Machine
-  **Android Runtime (ART)** is a alternative to Dalvik Virtual Machine which has been released with Android 4.4 as an experimental release, in Android Lollipop(5.0) it will completely replace Dalvik Virtual Machine.
- Major change in ART is because of Ahead-of-time(AOT) Compilation and Garbage Collection. In Ahead-of-time(AOT) Compilation ,android apps will be compiled when user installs them on their device whereas in the Dalvik used Just-in-time(JIT) compilation in which byte-code are compiled when user runs the app. 

### 4.**Application Framework**
- The Application Framework layer provides many higher-level services to applications in the form of Java classes.