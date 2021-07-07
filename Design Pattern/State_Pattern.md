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

# 3. 특이점
* 가질 수 있는 '상태'가 **한정적이다(=유한하다)**
* 한 번에 **한 가지** 상태만 가질 수 있다
* 각 상태에는 입력에 따라 다음 상태로 바뀌는 **전이** 가 있다

# 4.구현 방법
* Interface(또는 abstract)를 통해 State Pattern으로 쓰이는 Class들에게 동일한 메소드를 구현하도록 설정   
Ex)
``` 
public interface IState
{
    /// <summary>
    /// 상태 진입에 수행해야 할 행동
    /// </summary>
    void OperateEnter();
    
    /// <summary>
    /// 매 프레임마다 수행해야 할 행동
    /// </summary>
    void OperateUpdate();
    
    /// <summary>
    /// 상태에 빠져나올 때 수행해야 할 행동
    /// </summary>
    void OperateExit();
}

```

* 각 상태 Class에 Action()을 정의한다.
* **내부에 세부 기능을 정의**하고 **외부에서 Action() 메소드만 호출**하면 상태가 돌아갈 수 있도록 구현
Ex)
    * Jump    (Action() => 점프)
    * Run     (Action() => 달리기)
    * Idle    (Action() => idle)
    * Attack  (Action() => 공격)
  * 객체가 가질 수 있는 상태를 **ENUM 으로 정의**해 현재 구현되어 있는 **상태를 보기 쉽게 설정하면 더 좋다**
* 상태를 이용할 객체에서 Action() 메소드를 호출해 자신에게 맞는 상태를 행동한다.

# 4. 구현 구조
![image](https://user-images.githubusercontent.com/48194683/124619916-01c37b80-deb4-11eb-8b99-a7ca97ab7240.png)

# 4-1. 예시 코드
* Player
```
public class Player : MonoBehaviour
{
    enum EState
    {
        IDLE,
        RUN,
        ATTACK,
        DEAD,
    }

    // State Machine을 통해 Player 에서 State에 따라 행동을 할 수 있음 (State의 관리는 전적으로 State Machine에게 위임)
    StateMachine stateMachine;
    
    Dictionary<EState, IState> dicStates = new Dictionary<EState, IState>();

        private void Awake()
        {
            dicStates.Add(EState.IDLE, new State.IdleState());
            dicStates.Add(EState.RUN, new State.RunState());
            dicStates.Add(EState.ATTACK, new State.AttackState());
            dicStates.Add(EState.DEAD, new State.DeadState());

            // 첫 State는 Idle State로 설정
            stateMachine = new StateMachine(dicStates[EState.IDLE]);
        }
}
```
***
* State Machine
```
public class StateMachine
    {
        public IState CurrentState { get; private set; }

        /// <summary>
        /// Default State로 처음 세팅되도록 설정
        /// </summary>
        /// <param name="defaultState"></param>
        public StateMachine(IState defaultState)
        {
            CurrentState = defaultState;
        }

        /// <summary>
        /// State 세팅
        /// </summary>
        /// <param name="state"></param>
        public void SetState(IState state)
        {
            if(CurrentState == state)
            {
                DebugHelper.LogError(state.GetType() + " - 같은 상태 반복");
                return;
            }

            // State 변경 전, OperateExit() 메소드 실행
            CurrentState.OperateExit();

            CurrentState = state;

            // State 변경 후, OperateEnter() 메소드 실행
            CurrentState.OperateEnter();
        }

        /// <summary>
        /// State가 매 프레임마다 실행해야 할 행동 실행
        /// </summary>
        public void DoOperateUpdate() => CurrentState.OperateUpdate();
    }
```
***
* 각 State들 (내부 구현은 상황에 맞게)
```
public class IdleState : IState
    {
        public void OperateEnter()
        {

        }

        public void OperateExit()
        {

        }

        public void OperateUpdate()
        {

        }
    }
```
