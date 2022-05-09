---
title: "Shader Complexity"
categories:
  - CG
tags:
  - Shader Complexity
---

<h2>

- 쉐이더 복잡도 (Shader Complexity)

</h2>

<br>

<h3>

- 대부분의 GPU작업은 shader에서 수행
  
	- Shader에서 많은 병목의 주요 원인이 발생

	- 병목이 shader instruction(ALU)으로 판명된다면, vertex shader나 pixel shader가 너무 많은 일을 하고 있어서 
  
    - 파이프라인이 대기중임을 의미

<br>
<br>

- 진단

	- Shader 자체의 복잡도가 높은 경우를 파악하자 ! : 너무 많은 명령어

	- Shader 자체의 복잡도는 높지 않으나 너무 많은 데이터 처리가 원인이 될 수도 있다 !

		- Vertex shader는 문제가 없으나, 처리하는 메시가 지나치게 많은 정점을 포함하고 있는 경우

	- 지나친 overdraw의 발생

<br>
<br>

- 간단한 점검

	- 명령어가 많다면 명령어를 줄인다.

	- Pixel shader : 복잡한 머티리얼, Post Processing 연산(Color Grading, Bloom, DOF etc)

		- 이를 확인하는 방법은 해상도를 줄여 보는 것임

	- Vertex shader

		- 이를 확인하는 방법은 정점 수를 줄여 보면 된다.

		- LOD(Level of Detail) 사용 -> 자동 메시 생성 활용 (게임 엔진)

<br>
<br>
		
- Shader instruction 자체가 아닌 다른 부분의 문제를 암시하는 경우도 많다.

	- Overdraw 문제

		- 불투명 오브젝트, 반투명 / 투명 오브젝트

		- 파티클 -> 시뮬레이션보다는 텍스쳐, 텍스쳐 애니메이션 활용
	
</h3>