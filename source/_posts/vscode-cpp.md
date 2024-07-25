---
layout:     post
title:      "Ubuntu18 VsCode搭建C++编译环境(已测试)"
date:       2018-11-21 14:43:00
categories: Computer Programs
tags: [๑C++, ๑VsCode, ๑Ubuntu]
description: "学习记录"
---

> 坑了一早上,终于摸索出两个编译运行C++的方法,特此记录.

## 环境
---

- 安装VsCode和g++环境这里就不赀述了

## 安装C++插件
---

- 安装一系列C++的插件,我安装的有:
```
C/C++
C/C++ Intellisense
```

## 重点
---

### 两种方法编译C++文件

#### 第一种:安装C/C++ Compile Run插件(简单,推荐)

- 人生苦短,何必浪费时间在环境搭建上~

- 虽然只支持单文件(single file)的编译和运行,但是日常使用足够了啊

- 打开C++文件F6即可运行

- 官方使用手册:
>Requirements
If you are on linux you must install gcc
If you are on window you must install mingw
How to use
Make sure you have .c or .cpp file open and press "F6", this will compile the file. If you want to register gcc/g++ path manually you can set it under settings. You can also set to save file before compiling.

#### 第二种:手动添加task.json和launch.json

- 打开C++文件,切换到Debug下,运行一次,他会创建一个默认文件,改成如下即可:
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceRoot}/${fileBasenameNoExtension}.o",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceRoot}",
            "environment": [],
            "externalConsole": true,
            "preLaunchTask": "build",  
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

- 然后切回C++文件,`Ctrl + Shift + B` build >> 选择other新建一个 >> 修改tasks.json如下:
```
{  
    "version": "0.1.0",  
    "showOutput": "always",  
    "tasks": [
        {
            "taskName": "build",
            "command": "g++",
            "isShellCommand": true,
            "showOutput": "always",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${workspaceRoot}/${fileBasenameNoExtension}.o"
            ],
            "problemMatcher": [
                "$g++"
            ]
        }
    ]  
}
```

### 最后

- `Ctrl + Shift + B` build

- 点击debug下的绿色箭头即可运行

> 愿天下再没有配环境的坑~
