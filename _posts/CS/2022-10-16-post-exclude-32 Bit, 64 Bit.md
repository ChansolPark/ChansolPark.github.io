---
title: "32bit, 64bit"
categories:
  - CS
classes : wide
tags:
---

<br>
<h2>
32bit, 64bit
</h2>
<br>

통상적으로 Fetch 시 I/O Bus 로 데이터가 이동할때 최대 크기, CPU가 한번에 읽어 드릴 수 있는 명령의 크기를 말한다. 따라서 32bit면 Memory에서 CPU로 이동할때 최대 32bit씩 이동되어 처리되는 것이고, 64bit는 최대 64bit씩 처리된다.

<br>

<br>
<h2>
32bit -> 64bit에 따른 포인터의 변화
</h2>
<br>

32bit에서 64Bit의 시스템으로 변경되어도 프로그래밍에 거의 차이는 없다고한다. 다만 자료형들의 크기에 변화가 있다. 그중 포인터를 살펴보자면, 32bit에서는 포인터의 크기가 4Byte이나, 64bit에서는 포인터의 크기가 8Byte이다. 그 이유는 위에서 설명했듯 bit 수에 따라 한번에 처리가능 한 양이 결정되기 때문인데, 시스템이 32bit인데 포인터의 크기가 64bit라면 주소 정보를 전달할때 2번에 걸쳐서 주소를 전달해야 하고, 해당 방식은 시스템의 성능 저하를 부른다고 한다. 

<br>


<br>
<h2>
포인터의 크기가 클 수록 생기는 장점
</h2>
<br>
만약 메모리의 크기가 1GB인 시스템에서 포인터의 크기가 4bit일 경우 포인터로 16가지(0 ~ 2^⁴ -1) 의 주소값을 표현할 수 있게 되는데, 그럼 메모리의 크기가 1 GB여도 실제 사용가능한 메모리는 8Byte인 현상이 일어난다. 메모리가 커도 표현 가능한 주소 값기 떄문, 따라서 포인터의 크기가 클수록 사용가능한 메모리의 크기도 정비례하기 때문에, 시스템이 허용하는 선에서 최대한 포인터의 크기를 키우다보니, 32bit 시스템에선 32bit의 포인터를 사용하고, 64bit에선 64bit의 포인터를 사용하는 것이 일반적이다.
그럼 떠오르는 생각으로, 만약 메모리가 엄청 작다면 ? 포인터의 크기가 아무리 커도 소용 없는 것이 아닌가? 라는 것인데, 그에 대한 대안책으로 '가상 메모리'를 사용한다고 한다.

<br>


<br>
<h2>
지식 출처 :
</h2>
<br>

뇌를 자극하는 윈도우즈 프로그래밍 https://www.youtube.com/watch?v=eiQViBnTxtw&list=PLVsNizTWUw7E2KrfnsyEjTqo-6uKiQoxc&index=5