---
title: Zephyr RTOS
author: zyr
pubDatetime: 2024-08-01T14:26:00+08:00
slug: blog-zephyr
featured: true
draft: false
tags:
  - zephyr
ogImage: ""
description: zephyr rtos
canonicalURL: https://example.org/my-article-was-already-posted-here
---
## <font face='微软雅黑' color=#F0F8FF size=5>常用命令</font>
激活环境(每次开始时都需要重新激活)
```bash
source ~/zephyrproject/.venv/bin/activate
```
<font face='微软雅黑'>编译</font>
```bash
west build -p always -b nucleo_l476rg
```

## <font face='微软雅黑' color=#F0F8FF size=5>环境变量</font>
添加环境变量  
```bash
sudo vim ~/.zephyrrc
```
```
export MY_VARIABLE=foo
```
在当前命令窗口导入环境变量  
进入zephyrproject/zephyr
```bash
source zephyr-env.sh
```

## <font face='微软雅黑' color=#F0F8FF size=5>程序编写</font>
```
<app>
├── CMakeLists.txt
├── app.overlay    //设备树覆盖文件
├── prj.conf
├── VERSION
└── src
    └── main.c
```