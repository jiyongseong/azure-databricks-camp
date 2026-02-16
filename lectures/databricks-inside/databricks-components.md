# [Databricks Inside] Databricks 플랫폼의 주요 구성요소들
해당 글에서는 Databricks의 구성 요소들에 대한 간략한 개념을 정리하였습니다.

## Databricks Account
Databricks account는 **조직 단위의 최상위 관리 영역** 입니다. 

하나의 Account 안에 여러 Workspace _워크스페이스(팀이 협업하는 실행 환경)를 만들고, 사용자·그룹·서비스 프린시펄, 결제/사용량, 그리고 Unity Catalog(데이터 거버넌스)를 중앙에서 일관되게 관리합니다. 
반대로 워크스페이스는 노트북·쿼리·잡을 돌리고 결과를 공유하는 "작업 공간"이라고 할 수 있습니다(뒤에서 좀 더 설명이 이어집니다).

즉 **Account=조직 전체의 제어**, **Workspace=팀/프로젝트 실행 환경**으로 정리할 수 있습니다.
Databricks account에는 여러 개의 워크스페이스를 생성할 수 있습니다.

<img src='https://learn.microsoft.com/en-us/azure/databricks/_static/images/getting-started/object-hierarchy.png'>

## Workspace
Databricks Workspace는 팀이 **노트북(_notebook), SQL, 작업(_Job)을 실행하며 데이터를 다루는 협업 환경** 입니다. 

하나의 account 아래에 여러 Workspace를 만들 수 있고, 계정 수준에서 사용자, 그룹과 Unity Catalog 같은 거버넌스를 중앙 관리합니다. 

Unity Catalog 메타스토어를 workspace에 연결하면 카탈로그–스키마–테이블 구조와 권한을 모든 워크스페이스에 일관되게 적용할 수 있습니다.

## Cluster / Compute
클러스터(_cluster)는 **스파크 작업을 실행하는 컴퓨팅 자원(Virtual machines) 묶음과 설정** 을 말합니다.
Databricks UI 또는 API/CLI를 통해서 생성, 관리가 가능하며, autoscaling, spot instance 같은 기능들을 제공합니다.
클러스터에는 데이터가 저장되지 않으며, 별도로 분리된 스토리지(Azure Storage Account 등)에 저장됩니다.

Databricks는 용도에 따라 All‑purpose(인터랙티브 협업) 과 Job(자동화 작업 전용) 클러스터로 구분합니다. 노트북 실험·탐색은 All‑purpose, 스케줄·파이프라인은 Job이 적합합니다.

컴퓨트에 대한 자세한 내용은 [여기](../azure-databricks/what-is-azure-databricks-data-intelligence-platform.md#412-compute-plane-연산-영역)를 참고하세요.

## Catalog
Catalog는 Unity Catalog 오브젝트 모델에서 메타스토어 → 카탈로그 → 스키마 → 테이블로 이어지는 3계층 네임스페이스의 최상위 논리 단위입니다. 

즉, **조직의 데이터 자산을 큰 단위로 분리/정리하는 컨테이너(조직 내 모든 데이터 자산에 대해 신뢰 가능한 단일 기준 _Single Source of Truth 을 제공하는 중앙화된 메타데이터 브라우저)** 라고 할 수 있습니다.

거버넌스(권한, 감사, 리니지)를 중앙에서 일관되게 적용할 수 있고, 지역별 메타스토어를 여러 워크스페이스에 연결해 운영합니다

## Workflows
Workflows(=Lakeflow Jobs) 는 **데이터 처리 작업을 오케스트레이션하는 기능** 입니다. 

하나의 Job에 Notebook/SQL/파이프라인 등 여러 Task를 묶고, 분기/의존성(DAG), 파라미터, 알림, Git 연동을 설정해 반복 업무를 자동화합니다. 

트리거는 일정·테이블 업데이트·파일 도착·연속 실행 등을 지원하며, 실행 이력과 메트릭으로 모니터링할 수 있습니다. 

또한 외부 오케스트레이터(Airflow/ADF) 및 CLI·SDK·REST API로도 관리·연동이 가능합니다.

## DBR(Databricks Runtime) 
DBR(Databricks Runtime)는 **Azure Databricks 클러스터가 구동하는 런타임 소프트웨어 스택** 으로, 각 버전은 특정 Apache Spark 버전과 함께 사용성/성능/보안 개선을 포함합니다. 

운영 안정성을 위해 LTS(장기 지원) 릴리스가 제공되며, 지원 중인 버전, Spark 매핑, 지원 종료(EoS) 일정은 릴리스 노트에서 확인할 수 있습니다. 

또한 DBR ML은 TensorFlow, PyTorch 등 주요 ML 라이브러리와 GPU 스택을 사전 포함해 즉시 학습/추론 환경을 제공합니다. 

일반적으로 프로덕션에는 LTS 채택이 권장되며, 기능 시험이나 성능 검증은 최신 메이저 런타임에서 수행합니다.

## DBU(Databricks Unit) 
DBU(Databricks Unit)는 Databricks가 **컴퓨팅 사용량을 과금하기 위해 쓰는 표준 단위** 로, 워크로드가 소비한 처리능력을 시간(초 단위 청구) 기준으로 계량합니다. 

실제 비용은 소비 DBU × DBU 단가(워크로드/에디션/클라우드에 따라 상이)이며, 클라우드 인프라 비용(VM, 스토리지 등)은 별도 청구될 수 있습니다(서버리스는 계산기에 인프라 포함 표기). 

워크로드 유형(인터랙티브/잡/SQL Warehouse)과 구성에 따라 DBU 소모가 달라지며, 오토스케일·자동 종료로 비용을 최적화합니다.

## Delta Lake
Delta Lake은 Azure Databricks **레이크하우스 테이블의 기반이 되는 오픈 소스 스토리지 레이어** 로, Parquet 위에 파일 기반 트랜잭션 로그를 더해 ACID 트랜잭션, 확장 가능한 메타데이터, 스키마 강제/진화를 제공합니다. 

배치와 스트리밍을 단일 데이터 사본으로 처리하고 시간여행(버전 조회)을 지원합니다. 

Azure Databricks에서는 기본 테이블 형식이 Delta이므로, 별도 지정이 없으면 모든 테이블이 Delta로 생성, 관리됩니다. 

또한 Change Data Feed(CDF)로 행 수준 변경을 추적해 증분 처리를 구현할 수 있습니다.

<img src='https://www.databricks.com/wp-content/uploads/2019/09/delta-lake-logo.png'>

- [Diving Into Delta Lake: Unpacking The Transaction Log](https://www.databricks.com/blog/2019/08/21/diving-into-delta-lake-unpacking-the-transaction-log.html)

✍️ 2026년 2월 1일 씀.