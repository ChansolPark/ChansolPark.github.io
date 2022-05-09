---
title: "DrawCall_2"
categories:
  - CG
tags:
  - DrawCall
---

<h2>

- DrawCall 최적화_1

</h2>

<br>

<h3>

- 렌더링 되는 오브젝트 줄이기

  - 단순히 scene에 보이는 오브젝트 수 줄이기

<br>

- 카메라의 Near, Far Clipping Plane의 거리줄이기 (View Frustum Culling)
  
	- 실 세계에선 멀리있다고 해도 우리가 눈으로 볼 수 있지만 CG에선 성능을 위해 가림

<br>

- Near Clipping Plane

	- 그릴 대상의 최소 거리 값을 지정해 조건을 벗어난 오브젝트는 클리핑

<br>

- Far Clipping Plane

	- 그릴 대상의 최대 거리 값을 지정해 조건을 벗어난 오브젝트는 클리핑

    - 먼 곳에 위치한 오브젝트가 화면에 안 보이도록 하기 위해 Fog 적용

      - 위의 조건만 넣을 경우 없던 물체가 갑자기 뚝 하고 생겨나는 현상이 있기 때문에 안개를 이용해 자연스러움을 연출

<br>

- 오클루전 컬링 (Occlusion Culling)

    - 시야에 보이지 않는 물체를 그리지 않음

<br>

- LOD 

  	- 물체를 그리는 디테일에 Level을 둬서 최적화를 진행

		- 복수의 모델을 하나의 오브젝트가 들고있다.

		- 각각의 모델은 디테일의 정도가 다르다.

		- 그리는 대상과의 거리에 따라 퀄리티를 다르게 함

		- 가까우면 10만개의 폴리곤으로, 멀면 1만개의 폴리곤으로

<br>

- 리얼타임 라이트 대신 Baked 라이트 사용

	- 라이트 개수 만큼의 드로우 콜 필요 (포워드 렌더링 기준)

		- 라이트 Baking으로 Light map을 생성해 최적화를 진행 (Static object에 한함)

		- PS. 포워드 렌더링, 디퍼드 렌더링에 관한 내용이 많이 나오는데 한번 리서칭이 필요할듯 하다.

  - Reflection Probes의 사용 최소화
  
</h3>