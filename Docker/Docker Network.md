docker engine 설치 시 `docker0`라는 인터페이스가 기본적으로 생성된다.

서비스 운영 시 독립된 사용자 정의 네트워크를 생성하여 사용하는것이 좋다.

docker network = linux network



## 리눅스 네터워킹 빌딩 블록
- 리눅스 브릿지
- 네트워크 네임스페이스
- veth pair 및 iptables