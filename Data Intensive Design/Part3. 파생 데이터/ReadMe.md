# Part3. 파생 데이터
데이터 모델도 다르고 최적화된 접근 양식도 다른 여러 데이터 시스템을, 일관성있는 하나의 애플리케이션 아키텍처로 통합하는 문제를 다룬다.

**데이터를 저장하고 처리하는 시스템의 종류**

레코드 시스템

진실의 근원(source of truth). 원천 데이터.

사용자 input으로 받은 데이터를 저장한것.

(일반적으로)정규화를 거쳐 저장함.

파생 데이터 시스템

다른 시스템에 있는 데이터를 가져와서 특정 방식으로 변환하고 처리한거.

데이터를 잃게되더라도 원천데이터로부터 다시 생성 가능

e.g.) 캐시, 비정규화 값, 생긴, 구체화 뷰

중복(rebundant)

읽기질의 성능을 높이는데 도움됨.

batch처리 데이터플로 시스템 + 관련된 도구

[10. 일괄처리 (batch)](https://maisy.notion.site/10-batch-a26f3115e12042bbb6efb2431774abec)

데이터 스트림 시스템 + 관련된 도구

11. 스트림 처리

위 도구들을 어떻게 잘 사용할 수 있을까?

12. 데이터 시스템의 미래