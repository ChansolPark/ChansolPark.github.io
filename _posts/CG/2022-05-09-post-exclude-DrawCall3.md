---
title: "DrawCall_3"
categories:
  - CG
tags:
  - DrawCall
---

<h2>

- DrawCall 최적화_2

</h2>

<br>
<br>

<h3>

- 아틀라스(atlas) 사용

	- 하나의 메쉬에 사용되는 N개의 머테리얼을 하나의 머테리얼로 합쳐 DrawCall # N -> DrawCall # 1로 최적화

	- 흔히 Sprite 리소스에서 찾아 볼 수 있다.

</h3>

<br>
<br>

<h3>

- 배치(batch) 렌더링

	- 1Batch == 1DrawCall

	- Mesh #N + Material # 1 = DrawCall #N -> Mesh #1 + Material #1 = DrawCall #1

		- 머테리얼이 기준 : 다른 오브젝트 다른 메시를 사용하더라도 같은 머티리얼을 사용 시 하나의 batch 구성이 가능

		- 텍스쳐만 다른 2개의 머티리얼이 있다면 아틀라스를 이용해 1개의 머티리얼로 만든 후 batching 사용

	- 정적 배칭 (Static Batching) : 정적인 게임 오브젝트를 큰 메시로 합치고 더 빠른 방법으로 렌더링

	- 동적 배칭 : 메시가 충분히 작은 경우 이 기법을 사용하면 메시의 정점이 CPU에서 트랜스폼되고, 여러 유사한 메시가 그룹화되고, 모든 것이 한꺼번에 드로우됨

		- 메시가 충분히 작은 경우에 추천.
	
</h3>

<br>
<br>

<h3>

- 배치렌더링의 사용

	- 정적이고 움직이지 않는 오브젝트 -> 주로 배경 오브젝트

		- 동적배칭보다 효율적 : 동적배칭은 매번 배칭 구성을 위한 버텍스 연산 필요

	- 주의점 : 메모리가 추가로 필요 (Vertex, Index 배열의 크기가 커지기 때문)

		- 드로우콜을 줄이기 위해 오브젝트들을 합쳐서 내부적으로 하나의 메시로 만듦 -> 통합된 메시를 GPU로 가져가서 그대로 렌더링

			- 메모리가 문제된다면 스태틱 배칭의 대상을 줄여야 함

	- Scene을 모듈화하여 제작하는 방식 사용가능

		-다만 Scene을 하나의 단일 메시로 만드는 것은(merging 기법), visibility culling의 문제 발생
	
</h3>

<br>
<br>

<h3>

- Merging -> visibility culling problem

	- merging기법으로 인해 전체 배경이 하나의 메쉬로 묶이면 visibility culling이 정상적으로 작동되지 않음.

		- 작은 오브젝트 하나만 카메라에 담겨도 모두 카메라에 담김 처리가 됨 (하나의 메쉬이기 때문에)

	- 스태틱 배칭의 경우 원래의 게임 오브젝트 기준으로 컬링이 이루어지므로 문제 없음

		- 통상적으로는 같은 메쉬를 가진 오브젝트끼리 모듈화를 거쳐 스태틱 배칭을 이용하여 렌더링
	
</h3>

<br>
<br>

<h3>

-  visibility culling

	- View frustum culling

		- 플레이어 시야 밖의 오브젝트를 컬링

	- Back-Face Culling

		- 플레이어 시야 기준 물체의 뒷면을 컬링

	- Occlusion Culling

		- 플레이어 시야 기준 가려진 물체를 컬링
	
</h3>

<br>
<br>

<h3>

- 배치 렌더링 사용 : 동적 배칭

	- 동적으로 움직이는 오브젝트들끼리 배칭처리

		- 동일한 머티리얼을 사용하고 특정 조건들을 만족하는 다이나믹 오브젝트들에 대한 자동 배칭

		- 다이나믹 배칭에 쓰이는 정보를 모아 정점 버퍼와 인덱스 버퍼에 담음

	- 매 프레임마다 오버헤드 발생

		- 매번 데이터 구축과 갱신 발생

	- 오버헤드에도 불구하고 드로우 콜을 줄임으로 전체적인 성능 향상 (오버헤드로 인한 성능저하 < 드로우콜로 인한 성능향상)

	- 한계

		- Skinned Mesh 적용불가 (unity3d) : GPU 고속 연산 수행 (배칭으로 처리할 경우 GPU 고속 연산 불가로 성능저하)

		- 정점이 너무 많은 메시는 대상에서 제외 : 오버헤드로 인한 성능저하 > 드로우콜로 인한 성능향상

	
</h3>