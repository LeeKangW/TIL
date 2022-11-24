---
layout: post
title: Event 와 Delegate 차이
date: 2022-03-17 15:14 +0900
categories: [C#, syntax]
tags: [c#]     # TAG names should always be lowercase
---

# 1. Delegate란?
- delegate: 대리자
- 남의 일을 대신 해주는 역할 이라고 생각하면 된다
- 즉, 대리자를 통해 들어온 업무(메소드)들을 대리자 호출을 통해 한번에 처리하는 개념
- C++ 에선 함수 포인터랑 비슷하다


# 2. Event란?
- delegate의 일종
- delegate가 변수라면 Event는 Property라 볼 수 있다
- Event의 경우 할당을 "="이 아닌 "+=" 으로 해주어야 한다. (추가, 삭제만 가능)
- ⭐⭐⭐⭐⭐⭐ 클래스 외부에서 직접 **이벤트 호출이 불가능** ⭐⭐⭐⭐⭐⭐

### Event: Add 와 Remove
- Property에서 get, set을 사용하듯 event에선 add, remove를 사용
- get, set에서 대입과 리턴하는 일 외에 간단한 체크 코드를 설정하듯 add, remove에서도 이러한 코드를 넣을 수 있음
- add: += (추가)
- remove: -= (삭제)

```cs
class Test
{
  private EventHandler eventWork;
  public event EventHandler EventWork
  {
    add
    {
      eventWork += value;
    }
    remove
    {
      eventWork -= value;
    }
  }
}
```


# 3. 무엇을 써야 하나??
### delegate
- 콜백 메소드

### event
- 객체의 상태 변화
- 사건의 발생을 알림(Ex. 무기로 공격해서 데미지를 줌)
