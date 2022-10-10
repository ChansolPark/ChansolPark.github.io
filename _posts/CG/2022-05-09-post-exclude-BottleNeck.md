---
title: "BottleNeck"
categories:
  - CG
classes : wide
tags:
  - BottleNeck
---

<h2>

- 병목 (Bottle Neck)

</h2>

<br>
<br>

<h3>

- 전체 시스템의 성능이나 용량이 하나의 구성요소로 인해 제한을 받는 현상

	- 병목을 제거하는 것 = 최적화

	- Drawcall에 의한 병목 = CPU BottleNeck

<br>
<br>

- 무엇이 병목을 발생시키는가?에 대한 파악이 중요

	- 병목 지점을 찾는 과정 : 프로파일링 (Profiling)

	- 디바이스 의존적 : PC vs Mobile, 최소 사양

	- 기기마다 병목의 상황이 다를 수 있음 : HW spec, Image resolution..

<br>
<br>

- 측정 단위

	- FPS? X -> ms/frame (프레임 타임)이 적절

<br>
<br>

- 프로파일러 (Profiler)

	- 프로파일링 툴은 어느 부분에서 GPU가 시간을 많이 소비하는지, 어떤 부분을 바꾸면 속도가 향상되는지를 보여주는 도구.

<br>
<br>
	
- 플랫폼 별 다양한 프로파일러 존재

	- PC : GPU vender에 따라 존재 (NVIDIA's Nsight, AMD's GPU PerfStudio, Intel's GPA), RenderDoc

	- Game Engine : Unity, Unreal Profiler
		
</h3>

- 쉐이더 복잡도 (Shader Complexity)

	- 대부분의 GPU작업은 shader에서 수행
		- Shader에서 많은 병목의 주요 원인이 발생
		- 병목이 shader instruction(ALU)으로 판명된다면, vertex shader나 pixel shader가 너무 많은 일을 하고 있어서 파이프라인이 대기중임을 의미

	- 진단
		- Shader 자체의 복잡도가 높은 경우를 파악하자 ! : 너무 많은 명령어
		- Shader 자체의 복잡도는 높지 않으나 너무 많은 데이터 처리가 원인이 될 수도 있다 !
			- Vertex shader는 문제가 없으나, 처리하는 메시가 지나치게 많은 정점을 포함하고 있는 경우
		- 지나친 overdraw의 발생

	- 간단한 점검
		- 명령어가 많다면 명령어를 줄인다.
		- Pixel shader : 복잡한 머티리얼, Post Processing 연산(Color Grading, Bloom, DOF etc)
			- 이를 확인하는 방법은 해상도를 줄여 보는 것임
		- Vertex shader
			- 이를 확인하는 방법은 정점 수를 줄여 보면 된다.
			- LOD(Level of Detail) 사용 -> 자동 메시 생성 활용 (게임 엔진)
		
	- Shader instruction 자체가 아닌 다른 부분의 문제를 암시하는 경우도 많다.
		- Overdraw 문제
			- 불투명 오브젝트, 반투명 / 투명 오브젝트
			- 파티클 -> 시뮬레이션보다는 텍스쳐, 텍스쳐 애니메이션 활용

	
</h3>