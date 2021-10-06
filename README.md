Game Developer Document
========================
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
* 개발을 하면서 개인적으로 정리하고 싶은 내용들이 정리되어 있습니다.
* 오류가 있다면 언제든지 말해주세요.

Design pattern
===
<details>
  <summary> Contents </summary>
  
<br>  
 
**[게임 프로그래밍 패턴](https://www.hanbit.co.kr/store/books/look.php?p_code=B4342659595)을 보고 정리한 내용입니다.**  
**책 내용을 정리한 것이므로 Private repository 에 저장되어 있습니다.**   
  
### Singleton Pattern⭐
[Singleton Pattern(싱글톤 패턴)](https://github.com/LeeKangW/Private_Game-Developer_Document/blob/main/Desgin%20Pattern/Singleton%20Pattern.md)

### Command Pattern ⭐
[Command Pattern(명령 패턴)](https://github.com/LeeKangW/Private_Game-Developer_Document/blob/main/Desgin%20Pattern/Command%20Pattern.md)   

### State Pattern ⭐
[State Pattern(상태 패턴)](https://github.com/LeeKangW/Private_Game-Developer_Document/blob/main/Desgin%20Pattern/State%20Pattern.md)   

### Flyweight Pattern
[Flyweight Pattern(경량 패턴)](https://github.com/LeeKangW/Private_Game-Developer_Document/blob/main/Desgin%20Pattern/Flyweight%20Pattern.md)

### Component Pattern

### observer pattern ⭐
[Observer Pattern(관찰자 패턴)](https://github.com/LeeKangW/Private_Game-Developer_Document/blob/main/Desgin%20Pattern/Observer%20Pattern.md)   

</details>


AI
===
<details>
  <summary> Contents </summary>
    
<br>

[1. FSM(Finite State Machine)](AI/FSM.md)   
[2. HFSM](AI/HFSM.md)   
[3. Behavior Tree](AI/Behavior_Tree.md)   

</details>

mathematics
===
<details>
  <summary> Contents </summary>

### Vector  
[1.Vector란?](/Vector/What-is-a-Vector.md)  
  
</details>

Language
===
### C#
<details>
  <summary> Contents </summary>

#### 숫자 서식
[1. 표준 숫자 서식 문자열](https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/standard-numeric-format-strings)  
[2. 사용자 지정 숫자 서식 문자열](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/%EC%82%AC%EC%9A%A9%EC%9E%90-%EC%A7%80%EC%A0%95-%EC%88%AB%EC%9E%90-%EC%84%9C%EC%8B%9D.md)

#### 날짜 및 시간 서식
[1. 표준 날짜 및 시간 서식 문자열](https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/standard-date-and-time-format-strings)  
[2. 사용자 지정 날짜 및 시간 서식 문자열](https://docs.microsoft.com/ko-kr/dotnet/standard/base-types/custom-date-and-time-format-strings)

#### 메모리 관리 ⭐
[1. Strong Reference 와 Weak Reference](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Strong_Reference_%EC%99%80_Weak_Reference.md)   
[2. Class 와 Struct 차이](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Class%20%EC%99%80%20Struct%20%EC%B0%A8%EC%9D%B4.md)

#### Garbage Collection
[1. Garbage Collection 개념 및 작동 원리](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Garbage%20Collection.md)   
[2. Generational Garbage Collection](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Generational%20%20Garbage%20Collection.md)   
[3. Garbage Collection을 인지한 효율적인 코드 작성법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Garbage%20Collection%EC%9D%84%20%EC%9D%B8%EC%A7%80%ED%95%9C%20%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8%20%EC%BD%94%EB%93%9C%20%EC%9E%91%EC%84%B1%EB%B2%95.md)

#### Delegate 와 Event의 차이 ⭐
[Delegate 와 Event 차이](https://github.com/LeeKangW/Game_Developer_Document/blob/main/C%23/Event%20%EC%99%80%20Delegate%20%EC%B0%A8%EC%9D%B4.md)

</details>

Game Engine
===
### Unity
<details>
  <summary> Contents </summary>

<br>

[Unity Blog 링크](https://blog.unity.com/kr) -> 각종 Unity 정보를 얻을 수 있음

### Unity에서 지원하는 기능
[1. Unity blog - Input System](https://blog.unity.com/kr/technology/introducing-the-new-input-system)

#### 연산
[1. Vector 와 Quaternion 연산](/Unity/Vector-와-Quaternion의-연산.md) 

#### 3인칭 RPG 게임 만들면서 정리한 내용
[1. 3인칭 RPG 게임 내 캐릭터 움직임 구현 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/RPG%20%EA%B0%9C%EB%B0%9C/3%EC%9D%B8%EC%B9%AD%20%EC%BA%90%EB%A6%AD%ED%84%B0%20%EC%9B%80%EC%A7%81%EC%9E%84%EC%97%90%20%EB%8C%80%ED%95%9C%20%EC%A0%95%EB%A6%AC.md)  
[2. 캐릭터 콤보 공격 구현 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/RPG%20%EA%B0%9C%EB%B0%9C/%EC%BA%90%EB%A6%AD%ED%84%B0%20%EC%BD%A4%EB%B3%B4%20%EA%B3%B5%EA%B2%A9%20%EA%B5%AC%ED%98%84%20%EB%B0%A9%EB%B2%95.md)   
[3. "상태 패턴"을 이용한 캐릭터 움직임 구현 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/RPG%20%EA%B0%9C%EB%B0%9C/%22%EC%83%81%ED%83%9C%20%ED%8C%A8%ED%84%B4%22%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%EC%BA%90%EB%A6%AD%ED%84%B0%20%EC%9B%80%EC%A7%81%EC%9E%84%20%EA%B5%AC%ED%98%84.md)   
[4. 캐릭터 공격 시스템 및 데미지 적용 구현 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/RPG%20%EA%B0%9C%EB%B0%9C/%EA%B3%B5%EA%B2%A9%20%ED%8C%90%EC%A0%95%20%EB%B0%8F%20%EB%8D%B0%EB%AF%B8%EC%A7%80%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EA%B0%9C%EB%B0%9C.md)   
[5. 캐릭터 Foot IK 구현](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/RPG%20%EA%B0%9C%EB%B0%9C/%EC%BA%90%EB%A6%AD%ED%84%B0%20Foot%20IK%20%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0.md)   

### Rendering Pipeline
[Rendering Pipeline](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/Rendering%20Pipeline.md)

### 최적화 ⭐
[1. Batch, Draw Call, SetPass](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/Batch,%20Draw%20Call,%20SetPass.md)

### 알아 두면 좋은 내용들 ⭐
[1. N초 동안 특정 작업을 진행하는 메소드 구현](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/N%EC%B4%88%20%EB%8F%99%EC%95%88%20%ED%8A%B9%EC%A0%95%20%EC%9E%91%EC%97%85%EC%9D%84%20%ED%95%98%EB%8A%94%20%EA%B8%B0%EB%8A%A5%20%EB%A7%8C%EB%93%9C%EB%8A%94%20%EB%B2%95.md)   

</details>


### Unreal Engine

<details>
  <summary> Contents </summary>

## UE4
[Unity 개발자를 위한 언리얼 엔진 4](https://docs.unrealengine.com/4.27/ko/Basics/UnrealEngineForUnityDevs/)  

[1. Level Blueprint](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/1.%20Level%20Blueprint.md)  
[2. Class 구조 (Object, Actor, Pawn, Character)](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/2.%20UE4%20Class%20%EA%B5%AC%EC%A1%B0.md)    
[3. 리플렉션(Reflection)](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/3.%20%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98(Reflection).md)  
[3-1. Property System](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/3-1.%20Property%20System.md)  
[3-2. 언리얼 엔진의 Garbage Collection](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/3-2.%20%EC%96%B8%EB%A6%AC%EC%96%BC%20%EC%97%94%EC%A7%84%EC%9D%98%20Garbage%20Collection.md)  
  
### Actor  
[4. Actor란?](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/4.%20Actor%EB%9E%80.md)  
[4-1. Actor 생성하기](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/4-1.%20%EC%95%A1%ED%84%B0%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0.md)  
[4-2. C++을 이용하여 Static Mesh 추가해보기](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/4-2.%20C%2B%2B%EB%A1%9C%20%EC%95%A1%ED%84%B0%EC%97%90%20Static%20Mesh%20%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0.md)  
[4-3. FVector를 사용해 변수를 생성해서 조작해보기](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/4-3.%20FVector%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%B4%20%EB%B3%80%EC%88%98%EB%A5%BC%20%EC%83%9D%EC%84%B1%ED%95%B4%EC%84%9C%20%EC%A1%B0%EC%9E%91%ED%95%B4%EB%B3%B4%EA%B8%B0.md)  
  
### Collision
[5. Collision 사용법](https://docs.unrealengine.com/4.26/ko/InteractiveExperiences/Physics/Collision/)  
[6. Sweeping](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/6.%20Sweeping.md)  
  
### 필요없는 C++ 파일 삭제하는 방법
[7. 필요없는 C++ 파일 삭제하는 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/7.%20%ED%95%84%EC%9A%94%20%EC%97%86%EB%8A%94%20C%2B%2B%20%ED%81%B4%EB%9E%98%EC%8A%A4%20%EC%82%AD%EC%A0%9C%ED%95%98%EA%B8%B0.md)  
  
### Pawn
[8. Pawn 이란?](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/8.%20Pawn%20%EC%9D%B4%EB%9E%80%3F.md)  
[9. 키 입력을 통해 Pawn 객체를 움직여보자](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/9.%20%ED%82%A4%20%EC%9E%85%EB%A0%A5%EC%9D%84%20%ED%86%B5%ED%95%B4%20Pawn%20%EA%B0%9D%EC%B2%B4%EB%A5%BC%20%EC%9B%80%EC%A7%81%EC%97%AC%EB%B3%B4%EC%9E%90.md)  
[10. Movement Component](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unreal%20Engine/10.%20Movement%20Component.md)  
  
</details>

Shader
===

<details>
  <summary> Contents </summary>

### Shader의 개념 
**[유니티 쉐이더 스타트업](https://vielbooks.com/235)을 보고 정리한 내용입니다.**  
**책 내용을 정리한 것이므로 Private repository 에 저장되어 있습니다.**   

[0. 쉐이더란 무엇인가?](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/0.%20%EC%89%90%EC%9D%B4%EB%8D%94%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80.md)<br/>
[1. 렌더링 파이프라인](https://github.com/LeeKangW/Unity_Shader_Project/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/0-1.%20%EB%A0%8C%EB%8D%94%EB%A7%81%20%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8.md)  
[2. UV란 무엇인가](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/UV%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80.md)  
[3. 디지털 라이팅의 이론](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/3.%20%EB%94%94%EC%A7%80%ED%84%B8%20%EB%9D%BC%EC%9D%B4%ED%8C%85%EC%9D%98%20%EC%9D%B4%EB%A1%A0.md)  
<br>

## Unity Shader
[1. Unity Shader 작성 요령](https://github.com/LeeKangW/Unity_Shader_Project/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/1.%20%EC%9C%A0%EB%8B%88%ED%8B%B0%20%EC%89%90%EC%9D%B4%EB%8D%94%EC%9D%98%20%EC%9E%91%EC%84%B1%20%EC%9A%94%EB%A0%B9.md)   
[2. surface Shader 적용 및 코드 작성법 설명](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/2.%20surface%20Shader%20%20%EC%A0%81%EC%9A%A9%20%EB%B0%8F%20%EC%BD%94%EB%93%9C%20%EC%9E%91%EC%84%B1%EB%B2%95%20%EC%84%A4%EB%AA%85.md)   
[3. 색상 표현하기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/3.%20%EC%83%89%EC%83%81%20%EC%B6%9C%EB%A0%A5%ED%95%98%EA%B8%B0.md)  
[4. Surface Shader를 이용한 텍스쳐 제어](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/4.%20Surface%20Shader%EB%A5%BC%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%85%8D%EC%8A%A4%EC%B3%90%20%EC%A0%9C%EC%96%B4.md)  
<br>
[5. UV 이용하기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/5-0.%20UV%20%EC%9D%B4%EC%9A%A9%ED%95%98%EA%B8%B0.md)  
[5-1. UV를 이용해 불 이펙트 만들어보기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/5-1.%20UV%EB%A5%BC%20%EC%9D%B4%EC%9A%A9%ED%95%B4%20%EB%B6%88%20%EC%9D%B4%ED%8E%99%ED%8A%B8%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)  
<br>
[6. Vertex 컬러 이용하기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/6-0.%20Vertex%20%EC%BB%AC%EB%9F%AC%20%EC%9D%B4%EC%9A%A9%ED%95%98%EA%B8%B0.md)  
[6-1. Vertex Color를 이용해 마스킹 기능을 이용해보기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/6-1.%20Vertex%20Color%EB%A5%BC%20%EB%A7%88%EC%8A%A4%ED%82%B9%20%EA%B8%B0%EB%8A%A5%EC%9C%BC%EB%A1%9C%20%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0.md)  
<br>
### SurfaceOutputStandard 사용하기  
[7-1. Metallic 과 Smoothness](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/7-1.%20Metallic%20%EA%B3%BC%20Smoothness.md)  
[7-2. NormalMap 적용하기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/7-2.%20NormalMap.md)  
[7-3. Occlusion(오클루젼)](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/7-3.%20Occlusion(%EC%98%A4%ED%81%B4%EB%A3%A8%EC%A0%BC).md)  
[7-4. 6번 내용 업그레이드 시켜 보기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/7-4.%206%EB%B2%88%20%EB%82%B4%EC%9A%A9%20%EC%97%85%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9C%20%EC%8B%9C%EC%BC%9C%20%EB%B3%B4%EA%B8%B0.md)  
  
### 유니티에 내장된 라이팅 구조인 `Lambert(램버트)` 와 `Blinn Phong(블린 퐁)` 사용하기
[8. 유니티에 내장된 라이팅 구조 설명](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/8.%20%EC%9C%A0%EB%8B%88%ED%8B%B0%EC%97%90%20%EB%82%B4%EC%9E%A5%EB%90%9C%20%EB%9D%BC%EC%9D%B4%ED%8C%85%20%EA%B5%AC%EC%A1%B0.md)  
[8-1. Lambert(램버트)라이팅 만들기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/8-1.%20Lambert(%EB%9E%A8%EB%B2%84%ED%8A%B8)%EB%9D%BC%EC%9D%B4%ED%8C%85%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)  
[8-2. Blinn-Phong(블린-퐁) 라이팅 만들기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/8-2.%20Blinn-Phong(%EB%B8%94%EB%A6%B0-%ED%90%81)%20%EB%9D%BC%EC%9D%B4%ED%8C%85%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)  
<br>
  
### 커스텀 라이트 만들기
[9. 커스텀 라이트 기본형 만들기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/9.%20%EC%BB%A4%EC%8A%A4%ED%85%80%20%EB%9D%BC%EC%9D%B4%ED%8A%B8%20%EA%B8%B0%EB%B3%B8%ED%98%95%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)   
[9-1. Lambert 라이트 연산 만들기](https://github.com/LeeKangW/Unity_Shader_Study/blob/main/%EC%B1%85%20%EC%A0%95%EB%A6%AC/Unity/9-1.%20Lambert%20%EB%9D%BC%EC%9D%B4%ED%8A%B8%20%EC%97%B0%EC%82%B0%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)  

</details>

Others
===
<details>
  <summary> Contents </summary>
  
### 메모리 누수
[메모리 누수 방지 방법](https://github.com/LeeKangW/Game_Developer_Document/blob/main/Unity/%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EB%88%84%EC%88%98%20%EB%B0%A9%EC%A7%80%EB%B2%95.md)
  
</details>
