---
layout: post
title: "Singleton Pattern"
date: 2021-08-15 20:00 +0900
categories: [Desgin Pattern,Singleton Pattern]
tags: [desgin pattern]     # TAG names should always be lowercase
---

# 1. 싱글톤 패턴이란?
- 객체를 딱 하나만 생성해 생성된 객체를 이용해 프로그램 어디에서나 접근하여 사용할 수 있도록 하는 패턴
- DBCP(DateBase Connection Pool)처럼 공통된 객체를 여러 개 생성해서 사용해야 하는 상황에 많이 사용
  - 쓰레드풀, 캐시, 대화상자, 로그 기록 등
  
![image](https://user-images.githubusercontent.com/48194683/126578659-0047937d-9415-4f2b-b7d2-cc917db9e2c9.png)

### 장점
- 고정된 메모리 영역을 얻으면서 한번의 new 를 통해 인스턴스를 만들기 때문에 **메모리 낭비를 방지**
- 싱글톤으로 만들어진 클래스의 인스턴스는 **전역 변수**이기 때문에 다른 클래스 인스턴스들의 데이터 공유가 쉽다.
- 인스턴스가 절대적으로 한 개만 존재함을 보증할 수 있음
- 싱글톤 객체를 사용하지 않을 경우 **인스턴스를 생성하지 않는다.**
- 싱글톤 상속이 가능하다

### 단점
- 싱글톤의 역할이 커질수록 결합도가 높아져 객체 지향 설계 원칙에 어긋날 수 있다
- 멀티쓰레드 환경에서 컨트롤이 어렵다
- 객체 파괴 시점을 컨트롤하기 어렵다

<br>

# 2. 구현 방법
- 외부에서 객체를 상성할 수 잆도록 **생성자를 Private** 로 선언 (즉, 객체 생성을 내부에서 관리)
- 외부에서 싱글톤 클래스의 객체에 접근할 수 있도록 GetInstance()메소드를 정의
  - 생성자를 Private로 했기 때문에 GetInstance() 메소드를 접근하기 위해 **Static으로 정의**해야 한다

```cs
public class SingleTonObject
{
    private SingleTonObject() { }
    private static SingleTonObject instance = null;

    public static SingleTonObject GetInstance()
    {
        // 객체 할당이 되어 있지 않다면, 새로운 객체 생성
        if (instance == null)
            instance = new SingleTonObject();

        return instance;
    }
}
```
<br>

# 3. 멀티 스레드 환경
- 멀티 스레드 환경에선 고려해야 할 사항들이 있다.
- 두 개 이상의 스레드가 싱글톤 클래스의 인스턴스를 획득하기 위해 GetInstance() 메소드에 접근하면 경합을 벌이는 과정 중 **서로 다른 두 개의 인스턴스**가 만들어질 수 있다.



### 해결 방법 1
### 인스턴스를 필요할 때 생성하지 않고 처음부터 인스턴스를 만든다.

- 인스턴스를 미리 만들어버리면 인스턴스가 자원을 많이 차지하는 컴포넌트일 경우 **시스템 리소스가 쓸데없이 낭비될 가능성**이 있다

```cs
public class SingleTonObject
{
    private SingleTonObject() { }
    
    // 미리 인스턴스를 생성해 둔다
    private static SingleTonObject instance = new SingleTonObject();

    public static SingleTonObject GetInstance()
    {
        return instance;
    }
}
```

### 해결 방법 2
### GetInstance() 메소드를 동기화시킨다.

- 메서드를 동기화시키면 일반적으로 **성능이 100배 정도 저하**된다고 한다.
- 동기화 시키면 GetInstnace() 속도가 엄청나게 저하되므로 **속도가 그렇게 중요하지 않다고 판단될 경우에만 사용**
- **동기화로 인한 오버헤드를 감수**해야 함 

\<C# 예시\>
```cs
public class SingleTonObject
{
    private SingleTonObject() { }
    private static SingleTonObject instance = null;

    public static SingleTonObject GetInstance
    {
        get
        {
            lock (instance)
            {
                if (instance == null)
                    instance = new SingleTonObject();

                return instance;
            }
        }
    }
}
```

<br>

# 4. Singleton Vs Static Class

- 두 개의 성능 차이는 무시해도 될 정도로 크게 나지 않음


### 차이점
- 싱글톤 패턴은 static 인스턴스를 미리 생성해놓는 경우를 제외하고 **객체가 필요한 상황이 되었을 때 인스턴스를 생성**


- (주관적인 생각)   
반면, Static 변수를 사용하면 대부분 경우 프로그램이 시작할 때 미리 객체가 생성된다.
   - **이 객체가 자원을 많이 차지하고 어플리케이션이 종료될 때까지 한번도 쓰지 않는다면 자원을 낭비하는 꼴이 된다.**

|                차이점               	|                               SingleTon                              	|                  Static Class                 	|
|:-----------------------------------:	|:--------------------------------------------------------------------:	|:---------------------------------------------:	|
|                 원리                	| 사용자 요청 시 하나의 인스턴스를 생성해<br> 생성된 인스턴스를 재사용 	| 인스턴스를 만들 수 없고 생성자 또한 갖지 않음 	|
| 인터페이스 구현<br>(가장 큰 차이점) 	|                                   O                                  	|                       X                       	|
|              Follow OOP<br>(나름 중요한 이유라 생각)             	|                                   O                                  	|   X <br>(절차적 디자인으로 '함수'에 가까움 )  	|
|               Override              	|                                   O                                  	|                       X                       	|
|                 load                	|                       필요할 때 Lazy Load 가능                       	|               컴파일 타임에 생성              	|
|             performance             	|                            상대적으로 느림                           	|                      빠름                     	|


##### 싱글톤 클래스 쓰는 경우
- **하나의 인스턴스**만 있어야 하는 경우 (로깅, DB커넥션 등 하나의 인스턴스를 통해 처리해야 할 때)
- Static 클래스처럼 사용해야 하지만 **인터페이스와 다형성 구현이 필요할 때**
- 프로그램 실행 중에 **항상 사용하는 것이 아닌 경우** (즉, 사용하지 않는 경우가 있을 때)

##### Static 클래스를 쓰는 경우
- 간단하게 Utility 용도로 사용되는 함수와 같이 **Static 만으로 간단히 해결할 수 있는 것들**
- 싱글톤이 상태를 가지지 않고 **global access를 제공할 때**


\<참고 자료\>   
[os94 님의 네이버 블로그](https://m.blog.naver.com/ss1511/221586516299)   
[bradkwon.github.io - 싱글톤 패턴 VS Static 클래스 in C#](https://bradkwon.github.io/tech/2019/03/07/singleton-vs-static-kr/)
