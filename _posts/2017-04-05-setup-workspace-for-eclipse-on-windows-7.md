---
published: true
---
_For using Eclipse, the first step is creating your coding workspace which everytime you can open it and load your preferences to get on work. In this article you will learn how to setup network disk and import your project on that to your workspace so later you can build your Android codes with Eclipse._

### Connect Your Computer with Network Disk
<img src="https://raw.githubusercontent.com/mania7539/articles/gh-pages/images/win7-network-disk-1.png" style="width: 500px;" /></br>

Follow the steps which shows on previous image:
```
Start > Computer > Map Network Drive Button > Enter details of you network disk > Click "Fisish" 
```

### Create Eclipse Workspace
When the first time you open your Eclipse, you will be asked to locate an local address which later you will always use to load preferences of projects. For now, just choose which directory you like to get it started, and I will recommend you to use second disk which your Windows 7 OS doesn't locate.

### Import You Projects
If you already have Android project which you've written before, then via the importing function of eclipse, it will help you to manage them, see if there's any syntax error, potential warning and generate .APK files for you to later install / test on Android devices.

You will get the window for detail Android project setup. According to your status of existing code, there will be different path of importing you need to go through. 

If you don't have .project file in your Android project directory, it means Eclipse has used it before to remember relative project settings to use. So follow the steps below to start importing:</br>

```
Click File > New > Android Project 
	> Project name: better remain your folder name, 
    > Toggle "create project from existing source"
    > Choose the SDK level which you've written on your AndroidManifest.xml 
      (You must know it since it's from your existing codes)
    > Click "Finish"
```

However, if you actually have .project file, then it's purely even simpler just: </br>

```
Click File > Import 
	> General > Existing Projects into Workspace 
    > Select root directory: browse your project directory
    > Click "Finish"
```

Then we can make things done!

### (Optional) Multiple Workspaces for Easily Switching Preferences 
Since you can use different workspace to store different settings and preferences of Eclipse environment, creating more than one workspaces will help you easily get into another working environment quick if you have more than one huge projects which includes multiple Android library projects and main project.

### Relevant Articles for Further Reading
