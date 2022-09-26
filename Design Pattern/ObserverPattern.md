객체의 상태가 변할 때, 그를 관찰하는 옵저버 객체들에게 통지하는 디자인패턴

→ 객체의 상태 변화를 관찰하는 옵저버들의 목록을 객체에 등록하여, 상태변화가 있을 때마다 객체가 직접 옵저버에게 통지하도록 하는 디자인 패턴

### 장점

- 한 객체의 변경사항을 실시간으로 다른 객체에 전파할 수 있다.
- 느슨할 결합으로 객체간의 의존성을 제거할 수 있다.

### 단점

- 너무 많이 사용하게 되면 상태 관리가 힘들어 질 수 있다.

### 구현

```java
public interface General {

    void orders(String command);
}
```

```java
public interface Soldier {

    void takeOrders(String command);
}
```

```java
public class EastGeneral implements General{

    private final List<Soldier> soldiers;

    public EastGeneral(List<Soldier> soldiers) {
        this.soldiers = soldiers;
    }

    public void advance() {
        final String command = "병사들이여 진격하라~";
        System.out.println(command);
        orders(command);
    }

    @Override
    public void orders(String command) {
        soldiers.forEach(soldier -> soldier.takeOrders(command));
    }
}
```

장군이 병사들에게 진격 명령을 내리고, 병사 객체들에게 이를 알린다.

```java
public class Thor implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}

public class Josh implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}

public class Chris implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}

public class DonkeyKong implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}

public class Hunch implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}

public class Movie implements Soldier{

    @Override
    public void takeOrders(String command) {
        System.out.println(command + " 명령을 받들겠습니다~");
    }
}
```

명령을 받은 병사들은 이를 인지한다!

```java
@Test
    void observe() {
        final EastGeneral eastGeneral = new EastGeneral(
                List.of(new Thor(), new Josh(), new Chris(), new DonkeyKong(), new Hunch(), new Movie()));

        eastGeneral.advance();
    }
```

<img width="337" alt="image" src="https://user-images.githubusercontent.com/64204666/192331519-9fd7b596-f195-4460-80a0-18fa4f572034.png">

테스트 코드를 통해 확인해보니 예상대로 명령을 받은 병사 객체들이 이를 잘 인지하고 명령을 받들었다.