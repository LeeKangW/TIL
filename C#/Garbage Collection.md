Garbage Collection 이란?
===
### Garbage Collection이 없다면...
* C++에서는 객체를 할당하기 위해 일일이 메모리 공간을 확보해야 하고, 할당 후 힙을 가리키는 포인터를 유지하다 객체를 더 이상 사용하지 않으면 포인터가 가지고 있는 메모리를 해지해주어야 함
* C/C++에서 프로그래머들은 위와 같이 메모리를 해제하는 걸 깜빡하기 쉬움
* 해제를 했더라도, 해제한 포인터를 해제한지 모르고 접근해 코드를 실행시키는 실수를 하기 쉬움
* 즉, 메모리를 직접 다루고 관리하는 일은 귀찮고 어려운 일 ( 개발자도 사람이기에 이 문제를 100% 해결할 수 없음 )

### C# 에선
* CLR이 자동 메모리 관리(Automatic Memory Management) 기능을 제공
* 위 기능의 중심엔 가비지 컬렉션(Garbage Collection)이 존재


### Garbage Collection
* 우리말로 "쓰레기 수거"
  * 쓰레기 -> 더 이상 사용하지 않는 객체
* Garbage Collection을 통해 프로그래머는 메모리 걱정 없이 코드를 작성할 수 있음

### Garbage Collector
* CLR안에 Garbage Collection을 담당
* 객체 중에 쓰지 않는 것과 쓰는 것을 분리해 쓰지 않는 객체만 수거해 가는 역할

### 그렇다고 항상 좋은 건 아니다
* Garbage Collector도 소프트웨어이기 때문에 CPU와 메모리 같은 컴퓨팅 자원을 소모
* 즉, 코드가 사용해야 하는 자원을 Garbage Collector도 같이 사용
* 즉, Garbage Collector가 사용하는 자원의 양을 최소한을 줄이면 그만큼 많은 자원을 사용할 수 있음

***
Garbage Collection의 원리
===

