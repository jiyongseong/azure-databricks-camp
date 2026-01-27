# [Databricks Inside] Apache Spark란?

***"빅데이터 이야기만 나오면 왜 항상 Spark가 따라붙을까?"***

Apache Spark를 처음 접하면 이런 생각부터 들 수 있습니다.

이번 글에서는 **빅데이터(Big Data)가 도대체 뭔지, 왜 Spark가 빅데이터 처리의 대표 기술이 되었는지** 에 대한 의문을 풀어보도록 하겠습니다.

## 빅데이터(Big Data)란 무엇일까?
### 데이터가 많으면 다 빅데이터인가?

결론부터 말하면 그냥 데이터가 많다고 해서 빅데이터는 아닙니다.
빅데이터라는 말에는 보통 아래 세 가지 특징이 함께 따라옵니다.

- Volume (양): 데이터 크기가 GB, TB, PB 단위로 커짐
- Velocity (속도): 데이터가 매우 빠르게 생성되고 유입됨
- Variety (다양성): 데이터 형태가 제각각 (텍스트, 로그, JSON, 이미지 등)

잘아시는 것처럼, 이걸 흔히 3V라고 부릅니다.

<img src='https://www.techtarget.com/rms/onlineimages/3_vs_of_big_data-f_mobile.png'>

### 예를 들면,
예를 들어, 보안/컴플라이언스/로그 분석 같은 시스템에서는

- 수억 ~ 수십억 건의 로그 데이터
- 웹, 모바일, IoT 기기에서 초 단위로 계속 생성
- 구조가 제각각인 이벤트 데이터

가 한꺼번에 들어옵니다.

즉, 우리는 엄청난 양의 데이터를 실시간 또는 준실시간(near real-time)으로 처리해야 하는 상황이 많습니다.

그래서 다양한 솔루션들은 크게 두 가지 방향으로 일합니다.
-	어떤 것들은 실시간 처리(real-time processing)에 집중하고,
-	어떤 것들은 데이터를 분석해 가치 있는 인사이트(analytics)를 만들기 위해 처리합니다.

결국 빅데이터라는 건 한마디로,
**한 대의 컴퓨터에서 감당하기 어려울 정도로 데이터 양이 커서
여러 자원을 활용해 대규모로 처리해야 하는 데이터**를 의미한다고 보면 됩니다.

### 분산 컴퓨팅
빅데이터를 처리하는 방법은 크게 두 가지입니다.

- 아주 강력한 서버 1대가 모든 데이터를 처리
- 여러 대의 평범한 서버를 묶어서 함께 처리

현실적으로는 2번이 훨씬 효율적이고 확장성도 좋습니다.

이게 바로 **분산 컴퓨팅(Distributed Computing)** 입니다.

<img src='https://upload.wikimedia.org/wikipedia/commons/thumb/c/c6/Distributed-parallel.svg/330px-Distributed-parallel.svg.png'>

하지만 여기서 또 하나의 문제가 생깁니다.

"여러 대가 있긴 한데…
누가 어떤 데이터를 처리해야 하는지 누가 조율하지?"

바로 이 지점에서 Spark 같이 전체 작업을 **조정하고 관리해주는 엔진**이 필요해집니다.

즉, 데이터를 나누고 어떤 순서로 처리할지 결정하고, 여러 프로세서가 같은 목표로 움직이도록 전체를 오케스트레이션 해주는 역할이 필요하게 됩니다.

## Apache Spark란
여기서 Spark가 등장합니다.

Spark는 방금 말한 것처럼, 방대한 빅데이터를 낮은 지연 시간(low latency) 으로 처리하기 위해 필요한 **엔진(engine)** 을 제공합니다.

### Apache Spark는

- 대규모 데이터를
- 여러 대의 컴퓨터에서
- 빠르게 처리하도록 만들어진 분산 처리 엔진입니다.

Spark는 UC Berkeley에서 시작되었고, 현재는 Apache 공식 오픈소스 프로젝트입니다. (자세한 내용은 [Databricks의 여정](./databricks-history.md)을 참고하세요.)

### Spark는 무엇을 해주는 도구일까?
Spark는 

- 데이터를 여러 조각(파티션) 으로 나누고
- 여러 서버(노드)에 작업을 분배하고
- 중간에 실패가 나도 자동 복구하고
- 전체 실행 흐름을 하나의 엔진처럼 관리

하는 역할을 수행합니다.

즉, 우리는 "어떤 데이터를 어떻게 처리할지만" 작성하면, Spark가 알아서 분산 처리합니다.

<img src='https://spark.apache.org/images/spark-stack.png'>

### Spark가 빠른 이유 – In-Memory 처리
기존 Hadoop(MapReduce)은

- 매 단계마다 디스크에 쓰고
- 다시 읽고
- 또 쓰는 방식이었습니다.

Spark는 다르게 동작합니다.
- **메모리(In-Memory)** 에 데이터를 올려두고
- 여러 연산을 한 번에 처리합니다.

그래서 반복 연산이나 복잡한 분석에서
- 훨씬 빠른 속도를 냅니다.

<img src='https://spark.apache.org/docs/latest/img/spark-connect-api.png'>

## 바로 이것이 Apache Spark

데이터 규모가 커질수록 처리 속도가 느려지면 전체 작업 시간이 너무 길어질 수 있습니다. 그래서 낮은 지연 시간이 핵심입니다.

Spark는 DataFrame을 기반으로 한 **인메모리 컴퓨팅(in-memory computing)** 을 통해 지연 시간을 낮춥니다.

또한, DAG(Directed Acyclic Graph) 그래프를 활용한 장애 허용(fault tolerant) 메커니즘도 갖추고 있습니다.

그리고 데이터를 다루기 위한 DataFrame API 같은 API들을 제공하는데, 이 API들은 여러 형태의 데이터를 처리할 수 있도록 통합된 인터페이스(unified front)를 제공합니다.

<img src='./images/unified-front.png'>

위 그림은 Apache Spark가 분산 네트워크 환경에서 어떻게 동작하는지를 설명합니다.

아래쪽에는 서로 다른 하드웨어 노드(node)들이 위치합니다. 즉, 여러 대의 컴퓨터가 모여 있는 클러스터(cluster)입니다.

그리고 각 노드 위에는 운영체제(OS)가 올라가 있는데, 운영체제가 하드웨어의 세부 사항을 감춰주기 때문에(추상화/마스킹) 상위 계층에서 공통된 방식으로 자원을 사용할 수 있게 됩니다.

그 위에 Apache Spark 계층이 있고, 이 계층이 여러분에게 데이터와 상호작용할 수 있는 기능들을 제공합니다.
(Apache Spark component에 대한 자세한 내용은 [Apache Spark 구성 요소 아키텍처](./spark-components.md)를 참고하시기 바랍니다.)

 예를 들면:
-	Spark SQL: SQL처럼 질의해서 데이터를 분석할 수 있게 해줍니다.
-	Spark Streaming API: 스트리밍 형태로 계속 들어오는 데이터를 처리하는 데 사용됩니다.
-	MLlib(Machine Learning libraries): Spark에서 머신러닝 모델을 학습하거나 적용할 수 있게 도와주는 라이브러리입니다.
-	GraphX(그래프 처리): 그래프 형태의 데이터(관계/연결 구조)를 분석하고 그래프 알고리즘을 적용할 수 있는 기능입니다.

이런 구조에서 사용자가 작성하는 애플리케이션(여러 개의 앱/작업)은 모두 같은 Spark 플랫폼 위에서 실행됩니다.

중요한 점은, 사용자는 보통 아래쪽 인프라(클러스터 구성, 노드 관리 등)를 직접 신경 쓰지 않아도 된다는 겁니다.

사용자 입장에서는 **Spark에 애플리케이션(잡/job)을 제출(submit)** 하기만 하면 되고, Spark가 알아서 **할당된 노드들로 작업을 어떻게 분배하고 실행할지를 관리**합니다.

***바로 이것이 Apache Spark***입니다.

********

### 참고 문서
* [Apache Spark(Databricks)](https://www.databricks.com/glossary/what-is-apache-spark)

✍️ 2026년 1월 22일 씀.