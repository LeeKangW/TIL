명령 패턴(Command Pattern)
===

## 1. 명령 패턴이란?
- 메소드 호출을 **실체화**한 것
  - 실체화: 실제하는 것으로 만듦 (프로그래밍 분야에서는 무엇인가를 일급(first-class)로 만든다 라는 뜻으로도 통함)
  - '실체화','일급': 어떤 개념을 변수에 저장하거나 함수에 전달할 수 있도록 데이터.즉, 객체로 바꿀 수 있다는 것을 의미
  - 즉, **함수 호출을 객체로 감쌌다는 의미**
- **콜백을 객체지향적으로 표현**한 것

## 2. 예시 ( C++ 사용 )
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
