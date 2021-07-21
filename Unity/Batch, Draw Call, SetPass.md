
# Draw Call

### 1.Draw Call 이란?
- CPU가 GPU에게 "**오브젝트를 그려라"** 라고 명령을 내리는 것
  - 그려라 명령 안에는 **하나의 오브젝트를 그리기 위한 정보**가 담겨져 있다.(Ex. 메시, 텍스쳐, 쉐이더, 라이트 등의 정보)
- 한 프레임이 그려지는 것은 CPU와 GPU의 작업이 끝난 경우
  - 게임 최적화를 위해서 CPU, GPU 중 어느 쪽에 부하가 생기는지 확인이 필요

##### Render States(렌더 상태)
- GPU가 가지고 있는 그려야 하는 상태의 정보 테이블
- 

##### Command Buffer
- CPU가 GPU에게 내린 명령이 잠시 대기하는 곳
  - CPU가 명령을 내렸는데 GPU가 작업 중에 있으면 GPU 작업이 끝나는 동안 CPU는 다른 작업을 할 수 없음.
  - 이런 현상을 방지하기 위해 
    - CPU는 Command Buffer로 명령을 저장하고
    - GPU는 Command Buffer에서 명령을 가져온다


# Batch
- **DP Call**과 **상태 변경**들을 합친 넓은 의미의 Draw Call

# SetPass
- 렌더상태 변경의 발생 여부(메시 변경은 미포함)
