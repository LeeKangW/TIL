---
layout: post
title: "[Unity] UI에 Particle 띄우기"
date: 2022-07-07 11:29 +0900
categories: [Tips,Tips-Unity]
tags: [tips]     # TAG names should always be lowercase
---

# [Unity] UI에 Particle 띄우기

> 일하다가 질문을 받아 처리하는 중 문득 “UI에 Particle이 원래 노출이 안되었던 것 같은데…” 
하고 테스트를 해보면서 얻은 내용을 정리했습니다.
> 
> 
> 
> UI에 Particle를 띄우는 일이 흔하게 있는데
> 한글로 된 정보가 많이 없어서 유니티 개발자분들에게 도움이 되었으면 합니다.
> 
> 추가로
> **더 좋은 방법**이나 **설명** 또는 **왜 이렇게 되는지 원리**에 관해 좋은 의견이 있으시다면 **댓글로 공유해주세요!**

<br>

업무로든 프로젝트로든 Unity를 사용하는 게임 개발자는 UI 작업은 피할 수 없는 작업이다.

그리고 UI에는 당연하게도 Particle System이 들어가게 되는데 Particle를 넣어도 게임 화면에 노출이 되지 않는 현상을 한 번은 경험했을 것이다.

그럼 UI에 Particle System을 어떻게 띄워야 하는 것일까??

어떻게 띄워야 하는지 알아보자

---

## 문제 상황 예시

> 게이지 바에 변화가 생길 때 게이지 끝에 파티클 이펙트가 발생해야 하는 경우를 예로 들어 설명했습니다.
> 

일단 기본 세팅을 해보자

게이지 바 UI를 만들기 위해 아래와 같이 만들었다.

![Untitled](https://user-images.githubusercontent.com/48194683/177677753-ae3cfb28-be18-4f73-b7be-e859418a5f8d.png)  


Canvas의 Render Mode는 초기 세팅인 `Screen Space - Overlay` 로 되어 있다.

![Untitled 1](https://user-images.githubusercontent.com/48194683/177677776-b6c80267-cf5b-4639-a4fd-e9388f4f9a44.png)  


그리고 검은색 게이지 바 우측에 Particle System을 붙여보자

![Untitled 2](https://user-images.githubusercontent.com/48194683/177677831-d4f815f4-c8c6-4c81-a03a-fffba32faa6b.png)  

이렇게 세팅을 해두고 게임 플레이를 해보면 **파티클이 노출되지 않는 것을 볼 수 있다.**

![Untitled 3](https://user-images.githubusercontent.com/48194683/177677834-c8e0d50b-2f24-4c13-85da-8191d6b023c5.png)  

---

## UI에 Particle를 띄워보자!

### 1. Canvas의 Render Mode를 변경하자!

일단 Canvas의 `Render Mode` 를 `Screen Spcae - Camera` 로 변경해야 한다.

![Untitled 4](https://user-images.githubusercontent.com/48194683/177677852-76488023-eae3-4ddc-a055-579a89194aa9.png)  


설정에 대한 자세한 내용은 [Unity 공식 문서](https://docs.unity3d.com/kr/530/Manual/UICanvas.html)에서 확인할 수 있다.

### 2. UI용 Camera 생성

`Screen Space - Camera` 로 변경하게 되면 `Render Camera` 가 필요하다.

> Render Camera 란?
선택한 `Canvas` 를 렌더링 해주는 Camera 이다.
그러므로, 해당 Camera가 비활성화 되어 있으면 연결된 Canvas가 게임 화면에 노출되지 않는 것을 볼 수 있다.
> 

`Render Camera` 를 만들어주기 위해 UI용 Camera를 생성해주자!

그리고 Camera의 `Clear Flags` 를 `Depth Only` 로 설정해주고 Canvas의 `Render Camera`에 만든 UI용 `Camera` 를 넣어주자.

> 카메라에 관련된 설명은 [Unity 공식 문서](https://docs.unity3d.com/kr/2018.4/Manual/class-Camera.html)를 확인하자.
> 

### 3. 결과

아래와 같이 정상적으로 UI에 Particle이 노출되는 것을 확인할 수 있다.

![Untitled 5](https://user-images.githubusercontent.com/48194683/177677886-2c140c07-628b-4872-a425-89a0a43fdf62.png)
