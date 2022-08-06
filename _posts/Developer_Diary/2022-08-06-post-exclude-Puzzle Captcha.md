---
title: Puzzle Captcha

categories:
  - Developer_Diary
tags:
---
<br>


Captcha 방식의 퍼즐을 구현하는 작업을 맡게되었다. 랜덤한 이미지에 랜덤한 빈칸이 생기고, 주어진 조각을 해당 빈칸에 Drag & Drop하는 퍼즐이다.

<p>
    <img src="https://github.com/ChansolPark/ChansolPark.github.io/blob/3c861e4eff679bffc070a79c7e5746ee47ded827/Resource/Image/CaptchaPuzzle.png" 
    width="200" height="200" />
</p>

처음에 든 생각은 UE4에서 제공하는 Drag & Drop 전용 클래스와 함수를 이용해 구현하면 되겠지 ~ 였다. 그러나 기획서의 내용 중 지점이동이라는 요소가 내 발목을 잡았다. 해당 지점이동이란 '퍼즐 조각이 유저의 마우스를 따라 이동하되, N 단위로 이동한다.' 라는 조건이 였는데, 
내가 아는선에서 UE4에서 제공하는 Drag & Drop은 유저의 마우스를 따라가는 위젯의 이동 규칙을 지정할 방법은 없었다.
멘붕이 온 나는, 긴 고민과 여러 시도 끝에 해당 기획서에 맞는 Drag & Drop 기능을 손수 제작해야겠다고 판단해 구현을 시작하였다.

먼저 마우스의 위치를 구해야했다. 마우스의 위치는 UWidgetLibrary의 GetMousePositionInViewPort 함수를 사용해 간단히 구할 수 있었고, 
해당 마우스의 좌표를 N 단위로 이동하도록 가공한 후, 퍼즐 조각 (UWidget)의 SetPositionInViewPort 함수로 '지점이동' 기능이 탑재된 Drag & Drop은 구현이 완료되었다.

다음으로 내 발목을 잡은 기획 요소는 '바운더리' 규칙이였다. '드래그 중 퍼즐 조각이 퍼즐 보드를 벗어나선 안된다.' 였는데, 이게 생각보다 어려웠다. 
먼저 현재 퍼즐조각이 바운더리를 벗어났는지를 알아내야 했는데, 관련 이해가 없었던 나는 무작정 바운더리의 AbsoluteSize를 구해 (AbsoluteSize에 대한 이해 없이 화면상 실제 사이즈를 반환한다라고만 이해하고 있었다.) 현재 ViewPort상의 퍼즐조각의 위치와 비교 연산을 통해 바운더리를 구현했다. 그리고 실행결과를 보니, 화면의 크기가 변함에 따라서 바운더리되는 영역의 크기도 변하는 모습을 볼 수 있었다. 여기서 막혀버린 나는 원인을 찾으려 매 프레임마다 좌표 정보들의 Log를 남겨 화면의 크기가 변함에 따라 각 변수들의 동작이 어떠한지 보니, 문제는 바운더리의 Absoltue Size는 화면의 크기에 따라 변동되지만, 퍼즐조각의 좌표는 ViewPort기준의 Local좌표이다보니 둘간의 비교연산이 부적절한 것이였다. 

관련 이해가 없던 나는 구글링을 통해 모니터 좌표계,  ViewPort 좌표계에 대한 이해를 얻었고 현재 내 작업에서의 모니터 좌표계는 AbsoluteSize, ViewPort 좌표계는 퍼즐조각의 위치좌표였으므로, 둘을 연산하기 위해선 좌표계 통일이 필요했다. 관련 방법을 찾기 위해 여러 함수를 기웃거리던 나는, 내가 사용중인 GetMousePositionInViewPort 함수에서 답을 찾을 수 있었다.GetMousePositionInViewPort 함수에선 GetMousePositionInPlatform 함수를 이용해 모니터 상의 마우스 좌표값을 받아온 후 GetViewportWidgetGeometry 함수로 ViewportWidgetGeometry를 받아와, AbsoluteToLocal 함수를 이용해 현재 Absolute 좌표를 ViewPort 좌표로 변환 하고 있었다. 해당 방법대로 현재 바운더리의 AbsoluteSize를 VIewPort 기준으로 변환해 비교 연산을 진행하였고, 
둘간의 비교연산은 이제 화면의 크기에 따른 변함 없이, 잘 동작하였다. 

글로 핵심 내용만 쓰다보니 나에게 쉬웠떤 작업처럼 보이지만, 실제론 정말 많이 머리를 싸매고 고민을 했던 작업이였다..ㅜ 하지만 그만큼 작업을 하며 내가 성장하고 있다는 느낌을 실시간으로 받았던, 재밌었던 작업이기에 블로그에 글로 남기게 되었다.



