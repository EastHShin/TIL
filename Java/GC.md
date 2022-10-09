**Heap 메모리에 저장된 객체들 중 사용하지 않는 것들을 지우는 것**

### GC 대상

- 객체가 Null 인 경우
- 블럭 안에서 생성된 객체인데, 블럭 실행 종료 후
- 부모 객체가 Null 인 경우에, 포함하는 자식 객체

### GC의 메모리 해제 과정

1. Marking
    - 메모리가 사용되는지 아닌지를 찾아내는 과정
    - 모든 오브젝트를 스캔하기 때문에 매우 많은 시간 소모
2. Normal Detection
    - 참조되지 않는 객체를 제거하고, 메모리를 반환
    - Memory Allocator는 반환되어 비어진 블럭의 참조 위치를 저장해 두었다가 새로운 오브젝트 선언시 할당
3. Compacting
    - 참조되지 않는 객체를 제거하고,  남은 참조되어지는 객체들을 묶는다.
    - 객체들을 묶음으로서 공간이 생기므로 새로운 메모리 할당 시에 더 쉽고 빠르게 진행

→ 메모리 파편화 문제

- 빈 메모리 공간들을 합치면 사용 가능한 메모리가 있지만, 그 공간들이 파편화 되어 있기 때문에 사용할 수 없는 문제
- Compacting으로 해결

→ 가비지 컬렉션 수행중에 프로그램의 실행이 잠시 중단되는 문제

위와 같은 문제로, 모든 객체들을 전부 Mark and Sweep 하는 것은 비효율적임

### Generational Garbage Collection

Young Generation 에서 Minor GC 발생

Old Generation에서 Major GC 발생

Young Generation 영역

- 최초에 객체가 생성되면 이 영역의 Eden 영역에 생성됨
- Eden 영역이 가득 차게 되면 Minor GC 일어남
- Mark and Sweep 과정이 일어나고 살아남은 객체들은 Survivor 영역으로 옮겨지고 Age 값 증가
- 하나의 Survivor 영역이 가득 차게 되면 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동
- 이 과정을 반복하다가 계속해서 살아남은 객체는 Old 영역으로 이동

Old Generation 영역

- Old Generation 영역이 가득차게 되면 Major GC 실행
- Minor GC보다 더 많은 시간을 사용하기 때문ㄴ에 자주 발생하게 되면 성능 저하

**Stop-the-world**

- GC를 실행하기 위해 JVM이 어플리케이션 실행을 멈추는 것을 뜻함