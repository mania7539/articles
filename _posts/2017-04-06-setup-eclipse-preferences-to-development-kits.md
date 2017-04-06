---
published: true
---
_Hey pals, in this article, we will focus on how to connect your development kits and tools to Eclipse, so later soon Eclipse can help you build .APK file and deploy to your Android devices._

_Before you go on with this article, please check if you've already get all the development kits and tools needed. If you don't know what exactly I am talking about, read [Tools Eclipse Required for Custom Android Libraries](https://mania7539.github.io/articles/tools-eclipse-required-for-custom-android-libs.html) first._

_Once make sure you've all done, then move on to the contents below._

### Project Build Settings for Custom Android Package Library

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-android-project-build-path-uncheck-private-lib.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Right click on your target project in left panel 
	> Properties 
    	> Java Build Path > Order and Export > Uncheck "Android Private Libraries > Press "OK"
```

### Locate the Custom Debug.keystore for Your Android Device

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-debug-keystore.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Windows > Preferences 
	> Android > Build 
    	> Browse to fill in debug.keystore location in "Custom debug keystore"
```

### Locate the JDK Folder and Set Compatibility to 1.6

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Windows > Preferences 
	> Java > Installed JREs 
    	> Add "Standard VM" > Next
        	> Browse the directory where your JDK is located > Click "Finish"
```

In additional to JDK location, also check if your compliance level is set to **1.6** as shown in below image.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk-compliance-level.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Windows > Preferences 
	> Java > Compiler
    	> Compiler compliance level: 1.6 > Press "OK"
```

Then we can make things done!

### Locate Your Default Android SDK Library
<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/android-sdk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Windows > Preferences 
	> Android 
    	> Browse to fill in Android SDK folder location in "SDK Location" > Press "OK"
```

### Locate Your NDK Library
<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-android-ndk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Windows > Preferences 
	> Android > NDK
    	> Browse to fill in NDK folder in "NDK Location" > Press "OK"
```

### Relevant Articles for Further Reading
