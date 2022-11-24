---
layout: post
title: Strong Reference 와 Weak Reference
date: 2022-03-17 14:46 +0900
categories: [C#, 메모리 관리]
tags: [c#]     # TAG names should always be lowercase
---

## 1. Strong Reference VS Weak Reference
* 우리 말로 **강한 참조 VS 약한 참조**

* new() 메소드를 사용 -> 강한 참조

* WeakReference 클래스를 사용 -> 약한 참조

* GC가 메모리를 정리할 대상인지 판단하는 여부
   * 강한 참조 : 참조 되어지는 root 객체로부터 사슬이 계속 연결되어 있는가 여부
     * root 란? : 힙에 할당된 메모리의 위치를 참조하고 있는 객체 ( Ex. Object a = new Object(); 에서 변수 a가 root 객체 )
   * 약한 참조 : **가비지 수집에 의한 개체 회수를 허용**하면서 개체를 참조

## 2. 약한 참조를 왜 써야 하는가?

**강한 참조**를 통해 객체를 생성(이하 A)하고 생성한 A 객체를 또 다른 객체인 B가 참조하는 경우,  
A 객체를 정리해도 B 객체는 A 객체를 계속 참조하고 있음으로 **GC에 의해 메모리가 회수되지 않는다.**  
그러므로, 위와 같은 상황에선 **약한 참조**를 사용해야 한다.

```
즉,
어떤 객체의 '생명 주기'에 관여하지 않고 그 객체를 참조하고 싶을 때 사용하는 것이다.
```
  

## 3. 사용 방법

```cs
Test temp = new Test();
  
// 약한 참조
WeakReference weakReference = new WeakReference(temp);

// 객체가 존재하는지 확인
if (weakReference.IsAlive)
{
    // Target => 참조 중인 객체의 정보를 반환한다.
    Console.WriteLine(weakReference.Target);
}
  ```
