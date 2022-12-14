Hippo

- 월급이 가장 많은 사람의 의견
- 데이터 기반 제품 개발을 가장 방해하는 사람…

### 데이터 기반의 제품 개발

일반적인 서비스 출시 과정

→ waterfall 방식

데이터 기반

→ Agilie 방식

- 작은 단위로 쪼개서 출시
- 데이터를 보고 고객이 원하는 것이 무엇인지 정함

기존 홈페이지와 변경된 홈페이지 비교

→ 구매율에 얼마나 차이가 났는지?

→ 이것은 잘못된 데이터 측정 방법

![1](https://user-images.githubusercontent.com/64204666/194036809-ebe011c0-5c8e-4008-8c4c-3dc85306bce0.png)


외적인 요인이 많다

실제로는 바꾼 개발이 악영향을 끼쳤을지도 모른다.

A/B 테스트

- 동일한 시간에 두 버전을 비교할 수 있다.
- 추측을 통한 변경이 아닌, 논리적으로 데이터를 통해 의사소통 할 수 있다.

예시

- 넷플릭스에서 영화에 대한 포스터를 여러개로 나누어 보여준다.

![2](https://user-images.githubusercontent.com/64204666/194036829-519697ec-9030-46a3-9eba-81142c32cd8d.png)


왜 A/B 테스트를 하는가?

- 실제 대부분의 아이디어는 실패하기 때문에 실험을 통해 검증해야 한다.
- A/B 테스트 없이 변화를 통한 아이디어 실현을 하게 되면, 실패에 대한 리스크가 있다.

구현은?

- 사용자에 따라 A/B 분배
- A/B 그룹에 따른 로직 구현
- 그룹별 결과 트랙킹

작은 규모의 회사는 실패를 맞닥뜨리면서 빠르게 개발하는게 낫다.

매출 외에 어떤 데이터를 측정할 수 있을까?

→ 클릭수, 방문율, 회원가입, 재방문율

### 장애리스크 줄이는 배포 방법

배포를 두려워 하는 이유?

- 문제가 발생했을때 회사에 발생시킬 문제에 대한 영향도
- 롤백에 대한 어려움 (어떤 코드로 되돌려야 할 지 즉각적인 판단 필요)

→ 영향도 최소화, 빠른 롤백

### 점진적 전달

- 기능 출시를 제어
- 새로운 기능에 문제가 없는지 일부 사용자들에게만 보여준다.
    - 새로운 기능을 보는 사람들은 새로운 기능만 보아야 한다.(왔다갔다 하면 안됨)

기능플래그

- on/off 스위치

![3](https://user-images.githubusercontent.com/64204666/194036849-a4f4765c-3663-4a88-aca6-9494b1d2234f.png)


blue/green 배포

canary 배포

기능 플래그

- 일단 배포를 다 한다.
- 기능을 다 키진 않은 상태
- 기능을 하나씩 켜가면서 점진적으로 확인
- 코드를 배포해도 기능 출시는 되지 않음
- 운영환경에서 쉽게 테스트할 수 있음
- 점진적 출시를 통한 영향도 최소화
