---
title: "DrawCall_1"
categories:
  - CG
classes : wide
tags:
  - DrawCall
---

<h2>

- DrawCall

</h2>

<h3>

- DrawCall

	- CPU가 GPU에게 오브젝트를 그리라고 명령을 내리는 것

	- Drawcall을 통해 RenderState 변경 -> Render State변경을 위해서는 Draw Call이 필요

	- Drawcall의 횟수는 장면의 복잡도와 비례

	- Draw Call이 많이 발생할 경우 (CPU Bound가 커질경우) CPU와 GPU와의 처리 싱크가 어긋나 한 프레임이 누락되는 현상이 일어난다.

		- 해당 설명은 이해를 위해 Command Queue를 고려하지 않은 설명임.

	- HW의 명령어를 각각의 GPU (NVIDIA, AMD 등)에 맞는 명령어로 변역하는 과정이 필요하다.

	- 그래픽 드라이버가 해당 번역작업을 진행한다.

	- 해당 번역작업은 비용이 매우 비싸다. (시간이 오래 걸림)

<br>

- Render State에 포함된 정보들
  
	- vertex/index buffers, vertex/pixel shader programs 등
		 
<br>

- DrawCall의 상한치

	- Console Game : 2000 ~ 3000 range

	- PC : 1000 ~ 1999

	- Mobile : 100개도 많은 편 (최신 모바일 기기 : 200개 가능)

	- PS. 내가 아는 바로는 PC가 콘솔보다 사양이 더 좋다고 알고있는데 DrawCall의 상한치가 왜 Console이 더 높은가?? 강의 시점이 2020년도이고 현재가 2022년도이니 큰 차이는 없을텐데.. 관련해서 리서치를 해봐야겠다.

<br>

- DrawCall의 발생 
  
- Mesh #1 + Material #1 = Draw call #1
  
  - Mesh #N = Draw call #N
  - Mesh #N + Material #1 = Draw call #N

<br>

- Mesh #1 + Material #N = Draw call #N

	- Mesh #N = Draw call #N

<br>

- ByShader

	- Multi Pass

	- Multi Pass란 하나의 장면을 여러번 그리는 것.

	- 이 경우 단일 Mesh에 대해서도 여러 번의 드로우 콜 발생
  