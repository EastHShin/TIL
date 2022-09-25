### Multipart란?

- 서버로 파일 혹은 데이터를 보내기 위해 사용하는 방식
- 이미지 등의 파일을 보낼 때 이미지에 대한 설명과 같은 데이터를 같이 보내게 되는데, 이 둘의 Content-type 이 다르다 → 이를 multipart를 통해 해소
- 전송하는 데이터가 클 때도 이용
- Content-type 필드 값을 `multipart/form-data` 혹은 `multipart/byterange` 로 지정
- boundary로 엔티티를 구분
- 보통 POST 요청으로 보냄
    - GET 방식으로는 보낼 수 있는 데이터의 길이에 한계가 있음
    - POST 요청은 길이 제한이 없음

### Boundary란?

- 여러개의 엔티티가 전송될 때 구분하기 위해 사용
- 각 엔티티의 맨 앞에 `--` 를 붙여 사용
- 마지막 엔티티는 바운더리 앞, 뒤로 `--` 가 붙음

![리퀘스트헤더](https://user-images.githubusercontent.com/8912548/31535308-40b3f798-b02d-11e7-81b3-a50670201d44.png)

### Content-Disposition

- mutlipart는 각 파트마다 헤더필드가 포함됨
- 그 파트가 multipart 의 엔티티라고 알려주는 역할
    - Content-Disposition: form-data