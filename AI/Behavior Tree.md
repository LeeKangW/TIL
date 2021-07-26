Behavior Tree
===
<참고 자료>   
[Line Engineering - Behavior Tree를 알아봅시다.](https://engineering.linecorp.com/ko/blog/behavior-tree/)   
[병아리 개발자의 삐약삐약 - 0708 Game AI Behaviour Tree](https://bin-repository.tistory.com/23)
[그냥 그런 블로그 - Behavior Tree 개념 및 동작](https://lifeisforu.tistory.com/327)

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


# 2. TASK
- BT는 태스크(TASK) 집합으로 구성
- BT는 모든 것을 노드(Node)로 표현
- 보통 Task와 Node 용어를 **같은 의미**로 사용하는 경우가 많음 
- BT의 구현에 따라 조금씩 다르지만, Task의 종류는 크게 4개로 나누어진다.
  - Composite
  - Decorator
  - Condition
  - Action

### Action
Action Task는 **실제 행동을 표현하는 단말 노드** 이고, 이것은 항상 **True** 나 **False**를 반환하게 되어 있다.

일반적으로
- Action.OnStart()
- Action.OnUpdate()
- Action.OnEnd()   
와 같은 메소드를 가지는데, **Action.OnUpdate()에서 true나 false를 반환**하면 그 Action의 작업은 끝이 난다.

