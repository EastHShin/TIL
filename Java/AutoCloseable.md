이 인터페이스를 구현한 객체는 try(…) 안에 들어갔을 때 try-with-resources 블럭을 벗어나게 되면 close 메서드가 자동으로 호출된다. 

**AutoCloseable 을 구현했다 해서 아무 조건 없이 자원을 반납하는 것이 아니다!**