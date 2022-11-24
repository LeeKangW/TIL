---
title: Animation을 연결해보자
date: 2022-01-24 23:40:00 +0000
categories: [UE4(TIL), Animation]
tags: [ue4]     # TAG names should always be lowercase
---

>Animation Blueprint를 이용해서 캐릭터에 달리는 Animation을 연결해보자!
>
>애니메이션은 [Mixamo](https://www.mixamo.com/#/)를 사용하였습니다.
>글의 내용은 예전에 공부했던 [Udmey 강좌](https://www.udemy.com/course/unreal-engine-the-ultimate-game-developer-course/)을 바탕으로 작성하였습니다.


# 1. AnimInstance 생성

### AnimInstance 란?
AnimInstance란 애니메이션을 만들기 위해 필요한 데이터나 기능들을 모아둔 객체 인스턴스이다.

예를 들어,  
캐릭터 속도에 따라 애니메이션이 달라져야 한다고 가정하면,  
캐릭터 속도에 대한 데이터를 AnimInstance에 구현해두고 이를 가져와 적용할 수 있다.  

***

### C++ Class 생성하는 방법
C++ Class를 생성하려고 하면, AnimInstance가 보이지 않는데  
우측 `Show All Classes`를 클릭해야 AnimInstance를 선택할 수 있다.


![](https://images.velog.io/images/night/post/ffe6f288-e1c7-4ed7-92fe-660c60174392/image.png)

***

# 2. 코드 작성
달리는 애니메이션을 만들 것이기 때문에 **캐릭터 속도**와 **현재 땅을 밟고 있는지**에 대한 변수를 생성했다.

### .h 파일
```cpp
private:
	UPROPERTY(EditAnywhere,BlueprintReadOnly,Category="Movement Properties",meta =(AllowPrivateAccess="true"))
	float MovementSpeed;

	UPROPERTY(EditAnywhere,BlueprintReadOnly,Category="Movement Properties",meta =(AllowPrivateAccess="true"))
	bool bIsAir;
```

그리고 캐릭터 객체를 가져오기 위해서 Pawn 변수도 하나 생성했다.
```cpp
	UPROPERTY(EditAnywhere,BlueprintReadOnly,Category="Movement Properties",meta =(AllowPrivateAccess="true"))
	class APawn* Pawn;
```

Properties를 업데이트해주기 위해 메소드를 하나 구현했고, Blueprint에서 조작하기 위해 아래와 같이 세팅했다.
```cpp
	UFUNCTION(BlueprintCallable, Category="Update Properties")
	void UpdateProperties();
    
```

### .cpp 파일
이제 **cpp 파일로 넘어와서**, 아래와 같이 코드를 구현했다.
```cpp
void UPlayerCharacterAnimInstance::NativeInitializeAnimation()
{
	if(Pawn == nullptr)
	{
    		// 현재 스켈레톤의 주인(폰)을 가져온다.
		Pawn = TryGetPawnOwner();
	}
}

// Properties를 업데이트 해주기 위해 만든 메소드
void UPlayerCharacterAnimInstance::UpdateProperties()
{
	// 폰이 없어졌다면?
	if(Pawn == nullptr)
	{
    		// 다시 폰을 가져온다.
		Pawn = TryGetPawnOwner();
	}

	// 폰이 존재한다면,
    	// 애님이 실행되기 전 폰이 삭제된다면, 
    	// 없는 객체를 참조할 수 있기에 아래와 같이 if문으로 묶어주었다.
	if(Pawn)
	{
		// is Air Check
		bIsAir = Pawn->GetMovementComponent()->IsFalling();
		
		// Movement Speed Check
		FVector Velocity = Pawn->GetVelocity();
        
        // Z축은 필요가 없으니, 0으로 초기화해준다.
		FVector NewVelocity = FVector(Velocity.X,Velocity.Y,0.f);
		MovementSpeed = NewVelocity.Size();
	}
}
```
### NativeInitializeAnimation()
C++ Class를 만들고 나면 UAnimInstance가 부모 클래스로 되어 있는데 그 클래스 안에  
NativeInitializeAnimation() 이 가상 함수로 구현되어 있다.  

```cpp
// the below functions are the native overrides for each phase
// Native initialization override point
virtual void NativeInitializeAnimation();
```
이 메소드를 통해 애니메이션 인스턴스의 다양한 속성들을 초기화할 수 있다.  
( 액터의 InitializeComponent 또는 BeginPlay 메소드와 유사하게 작동된다.)  
[참고 자료](http://jollymonsterstudio.com/2019/01/12/unreal-engine-c-fundamentals-override-uaniminstance/)

***

### AnimInstance Blueprint 생성
1. AnimInstance Blueprint를 생성하자
2. 블루프린트를 열어 보면, `Event Blueprint Update Animation`이 존재하는데 여기에 아까 만든 `UpdateProperteis()`를 연결해주자.  
![](https://images.velog.io/images/night/post/dc0f750b-15ac-4d37-8b6d-e9b10f69cad3/image.png)

### Event Blueprint Update Animation ?
툴팁에서 볼 수 있듯이, 애니메이션이 업데이트 될 때마다 실행된다.  
![](https://images.velog.io/images/night/post/8dbb7b19-9d2b-4826-81cc-424d80ff9058/image.png)

***

# 3. Blend Space 1D 생성
Blend Space 1D를 통해 Idle -> Run 까지의 블랜딩된 애니메이션을 만들어보자.  

Blend Space 1D는 `Content Browser`에서 우클릭을 통해 생성이 가능하다.  
![](https://images.velog.io/images/night/post/f5cb8f62-ebab-4ffa-867c-ef25dcebedea/image.png)

***

### 애니메이션 넣기
![](https://images.velog.io/images/night/post/8033a018-020b-493d-849e-c6f625a6e0a7/image.png)

아래 빨간 동그라미를 보면 0 ~ 600.0으로 되어 있는데 좌측 `Asset Details`에서 조작이 가능하다.  
(600은 Character Movement Component의 MaxWalkSpeed 값에 맞춘 것이다. )  
![](https://images.velog.io/images/night/post/74c651be-d8b7-4042-9beb-f1a5f6a623f7/image.png)

이제 0에는 Speed가 0임을 의미함으로 **Idle Animation**을 넣고,  
중간에는 **Walk Animation**을  
600에는 Max Speed를 의미하기에 **Run Animation**을 넣어주자.  

***

# 4. Animation Blueprint 생성
`Content Browser`에서 우클릭을 통해 생성이 가능하다.  
![](https://images.velog.io/images/night/post/991a5a09-7734-40c0-8d0f-e959e793932b/image.png)
 
생성하게 되면 아래와 같이 팝업이 뜨게 되는데,
Parent Class에는 위에서 만든 AnimInstance의 Blueprint를 넣어주고
Target Skeleton에는 애니메이션을 적용할 Skeleton을 넣어주자.  
![](https://images.velog.io/images/night/post/ff28cda6-4411-4bbf-b8d3-e23bcd07cfe8/image.png)

***

### AnimGraph 세팅
애님 그래프에서 `New State Machine`을 통해 state Machine을 생성하자  
![](https://images.velog.io/images/night/post/2186bb76-b88a-4c67-a5ed-192e7a45ccc2/image.png)

***

### State Machine 세팅
생성한 State Machine을 더블 클릭하면 아래와 같이 생성이 된다.  
![](https://images.velog.io/images/night/post/a90add87-e469-4a40-89ef-65531b721def/image.png)

여기서, `IdleWalkRun` 이란 새로운 State를 생성하자.  
![](https://images.velog.io/images/night/post/bebc328e-3a8e-42a6-9f25-401c5e665250/image.png)

***

### IdleWalkRun State 세팅
1. 위에서 만든 Blend Space 1D 를 드래그 앤 드랍한다.
2. AnimInstnace에서 만든 MovementSpeed를 가져와 연결한다.  
![](https://images.velog.io/images/night/post/c3328a0a-0fcd-4402-b683-b2dcf2eaf7b7/image.png)

***

# 5. 왜 적용이 안돼?
위 내용을 전부 진행하고 난 뒤 플레이를 해보면 애니메이션이 적용되지 않아 T-Pos가 실행됨을 알 수 있다.  
![](https://images.velog.io/images/night/post/5fc2c758-f3d4-4bc4-a2c8-74c7b72a643f/image.png)

해결하기 위해 **Character Blueprint 파일**을 열어보자.

열고 난 뒤  
`Component`에서 Mesh의 Details를 보게 되면 Animation 이 있는데  
여기서 `Anim Class`를 위에서 만든 블루프린트로 설정해준다.  
![](https://images.velog.io/images/night/post/fdde34f1-60f5-4de3-8182-63bb1f348ace/image.png)

***

# 6. 결과

{% youtube "https://youtu.be/VFxtd_jEGnU" %}