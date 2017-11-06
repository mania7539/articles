---
published: true
tags:
  - IDE
  - eclipse
  - android
---
_Hey pals, in this article, we will focus on how to connect your development kits and tools to Eclipse, so later soon Eclipse can help you build .APK file and deploy to your Android devices._

_Before you go on with this article, please check if you've already get all the development kits and tools needed. If you don't know what exactly I am talking about, read [Tools Eclipse Required for Custom Android Libraries](https://mania7539.github.io/articles/tools-eclipse-required-for-custom-android-libs.html) first._

_Once make sure you've all done, then move on to the contents below._

### Project Build Settings for Custom Android Package Library
Since our purpose is to use our custom build Android Package Library, this step is **incredibly important** to make sure you won't include the default Android Library to your build path which will cause build fail and syntax errors result in not using the exact library.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-android-project-build-path-uncheck-private-lib.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:

```
Right click on your target project in left panel 
	> Properties 
    	> Java Build Path > Order and Export > Uncheck "Android Private Libraries 
        > Press "OK"
```
**Note:** Everytime you restart Eclipse, it will **automatically check** "Android Private Libraries", so make sure you are fimiliar with this step.

### Locate the Custom Debug.keystore for Your Android Device
Normally Eclipse will use a default Debug.keystore to build .APK file. However, we are using custom Android Package Libraries, most of the time we build our own Debug.keystore. Even more, you may further use system key to generate it to satisfy the authentication of firmware.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-debug-keystore.png" style="width: 500px;" />
</p>

It is how you can locate it to Eclipse:

```
Windows > Preferences 
	> Android > Build 
    	> Browse to fill in debug.keystore location in "Custom debug keystore"
        > Press "OK"
```

**Note:** Make sure you **restart Eclipse** after finish this step or you will not get the correct result to sign the new keystore. 

### Locate the JDK Folder and Set Compatibility to 1.6
Android is using syntax of Java, so it's necessary you provide JDK to make it work. Take a note that for custom Android Pacakge Library, JDK version above 1.6 will have issues during building and bundling .APK due to the evolution of Android VM. So make sure you do things right to choose JDK 1.6.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk.png" style="width: 500px;" />
</p>

The exact steps are:

```
Windows > Preferences 
	> Java > Installed JREs 
    	> Add "Standard VM" > Next
        	> Browse the directory where your JDK is located 
            > Click "Finish"
```

More than careful just check if your compliance level is set to **1.6** as shown in below image.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk-compliance-level.png" style="width: 500px;" />
</p>

Go over the steps like this:
```
Windows > Preferences > Java > Compiler > Compiler compliance level: 1.6 > Press "OK"
```

### Locate Your Default Android SDK Library
Just follow the simple steps below to finish this setup. Notice that this directory will later grow fat once every time you use "SDK Manager" to download latest development tools and kits, so better choose a disk with big enough hard drive space.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/android-sdk.png" style="width: 500px;" />
</p>

Move your fingers and hands now, go!

```
Windows > Preferences 
	> Android 
    	> Browse to fill in Android SDK folder location in "SDK Location" 
        > Press "OK"
```

### Locate Your NDK Library
NDK is what the amazing part which Android connects Java codes with C/C++. If you're interested to write codes with them, you will absolutely use it. For now just finish your work to locate your NDK folder to Eclipse.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-android-ndk.png" style="width: 500px;" />
</p>

Here's where the setup windows at:

```
Windows > Preferences 
	> Android > NDK
    	> Browse to fill in NDK folder in "NDK Location" 
        > Press "OK"
```

Then we're done, isn't it as simple as piece of cake?! :)

<!--
### Relevant Articles for Further Reading
-->
