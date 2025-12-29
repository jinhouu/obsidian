Kafka 안에서 메시지가 저장되는 논리적인 장소

## Partition
Commit Log 단위, 하나의 Topic은 하나 이상의 Partition으로 구성
병렬처리(Troughput 향상)를 위한 Multi Partition 사용 권장


## Segment
메시지(Data)가 저장되는 실제 물리 File
Segment File 이 지정된 크기보다 크거나 지정된 기간보다 오래되면 새 파일이 열리고 메시지는 새 파일에 추가됨
Partition 하나당 오직 하나의 Segment 가 활성화 되어있음 (데이터가 쓰여지는 중)
![[Pasted image 20251229174903.png]]




---

![[Pasted image 20251229174540.png]]



