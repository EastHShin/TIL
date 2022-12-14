**대용량 데이터베이스에서 조회 속도를 높이기 위한 기술**

대용량이 아니면 의미가 없는가?
- 적은 데이터에서는 조회 성능이 그리 차이 나지 않음
- 삽입, 수정, 삭제에서 성능이 희생되기 때문에 메리트가 없다.

### 검색 알고리즘

- B-Tree
- Hash
- B+Tree
- B*Tree
- R-Tree

### Cluster Index

데이터와 무리를 이루고 있는 인덱스

- 인덱스 안에 데이터를 포함
- 테이블의 프라이머리 키에 대해서만 적용
- PK 값에 의해 레코드의 저장 위치가 결정되므로 인덱스 알고리즘이라기 보다는 테이블 레코드 저장 방식이라고 볼 수 있음
- 인덱스에 데이터 페이지가 함께 존재
- 리프페이지 == 데이터 페이지

프라이머리 키가 없는 경우의 InnoDB 테이블은 어떻게 클러스터링 테이블로 구성될까?

→ PK가 없는 경우 우선순위 대로 PK 대체 컬럼을 선택

1. PK가 있으면 PK를 클러스터링 키로 선택
2. NOT NULL 옵션의 유니크 인덱스 중에서 첫번째 인덱스를 클러스터링 키로 선택
3. 자동으로 유니크한 값을 가지도록 증가되는 컬럼을 내부적으로 추가한 후, 클러스터링 키로 선택
    - 이렇게 추가된 컬럼은 사용자에게 노출되지 않고, 쿼리 문장에 명시적으로 사용할 수 없다.

### Non-Clustered Index

데이터와 무리를 이루고 있지 않은 인덱스

- 인덱스 안에 데이터를 포함하지 않음
- Secondary Index (보조 인덱스) 라고도 함
- 테이블에 여러개 존재 가능
- 유니크 제약조건으로 컬럼 생성하면 자동으로 생성
- 리프 페이지에서 데이터가 있는 곳의 주소를 가짐
- 데이터 페이지에 데이터가 정렬되지 않아도 됨
    - Cluster Index 보다 삽입,수정,삭제시 부하가 적음