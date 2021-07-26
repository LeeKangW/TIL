Behavior Tree
===
<참고 자료>
[Line Engineering - Behavior Tree를 알아봅시다.](https://engineering.linecorp.com/ko/blog/behavior-tree/)
[병아리 개발자의 삐약삐약 = 0708 Game AI Behaviour Tree](https://bin-repository.tistory.com/23)

# 1. Behavior Tree란?
[자세한 내용은 Wikipedia](https://en.wikipedia.org/wiki/Behavior_tree_(artificial_intelligence,_robotics_and_control))

- 복잡한 Game AI를 구현할 때 많이 사용
- Halo, Bioshock 및 Spore와 같은 다양한 게임에서 광범위하게 사용
- 행동(Behavior)를 트리(tree)구조로 기술
  - 구축이 완료된 Behavior Tree의 데이터 구조는 [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) 또는 [트리](https://en.wikipedia.org/wiki/Tree_(data_structure)) 이다.
- [Unreal Engine](https://docs.unrealengine.com/4.26/ko/InteractiveExperiences/ArtificialIntelligence/BehaviorTrees/)에는 기본 AI로 기능 지원
- 개발 유지 보수가 편리

### 탐색 방법
- 탐색 시, 각 노드는 [깊이 우선 탐색](https://en.wikipedia.org/wiki/Depth-first_search) 으로 탐색
- 탐색 결과, 자식 노드에서 부모 노드로 상태가 반환
  - Success: 실행 성공
  - Failure: 실행 실패
  - Running(Continue): 실행 중. 다음 번에 running을 반환한 노드가 다시 호출
- 모든 노드에 탐색 기능 여부를 나타내는 active/inactive 상태를 설정 가능


# 2. 각 노드의 역활가 사용 방법

### Control flow 노드
- 역할: 노드 아래에 있는 서브 트리(브랜치라 불림)를 통해 표현되는 행동(서브 테스크)을 제어

### Selector
- 역할: 자식 노드 가운데 하나를 실행하기 위한 노드
- 탐색 시, selector의 자식 노드를 왼쪽부터 오른쪽(우선도가 높은 쪽에서 낮은 쪽)의 순서로 깊이 우선 탐색 방식으로 평가
  - 자식 노드 중 하나가 **success**나 **running**을 반환하면, selector는 즉시 success나 running을 **부모 노드에 반환**
  - 모든 자식 노드가 **failure**를 반환했을 때, selector도 부모 노드에 **failure를 반환**
- 
