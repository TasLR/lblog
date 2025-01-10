---
title: eventRecord
published: 2025-01-10
description: ''
image: ''
tags: [debug]
category: Debug
draft: false 
---
### eventRecord use

#### step
1. keil pack setting
![Image](./demo/packSetting.jpg)
2. eventRecord component setting
![Image](./demo/componentSet.png "icon")
3. include file **EventRecorder.h** and intialize component
```
  EventRecorderInitialize(EventRecordAll, 1U);
  EventRecorderStart();
  printf("log");
```
4. debug view setting
 - enable **periodic windows update**
 - enable **analysis->event Recorder**
 - enable **serial windows->debug viewer**
 [!NOTE] 
    do not use arm6 complier
