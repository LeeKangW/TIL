---
title: Weapon Trail
date: 2022-01-24 23:55:00 +0000
categories: [UE4(TIL), VFX]
tags: [ue4]     # TAG names should always be lowercase
---

>캐릭터 근접 무기에 **Trail Effect**를 붙이는 방법에 대한 내용입니다.

# 1. Weapon Trail 이란?

**Trail** 의 뜻을 검색해보면 `자취`, `꼬리`, `끌고 간 자국` 이라 뜬다.  

![](https://images.velog.io/images/night/post/fc810b53-09fc-4e71-b3eb-23ba5079a1ad/image.png)

말 그대로,  
무기 또는 오브젝트가 **지나간 흔적을 보여주는 Effect** 라 볼 수 있다.

> Google에 **Weapon Trail** 이라 검색해보면 많은 예시를 볼 수 있다.  
>![](https://images.velog.io/images/night/post/cfe1cb9b-fef4-4e47-a00f-894fafd6a7b7/image.png)


# 2. UE4에 적용해보기

[저번에 정리했던 내용(무기 장착)](https://velog.io/@night/UE4-Skeletal-Mesh-Socket%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%AC%B4%EA%B8%B0-%EC%9E%A5%EC%B0%A9)과 동일하게 Socket을 이용하여 적용할 수 있다.

하나씩 순서대로 살펴보자.

### 2-1. Trail Socket 생성
1. 무기를 쥔 손의 `Bone`에 **Socket 2개**를 생성 ( Trail의 **시작과 종료 지점**으로 사용 )  
2. `Weapon Socket`에 `Add Preview Asset`으로 무기를 장착  
3. `Preivew` 된 무기를 보면서 `Trail`의 `시작`과 `끝`을 지정  
![](https://images.velog.io/images/night/post/668b5e5e-0b19-4f18-a9ef-2b18da828ed1/image.png)  


### 2-2. Animation Montage 설정
가지고 있는 Combat Montage를 가지고 Trail을 설정할 수 있다.  
만약, 가지고 있지 않다면 [여기서](https://velog.io/@night/UE4-Animation-Montage%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%BD%A4%EB%B3%B4-%EA%B3%B5%EA%B2%A9%EC%9D%84-%EA%B5%AC%ED%98%84%ED%95%B4%EB%B3%B4%EC%9E%90) 확인할 수 있다.  

여기서는 `Notify State`란 것을 사용하게 되는데 자세한 내용은 **공식 문서**를 통해 확인하자!
(언리얼은 공식 문서의 설명이 너무 잘 되어 있다.)
[언리얼 엔진 문서 - Notify](https://docs.unrealengine.com/4.27/ko/AnimatingObjects/SkeletalMeshAnimation/Sequences/Notifies/#:~:text=%EB%B3%80%EA%B2%BD%ED%95%A0%20%EC%88%98%EB%8F%84%20%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4.-,%EB%85%B8%ED%8B%B0%ED%8C%8C%EC%9D%B4%20%EC%8A%A4%ED%85%8C%EC%9D%B4%ED%8A%B8%20%EC%B6%94%EA%B0%80...,-Anim%20Notify%20State)

모든 준비가 되었다면, 하나씩 순서대로 살펴보자.

1. `Add Notify State` 에서 `Trail` 추가  

![](https://images.velog.io/images/night/post/0d45f17c-c429-41a0-a62e-3c7d2a197b29/image.png)  

2. 가지고 있는 `Animation`에 맞추어 `Trail` 생성 위치 잡기

![](https://images.velog.io/images/night/post/ce68e523-275e-46af-aecf-9360286e3a06/image.png)  

3. `Trail Notify State Details` 세팅   
- PSTemplate (파티클 시스템 템플릿): 애님 트레일이 들어있는 파티클 시스템  
- First Socket Name: Trail을 정의하는 첫 번째 본/소켓 이름  
- Second Socket Name: Trail을 정의하는 두 번째 본/소켓 이름  

>[자세한 세팅은 공식 문서에서 확인하자!](https://docs.unrealengine.com/4.27/ko/AnimatingObjects/SkeletalMeshAnimation/Sequences/Notifies/#:~:text=%EC%A1%B0%EC%A0%95%ED%95%A0%20%EC%88%98%20%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4.-,%EC%95%A0%EB%8B%88%EB%A9%94%EC%9D%B4%EC%85%98%20%ED%8A%B8%EB%A0%88%EC%9D%BC,%EC%83%98%ED%94%8C%EB%A7%81%ED%95%9C%20%EB%92%A4%20%EA%B7%B8%20%EC%86%8C%EC%BC%93%20%EC%82%AC%EC%9D%B4%20%ED%8A%B8%EB%9D%BC%EC%9D%B4%EC%95%B5%EA%B8%80%EC%9D%84%20%ED%9D%94%EC%A0%81%20%EA%B8%B8%EC%9D%B4%EB%A7%8C%ED%81%BC%20%EC%9D%B4%EC%96%B4%20%EB%B6%99%EC%9E%85%EB%8B%88%EB%8B%A4.,-%EC%95%84%EB%9E%98%EB%8A%94%20%EC%95%A0%EB%8B%88%EB%A9%94%EC%9D%B4%EC%85%98%20%EC%BA%90%EB%A6%AD%ED%84%B0%EC%97%90)

![](https://images.velog.io/images/night/post/384fc831-411b-4946-b3c2-ad4eb3fee685/image.png)  


# 3. 결과
위 내용을 차례대로 진행한 결과, 아래와 같이 `Weapon Trail`이 적용된 것을 볼 수 있다.

{% youtube "https://youtu.be/bJZvloiSANY" %}