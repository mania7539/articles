---
published: false
---
_Hey pals, in this article, we will focus on how to connect your development kits and tools to Eclipse, so later soon Eclipse can help you build .APK file and deploy to your Android devices. 

Before you go on with this article, please check if you've already get all the development kits and tools needed. If you don't know what exactly I am talking about, read [Tools Eclipse Required for Custom Android Libraries](https://mania7539.github.io/articles/tools-eclipse-required-for-custom-android-libs.html) first.

Once you've all done, move on to the contents below._

### Project Build settings for custom Android package library
<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-android-project-build-path-uncheck-private-lib.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

### Locate the custom Debug.keystore for your Android device
<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/custom-debug-keystore.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

### Locate the JDK folder and set compatibility to 1.6
If you already have Android project which you've written before, then via the importing function of eclipse, it will help you to manage them, see if there's any syntax error, potential warning and generate .APK files for you to later install / test on Android devices.

You can get a window for detail Android project setup. According to your status of existing code, there will be different steps of importing you need to go through. 

If you don't have .project file in your Android project directory, it means Eclipse has used it before to remember relative project settings to use. So follow the steps below to start importing:</br>

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-jdk-compliance-level.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

Then we can make things done!

### Locate your default Android SDK library
Since you can use different workspace to store different settings and preferences of Eclipse environment, creating more than one workspaces will help you easily get into another working environment quick if you have more than one huge projects which includes multiple Android library projects and main project.

<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/android-sdk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

### Locate your NDK library
<p align="left">
	<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/eclipse-android-ndk.png" style="width: 500px;" />
</p>

Follow the steps which shows on previous image:
```
Windows > Preferences > Android > Build > Browse to fill in debug.keystore location in "Custom debug keystore"
```

### Relevant Articles for Further Reading
