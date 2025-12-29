추가만 가능하고 변경 불가능한 데이터 구조 (Append Only File)
데이터(Event)는 항상 로그 끝에 추가되고 변경되지 않는다.


### Offset
Offset 은 Commit Log에서의 Event의 위치를 표시함

Producer가 Write하는 위치를 LOG-END-OFFSET 이라고 한다.
Consumer가 Read 후 Commit 한 CURRENT-OFFSET 과 차이(Consumer Lag)가 발생할 수 있음

