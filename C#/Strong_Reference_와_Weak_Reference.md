## 1. Strong Reference VS Weak Reference
* 우리 말로 **강한 참조 VS 약한 참조**

* new() 메소드를 사용 -> 강한 참조

* WeakReference 클래스를 사용 -> 약한 참조

* GC가 메모리를 정리할 대상인지 판단하는 여부
   * 강한 참조 : 참조 되어지는 root 객체로부터 사슬이 계속 연결되어 있는가 여부
     * root 란? : 힙에 할당된 메모리의 위치를 참조하고 있는 객체 ( Ex. Object a = new Object(); 에서 변수 a가 root 객체 )
   * 약한 참조 : **가비지 수집에 의한 개체 회수를 허용**하면서 개체를 참조

## 2. 약한 참조를 왜 써야 하는가?
* **강한 참조**에서 아래와 같은 경우가 발생할 시, **사용하지 않는 객체가 GC에 의해 회수되지 않아 메모리 누수가 발생한다.**
* 그러므로, 위와 같은 상황에선 **약한 참조**를 사용해야 한다.

```
즉,
어떤 객체의 '생명 주기'에 관여하지 않고 그 객체를 참조하고 싶을 때 사용하는 것이다.
```

#### 메모리 누수 예시
* class A에서 객체들을 생성
* class B에서 객체 하나를 참조
<p align="left">
  <img src="https://user-images.githubusercontent.com/48194683/124260645-e2061d80-db6a-11eb-8dfa-de98639f04bb.png" width="50%" height="50%">
  
* class A에서 객체를 제거
* GC에서 참조가 끊긴 instance를 삭제
<p align="left">
  <img src="https://user-images.githubusercontent.com/48194683/124260788-0cf07180-db6b-11eb-957f-0ab6fd134b35.png" width="50%" height="50%">
  
* class B가 참조하고 있는 객체는 GC에 의해 수거되지 않음
<p align="left">
  <img src="https://user-images.githubusercontent.com/48194683/124260842-1ed21480-db6b-11eb-863d-c068589079c7.png" width="50%" height="50%">
  

## 3. 사용 방법
```C#
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
