---
title: Create React App Not Working?
date: 2020-12-21 22:56:43
tags: [react, wsl, create-react-app, CHOKIDAR_USEPOLLING]
categories:
- [WebDev]
- [ReactJS]
- [Issue]
---

## If You are using WSL2 on Windows 10, And your Create React App is not refreshing or Hot reloading after you make changes to the file and save. Then this article is for you.

### Problem : **WSL 2: ReactJS not reloading after saved.**


**Solution** : I recently installed WSL 2 but when I create an app using ```create-react-app``` and use ```npm start``` the app was’t reloaded when I edited and saved some file. So I searched the web looking for solutions. And got to know that, here problem is not with ```Create React App``` or *React JS* but with the *WSL2 windows*, WSL2 changed the file sharing protocol, from using their own custom developed protocol using the *9P protocol*, which at this time might not support file changes event. 


**How to FIX this issue** :

### **Solution 1**:

The simplest solution is, 

You can put your code on the *Linux file system* 
(example : in your user’s home directory ```~/home/user/```),
and access these files through the *WSL share*, 

i.e. Simply write ```\\wsl$\DISTRO_NAME``` in Windows File Explorer.

In the Windows explorer, if you go to ```\\wsl$\``` ,

You should see all your WSL Linux distros installed and can access all the files on their file systems.

**In simple words : Move your files to your WSL2 distro (ubuntu) File System.**

- BONUS : You only get the speed improvements (inside WSL) if your files are on the Linux side too.

### **Solution 2**:

Above Problem can be solved by Tweaking our File Watcher i.e. CHOKIDAR

*Chokidar* is a file watcher for *Node* , so it handles the *"proxy"* part of your development setup (remote container, WSL, VM, etc.).

Hence to Solve this issue,
Inside your ```package.json```

**Find**

```json
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```

and **Replace** it with

```json
"scripts": {
    "start": "CHOKIDAR_USEPOLLING=true react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```

If You Find This Helpful Make Sure To [Follow Me On Twitter](https://twitter.com/prajjwal_datir)
For Latest Updates & Knowledge.