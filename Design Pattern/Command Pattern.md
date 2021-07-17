명령 패턴(Command Pattern)
===
[게임 프로그래밍 패턴](https://www.hanbit.co.kr/store/books/look.php?p_code=B4342659595) 책으로 공부하면서 정리한 내용입니다.
자세한 내용을 원한다면, 책을 구매해서 확인해주세요.

## 1. 명령 패턴이란?
- 메소드 호출을 **실체화**한 것
  - 실체화: 실제하는 것으로 만듦 (프로그래밍 분야에서는 무엇인가를 일급(first-class)로 만든다 라는 뜻으로도 통함)
  - '실체화','일급': 어떤 개념을 변수에 저장하거나 함수에 전달할 수 있도록 데이터.즉, 객체로 바꿀 수 있다는 것을 의미
  - 즉, **함수 호출을 객체로 감쌌다는 의미**
- **콜백을 객체지향적으로 표현**한 것

## 2. 언제 사용??
- AI가 제어하는 캐릭터들에 대한 명령
- AI 엔진과 액터 사이에 인터페이스용으로 사용(즉, AI 코드에서 원하는 Command 객체를 사용)

## 3. 예시 ( C++ 사용 )
- 게임 패드에 A, B, X, Y 버튼이 존재하고 각 버튼에 특정 행동이 연결되어 있다면

명령 패턴을 쓰지 않을 시   
```
void InputHandler::handleInput()
{
  if (isPressed(ButtonX)) jump();
	else if (isPressed(buttonY)) fireGun();
	else if (isPressed(buttonA)) swapWeapon();
	else if (isPressed(buttonB)) lurchIneffectively();
}
```
위와 같이 코드가 구성되어 있으면, 입력 키에 대한 행동이 연결되어 있어 **키 변경이 불가능**하다.

그러므로,
아래와 같이 행동에 대한 메소드를 객체화를 하면, 유연하게 버튼과 행동을 연결할 수 있다.

명령 패턴 사용

#### Command class
<details>
    <summary>Command.h</summary>

```
#pragma once
class Command
{
public:
	virtual ~Command(){}
  // 원하는 액터의 메소드를 호출하기 위해 파라미터로 액터를 받는다
  // 이렇게 함으로써, Command 클래스의 유용성을 늘릴 수 있다(파라미터로 받지 않았다면, 캐릭터 객체를 미리 찾아두어야 하기에 유용성이 떨어진다)
	virtual void execute(GameActor& actor) = 0;
};
```

</details>

***
#### InputHandler class
<details>
    <summary>InputHandler.h</summary>

```
#pragma once
#include "Command.h"
class InputHandler
{
public:
	Command* handleInput();

private:
	Command* buttonX;
	Command* buttonY;
	Command* buttonA;
	Command* buttonB;
};



```

</details>


<details>
    <summary>InputHandler.cpp</summary>

```
#include "InputHandler.h"

// 어떤 액터를 파라미터로 넘겨줘야 할지 모르기 때문에 handleInput()에서 명령 객체를 반환
Command* InputHandler::handleInput()
{
	if (isPressed(ButtonX)) return buttonX;
	if (isPressed(buttonY)) return buttonY;
	if (isPressed(buttonA)) return buttonA;
	if (isPressed(buttonB)) return buttonB;
  
  // 아무것도 누르지 않았다면, 아무것도 하지 않는다.
  return null;
}


```

</details>

***
#### FireCommand Class
<details>
    <summary>FireCommand.h</summary>

```
#pragma once
#include "Command.h"
class FireCommand :
    public Command
{
public:
    virtual void execute(GameActor& actor);
    void fireGun();
};
```

</details>

<details>
    <summary>FireCommand.cpp</summary>

```
#include "FireCommand.h"
  
void FireCommand::execute(GameActor& actor) 
{
	fireGun();
}

void FireCommand::fireGun()
{
	
}
```

</details>

***
#### JumpCommand Class
<details>
    <summary>JumpCommand.h</summary>

```
#pragma once
#include "Command.h"
  
class JumpCommand :
    public Command
{
public:
  // GameActor 객체를 파라미터로 받기 때문에 어떤  캐릭터라도 점프 행동을 작동하게 
    virtual void execute(GameActor& actor);
    void jump();
};

```

</details>

<details>
    <summary>JumCommand.cpp</summary>

```
#include "JumpCommand.h"

void JumpCommand::execute(GameActor& actor)
{
	jump();
}

void JumpCommand::jump()
{

}

```

</details>

***

위의 코드를 통해 actor에 명령 객체를 적용할 수 있다

<details>
  <summary> 명령 객체를 받아 플레이어를 대표하는 GameActor 객체에 적용하는 코드</summary>
  
```
  Command* command = inputHandler.handleInput();
  if(command)
  {
    command->execute(actor);
  }
```
  
</details>

이렇게 코드를 구성함으로써, **명령을 실행할 때 액터만 바꾸면 플레이어가 게임에 있는 어떤 액터라도 제어할 수 있게 된다**

## 4. 실행취소와 재실행 방법
- 명령 패턴 사용 예에서 가장 잘 알려져 있는 방법

#### 실행 취소(undo)
- undo()는 execute()에서 변경하는 상태를 반대로 바꿔주면 된다.
1. execute() 메소드 정의에서 실행 취소를 하기 위해 실행 전의 정보를 저장한다.

Ex) 특정 unit을 x,y 만큼 이동
```
virtual void execute()
{
   // 나중에 취소할 수 있도록 원래 위치를 저장
   xBefore = unit->x();
   yBefore - unit->y();
   
   unit->moveTo(x,y);
}
```
2. undo() 메소드 정의에서 1번에 저장한 정보 값을 사용한다.

Ex)
```
virtual void Undo()
{
   unit->moveTo(xBefore,yBefore)
}
```

- 여러 단계의 실행취소도 간단하게 구현 가능
- 가장 최근 명령만 기억하는 대신, 명령 목록을 유지하고 **현재**명령이 무엇인지만 알고 있으면 된다.
- 유저가 명령을 실행하면, 새로 생성된 명령을 목록 맨 뒤에 추가하고, 이를 **현재**명령으로 기억하면 된다.

Ex)
![image](https://user-images.githubusercontent.com/48194683/126031375-d873da35-4b8e-4689-84bc-4dc731cb3896.png)

- 유저가 **실행취소**를 선택하면, 현재 명령을 실행취소하고 현재 명령을 가리키는 포인터를 뒤로 이동
- 유저가 **재실행**을 선택하면, 포인터를 다음으로 이동시킨 후에 해당 포인터를 실행
- 유저가 몇 번의 **실행취소**한 뒤에 새로운 명령을 실행한다면, 현재 명령 뒤에 새로운 명령을 추가하고 그 다음에 붙어 있는 명령들은 버린다.


## 5. 클래스로만 가능하고, 함수형으론 불가능?
- 그렇지 않다.
- 예시 코드에서 **Class**로 처리되어 있는 것을 함수로 설정한다면 기능은 동일하게 돌아간다
