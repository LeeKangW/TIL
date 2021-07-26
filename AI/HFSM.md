HFSM(Hierarchical Finite State Machine)
===
<참고 자료>   
[늘상의 하루 - FSM - HFSM - BT 구조](https://neulsang-day.tistory.com/30)   

# 1. HFSM
- 계층적 유한 상태 기계
- **FSM의 복잡한 구조를 개선**한 버전
  - 항목별로 분류하여 정리된 FSM

![image](https://user-images.githubusercontent.com/48194683/126942956-580fcaba-988e-4cf0-a299-ea5c8aaa33f7.png)   
출처: https://neulsang-day.tistory.com/30

- FSM이 단순 AI에 최적화되어 있다면 HFSM은 보다 더 복잡한 행동 패턴을 직관적이고 깔끔하게 그릴 수 있음
- 대기, 이동, 공격 각각의 상태로 전이 후 조건에 맞는 하위 상태를 선택하는 구조
- 전체적인 틀은 FSM과 동일함으로 그 수가 늘어난나면 복잡한 구조를 띄게 되고 가독성과 유지 보수가 어렵다
