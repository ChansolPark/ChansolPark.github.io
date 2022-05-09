---
title: "DrawCall_3"
categories:
  - CG
tags:
  - DrawCall
---

<h2>

- DrawCall 최적화_3

</h2>

<br>
<br>

<h3>

- GPU Instancing 

	- 엔진마다 사용하는 명칭이 다르지만 전에 다뤘던 batching과는 다른 기능임.
  
	- 이 포스트에서 batching은 GPU Instancing이 아닌 전 포스트에서 다루었던 batching을 이야기 하겠음.
	
<br>
<br>

- Instancing == batching, clustering

	- 한번의 드로우 콜로 여러 오브젝트들을 한번에 처리

		- batching과 공유되는 개념
	
<br>
<br>

- Instancing != batching, clustering

	- 배칭과는 달리 동일한 메시의 복사본들을 만듦

	- 배칭에 비해 런타임 오버헤드가 적음

		- 배칭 : 지오메트리 정보들을 하나의 메시로 합치는 과정

		- 인스턴싱 : 별도의 메시를 생성하지 않음 (복사해 사용)

	- 처리 방법 

		- 인스턴싱되는 오브젝트들의 트랜스폼 정보를 별도의 버퍼에 저장

		- GPU는 트랜스폼 정보들이 담긴 버퍼와 원본 메시를 가져다가 여러 오브젝트들을 한번에 처리

		- Scaling, Reflection, Rotation등을 통해 각각 복사된 메시간의 차별점을 구현
  
<br>
<br>

- 사용처 예시

	- 초원의 푸른 잔디들

	- 행성파편들

	- 숲의 나무들

	
</h3>