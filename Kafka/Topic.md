Kafka 안에서 메시지가 저장되는 논리적인 장소

토픽은 Partition으로 구성된다.


## Partition
Commit Log 단위, 하나의 Topic은 하나 이상의 Partition으로 구성
병렬처리(Troughput 향상)를 위한 Multi Partition 사용 권장

## Segment
메시지(Data)가 저장되는 실제 무