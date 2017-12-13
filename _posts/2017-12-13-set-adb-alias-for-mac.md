---
published: true
tags: 'android, mac'
---

* Set a symbolic link on */Developer*

```bash
$ sudo ln -s /Users/manina7539/Desktop/Driver/Android/Sdk/platform-tools/adb /Developer/adb

```

* Edit */etc/bashrc*

```
alias adb='/Developer/adb'
```

* Export to OS

```bash
$ source /etc/bashrc
```
