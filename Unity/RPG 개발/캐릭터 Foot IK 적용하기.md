캐릭터 Foot IK 적용하기
===
- Unity Animator에서 지원하는 IK 기능을 사용했습니다.

<참고 자료>
- [b3agz의 REALISTIC Foot Placement Using IK in Unity](https://youtu.be/rGB1ipH6DrM)


# 1. IK Pass 활성화
- IK를 적용하려는 객체의 Animator Layer에 IK Pass를 활성화   
![image](https://user-images.githubusercontent.com/48194683/126750021-03c35bf3-b8aa-4fa1-9f9b-6da1933b476d.png)


# 2. 사용한 API 설명
- [SetIKPositionWeight](https://docs.unity3d.com/ScriptReference/Animator.SetIKPositionWeight.html): AvatarIKGoal에 해당하는 부분의 포지션 변환 가중치 설정 (0 = IK 이전의 원본 애니메이션, 1 = 목표)
- [SetIKRotationWeight](https://docs.unity3d.com/ScriptReference/Animator.SetIKRotationWeight.html): AvatarIKGoal에 해당하는 부분의 회전 변환 가중치 설정 (0 = IK 이전의 원본 애니메이션, 1 = 목표)
- [GetIKPosition](https://docs.unity3d.com/ScriptReference/Animator.GetIKPosition.html): AvatarIKGoal에 해당하는 곳의 Position 값 반환 <br>(Ex. AvatarIKGoal.LeftFoot 이면, 아바타의 LeftFoot에 매핑되어 있는 곳의 Position 값) 
<details>
  <summary> GetIKPosition의 AvatarIKGoal 관련 추가 설명 </summary>
  
<br>
 - 아바타 매핑   
  
![image](https://user-images.githubusercontent.com/48194683/126754074-6df872af-09dc-442d-9d30-8ce068a57d5d.png)
<br>
- Left Leg -> Foot 에 해당하는 곳   
  
![image](https://user-images.githubusercontent.com/48194683/126754152-07227d9b-6fcc-4edd-90bb-17e14e2f984d.png)
  
- Gizmo로 그려본 모습 (파란색 구에 해당)
  
  ![image](https://user-images.githubusercontent.com/48194683/126754399-2b1acbe1-9fb0-4fc6-8cbc-94dce83d958c.png)

</details>

# 3. 코드 설명

<details>
  <summary> IK 적용 코드 </summary>
  
```C#
if (animator)
      {
          // Left Foot
          // Position 과 Rotation weight 설정
          animator.SetIKPositionWeight(AvatarIKGoal.LeftFoot, 1);
          animator.SetIKRotationWeight(AvatarIKGoal.LeftFoot, 1);

          ///<summary>
          /// GetIKPosition 
          ///   => IK를 하려는 객체의 위치 값 ( 아래에선 아바타에서 LeftFoot에 해당하는 객체의 위치 값 )
          /// Vector3.up을 더한 이유 
          ///   => origin의 위치를 위로 올려 바닥에 겹쳐 바닥을 인식 못하는 걸 방지하기 위해
          ///      (LeftFoot이 발목 정도에 있기 때문에 발바닥과 어느 정도 거리가 있고, Vector3.up을 더해주지 않으면 발목 기준으로 처리가 되어 발 일부가 바닥에 들어간다.)
          ///</summary>
          Ray leftRay = new Ray(animator.GetIKPosition(AvatarIKGoal.LeftFoot) + Vector3.up, Vector3.down);

          // distanceGround: LeftFoot에서 땅까지의 거리
          // +1을 해준 이유: Vector3.up을 해주었기 때문
          if (Physics.Raycast(leftRay, out RaycastHit leftHit, distanceGround + 1f, layerMask))
          {
              // 걸을 수 있는 땅이라면
              if (leftHit.transform.tag == "WalkableGround")
              {
                  Vector3 footPosition = leftHit.point;
                  footPosition.y += distanceGround;

                  animator.SetIKPosition(AvatarIKGoal.LeftFoot, footPosition);
                  animator.SetIKRotation(AvatarIKGoal.LeftFoot, Quaternion.LookRotation(transform.forward, leftHit.normal));
              }
          }

          // Right Foot
          animator.SetIKPositionWeight(AvatarIKGoal.RightFoot, 1);
          animator.SetIKRotationWeight(AvatarIKGoal.RightFoot, 1);

          Ray rightRay = new Ray(animator.GetIKPosition(AvatarIKGoal.RightFoot) + Vector3.up, Vector3.down);

          if (Physics.Raycast(rightRay, out RaycastHit rightHit, distanceGround + 1f, layerMask))
          {
              if (rightHit.transform.tag == "WalkableGround")
              {
                  Vector3 footPosition = rightHit.point;
                  footPosition.y += distanceGround;

                  animator.SetIKPosition(AvatarIKGoal.RightFoot, footPosition);
                  animator.SetIKRotation(AvatarIKGoal.RightFoot, Quaternion.LookRotation(transform.forward, rightHit.normal));
              }
          }
      }
```
  
</details>

<details>
  
  <summary> animator.GetIKPosition(AvatarIKGoal.LeftFoot) + Vector3.up 관련 추가 설명 </summary>
  
![image](https://user-images.githubusercontent.com/48194683/126755654-8a2d88f8-df39-486a-bc95-d9407dd484e2.png)

</details>

# 4. 구현 작동 영상

https://user-images.githubusercontent.com/48194683/126756607-c328ecdb-6fbe-40bf-b203-665e5099ae2a.mp4



