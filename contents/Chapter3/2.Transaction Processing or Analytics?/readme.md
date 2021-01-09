# 트랜잭션 처리나 분석

여기서 트랜잭션은 배치에 비해 지연되는 시간이 낮게 읽기와 쓰기를 가능하게 한다는 의미.

보통 데이터를 넣고, 읽는 걸 온라인 트랜잭션 처리(OLTP, online transaction processing)이라고 하고, 카운트나 합, 평균과 같이 aggregation하는 걸 온라인 분석처리(OLAP, online analytic processing)이라고 해.

**데이터 웨어하우징**

- OLTP에 영향을 주지 않고 데이터 분석을 하기 위해서 데이터웨어하우스(data warehouse)라는 개별 데이터베이스를 만들어서 분석을 하는거.
    - ETL(Extract-Transform-Load): (OLTP DB로 부터) 데이터를 분석하기 쉬운 스키마로 변환(transform)하고 깨끗하게 정리해서 저장하는 것.
- 장점: 분석 패턴에 맞게 최적화할 수 있다.

OLTP: 분석 시스템
데이터 웨어하우스: ETL과정으로 저장을 한 DB.
데이터 레이크: 제일 raw한 데이터를 담는 DB. 분석이 필요한 시점에 가져와서 변환해서 씀.

상용 데이터웨어하우스 [redshift](https://aws.amazon.com/ko/redshift/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc)

**데이터 웨어하우스가 OLTP DB와 어떤 차이가 있을까?**

- 관계형 모델 사용.
- SQL 질의를 생성하고 결과를 시각화하고 분석가가 데이터를 탐색할 수 있게 해주는 그래픽 데이터 분석 도구가 있다. (drill-down, slicing, dicing)
- 둘다 SQL을 쓰지만 데이터웨어하우스는 분석 질의에 최적화되어 있다.

| Name           | OLTP                                      | OLAP                                  |
| -------------- | ----------------------------------------- | ------------------------------------- |
| 주요 읽기 패턴 | "질의당 적은 수의 레코드                  | 키 기준으로 가져옴"                   | 많은 레코드에 대한 집계 |
| 주요 쓰기 패턴 | "임의 접근                                | 사용자 입력을 낮은 지연시간으로 기록" | "bulk import(ETL)       | 또는 이벤트 스트림" |
| 주요 사용처    | 웹 애플리케이션을 통한 최종 사용자/소비자 | 의사결정 지원을 위한 내부 분석가      |
| 데이터 표현    | 데이터의 최신 상태(현재 시점)             | 시간이 지나며 일어난 이벤트 이력      |
| 데이터셋 크기  | GB~TB                                     | TB~PB                                 |
| 병목구간       | 디스크 탐색                               | 디스크 대역폭                         |

그럼 데이터 웨어하우스는 어떻게 모델링을 할까?

**분석용 스키마: 별 모양 스키마(star schema)와 눈꽃송이 모양 스키마**

- star schema = dimensional modeling (차원 모델링)
- **fact table(사실 테이블)**에 이벤트별로 데이터를 저장.(1 row = 1 event 발생). 로그를 쌓는 느낌으로?
- 정규화 테이블인데 fact table이 FK로 구성되어있다~
- 테이블이 매우 커질 수 있다.
- fact table의 일부 칼럼은 dimension table(차원 테이블)을 가르킨다. (외래키 참조)

    e.g.) fact_sale: date / product_id / price 가 칼럼이라고 했을 때
    dimension table은 product_id / product_name / category 칼럼으로 구성되어있는 product table이다.

- 더 변형된게 눈꽃송이 모양 스키마(snowflake schema)