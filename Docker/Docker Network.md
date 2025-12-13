docker engine 설치 시 `docker0`라는 인터페이스가 기본적으로 생성된다.
![[Pasted image 20251213234514.png]]

서비스 운영 시 독립된 사용자 정의 네트워크를 생성하여 사용하는것이 좋다.

docker network = linux network



## 리눅스 네터워킹 빌딩 블록
- 리눅스 브릿지
- 네트워크 네임스페이스
- veth(virtual ethernet) pair 및 iptables
이 조합은 복잡한 네트워크 정책을 위한 전달 규칙, 네트워크 분할 및 관리도구를 제공한다.

## 리눅스 브릿지
![[Pasted image 20251213234150.png]]

리눅스 커널 내부의 물리적 스위치를 가상으로 구현한 OSI 2계층 Device

도커의 브릿지 또한 사설 네트워크로 분리하여 내부 네트워크를 이용하여 사설 네트워크 망으로 사용

## 네트워크 네임스페이스
![[Pasted image 20251213234553.png]]

## Container의 veth
![[Pasted image 20251213235000.png]]


