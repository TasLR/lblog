---
title: c++之继承
published: 2024-07-25
description: ''
image: ''
tags: ["编程"]
category: 'C++'
draft: false 
---

> C++可以基于现有类派生新类的方式实现代码复用。派生类继承了基类的所有成员（数据成员和方法成员）。可以通过派生类来实现功能的扩展。继承分类根据继承的基类数量一般可以分为单一继承和多继承。其中按继承方式（public、protected、private）又可分为3类。

## 单继承

所谓单继承指的是派生类只有唯一的直接基类。

```c++
class Base {
public:
  void print(void) { std::cout << "Base info" << std::endl; }
};

class derive : public Base {
public:
  void print1(void) { std::cout << "derive info" << std::endl; }
};

int main(void)
{
    derive derive1;
    derive1.print();
    derive1.print1();
    return 0;
}
```

 

## 多继承

基于多个基类派生出新的类的方式。

```c++
class Base0 {
public:
  void print0(void) { std::cout << "Base0 info" << std::endl; }
};


class Base1{
public: 
    void print1(void){std::cout<< "Base1 info"<<std::endl;}
};
class derive:public Base0,public Base1{
public:
  void print2(void) { std::cout << "derive info" << std::endl; }
};

int main(void)
{
    derive derive1;
    derive1.print0();
    derive1.print1();
    derive1.print2();
    return 0;
}
```

### 多继承带来的问题

多继承很容易导致新类复杂化。比如多义性，棱型继承。

#### 多义性

子类会强制性继承所有父类的成员，即使这些成员不是子类需要的。这样就会导致子类的职责不明确。

#### 棱形继承

棱形继承即是派生类的多个直接父类派生自同一个父类，因而新派生类有重复的成员，此时通过新派生类对象调用对应的方法会导致歧义行为。

```c++
class Base0 {
public:
  void print0(void) { std::cout << "Base0 info" << std::endl; }
};

class Base1:public Base0{
public: 
    void print1(void){std::cout<< "Base1 info"<<std::endl;}
};
class Base2: public Base1{
public:
    void print2(void){std::cout<< "Base2 info"<<std::endl;}
};
class derive:public Base1,public Base2{
public:
  void print3(void) { std::cout << "derive info" << std::endl; }
};

int main(void)
{
    derive derive1;
    // derive1.print0(); //error
    derive1.print1();
    derive1.print2();
    return 0;
}
```

解决上述问题的方法是采用虚继承的方式派生新类：修改拥有相同父类的派生类的继承方式。

```c++
class Base1:virtual public Base0{
public: 
    void print1(void){std::cout<< "Base1 info"<<std::endl;}
};
class Base2:virtual public Base1{
public:
    void print2(void){std::cout<< "Base2 info"<<std::endl;}
};
```

#### 小结

一般情况下不建议使用类的多继承，因为一个类应当只有一个职责。为了避免继承导致的歧义性，优先考虑组合而非继承。
