* [이것이 C#이다](https://www.hanbit.co.kr/store/books/look.php?p_code=B6673972966) 책을 참고하여 정리하였습니다.
* 자세한 내용은 책을 구매하여 확인해주세요

Garbage Collection 이란?
===
### Garbage Collection이 없다면...
* C++에서는 객체를 할당하기 위해 일일이 메모리 공간을 확보해야 하고, 할당 후 힙을 가리키는 포인터를 유지하다 객체를 더 이상 사용하지 않으면 **포인터가 가지고 있는 메모리를 해지**해주어야 함
* C/C++에서 프로그래머들은 위와 같이 **메모리를 해제하는 걸 깜빡하기 쉬움**
* 해제를 했더라도, **해제한 포인터를 해제한지 모르고 접근해 코드를 실행시키는 실수를 하기 쉬움**
* 즉, 메모리를 직접 다루고 관리하는 일은 귀찮고 어려운 일 ( 개발자도 사람이기에 이 문제를 100% 해결할 수 없음 )

### C# 에선
* **CLR이 자동 메모리 관리(Automatic Memory Management) 기능을 제공**
* 위 기능의 중심엔 **가비지 컬렉션(Garbage Collection)**이 존재


### Garbage Collection
* 우리말로 "쓰레기 수거"
  * 쓰레기 -> 더 이상 사용하지 않는 객체
* Garbage Collection을 통해 프로그래머는 메모리 걱정 없이 코드를 작성할 수 있음

### Garbage Collector
* CLR안에 Garbage Collection을 담당
* 객체 중에 쓰지 않는 것과 쓰는 것을 분리해 **쓰지 않는 객체만 수거해 가는 역할**

### 그렇다고 항상 좋은 건 아니다
* **Garbage Collector도 소프트웨어이기 때문에 CPU와 메모리 같은 컴퓨팅 자원을 소모**
  * 즉, 코드가 사용해야 하는 자원을 Garbage Collector도 **같이 사용**
  * 즉, **Garbage Collector가 사용하는 자원의 양을 최소한을 줄이면 그만큼 많은 자원을 사용할 수 있음**
* Unsafe를 이용한 UnManaged Code는 CLR 기능을 지원받지 못함

***
Garbage Collector 가 Garbage를 체크하는 방법
===
### CLR이 어떻게 객체를 메모리에 할당하는 방법
* 프로그램을 실행하면, CLR은 프로그램을 위한 **일정 크기의 메모리를 확보**
* C-런타임처럼 메모리를 쪼개지 않고 넓은 메모리 공간을 통째로 확보해 **하나로 관리되는 힙(Managed Heap)을 마련**
* 확보한 메모리 첫 주소에 객체를 할당할 메모리 포인터를 세팅
![image](https://user-images.githubusercontent.com/48194683/124540454-6225cf00-de5a-11eb-99a9-b185cd908475.png)

< 설명에 적용되는 예시 코드 >
```
if(true)
{
 Object a = new Object();
}
```

* Object a = new Object(); 로  a 객체를 할당
 * a는 **스택**에 저장
 * Object 형의 객체(이하 객체 A)는 **힙**에 저장
 * a는 객체 A의 주소를 가진다.
![image](https://user-images.githubusercontent.com/48194683/124540505-7a95e980-de5a-11eb-8c01-379b59b57800.png)
* 다음 객체를 생성하게 되면 위와 동일하게 계속 생성

* if문 코드 블록이 끝남으로 **스택에 저장된 a가 해제**
 * 스택에 있는 a는 자연스럽게 메모리에서 사라지지만, **힙에 있는 A는 존재**하게 됨
![image](https://user-images.githubusercontent.com/48194683/124540523-85507e80-de5a-11eb-809e-2b1ca4ec0acb.png)

* **A에 접근할 수 있는 방법이 없기에 A는 더 이상 사용하지 않는 객체(=Garbage)**
* Garbage Collector 가 Garbage가 된 A를 처리

### 루트(Root)란?
* **해제된 a와 같이 할당된 메모리 위치를 참조하는 객체를 루트(Root)라 부름**
* 루트는 **스택에 생성될수도 있고, 정적 필드처럼 힙에 생성될 수 있음**
* .Net 애플리케이션이 실행되면 JIT 컴파일러가 이 루트들을 목록으로 만들고, CLR은 이 루트 목록을 관리하며 상태를 갱신
* **중요한 이유**
   * Garbage Collector가 CLR이 관리하는 루트 목록을 참조해 Garbage를 수집


Garbage Collector가 Garbage를 정리하는 방법
===
1. 루트 목록을 순회하면서 각 루트가 참조하고 있는 힙 객체와의 **관계 여부를 조사**
2. 만약, **루트가 참조하고 있는 힙의 객체가 또 다른 힙 객체를 참조하고 있다면, 이것도 해당 루트와 관계가 있는 것으로 판단**   
< 2번의 예시 이미지 >
![image](https://user-images.githubusercontent.com/48194683/124540772-145d9680-de5b-11eb-8bd4-0a5dd1243e12.png)
3. Garbage 객체가 차지하고 있는 메모리는 **"비어 있는 공간"**
4. 루트 목록에 대한 조사가 끝나면, Garbage Collector는 힙을 순회하면서 Garbage 객체가 차지했던 **"비어 있는 공간"** 에 쓰레기의 인접 객체들을 **이동시켜 채워 넣음**
5. 모든 객체 이동이 끝나면, **Garbage가 수거된 메모리**를 얻을 수 있음


< 3, 4, 5 예시 이미지 >
* 초록색 C, D가 Garbage일 때,
![image](https://user-images.githubusercontent.com/48194683/124540662-db252680-de5a-11eb-9a50-ed5261d61c10.png)
* Garbage인 C, D 객체를 지우고, 인접한 객체를 이동시켜 빈 공간에 채워 넣음
![image](https://user-images.githubusercontent.com/48194683/124540618-c21c7580-de5a-11eb-9c83-246ceb80fe73.png)
* Garbage를 제거한 메모리 
