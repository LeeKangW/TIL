
Observer Pattern(관찰자 패턴)
===
[게임 프로그래밍 패턴](https://www.hanbit.co.kr/store/books/look.php?p_code=B4342659595) 책으로 공부하면서 정리한 내용입니다.   
자세한 내용을 원한다면, 책을 구매해서 확인해주세요.

(정리하다 보니 내용이 지저분합니다 T.T)

***
```
객체 사이에 '일대 다의 의존 관계'를 정의해두어, 
어떤 객체의 상태가 변할 때 그 객체에 의존성을 가진 다른 객체들이 그 변화를 통지 받고 자동으로 업데이트 될 수 있게 만듭니다.
("GoF의 디자인 패턴" 382쪽)
```
모델-뷰-컨트롤러(Model-View-Controller)(MVC) 패턴 구조를 쓰는 프로그램이 엄청 많은데 그 기반에는 관찰자 패턴이 있다.   

관찰자 패턴이 워낙 흔해   
Java 에는 핵심 라이브러리(java.util.Observer)에 들어가 있고,   
C# 에는 event 키워드로 지원한다.

## 0. 관찰자 패턴 언제 사용하는가?
- A라는 이벤트가 있다고 가정할 때 A 이벤트 발생에 따라 여러 가지 작업이 이루어져야 할 때 사용

***
## 1. 관찰자 패턴 예시 및 설명(업적 시스템을 개발)
- 특정 기준을 달성하면 배지를 얻을 수 있고, 배지 종류는 수백 개가 넘는다고 가정
- 업적 종류가 광범위하고 달성할 수 있는 방법도 다양하다 보니 깔끔하게 구현하기 어렵다.

- 이럴 때 **관찰자 패턴** 을 사용한다.
- 관찰자 패턴을 사용하면, 어떤 코드에서 흥미로운 일이 생겼을 때 **누가 받든 상관없이** 알림을 보낼 수 있다.

Ex)   
<'다리에서 떨어지기'업적을 구현하는 예시>   
이 코드는 '방금 떨어지기 시작했으니 누군지는 몰라도 알아서 하시오' 라고 알려주는게 전부인 코드   
```C++
void Physics::updateEntity(Entity& entity)
{
  bool wasOnSurface = entity.isOnSurface();
  entity.accelerate(GRAVITY);
  entity.update();
  if(wasOnSurface && !entity.isOnSurface())
  {
    notify(entity, EVENT_START_FALL);
  }
}
```

- 업적 시스템은 물리 엔진이 알림을 보낼 때마다 받을 수 있도록 **스스로를 등록**한다.
- 업적 시스템은 떨어지는 물체가 업적 상황이 맞는지 확인한 뒤에 업적을 잠금해제한다.(이런 과정에서 물리 코드는 전혀 몰라도 된다.)
- 물리 엔진 코드는 전혀 건드리지 않은 상태로 업적 목록을 바꾸거나 아예 업적 시스템을 떼어낼 수도 있다. 단지 물리 코드는 누가 받든 말든 계속 알림만 보내는 것이다.

## 2. 작동 원리
책의 예시 코드를 사용했습니다.

<details>
  <summary>관찰자</summary>
  
#### 관찰자
- Observer Class는 아래와 같이 인터페이스로 정의한다.
- 어떤 Class든 Observer 인터페이스를 구현하기만 하면 관찰자가 될 수 있다.
``` C++
class Observer
{
  public: virtual ~Observer(){}
  // onNotify() 파라미터에 어떤 값을 넣을지는 개발 상황에 맞추어 하면 된다.
  // 이런 점이 '패턴'이라 불리는 이유
  // 보통은 알림을 보내는 '객체'와 다른 '구체적인 정보'를 담은 일반적인 데이터를 넘긴다.
  virtual void onNotify(const Entity& entity, Event event)=0;
}
```
  
</details>

***
<details>
  <summary>업적 시스템</summary>
  
#### 업적 시스템

```C++
class Achievements : public Observer
{
  public:
    virtual void onNotify(const Entity& entity, Event event)
    {
      switch(event)
      {
        case EVENT_ENTITY_FELL:
          if(entity.isHero() && heroIsOnBridge)
          {
            unlock(ACHIEVENT_FELL_OFF_BRIDGE);
          }
          break;
          // 그 외에 다른 이벤트를 추가하고
          // heroIsOnBridge 값을 업데이트
      }
    }
    
  private:
    void unlock(Achievement achievement)
    {
      // 아직 업적이 잠겨 있다면 잠금 해제
    }
    bool heroIsOnBridge;
};
```
  
</details>

***
<details>
  <summary>대상</summary>
  
#### 대상
- 알림 메서드는 관찰당하는 객체가 호출한다.
- GoF에선 이런 객체를 **대상(subject)** 라고 부른다.
- 대상에겐 두 가지 임무가 있는데
  - 1. 알림을 끈질기게 기다리는 관찰자 목록을 들고 있는 것
  - 2. 알림을 보내는 것

#### 예시

- 아래 코드에서 중요한 점은 **관찰자 목록을 밖에서 변경할 수 있도록 API를 public으로 열어두었다는 것**
```C++
class Subject
{
  private:
    Observer* oberservers[MAX_OBSERVERS];
    int numObservers;
  
  protected:
  void notify(const Entity& entity, Event event)
  {
    for(int i=0; i < numObservers; i++)
    {
        observers[i]->onNotify(entity, event);
    }
  }
  public:
    void AddObserver(Observer* observer)
    {
      // 배열에 추가
    }
    void RemoveObserver(Observer* observer)
    {
      // 배열에 제거
    }
  
}
```
- 이를 통해 누가 알림을 받을 것인지 제어할 수 있다.
- 대상은 관찰자와 상호작용하지만, 서로 **커플링**되어 있진 않다.

- 대상이 관찰자를 여러 개의 **목록**으로 관리하는 점이 중요
  - 자연스럽게 관찰자들은 암시적으로 **서로** 커플링되지 않게 된다.   
  - 예를 들어,
    - 오디오 엔진도 뭔가가 떨어질 때 적당한 소리를 낼 수 있도록 알림을 기다리는 중일 때
    - 대상이 관찰자를 **하나만** 지원한다면, 오디오 엔진이 자기 자신을 관찰자로 등록할 때 업적 시스템은 관찰자 목록에서 **제거**될 것이다.
    - 즉, 두 시스템이 서로 방해하는 것(나중에 추가된 관찰자가 먼저 있던 관찰자를 못 쓰게 만듦)

- 뭔가 중요한 일이 생기면, 알림을 보내는 메소드를 호출해 **전체 관찰자에게 알림을 전달**하여 일을 처리한다.

</details>

***
<details>
  <summary>관찰 하는 내용(예시는 다리에서 떨어지는 것임으로 '물리 관찰')</summary>
  
  
  - 관찰 할 내용에 훅(hook)을 걸어 알림을 보낼 수 있게 하고 스스로를 등록한다.
GoF의 디자인 패턴에 나온 방식과 비슷하게 구현하기 위해 Subject 클래스를 상속받는다.
  
```C++
  class Physics : public Subject
  {
    public:
  void updateEntity(Entity& entity);
  }
```
- 상속 받음으로써, Subject 클래스의 notify() 메서드를 protected로 사용할 수 있다.

- addObserver() 와 removeObserver()는 public이므로, 물리 시스템에 접근만 할 수 있다면 어디서나 물리 시스템을 관찰할 수 있다.

- 위와 같이 설정함으로써 물리 엔진에 중요한 일이 발생하면, 예제처럼 notify()를 호출해 전체 관찰자에게 알림을 전달하여 일을 처리할 수 있다.   
  
</details>

***
<details>
  <summary>요약</summary>
 
정리하면,
  - Observer 인터페이스: 관찰자로서 **알림을 받을 수 있는 메소드(이하 A메소드)** 를 가진 인터페이스

  - 관찰자: Observer 인터페이스를 상속받으며, A메소드에 알림을 받아 처리할 내용을 구현한다.

  - 대상: 여러 관찰자 목록을 가지고 있으며, 어떤 이벤트가 발생할 시 **관찰자에게 알림을 보낸다.** (즉, 관찰자에게 **관찰을 당하는 대상이다**)

  - 관찰 내용: 대상 클래스를 상속 받으며, **관찰 내용이 발생**하면 대상 클래스에 정의된 **알림 발생 메소드를 통해 관찰자에게 알림을 보낸다.**

순서로 보게 되면,

1. 관찰 내용이 발생
2. 관찰자에게 발생한 내용을 알림
3. 알림을 받은 관찰자는 알림 내용을 가지고 작업을 수행

이다.

</details>


## 3. 주의할 점
#### 관찰자 패턴은 동기적
- 관찰자 패턴은 **동기적**이다.
- 즉, 대상이 관찰자 메서드를 직접 호출하기에 모든 관찰자가 알림 메서드를 반환하기 전까지 다음 작업을 진행할 수 없다.

- 관찰자를 멀티스레드, 락(lock)과 함께 사용할 때는 더욱 조심해야 한다.
  - 어떤 관찰자가 대상의 락을 물고 있다면 게임 전체가 **교착상태**에 빠질 수 있기 때문
- 멀티스레드를 많이 쓰고 있는 프로그램이라면, **이벤트 큐**를 이용해 비동기적으로 상호작용하는게 더 좋은 선택일 수 있다고 한다
 
#### 동적할당 문제
- 관찰자 패턴은 관찰자 목록을 가지고 있어야 하기 때문에 동적 할당으로 관찰자를 추가, 삭제 해야 한다.
- 관찰자가 추가 될 때만 메모리를 할당함으로, 처음 세팅할 때 관찰자들을 등록해놓고 건드리지 않으면 메모리 할당은 일어나지 않는다.
- 이 방법을 해결하기 위해, **연결 리스트** 를 사용할 수 있다.

#### 대상과 관찰자 제거
- 대상이나 관찰자를 부주의하게 삭제하다 보면 대상이 있는 포인터가 이미 삭제된 객체를 가리킬 수 있다
- GC가 있을 경우, 제거를 하지 않으면 GC가 이를 수거하지 않고 쓸데 없는 비용 낭비를 초래할 수 있다.
  - 책에서는 **사라진 리스너 문제** 라는 이름이 생길 정도로 유명한 문제라고 한다.

<대상 제거 방법>
- 대상이 삭제되기 직전에 마지막으로 **사망** 알림을 보내면 된다.
- 사망 알림을 통해 대상의 존재 여부를 알 수 있다.

<관찰자 제거 방법>
- 가장 쉬운 방법은 관찰자가 삭제될 때 스스로를 등록 취소하는 것이다.
