LinkedIn 에서 하루 4.5조 개 이상의 이벤트, 3천억 개 이상의 사용자 관련 이벤트 스트림 처리 필요
기존의 Messageing Platform으로 처리 불가능, 이를 해결하기 위해 개발됨
 
Apache Kafka의 정의는 아래와 같이 할 수 있다.
- Data In Motion Platform
- Data(Event) Streaming Platform
### Event 란?
비즈니스에서 일어나는 모든 일(데이터)을 의미한다.
이 이벤트(데이터)를 비즈니스에 활용
### Event(Data) Stream 은 무엇인가?
연속적인 많은 이벤트(데이터)들의 흐름
따라서 이벤트는 BigData의 특징을 가지고있다.

## Apache Kafka의 특징
1. 데이터 스트림을 안전하게 전송 (Publish & Subscribe)
2. 디스크 스트림을 디스크에 저장 (Write to Disk)
3. 데이터 스트림을 처리 및 분석 (Processing & Analysis)
### Apache Kafka 유즈케이스
위 특성으로 인해 Event(메시지/데이터)가 사용되는 모든 곳에서 사용
- Legacy Messaging System 대체 -> BE 엔지니어
- IOT 디바이스 혹은 Application으로부터 데이터 수집 및 전송 -> App 개발자 / BE 엔지니어
- 시스템 혹은 Application 에서 발생하는 로그 수집 및 전송 -> BE 엔지니어
- Realtime Data Stream Processing (Fraud Detection, 이상 감지 등) -> 데이터 엔지니어
- 실시간 ETL -> BE 엔지니어
- Spark, Flink, Storm, Hadoop 과 같은 빅데이터 솔루션과 함께 사용 -> 데이터 엔지니어


## Apache Kafka 주요 요소
- [[Topic]]
- [[Consumer]]
- [[Producer]]