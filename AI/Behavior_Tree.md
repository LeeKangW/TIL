Behavior Tree
===
<참고 자료>   
[Line Engineering - Behavior Tree를 알아봅시다.](https://engineering.linecorp.com/ko/blog/behavior-tree/)   
[병아리 개발자의 삐약삐약 - 0708 Game AI Behaviour Tree](https://bin-repository.tistory.com/23)   
[그냥 그런 블로그 - Behavior Tree 개념 및 동작](https://lifeisforu.tistory.com/327)

<details>
  <summary>Behavior Tree란?</summary>
  
# 1. Behavior Tree란?
[자세한 내용은 Wikipedia](https://en.wikipedia.org/wiki/Behavior_tree_(artificial_intelligence,_robotics_and_control))

- 복잡한 Game AI를 구현할 때 많이 사용
- Behavior Tree를 구현하기 위해 일반적으로 **스택(Stack) 자료 구조**를 사용
- Halo, Bioshock 및 Spore와 같은 다양한 게임에서 광범위하게 사용
- 행동(Behavior)를 트리(tree)구조로 기술
  - 구축이 완료된 Behavior Tree의 데이터 구조는 [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) 또는 [트리](https://en.wikipedia.org/wiki/Tree_(data_structure)) 이다.
- [Unreal Engine](https://docs.unrealengine.com/4.26/ko/InteractiveExperiences/ArtificialIntelligence/BehaviorTrees/)에는 기본 AI로 기능 지원
- 개발 유지 보수가 편리

### 평가 및 탐색 방법
- 평가(어떤 행동을 수행해야 하는지를 찾는 행위) 시, 각 노드는 [깊이 우선 탐색](https://en.wikipedia.org/wiki/Depth-first_search) 으로 평가
- 탐색 결과, 자식 노드에서 부모 노드로 상태가 반환
  - Success: 실행 성공
  - Failure: 실행 실패
  - Running(Continue): 실행 중. 다음 번에 running을 반환한 노드가 다시 호출
- 모든 노드에 평가 기능 여부를 나타내는 active/inactive 상태를 설정 가능
  
  
</details>



<details>
  <summary> Task 설명(이론) </summary>

### 태스크 (Task)
- BT의 Leaf 노드로 정의한 Task를 실행
- Task 노드는 자식을 보유하지 않음
  
### Composite Node
- **특정 작업을 실행하지 않는 대신** 자식 노드를 보유한 노드
- 셀렉터(Selector), 시퀀스(Sequence), 심플 페러렐(Simple parallel) 이 있음

#### 셀렉터(Selector)
- 자식 노드 중 하나를 실행하기 위한 노드
- 복수의 선택 중 하나의 행동을 실행해야 할 때 사용
- 자식 노드 작동 순서: 왼쪽 -> 오른쪽 순서로 깊이 우선 탐색 방식으로 순회
- 자식 노드가 success를 반환할 때까지 순회
- 모든 자식 노드가 failure를 반환하면 failure를 반환하고 종료

  
#### 시퀀스(Sequence)
- 자식 노드를 순서대로 진행하는 노드
- 연속적인 행동의 구현이 필요할 때 사용
- 자식 노드 작동 순서: 왼쪽 -> 오른쪽 순서로 깊이 우선 탐색 방식으로 순회
- **자식 노드가 failure를 반환할 때까지 순회**
- 자식 노드 중 하나라도 failure를 반환하면 sequence는 종료
- 모든 자식 노드가 failure를 반환하지 않으면, 모든 자식 노드를 순회하고 sequence 종료

![image](https://user-images.githubusercontent.com/48194683/126947179-38a7cf07-be15-4d29-85c4-95d760869167.png)


### Decorator
- 노드를 실행할 조건을 정의한 노드
- Composite 혹은 Task 노드에 붙여 해당 노드를 실행할 건지 결정

![image](https://user-images.githubusercontent.com/48194683/126948261-a7fa5f6d-853d-41dd-ba39-2aab78b93b64.png)

  
<Node의 리턴 값>   
|   	| Node 리턴 값 	|                설명                	|
|:-:	|:------------:	|:----------------------------------:	|
| 1 	|    Success   	|                완료                	|
| 2 	|    Failure   	|                실패                	|
| 3 	|    Running   	|            현재 진행 중            	|
  
</details>



<details>
  <summary> Task 설명(코드 구현 느낌으로 설명) </summary>

<br/>

[그냥 그런 블로그 - Behavior Tree 개념 및 동작](https://lifeisforu.tistory.com/327)<br/>
의 내용을 정리했습니다. <br/>
자세한 내용은 위 블로그에서 확인해주세요.<br/>
<br/>
  
# 2. TASK
- BT는 태스크(TASK) 집합으로 구성
- BT는 모든 것을 노드(Node)로 표현
- 보통 Task와 Node 용어를 **같은 의미**로 사용하는 경우가 많음 
- BT의 구현에 따라 조금씩 다르지만, Task의 종류는 크게 4개로 나누어진다.
  - Composite
  - Decorator
  - Condition
  - Action

### Action Task
Action Task는 **실제 행동을 표현하는 단말 노드** 이고, 이것은 항상 **True** 나 **False**를 반환하게 되어 있다.

일반적으로
- Action.OnStart()
- Action.OnUpdate()
- Action.OnEnd()   

와 같은 메소드를 가지는데, **Action.OnUpdate()에서 true나 false를 반환**하면 그 Action의 작업은 끝이 난다.

<스택에서 작동법>
- 처음 올라갈 때 OnStart() 호출
- true나 false를 반환하지 않으면 계속해서 OnUpdate() 호출
- true나 false를 반환하면, 스택에서 빠지면서 OnEnd() 호출


### Composite Task
Composite Task는 우리말로 복합 태스크이다.   
이것은 말 그대로 **여러 개의 자식으로 구성된 Task**이다.   
자주 사용되는 Composite으로는 Select, Sequence 등이 있고, 이러한 Composite의 핵심 용도는 **node의 flow를 제어하는 것**이다.   

기본적으로 node의 실행 순서은
- 위에서 아래로
- 왼쪽에서 오른쪽

이다.

#### Select Composite
- 자식 노드가 **true를 반환**할 때까지 자식 노드를 실행
- 말 그대로 하나를 선택해서 실행

#### Sequence Composite
- 자식 노드가 **false를 반환**할 때까지 자식 노드를 실행
- 말 그대로 순차적 실행

#### Conditional Aborts
- 한국말로 조건부 취소
- 어떤 구현에서는 Reactive Evaluation 이라 한다.
- BT 말단 노드에 존재하는 Action이 true 나 false를 반환하지 않아 계속 OnUpdate()를 호출할 때 외부에서 강제적으로 그 Action을 종료하고 싶을 때 사용

<구성>
- Self: 자신의 하위에 있는 Task를 취소
- Lower Priority: 자신의 오른쪽에 있는 이웃 노드의 흐름을 취소
- Both: Self + Lower Priority

### Decoration Task
- **조건**을 의미
- **하나의 자식**만을 가질 수 있음
  - 조건 만족: 자식을 실행
  - 조건 만족하지 못함: false를 반환
- Probability, TimeOut, CheckEvnet 등에 사용
  
</details>


