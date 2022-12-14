**시스템 메모리를 관리하면서, 자바 기반 애플리케이션을 위해 이식 가능한 실행 환경을 제공한다.**

- 자바 기반 프로그램이 어느 기기나 운영체제 상에서도 실행될 수 있도록 한다.
- 프로그램 메모리를 관리하고 최적화한다.

**코드를 실행하고, 해당 코드에 대해 런타임 환경을 제공하는 프로그램이다.**

### Hot Spot VM

자바를 만든 Sun에서 자바의 성능을 개선하기 위해 JIT 컴파일러를 만들었고, 이름을 HotSpot으로 지음

HotSpot은 자바 1.3 버전부터 기본 VM으로 사용됨

JIT 컴파일러가 어플레케이션에서 각각의 메서드를 컴파일하기에는 바이트코드를 하나씩 인터프리팅 하는 것보다 훨씬 오래걸린다.

따라서, 모든 코드는 초기에 인터프리터에 의해서 시작되고, 해당 코드가 충분히 많이 사용될 경우에 컴파일할 대상이 된다.

인터프리터에 의해서 코드의 수행 카운트가 증가되고, 한계치를 도달했을 경우 컴파일을 요청한다.

주요 컴포넌트

- VM 런타임
- JIT 컴파일러
- 메모리 관리자

### 실행 순서

- 자바 프로그램 실행
- .java 파일이 컴파일러를 통해 .class 파일 (자바 바이트코드) 로 변환
- Class Loader 가 클래스 파일을 런타임에 Runtime Data Areas에 로딩시킴
- 로딩된 클래스 파일들은 Execution engine을 통해 해석됨
- 해석된 바이트 코드는 메모리 영역에 올라가 수행이 이루어짐.

### JVM 구조

![jvm](https://user-images.githubusercontent.com/64204666/194752785-f9612c48-285d-4530-9911-e4fdffc4b044.png)

### 클래스 로더

**자바는 컴파일 타임이 아니라 런타임에 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크하는 특징이 있는데, 이 동적 로드를 담당하는 부분이다.**

### Execution Engine

**Class Loader를 통해 JVM 내의 Runtime Data Areas 에 배치된 바이트코드를 실행**

바이트 코드는 인간이 보기 편하게 기술된 것이므로, JVM 내부에서 기계가 실행할 수 있는 형태로 변경하는데, 두가지 방식이 있음

- Interpreter
    - 바이트코드 명렁어를 하나씩 읽어서 해석하고 실행
    - 바이트코드 하나하나의 해석은 빠르다.
    - 전체적인 메서드의 인터프리팅 결과의 실행은 느리다는 단점
- JIT Compiler
    - 인터프리터의 단점을 보완하기 위해 도입
    - 인터프리터 방식으로 실행하다가 여러번 실행된다고 판단되면, 해당 메서드를 더 이상 인터프리팅 하지 않고 컴파일하여 네이티브 코드로 직접 실행한다.
    - 네이티브 코드를 실행하는 것이 하나씩 인터프리팅해 실행하는 것보다 빠르다.
    - 네이티브 코드는 캐시에 보관하기 때문에 한 번 컴파일된 코드는 계속 빠르게 수행

### Runtime Data Areas

![runtimeDataArea](https://user-images.githubusercontent.com/64204666/194752792-9ea53d36-948f-4d74-ba02-2f22c02d7ce1.png)

- PC (Program Counter) 레지스터
    - 스레드가 어떤 명령어로 실행되어야 할 지 기록하는 부분
    - 각 스레드마다 하나씩 존재
    - 스레드가 시작될 때 생성
    - 현재 수행중인 JVM 명령의 주소를 갖는다.
- JVM 스택
    - Stack Frame 이라는 구조체를 저장하는 스택
    - 각 스레드마다 하나씩 존재하고, 스레드 시작될 때 생성
    - Stack Frame
        
        ![StackFrame](https://user-images.githubusercontent.com/64204666/194752803-b8a0d73b-88a2-42f8-ad68-7ab1d7905200.png)
        
        - 지역 변수 배열, 피연산자 스택, 현재 실행중인 메서드가 속한 클래스의 런타임 상수 풀에 대한 레퍼런스를 갖는다.
        - JVM 내에서 메서드가 수행될 때마다 하나의 스택 프레임이 생성되어 해당 스레드의 JVM 스택에 추가되고, 메서드가 종료되면 스택 프레임이 제거됨
- Native Method Stack
    - 자바 외의 언어로 작성된 네이티브 코드를 위한 스택
- Method Area
    - JVM이 읽은 각각의 클래스와 인터페이스에 대한 런타임 상수 풀, 필드, 정적 변수, 메서드의 바이트 코드 등을 보관
    - JVM이 시작될 때 생성
    - 모든 스레드가 공유하는 영역
- Heap
    - 런타임에 동적으로 할당되는 데이터가 저장되는 영역
    - 객체를 저장하는 공간
    - 가비지 컬렉션 대상
