---
title: C++内存模型
published: 2024-07-16
description: ''
image: ''
tags: [编程]
category: C++
draft: false 
---
# c++上的内存模型

> c++ 的内存模型定义了程序的存储方式以及如何在计算机内存中访问数据。它主要包含了stack，heap，data，code四大段。

[TOC]

## stack内存

stack内存用于自动存储变量，如局部变量、函数形参、函数返回值等。由于栈内存由编译器来管理，其分配内存与释放内存的操作均是自动完成，而无需程序员干涉。同时由于是栈内存的LIFO数据结构，其最近分配的内存会最先被释放。

```c++
int function(int param)
{
    int i = 10;//i 存储在栈内存中
    // do something
    return 20;
}
```



## Heap 内存

与栈内存管理方式不同，Heap内存的释放均有程序员操作，其主要运用在需要动态(dynamically)分配内存的变量上，C++上的具体操作由new/delete 来完成动态内存的分配与释放，c语言中则是使用malloc/free完成同样的操作。与栈内存相比，堆内存拥有更大的内存可用，但其访问时间比栈内存要慢。

```c++
void function()
{
    int *p  = new int[10];// dynamically allocated int array in heap memory
    // do some thing 
    delete []p;//deallocate memory
} 
```

## Data 段（.rodata,.bss,.data）

Data 段又分为初始化的Data段(.data),未初始化的Data段(.bss),只读Data段（.rodata），其中初始化的Data段主要存储已初始化的全局、static 和const 变量，而未初始化的Data段（.bss）主要存储未初始化的static、global变量,只读Data段包含const变量与字符串常量

```c++
int globalVar0 = 0;//.data
static int globalVar1 = 0;//.data
const int constVar2 = 0;//.data
const char * str = "test";//.rodata
static int globalVar3;
int globalVar4;
```

## code 段（.text）

程序中的函数存储位置