State_Pattern
===
# 1. What is State Pattern?
* 객체가 **특정 상태에 따라 행위가 달라지는 상황**에 사용
* 상태를 객체화 하여 상태에 행위를 수행하도록 위임
* **각 Class**에서 수행하는 행위들을 메소드로 표현
* 외부로부터 **캡슐화**하기 위해 **Interface를 생성**하여 시스템의 각 상태를 나타내는 클래스로 실체화

# 2. 장점
* 내부 상태가 바뀜으로써 행동이 달라짐(=상태만 바꿔주면 행동이 바뀐다)
* **동적**으로 상태(=행동) 변경 가능
* 구현한 상태 Class 기능에 변화가 생겨도 **Class의 내부 기능만 수정**하면 되기에 **수정이 용이함**

# 3.구현 방법
* Interface(또는 abstract)를 통해 State Pattern으로 쓰이는 Class들에게 동일한 메소드를 구현하도록 설정
Ex)
``` 
public interface StatePattern
{
    void Action();
} 
```
* 각 상태 Class에 Action()을 정의한다.
* **내부에 세부 기능을 정의**하고 **외부에서 Action() 메소드만 호출**하면 상태가 돌아갈 수 있도록 구현   
  * Ex)
    * Jump    (Action() => 점프)
    * Run     (Action() => 달리기)
    * Idle    (Action() => idle)
    * Attack  (Action() => 공격)
  * 객체가 가질 수 있는 상태를 **ENUM 으로 정의**해 현재 구현되어 있는 **상태를 보기 쉽게 설정하면 더 좋다**
* 상태를 이용할 객체에서 Action() 메소드를 호출해 자신에게 맞는 상태를 행동한다.
