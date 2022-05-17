---
title: 내 인생 첫 최적화 작업_1

categories:
  - Developer_Diary
tags:
---
<br>

파트장님께서 신규맵의 최적화 작업을 진행할 희망인원 1명을 질의하셨다. 난 바로 자원했고 인생 첫 최적화 작업을 시작하게 되었다.
일단 난 쉐이더를 작성하며 알게된 지식 조금을 제외하면 그래픽스에 대한 지식이 없었기에 그래픽스에 대한 공부를 해야 했다. 그래픽스에 대한 공부는 해당 링크들에서 진행 했다.

<br>

// 게임 아티스트를 위한 CG 최적화 이론

https://www.youtube.com/watch?v=Ioetj_dK44g&list=PLyuV91SJJre7DeREVCzx8VG599PCGTtL2

// 리얼타임 렌더링의 기초, 심화 과정

https://www.unrealengine.com/ko/onlinelearning-courses/an-in-depth-look-at-real-time-rendering

<br>

언리얼이 제공하는 여러 프로파일링 커맨드, UI들을 활용해 문제점을 서치했고 발견된 큰 문제는 다음과 같았다.

- 컬링된 액터들에게서 여전히 애니메이션 틱이 돌고있었다.
  
  - 해당 문제는 2019, 2018 언리얼 서밋에서 발표된 Animation URO 기법을 이용해 최적화 하였다.
  
  - 기본적으로 URO를 적용하다 컬링이 되면 URO Rate를 int32::max를 넣어주는 방식으로 진행했다.

- 컬링된 액터들에게서 여전히 MovementComponent 틱이 돌고있었다. 

  - 해당 문제는 Movement의 State를 None - Walk로 토글해주는 방식으로 작업했다.

  - 플레이어간의 동기화에 문제가 생기지 않을까? 다른 플레이어가 점프중일때 컬링이 풀려 walk로 세팅되면 어떡하지? 라는 고민이 있었지만, 실 테스트 결과 아무 이상이 없어 적용해두었다.

<br>

해당 내용들을 수정해 20 ~ 25 FPS에서 35 ~ 40 FPS로 상향되는 효과를 보았다. 하지만 해당 내용들은 CPU Bound와 관련된 문제다보니 아직 GPU Bound를 해결해야 한다. 현재까지 찾아낸 GPU Bound는 다음과 같다. 

- 메쉬 그룹별로 병합이 되어있지 않음.
  
  - 병합이 되어 있지 않아 Drawcall 과다 호출 문제가 있는 것으로 판단함.

  
- Dynamic Shadow 관련 최적화 미흡

  - CSM, Mesh Distance Field 미 적용 중


- 각 오브젝트의 텍스쳐 해상도가 너무 높음

  - 맵을 둘러보다 freeze 현상이 나타나 텍스쳐 해상도의 크기를 확인해보니 부하가 예상되는 크기였음.


내일은 배경 작업자 분들과 최적화 관련 회의가 있다. 해당 회의에서 찾아낸 GPU Bound를 설명해드리려 한다. 

