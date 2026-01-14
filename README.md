# Azure Databricks Camp

이 저장소는 **Azure Databricks**의 핵심 기능을 **실습(Hands‑on)** 과 **강의(Lecture)** 형식으로 학습할 수 있도록 설계된 교육용 리포지토리입니다. 데이터 엔지니어링, Delta Lake, Structured Streaming, MLflow, Unity Catalog, Databricks SQL 등 Databricks의 주요 모듈을 단계적으로 설명합니다.

> ⚠️ **주의:** 클라우드 서비스와 Databricks Runtime은 지속적으로 업데이트되므로 캡처 화면과 UI가 시점에 따라 일부 달라질 수 있습니다. (원본 캠프 README의 고지 형식을 준용합니다.)

***

## 🎯 목표 (Goals)

*   **Databricks Lakehouse** 아키텍처의 전체 흐름 이해
*   **Delta Lake**/**Structured Streaming**/**Unity Catalog** 등 핵심 기능 실습
*   엔터프라이즈 데이터 파이프라인 설계와 운영 관점 이해
*   **MLflow** 기반 MLOps 워크플로우 실습 및 모델 추적/배포 경험
*   **Databricks SQL**을 활용한 BI 및 대시보드 연동


## 👥 대상 독자 (Audience)

*   Databricks를 처음 접하는 **데이터 엔지니어/데이터 분석가/솔루션 아키텍트**
*   **Spark/Delta** 기반 데이터 처리와 **Lakehouse** 아키텍처에 관심 있는 실무자
*   고객 워크샵, 사내 교육, **Databricks Camp** 진행자


## 🧰 사전 준비 사항

*   **Azure 구독** 및 **Azure Databricks 워크스페이스** (Premium 이상 권장)
*   **Unity Catalog** 활성화(가능한 경우)와 메타스토어 연결 권한
*   **Azure Data Lake Storage Gen2** (실습용 컨테이너/파일시스템 준비)
*   기본적인 **Spark**/**SQL**/**Python**(또는 **PySpark**) 이해
*   (선택적) **Power BI** 또는 **BI 도구** 연동을 위한 계정


## 📁 폴더 구조 (작성 중.)

    azure-databricks-camp/
    ├─ labs/                     # 실습 과제(Notebook, 코드, 지시문)
    │  ├─ lab0-overview/
    │  ├─ lab1-getting-started/
    │  ├─ lab2-lakehouse-delta/
    │  ├─ lab3-structured-streaming/
    │  ├─ lab4-mlflow/
    │  ├─ lab5-unity-catalog-governance/
    │  └─ lab6-databricks-sql-bi/
    ├─ lectures/                 # 강의 
    ├─ datasets/                 # 샘플 데이터셋
    ├─ scripts/                  # 유틸 스크립트
    ├─ resources.md              # 외부 참고 리소스 링크 모음
    └─ README.md                 # 저장소 안내(본 문서)


## 🧪 Hands‑on Labs (작성 중. 변경될 수 있습니다.)

### **Lab 0 — Databricks Overview**

*   Databricks Lakehouse와 워크스페이스 구성 요소 소개
*   Notebook, Cluster, SQL Warehouse, UC 개요

### **Lab 1 — Getting Started**

*   워크스페이스 및 Cluster/Workspace‑Level 설정
*   Notebook 실행, DBFS/ADLS 접근, 기본 PySpark 실습

### **Lab 2 — Lakehouse & Delta Lake (Bronze → Silver → Gold)**

*   데이터 수집(Bronze) → 정제(Silver) → 모델/BI(Gold) **메달리온 아키텍처** 실습
*   **Delta Lake** 테이블 생성/옵티마이즈/타임 트래블/스키마 진화

### **Lab 3 — Structured Streaming**

*   실시간 수집/처리 파이프라인 설계
*   **Auto Loader**와 **Delta Live Tables(DLT)** 개념 소개

### **Lab 4 — MLflow**

*   실험 관리(Tracking), 모델 레지스트리, 배포(Serving)
*   배치/스트리밍 inference 패턴

### **Lab 5 — Unity Catalog & Governance**

*   카탈로그/스키마/테이블 권한 모델
*   데이터/AI 자산 메타데이터 관리 및 감사(감사 로그 소개)

### **Lab 6 — Databricks SQL & BI**

*   SQL Warehouse에서 쿼리/뷰/대시보드 작성
*   외부 BI 연동(예: Power BI) 및 성능 팁


## 🎓 Lecture 

### Databricks Inside
*  [Databricks의 여정(오픈 소스에서 데이터 지능형 플랫폼까지)](/lectures/databricks-inside/databricks-history.md)

### Azure Databricks (작성 중)

* ...
* ...

### Databrocks hands-on (작성 중)

* ...
* ...

## 🚀 시작하기 (작성 중)

1.  **리포지토리 클론**
    ```bash
    https://github.com/jiyongseong/azure-databricks-camp.git
    ```
2.  **데이터 준비**  
    `datasets/` 폴더의 샘플 데이터를 **ADLS Gen2** 또는 **DBFS**에 업로드합니다.
3.  **Notebook 가져오기**  
    `labs/` 하위 폴더를 Workspace에 Import 후, 런타임/클러스터를 선택합니다.
4.  **Unity Catalog(선택)**  
    UC 메타스토어가 있다면 카탈로그/스키마를 생성하고 랩에서 해당 경로를 사용합니다.
5.  **권장 런타임**  
    최신 **Databricks Runtime**(LTS 권장)을 사용합니다.

## 📚 참고 리소스 (Resources)

*   Databricks 공식 문서, 튜토리얼, 블로그(추가 예정)

## 🤝 기여 방법 (Contributing)

이슈 제안, 문서/코드 개선은 **Issue** 또는 **Pull Request**로 자유롭게 참여해 주세요. 저장소 거버넌스와 기여 가이드라인은 오픈소스 관례를 따릅니다. 

## 📄 라이선스 (License)

이 프로젝트는 누구나 자유롭게 공유하고 활용할 수 있습니다.


## ✨ Maintainer

*   **[Ji Yong Seong (MSFT)](https://github.com/jiyongseong)** 

