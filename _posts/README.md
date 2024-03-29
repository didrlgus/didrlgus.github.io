# 면접준비자료

# JAVA

### Q. 자바의 특징은 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>  
        <p>JVM이라는 가상머신에서 동작하고 운영체제에 독립적 입니다.</p>
        <p>GC라는 프로세스가 자동으로 메모리 관리를 수행합니다.</p>
        <p>객체지향 언어입니다.</p>
        <p>멀티쓰레드 지원합니다.</p>
    </div>
</details>

### Q. JVM이 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>자바 가상 머신으로, 자바 컴파일러에 의해 생성된 자바 바이트 코드(.class)를 실행할 수 있는 주체입니다.</p>
        <p>또한, JVM은 OS로부터 메모리를 할당받아 자바 프로그램을 실행시킵니다.</p>
    </div>
</details>

### Q. JVM의 메모리 구조에 대해서 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바 프로그램이 실행되면 JVM은 OS로부터 자바 프로그램 실행에 필요한 메모리(Runtime Data Area)를 할당받고, 할당받은 메모리를 용도에 따라 여러 영역으로 나눕니다.
            그 중, 대표적인 영역으로는 static, Heap, Stack이 있습니다.
        </p>
        <p>
            static 영역에는 멤버 변수의 이름, 데이터 타입, 접근제어자에 대한 field 정보와 메서드의 이름, 리턴 타입, 
            파라미터, 접근 제어자에 대한 정보, 그리고 class 이름과 같이 class 정보들이 저장됩니다. 
            또한 static 으로 선언된 데이터들이 저장됩니다.
            static 영역에 로딩된 데이터들은 프로그램이 끝날때까지 유지되는 자원입니다.
            또한, static 영역에 저장된 데이터들은 모든 스레드에서 공유할 수 있는 자원입니다.
        </p>
        <p>
            Heap 영역은 new 키워드로 생성된 객체와 배열이 생성되는 영역입니다.
            메소드 영역에 로드된 클래스만 생성이 가능하고 Garbage Collector의 대상이 되는 영역입니다.
            Heap 영역에 저장된 데이터들도 모든 스레드에서 공유할 수 있는 자원입니다.
        </p>
        <p>
            Stack 영역은 메서드를 호출할때마다 해당 메서드를 실행하기 위한 스택 프레임이 생성되는 영역입니다.
            스택 프레임 내에 지역 변수, 파라미터, 리턴 값, 참조변수 등이 저장됩니다.
            Stack 영역은 스레드마다 독립적으로 존재하는 영역이기 때문에 스레드간 공유가 불가능합니다.
        </p>
    </div>
</details>

### Q. 자바 프로그램의 동작과정을 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            먼저 JAVA 원시 file (example.java)이 JAVA 컴파일러(javac.exe)에 의해 (example.class) 바이트코드 파일로 변환됩니다.
            그 후 JVM 내에 있는 Class Loader가 runtime data area로 해당 바이트코드 파일을 적재시킵니다.
            그 다음 JVM 내에 있는 Execution engine이 runtime data area에 적재된 바이트 코드들을 기계어로 변경해 명령어 단위로 실행합니다.
        </p>
    </div>
</details>

### Q. GC가 무엇인지 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            GC란 JVM의 Heap 영역에서 사용하지 않는 객체를 삭제하는 프로세스 입니다.
            GC의 수거 대상은 heap 영역에 있는 unreachable 즉, 참조를 갖고있지 않은 객체입니다.
            또한 GC는 내부적으로 Mark and Sweep 알고리즘을 사용하여 객체를 삭제하는데, 
            Mark는 GC의 root로부터 모든 변수를 스캔하면서 각각 어떤 객체를 참조하고 있는지 찾아서 마킹하는 과정입니다.
            즉, reachable과 unreachable을 판단하는 과정을 의미합니다. 여기서 GC root가 될 수 있는 조건은 stack 영역의 지역변수나 파라미터들, static 영역의 static 변수들입니다.
            그리고 sweep는 unreachable한 객체들을 heap에서 제거하는 과정입니다. 
            sweep과정이 끝나면 compact 과정이 추가될 수 있는데 compact 과정은 heap에서 제거된 객체가 있던 메모리 공간으로 인해 생길 수 있는 
            메모리 단편화 문제를 막아주는 작업입니다.
            또한 gc 작업을 수행하는 쓰레드를 제외한 모든 쓰레드가 작업을 중지하는 현상을 stop the world라고 부릅니다.
        </p>
    </div>
</details>

### Q. GC의 동작방식에 대해 좀 더 자세히 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            GC의 세부 동작방식을 말씀드리기에 앞서 heap의 구조를 먼저 말씀드리면, heap은 크게 young gen과 old gen으로 나뉩니다. young gen은 새로운 생성된 객체들이 할당되는 영역이고 old gen은 young gen에서 오래 살아남은 객체들이 존재하는 영역입니다.
            그리고 young gen은 다시 eden과 두개의 survivor 영역으로 나뉩니다. 앞으로 이 두개의 survivor 영역을 각각 survivor-1,survivor-2라고 가정하겠습니다.
            GC의 동작과정에 대해서 말씀드리면 먼저 새로운 객체들이 eden 영역에 추가됩니다. 그리고 eden 영역이 가득차면 young gen을 대상으로 mark and sweep 작업이 수행되는데 이를 'minor gc'라고 부릅니다.
            'minor gc' 작업을 통해 reachable 한 객체는 살아남고 unreachable한 객체는 제거됩니다. 그리고 'minor gc' 작업을 통해 살아남은 reachable한 객체는 survivor1 또는 survivor2 영역중 한곳으로 이동합니다.
            이때, 객체가 survivor1과 survivor2에 공존하지 않고 어느 한 영역에만 존재합니다.
            그리고 survivor에 이동된 살아남은 객체는 age가 하나씩 추가됩니다. 위의 과정이 반복되면서 하나의 Survivor 영역이 가득 차게 되면 'minor gc'가 수행되고 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동시킵니다. 
            그리고 이전 Survivor 영역은 아무 객체도 없는 상태로 비워둡니다.
            위의 과정을 반복하다 survivor에 있는 객체의 age가 특정 임계점에 다다르면 해당 객체는 old gen으로 이동되는데 이 과정을 promotion이라고 합니다.
            위의 모든 과정을 반복하면서 old gen이 가득차게 되면 old 영역에서 gc 작업을 수행하는데 이를 'major gc' 라고 합니다.
        </p>
    </div>
</details>

### Q. GC의 종류와 각각의 특징에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Serial GC는 가장 단순한 방식의 GC로 싱글 스레드로 GC를 동작시킵니다.
            싱글 스레드로 동작하여 느리고, 그만큼 STW 시간이 다른 GC에 비해 깁니다.
            Mark & Sweep & Compact 알고리즘을 사용합니다.
            보통 실무에서 사용하는 경우는 없습니다.
            Parallel GC는 GC 작업을 여러 스레드로 병렬처리하여, STW 시간을 최소화 시키기 위한 GC 입니다.
            young gen에 대한 minor GC를  병렬처리 합니다.
            Parallel Old GC라는 것도 있는데, 해당 GC는 old gen에서 수행되는 major GC도 병렬처리 합니다.
            Parallel GC는 자바 8의 디폴트 GC 입니다.
            CMS GC(Concurrent Mark Sweep GC)는 STW로 인해 Java Application이 멈추는 현상을 줄이고자 만든 GC입니다.
            reachable한 객체를 한번에 찾지 않고 4단계로 나눠서 찾는 방식을 사용합니다.
            Initial Mark는 GC Root가 참조하는 객체만 마킹합니다. 이 과정에서 stop-the-world 발생합니다.
            Concurrent Mark는 참조하는 객체를 따라가며, 지속적으로 마킹합니다. stop-the-world 없이 이루어집니다.
            Remark는 concurrent mark 과정에서 변경된 사항이 없는지 다시 한번 마킹하며 확정하는 과정입니다. stop-the-world가 발생합니다.
            Concurrent Sweep는 unrechable한 객체를 제거하는 과정입니다. stop-the-world 없이 이루어집니다.
            CMS GC는 가비지 수거 후 compaction을 수행하지 않습니다.
            G1GC는 Garbage first Garbage Collector 입니다.
            Eden, Survivor, Old 영역을 고정된 크기로 고정된 위치에 나누는 것이 아니라, 전체 힙 메모리 영역을 리전이라는 일정한 크기로 나눠서 각 리전의 상태에 따라 그 리전의 역할이 동적으로 부여되는 방식으로 동작합니다.
            전체 힙에 대해서 탐색하지 않고 부분적으로 리젼 단위로 탐색하며, 각각의 리젼에만 GC가 발생해 빠르게 GC를 수행할 수 있습니다.
            자바 9부터 디폴트 GC 입니다.
        </p>
    </div>
</details>

### Q. minor-gc 에서 발생하는 stw 와 major-gc, full-gc 에서 발생하는 stw 의 속도는 어떤 차이가 있을까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            stw의 속도는 minor-gc가 가장 빠르고 그다음 major-gc 그다음 full-gc가 가장 느릴 것이라고 생각합니다.
            일반적으로 major-gc의 대상인 old gen은 young gen보다  용량을 크게 잡고, 그렇기 때문에mark and sweep 작업을 할 객체의 수도 많아, major-gc에서의 gc 처리속도가 minor-gc에서의 gc 처리 속도보다 상대적으로 느릴 것입니다.
            stw는 결국 gc과정이 시작되고 종료될 때까지 모든 쓰레드를 정지하는 과정이므로, stw 속도도 이와 비례할 것이라고 생각합니다.
            full-gc는 minor-gc + major-gc인데, 마찬가지로 heap 내의 모든 객체를 대상으로 mark and sweep 작업을 수행해야 하기 때문에, gc를 하는데 시간이 오래걸릴 것이고, minor-gc나 major-gc 보다 stw의 속도가 느릴 것이라고 생각합니다.
        </p>
    </div>
</details>

### Q. 객체지향이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            실세계에 존재하는 사물을 추상화시켜 상태와 행위를 가진 객체로 만들고, 그 객체들이 서로 상호작용하며 동작하도록 프로그래밍하는 프로그래밍 기법 입니다. 
            객체지향은 프로그래머들이 프로그램을 더 쉽고 효율적으로 하기 위해 존재합니다.
            좋은 객체지향 설계를 기반으로 만들어진 애플리케이션은 그 규모가 커지더라도, 효율적인 유지보수를 가능하게 해주기 때문입니다.
        </p>
    </div>
</details>

### Q. 객체지향의 주요 특징에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            첫번째로, 클래스, 인스턴스라는 개념이 있습니다. 클래스는 객체를 생성하기 위한 설계도로 속성과 행위를 변수와 메소드로 정의한 것입니다.
            인스턴스는 클래스에서 정의한 것을 바탕으로 실제 메모리상에 할당된 데이터입니다.
            두번째로, 캡슐화라는 개념이 의있습니다. 캡슐화는 외부에서 접근할 필요가 없는 멤버들을 private으로 지정하여 외부에 노출시키지 않는 것을 말합니다.
            세번째로, 상속이라는 개념이 있습니다. 상속은 특정 클래스의 변수와 메소드를 그대로 이어받아 기능을 확장시키는 것을 의미합니다.
            다음으로 추상화라는 개념이 있습니다. 추상화는 서로 연관있는 클래스간의 공통점을 찾아내서 공통의 조상을 만드는 작업을 말합니다.
            다음으로 다형성이라는 개념이 있습니다. 다형성은 여러 객체에게 동일한 명령을 내렸을 때 서로 다르게 반응하는 현상을 의미합니다.
            예를들어, 핸드폰이라는 상위 클래스로 부터 확장된 iphone과 galaxy는 서로 동일한 행위라도 각각 다르게 동작할 수 있습니다.
            이를 다형성이라고 합니다.  
            또한, 자바에서의 다형성은 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 하는 것을 의미하기도 합니다. 
            객체지향의 여러가지 특징을 잘 활용하면 유연하고 확장성있는 코드를 작성할수 있어, 유지보수 비용을 최소화 시킬 수 있습니다.
        </p>
    </div>
</details>

### Q. 좋은 객체지향의 설계 5가지인 SOLID에 대해 설명하세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            먼저 S에 해당하는 SRP, single responsibility principle은 한 클래스는 하나의 책임만 가져야 한다는 원칙입니다.
            여기서 중요한 기준은 변경 입니다. 변경이 있을 때 파급 효과가 적으면 SRP를 잘 따른 것이라고 볼 수 있습니다.
        </p>
        <p>
            다음으로 O는 OCP, Open Closed Priciple, 개방-폐쇄 원칙을 의미합니다. 소프트웨어 요소는 확장이나 변경에는 열려 있으나 변경에는 닫혀 있어야 한다는 원칙입니다.
            즉, 내가 어떤 코드를 추가 했을 때, 기존 코드에 대한 변경이 없다면 OCP를 잘 따른 것이라고 볼 수 있습니다.
        </p>
        <p>
            다음으로, L은 Liskov Substitution Priciple, 리스코프 치환 원칙입니다. 
            이는 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것을 의미합니다.
            단순히 컴파일 성공하는 것을 넘어서는 이야기입니다. 예를들어, 자동차 인터페이스가 있고 엑셀이라는 기능이 선언되어있다고 할때, 
            자동차 인터페이스의 구현체는 엑셀 기능을 앞으로 가는 기능으로 만들어야지 뒤로 가는 기능으로 만들면 안됩니다.
        </p>
        <p>
            다음으로, I는 Interface Segregation Principle, 인터페이스 분리 원칙입니다.
            인터페이스 여러 개가 범용 인터페이스 하나보다 낫다는 원칙입니다.
            인터페이스를 분리하면 인터페이스가 명확해지고, 대체 가능성이 높아지기 때문입니다.
         <p>
            마지막으로 D는 Dependency Inversion Principle, 의존관계 역전의 원칙입니다.
            프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다는 원칙입니다.
            즉, 클라이언트가 인터페이스에 의존해야지 유연하게 구현체를 변경할 수 있습니다. 구현체에 의존하게 되면 유연성이 떨어집니다. 
        </p>
    </div>
</details>

### Q. 응집도와 결합도는 무엇을 말하는 것일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            응집도는 모듈에 포함된 내부 요소들이 연관돼 있는 정도를 나타냅니다.
            모듈 내의 요소들이 하나의 목적을 위해 긴밀하게 협력한다면 해당 모듈은 높은 응집도를 가지는 것이고, 모듈 내의 요소들이 서로 다른 목적을 추구한다면 그 모듈은 낮은 응집도를 갖습니다. 일반적으로 응집도를 높이는 것이 좋은 설계입니다.
            결합도는 다른 모듈과의 의존성 정도 입니다. 다른 모듈에 대해 얼마나 알고 있는지를 나타내는 척도입니다.
            어떤 모듈이 다른 모듈에 대해 너무 자세한 부분까지 알고 있다면 두 모듈은 높은 결합도를 가진 것입니다.
            어떤 모듈이 다른 모듈에 대해 꼭 필요한 지식만 알고 있다면 두 모듈은 낮은 결합도를 가진 것입니다.
            일반적으로 결합도를 낮추는 것이 좋은 설계입니다.
            응집도와 결합도는 캡슐화와도 관계가 있습니다.
            캡슐화의 정도가 객체의 응집도와 결합도를 결정하기 때문입니다.
            캡슐화를 잘 지키면 응집도는 높이고 모듈 사이의 결합도는 낮출 수 있습니다.
            그렇기 때문에 좋은 설계를 위해서 캡슐화를 향상시키기 위해 노력하는 것이 중요합니다.
        </p>
    </div>
</details>

### Q. 추상클래스와 인터페이스의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바 8에서 default 키워드가 추가되어 interface에서도 메서드의 내용을 구현할 수 있게 되면서, interface와 abstract class 간의 차이가 없어진 것으로 보일 수 있습니다.
            하지만, 사실 class의 근본적인 정의의 관점에서 볼 때, interface와 abstract class 간에는 중요한 차이점이 존재합니다.
            먼저, interface는 상태(속성)를 갖지 않습니다.
            또한, interface는 모든 멤버의 접근 제어자가 public 입니다.
            interface의 모든 멤버의 접근 제어자가 public인 이유는 interface를 구현한 구현체에서 정의된 메서드는 클라이언트에게 public으로 노출돼야 하기 때문입니다.
            결론적으로 인터페이스는 클라이언트가 해당 메서드를 어떻게 사용할지에 대한 계약을 제공합니다.
            반면에, abstract class는 기본적으로 class로써 상태(속성)와 행위를 갖습니다.
            그리고, abstract class는 interface와 다르게 해당 멤버들의 접근 제어자가 public일 필요는 없습니다.
            결론적으로, abstract class는 해당 class를 확장할 class에게 기본적인 context를 제공합니다.
            context는 추상화 시켜놓은 상태와 행위들을 모아놓은 템플릿이라고 볼 수 있습니다.
            그렇다면 interface는 언제 사용하고, abstract class는 언제 사용하는 것이 좋을까요?
            이는, 둘의 사용목적의 관점에서 바라볼 필요가 있습니다.
            인터페이스는 클라이언트에게 구현체의 메서드를 어떻게 사용할지에 대한 계약을 제공하는 것이 목적입니다.
            그에 반해, abstract class는 상위 클래스에서 공통된 기능은 그대로 물려받거나 혹은 별도로 구현하고, 새로운 속성과 행위를 확장하기 위함이 목적입니다.
            abstract class도 결국 상속을 이용해야하고, 꼭 필요한 경우를 제외하고는 상속은 피하는 것이 좋은 설계라고 생각합니다.
            상속은 특성상 서브 클래스가 슈퍼클래스의 상태와 행위를 공유하기 때문에 서브 클래스는 슈퍼클래스에 의존하는 관계가 되고, 이로인해, 둘간의 결합도가 높아져 코드의 유연성을 떨어뜨릴 수 있다는 단점이 있기 때문입니다.
            그에반해, 인터페이스는 어떠한 상태도 가지지 않으며, 행위에 대한 조건(parameter)과 결과(return) 타입만 강제할뿐 내용에 대한 구현은 하위 클래스에게 맡기기 때문에, 의존관계가 생기지 않고, 결합도가 느슨해 코드의 유연성을 높일 수 있다는 장점이 있습니다.
            결론적으로, 정말 꼭 상속이 필요한 IS-A 관계를 제외한 나머지 상황에서는 interface를 사용하는 것이 좋은 설계라고 생각합니다.
        </p>
    </div>
</details>

### Q. 메서드 오버로딩과 메서드 오버라이딩의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            한 클래스 내에 같은 이름의 메서드를 여러개 정의하는 것을 메서드 오버로딩이라고 합니다.
            오버로딩은 기존 메서드와 매개변수의 개수 또는 타입이 달라야 한다는 조건이 있습니다.
            오버로딩은 새로운 메서드를 정의하는 것입니다.
            메서드 오버라이딩은 부모 클래스로부터 상속받은 메서드의 내용을 자식 클래스에서 변경하는 것을 의미합니다.
            오버라이딩은 부모 클래스의 메서드와 매개변수와 리턴타입이 같아야 한다는 조건이 있습니다.
            오버라이딩은 기존에 있었던 메서드를 재정의하는 것입니다.
        </p>
    </div>
</details>

### Q. 업캐스팅과 다운캐스팅에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            업캐스팅은 서브 클래스의 객체가 슈퍼 클래스 타입으로 형변환 되는 것을 말합니다.
            슈퍼 클래스 타입의 참조변수로 서브 클래스의 인스턴스를 참조하면 묵시적으로 업캐스팅이 일어납니다.
            이때, 서브클래스의 멤버에는 접근이 불가합니다.
            다운캐스팅은 업캐스팅되어 자신의 고유한 특성을 잃은 서브클래스 타입의 객체를 다시 복구시켜주는 것을 말한다.
            업캐스팅이 선행된 상태에서 명시적으로 서브클래스 타입으로 형변환 시키면 다운캐스팅이 일어납니다.
        </p>
    </div>
</details>

### Q. 동적 바인딩이 뭔가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            다형성을 사용하여 메소드를 호출할 때 발생하는 현상 입니다.
            서브클래스가 슈퍼클래스의 메서드를 오버라이딩 하여 서브클래스와 슈퍼클래스 모두에 특정 메서드가 존재한다면 
            서브 클래스의 메서드가 호출되는 현상입니다.    
        </p>
    </div>
</details>

### Q. 자바의 예외처리에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바에서는 실행 시 발생할 수 있는 프로그램 오류를 에러(Error)와 예외(Exception) 두 가지로 구분합니다.
            에러는 프로그래머가 애플리케이션 내에서 처리할 수 없는 심각한 오류를 말하고, 
            예외는 프로그래머가 처리할 수 있는 오류를 말하며, 주로 프로그래머의 실수로 인해 발생하는 오류입니다.
            대표적으로 OutOfMemoryError, stackOverFlow 에러가 있습니다.
            그리고 예외는 내부적으로 CheckedException과 UncheckedException 으로 나뉘는데,
            CheckedException은 프로그래머가 별도의 예외처리를 하지 않으면 컴파일 단계에서 오류를 발생시키는 예외이고,
            대표적으로 SQLException, IOException 등이 있습니다.
            그리고 UncheckedException은 프로그래머가 별도의 예외처리를 하지 않아도 컴파일 단계에서 오류를 발생시키지 않는 예외입니다.
            대표적으로 NullPointerException이 있습니다.
            예외는 throws new 를 통해 발생 시킬 수 있으며, 예외를 처리하기 위해서는 try, catch 문이나 throw 키워드를 이용해 처리할 수 있습니다.
        </p>
    </div>
</details>

### Q. 트랜잭션 내에서 발생한 checked exception은 왜 롤백을 안할까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            기본적으로 Checked Exception는 복구가 가능하다는 메커니즘을 가지고 있습니다.
            예를들어, CDN 서버에서 프로필 이미지를 가져와야 하는 로직이 있다고 가정하겠습니다.
            그런데, CDN 서버의 통신 장애로 인해 프로필 이미지를 가져오지 못해 I/O Exception이 발생한다면, 이를 사용자에게 전달하는 것이 아니라 예외를 잡아 default image를 사용자에게 전달하는 방식으로 예외를 복구할 수 있습니다.
            즉, 이렇게 개발자가 이미 복구 작업을 진행했을 수 있으니까, 따로 rollback은 진행하지 않는다고 생각할 수 있습니다.
        </p>
    </div>
</details>

### Q. 자바의 final은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            final은 클래스나 멤버에 적용할 수 있는 keyword이고 어디에 적용하느냐에 따라 의미가 달라집니다.
            먼저, 클래스에 적용 시 해당 클래스를 상속받을 수 없습니다. 그리고 Primitive type의 변수에 적용 시 해당 변수의 값을 변경할 수 없습니다.
            그리고 Reference type의 변수에 적용 시 해당 referenct 변수가 힙(heap) 내의 다른 객체를 참조할 수 없습니다.
            그리고 메서드에 적용 시 해당 메서드를 오버라이딩 할 수 없습니다.
        </p>
    </div>
</details>

### Q. == 과 equals()의 차이는 뭘까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            동일성과 동등성에 대한 부분입니다.
            ==은 비교대상이 primitive type이면 값 비교, reference type 주소를 비교하여 boolean 값을 리턴합니다.
            즉, ==는 동일성 비교입니다.
            equals()는 Object 클래스에 정의된 메서드 이며 하위 클래스에서 오버라이딩을 통해 값비교가 가능합니다.
            대표적인 예로 String 클래스가 있습니다.
        </p>
    </div>
</details>

### Q. equals()와 hashCode()가 뭘까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            equals()와 hashCode() 모두 Object 클래스에 정의된 메서드입니다.
            일반적으로 equals()는 객체의 내용이 동일한지 확인하는 동등성 비교를 위한 메서드입니다.
            hashCode()는 해싱(hashing) 기법에 사용되는 해시함수(hash function)를 구현한 것이고, 기본적으로 메모리 주소에 대한 해시값을 반환합니다.
            만약, equals()를 재정의 한다면, hashCode() 또한 재정의 해야 합니다.
            그렇지 않으면, hashcode() 값을 사용하는 Collection인 HashSet, HashMap, HashTable을 사용할 때 문제가 발생할 수 있습니다.
            HashSet에서는 객체간의 중복여부를 파악할 때 hashCode()를 사용하고, HashMap과 HashTable에서는 key에 대한 해시값을 구할때 hashCode()를 사용하기 때문입니다.
            즉, hashCode()로 인한 문제를 일으키지 않기 위해서는 재정의 한 equals()의 반환 값이 true 라면, 두 객체의 hashCode()도 마찬가지로 동일한 값을 반환시킬 수 있게 재정의 해야 합니다.
            이와 반대로, equals()의 반환 값이 false 라고 하더라도, 두 객체의 hashcode()가 동일할 필요는 없습니다.
            다만, equals() 값이 false인 객체들에 대해서는 서로 다른 hashCode() 값을 반환해야 해시테이블의 충돌을 최소화 시킬 수 있고 성능을 높일 수 있습니다.
        </p>
    </div>
</details>

### Q. "" 와 new String("")에 대해서 설명하세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            "" 방식은 Heap 내의 별도 공간인 String Constant Pool에 문자열 생성하고 같은 문자열은 한번만 생성 됩니다.
            constant pool에 생성되는 String 객체는 변경 불가능한 immutable한 객체 입니다.
            new 연산자 방식은 일반 클래스와 마찬가지로 Heap에 문자열을 생성합니다.
        </p>
    </div>
</details>

### Q. String에는 얼마나 많은 문자를 넣을 수 있을까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Java의 String 객체는 char 형의 배열로 나타내며, heap memory 상에 저장됩니다.
            즉, String 객체의 길이는 heap memory의 크기에 따라 결정되며, JVM 내에 할당된 힙 memory 크기를 넘을 수 없습니다.
        </p>
    </div>
</details>

### Q. String, StringBuffer, StringBuilder의 차이점에 대해서 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            String 객체는 immutable하기 때문에 지정된 문자열을 변경할 수 없지만 StringBuffer, StringBuilder 클래스는 인스턴스는 변경이 가능합니다.
            또한, StringBuffer, StringBuilder는 문자열을 변경할 수 있기 때문에 많은 문자열 연산을 요구하는 프로그램일 경우 String 클래스보다 
            메모리 공간을 훨씬 더 효율적으로 사용할 수 있습니다.
            다만, StringBuffer 클래스는 String 클래스와 다르게 equals 메서드를 오버라이딩 하지 않는다.
            그리고 StringBuilder는 StringBuffer에서 쓰레드의 동기화 기능만 뺀 클래스입니다.
            즉, 멀티쓰레드가 아닌 환경에서는 StringBuilder가 StringBuffer보다 더 유리합니다.
        </p>
    </div>
</details>

### Q. mutable 객체와 immutable 객체에 대해서 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            mutable 객체는 생성된 후에도 속성값을 변경할 수 있는 객체입니다.
            mutable의 장점은 메모리 낭비를 최소화 시킬 수 있다는 것입니다.
            단점은 multithread 환경에서 thread safe를 보장할 수 없으며,
            변하지 말아야 하는 객체라면 추후에 변할 수도 있다는 우려가 있을 수 있습니다.
            immutable 객체는 객체가 생성된 후에 속성값을 변경할 수 없는 객체입니다.
            대표적으로 String과 wrapper 클래스가 있습니다.
            immutable은 multithread 환경에서 thread safe를 보장, 불변이기 때문에 객체가 안전하다는 장점이 있는 반면
            메모리 낭비를 유발할 수 있다는 단점이 있습니다.
        </p>
    </div>
</details>

### Q. 컬렉션 프레임워크가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 인터페이스와 클래스의 집합을 의미합니다.
        </p>
    </div>
</details>

### Q. Array, ArrayList, LinkedList의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Array는 정적배열이어서 선언 시 크기를 미리 지정합니다. 그에반해 ArrayList, LinkedList는 동적배열 이기 때문에 선언 시 크기를 따로 지정하지 않습니다.
            Array와 ArrayList는 연속된 메모리공간에 값을 할당하지만, LinkedList는 연속된 공간이 아닌 이전 노드가 다음 노드를 참조하는 식으로 데이터를 저장합니다.
            Array와 ArrayList는 데이터 무작위 조회에 유리하지만 중간 데이터를 삭제하거나 중간에 데이터를 추가하는 연산에서는 단점을 가지는 반면
            LinkedList는 중간에 데이터를 추가, 삭제하는 연산에 유리합니다. 다만, LinkedList는 데이터 무작위 조회에서 단점을 가집니다.           
        </p>
    </div>
</details>

### Q. HashMap, HashTable, ConcurrentHashMap의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            모두 Map 인터페이스를 구현한 구현체들이며 key, value구조를 가지는 자료구조 입니다. 또한 키에 대한 해시 값을 사용하여 값을 저장하고 조회합니다.
            먼저 hashMap은 주요 메소드에 synchronized 키워드가 없습니다. 그래서 hashtable 보다 hashMap 이 훨씬 빠르지만
            multi thread 환경에서 thread-safe를 보장하지 않습니다.
            또한 hashtable 이나 concurrentHashMap과 다르게 key, value에 null을 허용합니다.
            hashtable은 hashmap과 동일하지만, 주요 메소드에 synchronized 키워드가 선언 되어 있다는 것이 차이점입니다.
            즉, synchronized가 붙은 메서드에는 하나의 스레드 접근만 thread-safe가 가능하지만, hashmap 보다 성능이 떨어집니다.
            concurrentHashMap은 주요 메서드에 synchronized 키워드가 선언되어 있진 않지만, thread-safe를 보장하는 자료구조입니다.
            concurrentHashMap은 서로 다른 스레드가 같은 해시 버킷에 접근할 때만 해당 블록이 잠기게 하여 스레드 경합을 최소화 하기 때문에
            hashtable보다 성능이 뛰어납니다.
            그렇기 때문에 thread-safe를 보장하지 않는 환경이라면 hashmap을 thread-safe를 보장해야 하는 환경이라면 concurrentHashmap을 사용하는 것이 적합합니다.
        </p>
    </div>
</details>

### Q. HashMap, TreeMap, LinkedHashMap의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            HashMap은 내부적으로 Hashing을 사용해 데이터를 저장하고 TreeMap은 내부적으로 Red-Black 트리를 사용해 데이터를 저장합니다.
            그렇기 때문에 hashmap은 O(1)의 데이터 조회가 가능한데 반해 treemap은 O(logN)의 데이터 조회가 가능합니다.
            또한, TreeMap은 HashMap과 다르게 데이터 저장 시 데이터의 순서를 보장합니다.
            그리고 LinkedHashMap도 마찬가지로 HashMap과 다르게 데이터 저장 시 데이터의 순서를 보장합니다.
        </p>
    </div>
</details>

### Q. Java 에서 제공하는 java.util.Stack 클래스는 디자인이 잘못되어, 보통의 엔터프라이즈 환경에서는 잘 사용하지 않는데요. 왜 그럴까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Stack class를 직접 까보면 가장 눈에 띄는 특징 2가지가 있습니다.
            첫번째로, Vector라는 클래스를 상속받는다는 것입니다.
            Vector는 ArrayList처럼 동적 배열 객체를 만들 때 사용되는 클래스 입니다.
            근데, Stack은 Vector를 상속받으면서, LIFO 가 아닌 중간에 데이터를 삽입, 삭제하는 연산도 가능해집니다.
            이는 Stack의 본질을 깨버리는 설계가 되기 때문에 올바른 설계라고 볼 수 없습니다.
            두번째로, Stack의 일부 메서드에서는 synchronized 키워드를 이용해 thread-safe를 보장 받습니다.
            synchronized를 이용하면 완벽한 thread-safe를 보장받을 수 있지만, 성능적으로는 오버헤드가 큰 방식입니다.
            그렇기 때문에, 엔터프라이즈 환경에서는 좋은 성능을 보장하지 못할 확률이 크고 이로인해, Stack은 좋은 선택이 아닐 가능성이 높습니다.
            그렇다면, Java에서 LIFO 구조의 자료구조로는 어떤 것을 사용해야 할까요?
            Stack 자체의 Java API 문서에서도 더 완벽한 LIFO 자료구조를 사용하려거든 Deque 인터페이스를 구현한 구현체인 ArrayDeque를 사용하라고 추천하고 있습니다.
            ArrayDeque를 이용하면 thread-safe는 보장받을 수 없지만, Stack 보다 빠른 성능을 보장받을 수 있기 때문입니다.
            만약, thread-safe를 꼭 보장받아야만 하는 상황이라면, synchronized를 이용하는 Stack보다는 ConcurrentLinkedDeque과 같은 lock-free한 자료구조를 사용하여 thread-safe를
            보장받는 것이 성능상 유리할 것입니다.
        </p>
    </div>
</details>

### Q. Inner class와 Nested class가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바에서는 class 안에 class를 선언할 수 있습니다.
            이렇게, class 안에 선언된 class를 Nested class라고 부릅니다.
            Nested class는 특정 class가 한 곳에서만 사용될 경우, 논리적으로 군집화하기 위해 사용합니다.
            이로 인해, 불필요한 외부 노출을 줄이면서 캡슐화를 할 수 있고, 가독성을 높이며 유지 보수하기 좋은 코드를 작성할 수 있습니다.
            Nested class는 선언 방식에 따라 Static nested class, Inner class로 나뉘고, 또 Inner class는 Local Inner class와 Anonymous class로 나뉩니다.
            Static nested class와 Inner class의 차이는 static으로 선언되었는지의 여부입니다.
            먼저, Static nested class는 해당 class를 감싸고 있는 Outer class의 static으로 선언된 멤버를 제외한, 어떠한 멤버에도 접근할 수 없습니다.
            그에 반해, Inner class는 Outer class의 모든 멤버에 접근이 가능합니다.
            그리고 Static nested class의 객체는 Outer class 객체와 관계없이 독립적으로 객체를 생성할 수 있습니다.
            그에 반해, Inner class는 Outer class의 객체를 생성한 뒤 해당 객체를 이용해서 객체를 생성할 수 있습니다.
            Inner class의 경우 기본적으로 Outer class에 대한 참조를 갖고 있습니다.
            그렇기 때문에, Outer class는 더 이상 사용되지 않더라도, Inner class의 참조로 인해 GC의 대상이 되지 않아 Outer class의 메모리 헤제를 하지 못하는 메모리 누수의 가능성이 있습니다.
            결론적으로, Nested class가 필요한 상황에서 Outer class에 대한 멤버를 참조하지 않는 상황이라면, 무조건 Static nested class로 선언해주는 것이 좋습니다.
        </p>
    </div>
</details>

### Q. 익명 클래스가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Anonymous class는 Inner class의 일종입니다.
            다만, Anonymous class는 특이하게도 다른 Inner class와 달리 이름이 없습니다.
            class의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고, 오직 하나의 객체만을 생성할 수 있는 일회용 class입니다.
            이름이 없기 때문에, 생성자를 가질 수 없으며 오로지 단 하나의 class를 상속 받거나 단 하나의 interface만을 구현할 수 있습니다.
        </p>
    </div>
</details>

### Q. 제네릭에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            제네릭은 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에서 컴파일 시 타입체크를 해주는 기능 입니다.
            제네릭을 사용하면 컴파일 시점에서 타입 안정성을 보장받을 수 있으며, 불필요한 형변환 코드를 줄여주기 때문에 유용하게 사용됩니다.
        </p>
    </div>
</details>

### Q. 람다식이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            람다식은 간단히 말해서 메서드를 하나의 식 으로 표현한 것입니다.
            람다는 변수에 할당할 수 있는 로직입니다.
            즉, 람다식은 일급객체의 역할을 수행할 수 있어 메소드의 매개변수로 전달될 수도 있으며, 변수에 담거나, 메소드의 결과값으로 반환될 수도 있습니다.
            이를 통해, 자바에서도 함수형 프로그래밍이 가능합니다.
            기존의 불필요한 코드를 줄여주고, 작성된 코드의 가독성을 높여주기 위해 사용됩니다.
        </p>
    </div>
</details>

### Q. 함수형 프로그래밍이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            함수를 값으로 바라보고 명령형이 아닌 선언형으로 프로그래밍 하는 프로그래밍 방식을 말합니다.
            자바에서는 스트림 API와 람다를 이용하여 함수형 프로그래밍을 할 수 있습니다.
        </p>
    </div>
</details>

### Q. 스트림 API가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스트림 API는 컬렉션, 배열 등에 저장된 요소들에 쉽게 접근할 수 있도록 추상화된 기술을 제공합니다.
            stream은 시작, 중간, 최종 연산으로 이루어져 있으며 Immutable 하다는 특징이 있습니다. 
            즉, 원본의 데이터를 변경하지 않으며 또한, stream은 추후에 재사용할 수 없습니다.
            스트림 API 사용하면 for, if와 같은 불필요한 코딩을 걷어낼 수 있고 직관적이기 때문에 가독성이 좋아지고 실수의 여지를 줄여준다는 장점이 있습니다.
            또한 parallel stream을 이용하면 병렬처리가 가능해 빠른 처리가 가능하다는 장점이 있습니다.
        </p>
    </div>
</details>

### Q. 스트림 API의 연산중에서 map이랑 flatmap의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            map은 단일 스트림 안의 요소를 원하는 특정 형태로 변환시켜주는 중간 연산 메서드입니다.
            flatMap은 스트림의 형태가 배열이나 리스트 일때 각 리스트의 모든 원소를 단일 원소 스트림으로 반환시켜주는 중간 연산 메서드 입니다.
        </p>
    </div>
</details>

### Q. 접근제어자에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            접근 제어자란 클래스나 클래스의 멤버 선언 시 사용하여 부가적인 의미를 부여하는 키워드를 의미합니다.
            자바에서는 객체지향의 정보 은닉을 위해 접근 제어자라는 기능을 제공하며, public, protected, default, private 이 있습니다.
            public으로 선언된 클래스 멤버는 외부로 공개되며, 해당 객체를 사용하는 프로그램 어디에서나 해당 멤버에 직접 접근할 수 있습니다.
            protected로 선언된 클래스 멤버는 같은 패키지 혹은 다른패키지에서 해당 클래스를 상속한 클래스에서 접근이 가능합니다.
            접근 제어자가 따로 지정되지 않으면 자동적으로 default 접근 제어를 갖게 되는데, 
            default 접근 제어를 갖는 클래스 멤버는 같은 클래스의 멤버와 같은 패키지에 속하는 멤버에서만 접근할 수 있습니다.
            private으로 선언된 클래스 멤버는 같은 클래스 내에서만 접근이 가능하고 외부에서는 접근이 불가합니다.
        </p>
    </div>
</details>

### Q. 직렬화에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            직렬화는 Object를 연속된 문자열 데이터나 연속된 byte데이터로 바꾸는 과정을 말합니다.
            직렬화가 필요한 이유는 메모리상에 저장되는 Object는 네트워크 상에 두 컴포넌트가 통신을 할때 통신선을 통해 
            직접적으로 전송이 불가해서 통신선을 통해 전송이 가능한 JSON,XML,YAML,Byte 파일 등으로 바꾸어서 전송해야하기 때문입니다.
            이와 반대로, 직렬화된 데이터를 Object 형태로 변환시키는 작업을 역직렬화라고 합니다.
        </p>
    </div>
</details>

### Q. 자바 스트림을 사용하면서 실제 기본 for 문을 사용했을 때보다 어떤 장점이 있는지 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            데이터를 가공하거나 원하는 데이터를 필터링하는데 용이합니다.
            데이터를 그루핑하여 집계하기가 용이합니다.
            병렬처리가 가능합니다.
        </p>
    </div>
</details>

### Q. 리플렉션에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            리플렉션은 컴파일되어 JVM static 영역에 로딩돼있는 클래스의 메타데이터를 이용해 
            런타임 시점에 해당 클래스의 인스턴스를 생성하고 멤버에 접근할 수 있도록 해주는 자바 API입니다.            
            리플렉션은 애플리케이션 개발에서보다는 프레임워크나 라이브러리에서 많이 사용되는데, 대표적으로 스프링에서 bean을 
            등록하고 의존관계를 주입할때 리플렉션을 사용합니다.
            다만, 런타임 시점에서 객체를 생성하여 해당 멤버에 접근해 조작하는 방식이기 때문에 컴파일 상에서는 잡히지 않았던 
            버그가 런타임 시점에 생길 수 있습니다.
        </p>
    </div>
</details>

### Q. java8을 써보셨나요? java7에서 8로 올라오면서 어떤게 달라졌나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            람다가 생겨 자바에서도 함수형 프로그래밍이 가능해졌습니다.
            그리고 스트림 API가 새로 생겨 컬렉션, 배열 등에 저장된 요소들에 쉽게 접근할 수 있도록 추상화된 기술을 제공합니다.
            그리고 LocalDate, LocalDateTime 클래스가 새로 생겼습니다.
            LocalDate와 LocalDateTime은 이전에 날짜와 시간을 다뤘었던 Date 클래스와 Calendar 클래스 보다 직관적으로 
            코드를 작성할 수 있고 이전보다 더 많은 시간 관련 기능들을 제공합니다.
            그리고 인터페이스에서도 몸체가 있는 메서드인 default 메서드 정의할 수 있게 되었습니다.
        </p>
    </div>
</details>

### Q. java 8의 특징은 무엇이고 java8은 왜 중요할까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            java8 에서는 람다, Funtional Interface, 스트림 API, java.time 패키지 추가, Optional, interface에서의 default 키워드 등등... 많은 변화가 있었습니다.
            이중에서 가장 핵심이라고 생각되는 변화는 람다와 스트림 API를 이용해 함수형 프로그래밍이라는 새로운 프로그래밍 패러다임을 객체지향 프로그래밍인 Java에 접목시킨 것이라고 생각합니다.
            방대한 데이터를 병렬적으로 빠르게 처리 하면서, 동시에 안정적으로 처리하는 것의 중요성이 높아짐에 따라 함수형 프로그래밍의 가치가 높아졌습니다.
            함수형 프로그래밍을 잘 이용하면, 동시성에서 발생할 수 있는 side effect 없앨 수 있고, 멀티쓰레딩 환경에서 thread-safe를 보장하면서 안정적으로 병렬처리를 할 수 있기 때문입니다.
            즉, java8이 중요한 이유는 함수형 프로그래밍이라는 새로운 프로그래밍 패러다임을 객체지향 프로그래밍인 Java에 접목시켰다는 아주 큰 변화가 있었던 버전이기 때문입니다.
        </p>
    </div>
</details>

### Q. 쓰레드 세이프란?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            쓰레드 세이프란 멀티 쓰레드 프로그래밍에서 특정 자원에 대해 여러 스레드로부터 동시 접근이 이루어져도 프로그램의 실행에 문제가 없음을 의미합니다.
            자바에서는 JVM내 Method 영역 내의 데이터나 인스턴스 변수와 같은 Heap 영역 내에 저장되는 데이터들은 여러 스레드들 간에 공유되는 자원이기 때문에 쓰레드 세이프한 자원이 아닙니다.
            반면, 메서드 내 혹은 if문 내에 선언되는 로컬변수는 호출 시, thread의 stack frame 내에 생성되는 데이터이며, 여러 쓰레드들간 공유할 수 없는 자원이기 때문에 쓰레드 세이프한 자원입니다.  
        </p>
    </div>
</details>

### Q. Primitive type vs Reference type
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Primitive type은 자바에서 기본적으로 제공하는 기본 타입이며, 총 8가지가 있습니다.
            Primitive type의 변수 내에는 값자체가 할당됩니다.
            Reference type은 Primitive type을 제외한 모든 타입이며, 자바에서 기본적으로 제공해주는 타입도 있고, 개발자가 직접 만들어 사용하는 타입도 있습니다.
            Reference type의 변수 내에는 실제 값이 저장된 메모리 공간을 참조 할 수 있는 참조값이 할당됩니다.
            또한, Reference type을 이용해 객체를 생성할 수 있으며, 생성된 객체는 Heap 영역에 저장됩니다.
        </p>
    </div>
</details>

### Q. auto boxing과 unboxing 에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
          auto boxing이란 기본 타입의 데이터를 래퍼 클래스의 객체로 변환하는 것을 말합니다.
          Integer a = 100; 수행 시, auto boxing이 일어나면서 new Integer(100)을 알아서 수행시킵니다.
          unboxing은, 래퍼 타입의 객체를 기본 값으로 변환하는 것을 말합니다.
          래퍼클래스인 Integer 타입의 값을 primitivie 타입인 int 변수에 할당하면 Integer가 int로 알아서 unboxing되어 값이 할당됩니다.
        </p>
    </div>
</details>

### Q. System.out.println()를 절대 쓰지 말라고 하는데 이유가 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            일반적으로 애플리케이션에 로그를 찍을 때, System.out.println()을 사용하는 것보다는 Logback, Log4J 등의 라이브러리를 사용하는 것을 권장합니다.
            그 이유는 로깅 라이브러리를 이용하면 쓰레드 정보, 클래스 이름 같은 부가 정보를 함께 볼 수 있기 때문입니다.
            또한, System.out.println()과는 다르게 로깅 라이브러리를 이용하면, 로그 레벨에 따라 개발 서버에서는 모든 로그를 출력하고, 운영서버에서는 출력하지 않는 등 로그를 상황에 맞게 조절할 수 있습니다.
            그리고 System.out.println()은 로그가 시스템 아웃 콘솔에만 출력되는데 반해, 로깅 라이브러리를 이용하면 로그를 별도의 파일로도 남길 수 있습니다.
            특히 파일로 로그를 남길 때는 날짜별 혹은 용량에 따라 로그를 분할하는 것도 가능합니다.
            성능적으로도 System.out.println()는 좋지 않습니다. 왜냐하면, System.out.println()에는 내부적으로 멀티쓰레드 환경에서 thread safe를 보장하기 위한 synchronized를 이용하기 때문입니다.
            그래서 실무에서는 System.out.println() 보다는 꼭 로깅 라이브러리를 이용해 로그를 남겨야 합니다.
        </p>
    </div>
</details>

### Q. 실무에서 final을 붙이는 이유는?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            버그가 발생할 수 있는 가능성을 사전에 없애기 위해서 사용합니다.
            특히나, 멀티쓰레드나 함수형프로그램이에서 발생할 수 있는 의도치 않는 동작을 사전에 명시적으로 막을 수 있어 final의 가치가 더더욱 중요해진다.
        </p>
    </div>
</details>

### Q. java 8에서 변경된게 뭐냐/특징이 뭐냐 라는 질문이 면접에서 엄청 자주 나오는데요. 그 이유가 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            java8 에서는 람다, Funtional Interface, 스트림 API, java.time 패키지 추가, Optional, interface에서의 default 키워드 등등... 많은 변화가 있었습니다.
            이중에서 가장 핵심이라고 생각되는 변화는 람다와 스트림 API를 이용해 함수형 프로그래밍이라는 새로운 프로그래밍 패러다임을 객체지향 프로그래밍인 Java에 접목시킨 것이라고 생각합니다.
            방대한 데이터를 병렬적으로 빠르게 처리하면서, 동시에 안정적으로 처리하는 것의 중요성이 높아짐에 따라 함수형 프로그래밍의 가치가 높아졌습니다.
            함수형 프로그래밍을 잘 이용하면, 동시성에서 발생할 수 있는 side effect 없앨 수 있고, 멀티쓰레딩 환경에서 thread-safe를 보장하면서 안정적으로 병렬처리를 할 수 있기 때문입니다.
            즉, 면접에서 java8에 대해서 물어보는 질문은 자바에서 새롭게 적용된 함수형 프로그래밍에 대해 알고있는가? 에 대해서 물어보는 것일 가능성이 매우 크며, 이는 매우 중요한 변화였기 때문에 면접에서 많이 질문하는 것이라고 생각합니다.
        </p>
    </div>
</details>

### Q. Optional에서 orElse와 orElseGet의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            orElse의 파라미터는 일반 객체이며, 메서드를 파라미터로 전달할 시, Optional로 감싼 값이 null 이던 말던 항상 호출됩니다.
            반면 orElseGet 메서드의 파라미터는 Supplier 이며 Optional로 감싼 객체가 null이 아니면 호출되지 않고, null이면 호출됩니다.
        </p>
    </div>
</details>

### Q. ConcurrentModificationException 을 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            ConcurrentModificationException 예외는 멀티쓰레드 환경 또는 객체의 변경이 허용되지 않는 환경에서 concurrent modification이 일어날 때 이 예외가 발생할 수 있습니다.
            예를들면, 한 스레드가 Collection을 Iterating 하고 있을 때 다른 스레드에서 Collection을 modify 하는 경우, ConcurrentModificationException이 발생할 수 있습니다.
            여기서 말하는 modify는 Collection의 사이즈를 변경시키는 행동을 말합니다. (ex. add() or remove())
            이를 해결하기 위한 방법으로는 Iterator를 이용한 방법과, Stream API를 이용하는 방법이 있습니다.
        </p>
    </div>
</details>

### Q. Annotation이 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바에서 어노테이션은 코드 내에서 주석처럼 쓰이며 특별한 의미를 갖거나, 추가적인 기능을 수행할 수 있도록 정보를 제공하는 기술입니다.
            어노테이션은 여러가지 용도로 사용될 수 있습니다.
            먼저, 컴파일 시점에 에러를 체크하도록 컴파일러에게 정보를 제공할 수 있습니다.
            대표적인 예로는 @FuntionalInterface가 있습니다.
            또한, 컴파일 시점에 코드를 자동으로 생성할 수 있도록 정보를 제공하는데 사용될 수 있습니다.
            대표적인 예로는 Lombok 관련 어노테이션들이 있습니다.
            그리고 런타임 시점에 특정 기능을 실행하도록 정보를 제공할 수 있습니다.
            대표적인 예로는 스프링에서 사용되는 @ComponentScan, @Autowired와 리플렉션을 이용한 bean 등록 및 의존관계 자동 주입 기능이 있습니다.
        </p>
    </div>
</details>

### Q. MVC 패턴에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            MVC 패턴은 디자인 패턴 중 하나로써, 애플리케이션 코드를 각 역할에 맞게 나누는 것을 의미합니다.
            MVC에서는 애플리케이션 코드를 Model, View, Controller로 나눕니다.
            Model은 비즈니스 로직을 처리하는 영역입니다.
            View는 사용자의 눈에 보이는 화면을 담당하는 영역입니다.
            Controller는 사용자의 input을 처리하고, 비즈니스 로직을 호출하며 적절한 결과 값을 client에게 제공해주는 즉, Model과 View 사이에서 흐름제어를 담당하는 영역입니다.
            그렇다면, 왜 이렇게 역할을 나눠야 할까요?
            만약, 각 영역을 나누지 않고 하나의 서블릿이나 하나의 jsp 파일에 사용자에게 보여줄 화면에 대한 html 코드와 사용자가 입력한 input값 처리, 
            비즈니스 로직처리, database access 로직, 사용자에게 반환해 줄 output값 처리 등이 다 들어가 있다면 어떻게 될까요??
            이렇게 되면, 프론트엔드 개발자와 백엔드 개발자 간의 역할 분리도 힘들어지고, 코드의 유연성도 떨어지며, 기능을 추가할 때마다 코드가 길어져 가독성도 떨어질 것입니다.
            결국, 애플리케이션이 커지면 커질수록 유지보수 비용이 급격하게 올라갈 것입니다.
            그렇기 때문에, 유지보수 비용의 관점에서 보았을때 영역을 나누어 프로그래밍 하는 것이 유리하기 때문에 영역을 나눈다고 볼 수 있습니다.
        </p>
    </div>
</details>

### Q. Statement와 PreparedStatement의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Statement와 PreparedStatement는 모두 자바에서 DBMS에 쿼리를 요청하기 위해 사용되는 객체입니다.
            DBMS에서는 쿼리를 수행시킬 때, 쿼리문장 분석 -> 컴파일 -> 실행계획 작성의 단계들을 거칩니다.
            Statement는 쿼리를 수행할 때마다 위의 세단계를 매번 반복하는 방식으로 동작하고,
            PreparedStatement는 위의 세단계를 초기에 한번만 수행하고 해당 결과로 얻은 실행계획을 캐시에 담아 재사용하는 방식으로 동작합니다.
            PreparedStatement는 동일한 쿼리문에 대한 실행계획을 재사용하기 때문에, 컴파일 과정을 매번 수행할 필요가 없어, 동일한 쿼리문을 반복해서 수행해야 하는 상황이라면 성능적으로 장점을 가집니다.
            또한 PreparedStatement는 Statement와는 달리 where 조건에 사용될 파리미터를 바인딩 받는 방식으로 작성되기 때문에, SQL injection을 방어할 수도 있다는 장점을 갖습니다.
            그렇기 때문에, 일반적으로 PreparedStatment는 Statement보다 성능과 보안상 뛰어난 방식입니다.
        </p>
    </div>
</details>

### Q. 트래픽이 무지많이 몰리는 이벤트가 예정되어있어, 트래픽이 많을때 young gen /old gen 비율은 어떻게 하는 것이 좋을까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            트래픽이 많이 몰린다면 객체 생성도 그만큼 많이 될 것입니다.
            다만, 이러한 많은 객체들 중 수명이 짧은 객체들이 대부분일 것으로 예상됩니다.
            이러한 상황에서, young gen이 차지하는 비율이 작다면 그만큼 minor gc의 빈도가 늘어날 것이고, minor gc에 의해 발생하는 stop the world의 빈도가 많아져 성능에 악영향을 줄 것입니다.
            그렇다면, minor gc에 의한 stop the world의 빈도 수를 줄이기 위해, young gen이 차지하는 비율을 높이면 어떻게 될까요?
            minor gc에 의한 stop the world의 빈도수를 줄일 수 있지만, 해당 stop the world를 한번 수행할 때마다 그만큼 young gen에 객체가 많이 저장되기 때문에, 객체를 수거하는데 걸리는 시간은 이전보다 오래걸릴 것입니다.
            시간이 적게 걸리지만 많이 수행하느냐 vs 시간이 오래걸리지만 한번만 수행하느냐에 대한 차이 입니다.
            이 상황에서는 stop the world 빈도를 줄이는게 맞는 선택이라고 생각합니다.
            stop the world는 gc를 동작시키는 thread를 제외한 나머지 모든 thread를 all stop 하는 작업이기 때문입니다.
            하지만, young gen의 비율을 늘릴경우 old gen이 차지하는 비율은 상대적으로 작아져 old gen을 대상으로 하는 major gc의 빈도도 많아 질 것입니다.
            결국, young gen을 대상으로 한 minor gc 의 빈도수 vs old gen을 대상으로한 major gc의 빈도 수 사이의 trade off가 발생하는 상황이라고 생각합니다.
            다만, old gen은 young gen과 같이 eden이나 survivor space가 존재하는 게 아니기 때문에 메모리 단편화도 신경써야하고, 일반적으로 youn gen보다 더 많은 객체들을 관리하다 보니 major gc의 빈도가 높아지면 성능에 좋지 않은 역할을 줄 것은 분명합니다.
            그렇기 때문에, old gen의 비율을 줄여가면서까지, minor gc의 빈도를 줄이기 위해 young gen의 비율을 높이는 것이 위험한 선택이 될 수 있을것이라 생각합니다.
            결론적으로, 오직 트래픽이 많을것이라는 가정만을 가지고 young gen과 old gen의 최적화된 비율을 수치화 하기는 어렵지 않을까? 라고 생각합니다.
            각 애플리케이션마다 저마다의 특징을 갖고있고, 애플리케이션을 동작시키는 환경도 제각각이어서, 여러가지 변수들이 존재할 것이기 때문입니다.
            그렇기 때문에 각 애플리케이션마다 대용량 트래픽에 대한 성능 테스팅이나 모니터링 과정을 통해 young gen과 old gen에 대한 최적의 비율을 찾는 것이 중요할 것이라 생각합니다.
        </p>
    </div>
</details>


# Spring

### Q. 스프링이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바 엔터프라이즈 개발을 위한 오픈소스 애플리케이션 프레임워크 입니다.
        </p>
    </div>
</details>

### Q. 프레임워크가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            개발자들이 애플리케이션 개발을 빠르고 효율적으로 할 수 있도록 기본적인 뼈대를 제공하는 틀 입니다.
        </p>
    </div>
</details>

### Q. 스프링은 왜 쓰는 건가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바 애플리케이션의 개발에 필요한 기반, 뼈대를 제공함으로써 개발자들은 애플리케이션 비즈니스 로직의 개발에만 
            집중할 수 있게 되고 이로인해, 생산성을 높일 수 있기 때문에 씁니다.
        </p>
    </div>
</details>

### Q. 스프링의 주요 특징은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스프링의 주요 특징으로는 IOC/DI, AOP, PSA가 있습니다.
            먼저 IOC는 제어의 역전이란 의미로 객체의 생성 및 생명주기 관리까지 모든 객체에 대한 제어권 
            즉, 프로그램의 흐름이 개발자가 아닌 프레임워크로 넘어갔다는 것을 의미합니다.
            그리고 DI란 의존관계 주입이라는 의미입니다.
            의존관계란, 하나의 객체가 다른 객체의 상태에 따라 영향을 받는 것을 의미합니다. 스프링에서는 이러한 의존관계를
            개발자가 직접 관리하지 않고 스프링 컨테이너라는 곳에서 관리하며 의존관계가 필요할 때마다 스프링 컨테이너에서 개발자 코드상으로
            주입해줍니다. 즉, 스프링에서 IOC를 구현한 한가지 방법이 DI이며 IOC는 DI를 포함하는 개념입니다.
            이를 통해, 개발자는 객체의 라이프사이클이나 의존관계를 신경쓸 필요없이 자신의 비즈니스 로직에만 집중하여 생산성을 높일 수 있습니다.
            AOP는 대부분의 서비스들이 공통으로 가지고 있는 보안, 로깅, 트랜잭션과 같이 비즈니스 로직은 아니지만 반드시 처리가 필요한 부분을 별도로
            분리하여 프로그래밍하는 방식을 의미합니다. 
            이를통해, 코드의 중복을 없애 유지보수 비용을 최소화 할 수 있습니다.
            PSA는 Portable Service Abstraction으로서 외부 환경의 변화에 관계없이 일관된 방식으로 기술에 접근할 수 있게 해주는 것을 의미합니다.
            예를들어 @Cacheable을 사용하면 내가 캐시대상으로 redis를 사용하던 ehcache를 사용하던 @Cacheable을 처리하는 내부 코드는 변하지 않습니다.
            마찬가지로 @Transactional을 사용하면 JPA의 구현체로 hibernate를 이용하던 다른 구현체를 이용하던 @Transactional을 처리하는 내부 코드를 변경할 필요가 없습니다.
        </p>
    </div>
</details>

### Q. 생성자 주입이 권장되는 이유는 뭘까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
           대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없습니다. 
           오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안됩니다. 즉, immutable 해야하는데 생성자 주입은
           유일하게 final 키워드를 사용하여 immutable을 보장할 수 있습니다.
           immutable을 보장하면 추후에 발생할 수 있을 버그를 사전에 차단해 주는 효과를 얻을 수 있습니다.
           또한, 필드 주입방식은 생성자 주입이나 세터 주입과 달리, 테스트 시 application context 없이는 테스트가 불가하다는 단점이 있습니다.
           즉, 프레임워크 없이 순수한 자바 코드로만 단위 테스트를 수행이 불가합니다.
            i결과적으로, 생성자 주입은 필드 주입이나 세터 주입과 비교하여 많은 장점을 가지면서, 단점은 없으므로 생성자 주입이 권장됩니다.
        </p>
    </div>
</details>

### Q. 프레임워크와 라이브러리의 차이에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프레임워크와 라이브러리는 모두 개발자가 개발을 보다 더 효율적으로 하기 위해 도움을 주는 도구 입니다.
            프레임워크는 애플리케이션의 기본이 되는 뼈대나 틀입니다.
            프레임워크를 사용하면 개발 생산성이 높아지며, 공통적인 개발환경을 제공하여 다른 사람과의 협업을 함에 있어서 통일된 형태의 개발을 할 수 있어 작업의 효율을 높일 수 있다는 장점이 있습니다.
            반면, 개발자는 프레임워크에 의존하게 되고, 뼈대 자체에 대한 변경에 대해서는 유연하지 못하다는 단점이 있습니다.
            라이브러리는 재사용 가능한 코드의 집합 입니다.
            라이브러리는 개발하는 데 필요한 것들을 모아둔 일종의 저장소이며, 필요할 때마다 애플리케이션 코드에서 직접 호출해서 사용합니다.
            그렇다면, 프레임워크와 라이브러리의 차이점은 무엇일까요?
            프레임워크와 라이브러리를 구분짓는 가장 중요한 요소는 애플리케이션 코드의 흐름 즉, 제어권 입니다.
            애플리케이션 코드는 프레임워크에 의해 사용됩니다.
            이를 제어권이 역전 됐다고 말합니다.
            즉, 애플리케이션 코드는 프레임워크가 짜놓은 틀 안에서 수동적으로 동작합니다.
            그에 반해, 라이브러리는 제어권을 갖는 애플리케이션 코드에 의해 동작합니다.
            즉, 애플리케이션 코드는 자신이 직접 제어권을 갖고, 자신의 의도와 목적에 맞게 능동적으로 라이브러리에 정의된 코드를 사용한다는 점에서 프레임워크와 차이가 있습니다.
        </p>
    </div>
</details>

### Q. servlet과 servlet container에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            서블릿은 클라이언트의 http 요청을 받아 비즈니스 로직을 수행하고, 적절한 http 응답을 생성하는 자바 객체입니다.
            서블릿은 일반 자바 객체와 달리 서블릿 컨테이너 내에서만 실행됩니다.
            서블릿 컨테이너는 클라이언트로부터 http 요청 메시지을 받아 적절하게 파싱한 후, 스레드를 생성하여 서블릿을 실행시키고, 서블릿으로 부터 응답받은 요청 처리 결과를 이용해 http 응답 메시지를 만들어 클라이언트에게 응답해주는 기능을 하는 컴포넌트입니다.
            서블릿 컨테이너는 tcp/ip 소켓 연결 및 종료, http 요청 메시지 파싱 및 http 응답 메시지 생성, 멀티스레딩 처리와 같은 웹 개발에서 요구되는 공통적인 작업을 수행하기 때문에 개발자는 비즈니스 로직에 집중할 수 있습니다.
        </p>
    </div>
</details>

### Q. Bean 이란 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            spring Container가 관리하는 자바 객체를 bean이라고 합니다.
        </p>
    </div>
</details>

### Q. Bean의 scope에는 무엇이 있나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            싱글톤, 프로토타입, 웹 관련 스코프 들이 있습니다.
            싱글톤은 스프링 컨테이너의 시작될 때 빈이 생성되어 스프링 컨테이너가 종료될때까지 유지되는 가장 넓은 범위의 스코프 입니다.
            스프링 컨테이너 내에 싱글톤 bean은 단 하나씩만 존재합니다.
            프로토타입은 스프링 컨테이너가 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프입니다.
            즉, 클라이언트에 빈을 반환하고, 이후 스프링 컨테이너는 생성된 프로토타입 빈을 관리하지 않습니다.
            웹 관련 스코프로는 request, session, application, websocket이 있습니다.
            request는 웹 요청이 들어오고 나갈때 까지 유지되는 스코프 입니다.
            session은 웹 세션이 생성되고 종료될 때까지 유지되는 스코프 입니다.
            application은 서블릿과 같은 범위로 유지되는 스코프 입니다.
            websocket은 웹 소켓과 동일한 생명주기를 갖는 스코프 입니다.
        </p>
    </div>
</details>

### Q. spring container가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            bean을 생성하고 관리하면서 의존관계를 연결해 주는 역할을 수행하는 스프링의 핵심 객체 입니다.
        </p>
    </div>
</details>

### Q. @Bean, @Component의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            둘다 자바 객체를 스프링 컨테이너에 bean으로 등록하기 위한 방법입니다.
            다만, @Bean의 경우 개발자가 컨트롤이 불가능한 외부 라이브러리들을 Bean으로 등록하고 싶은 경우에 사용하고
            개발자가 직접 컨트롤이 가능한 Class들을 Bean으로 등록하고 싶은 경우엔 @Component를 사용합니다.
        </p>
    </div>
</details>

### Q. @ComponentScan이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            @Component 혹은 streotype, @Controller, @Service, @Repository 가 부여된 Class들을 자동으로 scan하여 Bean으로 
            등록해주는 역할을하는 어노테이션 입니다.
        </p>
    </div>
</details>

### Q. @Component 로 등록한 객체가 Bean 으로 등록되는 과정을 최대한 상세하게 설명해 보세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스프링에서는 빈을 스프링 컨테이너에 등록하기 위한 방법중 하나로 컴포넌트 스캔이라는 기능을 제공합니다.
            컴포넌트 스캔은 @Component가 붙은 클래스들을 스캔하여 스프링 컨테이너에 빈으로 등록하는 역할을 수행합니다.
            즉, 스프링 애플리케이션을 동작시키면 스프링 컨테이너가 생성되고, @ComponentScan은 해당 클래스가 부여된 클래스를 기준으로, 하위 패키지에 등록된 모든 
            @Component가 붙은 클래스를 스캔합니다.
            이때, @Component가 붙은 클래스를 찾기 위해 리플랙션이라는 기술이 사용됩니다.
            그리고 이렇게 스캔한 클래스에 대한 객체들은 스프링 컨테이너에 스프링 빈으로 등록됩니다.
            이때, 스프링 빈의 기본 이름은 클래스명을 사용하되, 맨 앞글자만 소문자를 사용하여 등록됩니다.
            스프링 bean이 등록될 때, @Autowired를 통한 의존관계 주입도 수행됩니다.
            스프링 컨테이너에 등록된 bean은 기본적으로 싱글톤으로 관리되며, 스프링 컨테이너가 종료될 때까지 유지됩니다.
        </p>  
    </div>
</details>

### Q. Spring 서버 부팅 시 동작과정에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            먼저 톰캣이 실행됩니다.
            다음으로, application context 즉, spring container가 생성됩니다.
            다음으로, 스프링 bean들이 spring container에 생성됩니다.
            다음으로, spring container내 bean들의 의존관계가 주입됩니다.
        </p>
    </div>
</details>

### Q. Spring이 bean을 관리하는 방식에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            기본적으로 spring은 bean을 싱글톤으로 관리합니다.
            Spring은 기본적으로 엔터프라이즈 애플리케이션 개발을 위한 프레임워크로서 request가 많은 환경입니다.
            이러한 환경에서 request이 요청이 들어올 때마다 bean을 새로 계속 생성하면 메모리 자원이 고갈될 것입니다.
            그렇기 때문에 spring container는 메모리를 효율적으로 사용하기 위해 기본적으로 bean을 singleton으로 관리합니다.
            이렇게 spring container에서 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라고 합니다.
        </p>
    </div>
</details>

### Q. 스프링 부트 스타터에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            개발에 필요한 연관된 의존성들을 모아 제공하며 각 의존성마다 필요한 기본 설정들까지 자동화 해주는 기능입니다.
            예를들어, spring-boot-start-web 의존성을 애플리케이션에 추가하면  web과 연관된 의존성들을 모두 패키징해서 제공하고, tomcat에 대한 default 설정들까지 자동으로 추가 해줍니다.
            즉, 스타터는 개발자가 더욱 더 비즈니스 로직에 집중할 수 있도록 도와주는 스프링 부트에서 제공하는 기능입니다.
        </p>
    </div>
</details>

### Q. threadLocal이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            각 thread마다 갖는 독립적인 지역변수를 말합니다.
            스프링은 bean을 싱글톤으로 관리하기 때문에 공유 필드로 상태값을 가질 시 
            멀티쓰레드 환경에서 큰 장애가 발생할 수 있습니다. 이럴 때 사용할 수 있는 것이 threadLocal 입니다.
            다만, 스프링에서는 thread 또한 thread pool에 저장되는 공유자원이기 때문에 하나의 요청이 끝나는 시점에
            thread local의 초기화 작업을 해주어야 다른 request에 영향을 주지 않습니다.
        </p>
    </div>
</details>

### Q. dispatcherServlet에 대해 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            DispatcherServlet은 Spring에서 사용되는 프론트 컨트롤러 입니다.
            DispatcherServlet은 Bean으로 등록되어 client의 요청이 controller로 가기전에 먼저, 
            package를 scan하고 @Controller, @RestController를 확인하여 적절한 Handler Method에 위임해주는 역할을 수행합니다.
        </p>
    </div>
</details>

### Q. Spring framework 안에는 어떠한 디자인 패턴들이 적용돼있을가요? 간단한 사례와 함께 소개해 주실 수 있을까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Spring Framework에는 Proxy pattern, Strategy pattern, Singletone pattern, template method pattern, adapter pattern 등이 적용돼있습니다.
            Proxy 패턴은 Spring AOP에서 JDK dynamic proxy, CGLIB을 통해 프록시 객체가 만들어져 사용될 때 적용돼있고, AOP를 사용하는 @Cachable, @Transactional 등이 적용된 코드 역시 프록시 패턴이 구현된 사례입니다.
            Singleton 패턴은 Spring Container가 Bean의 생명주기를 관리하는 방법으로 주로 사용됩니다.
            Template method 패턴은 Spring MVC의 핵심인 DispatcherServlet에 정의된 doService()가 호출되는 과정에서 적용돼있습니다.
            Adapter 패턴은 DispatcherServlet에서 핸들러(컨트롤러)를 실행시키기 위한 핸들러 어댑터를 조회하는 과정에 적용돼있고, 이를 통해 다양한 핸들러를 유연하게 실행시킬 수 있습니다.
        </p>
    </div>
</details>

### Q. spring mvc 동작 과정에 대해 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. Spring의 filter, interceptor의 차이는 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            둘다 웹과 관련된 공통 관심 사항을 처리하지만, 적용되는 순서와 범위, 그리고 사용방법이 다릅니다.
            또한, 필터가 서블릿이 제공하는 기술이라면, 인터셉터는 스프링 MVC가 제공하는 기술입니다.
            필터는 WAS와 서블릿(스프링 MVC를 쓰고있다면, 디스패처 서블릿) 사이에서 서블릿을 호출하기 이전에 호출됩니다.
            인터셉터는 스프링 MVC의 시작점인 디스패처 서블릿과 컨트롤러 사이에서 컨트롤러 호출 직전에 호출 됩니다.
            즉, 필터와 인터셉터는 다음과 같은 호출 순서를 갖습니다.
            HTTP 요청 -> WAS -> 필터 -> (디스패처) 서블릿 -> 인터셉터 -> 컨트롤러
            인터셈터와 필터는 각기 다른 Context의 기능을 갖기 때문에 예외를 처리하는데도 차이점을 갖습니다.
            인터셉터에서 예외 발생 시 Spring Context내에서 동작하기 때문에 스프링에서 제공하는 ExceptionResolver를 통해 처리가 가능합니다.
            그에반해, filter는 Web Application Context 즉, WAS내에서 동작하기 때문에, FilterChain 안에서 Exception 처리를 위한 Filter를 FilterChain 상위에 등록 하거나,
            FilterChain 안에서 모든 예외를 DispatcherServlet 까지 흘려보내거나, 예외 발생 시 에러페이지를 정의해야 합니다.
            그렇다면, 이 둘은 얼핏 보면 비슷해 보이는데 언제 필터를 사용하고 언제 인터셉터를 사용하는게 좋을까요?
            필터의 경우 단순히 request, response 객체만 제공하지만, 인터셉터는 어떤 컨트롤러(handler)가 호출되는지에 대한 호출 정보도 제공 받을 수 있습니다.
            또한, 필터의 경우 단순하게 doFilter() 하나만 제공되는데 반해, 인터셉터는 컨트롤러 호출 전(preHandle), 호출 후(postHandle), 요청 완료 이후(afterCompletion)와 같이 단계적으로 잘 세분화 되어 있습니다.
            또한, 필터는 Spring의 Context 밖에서 동작하기 때문에, 일반적으로 Spring과 관련된 DI와 같은 기능들을 사용할 수 없습니다.
            물론, GenericFilterBean과 같이 Spring의 Bean을 사용할 수 있게 도와주는 필터도 있긴 합니다.
            결론적으로, 개발자 입장에서 봤을 때, 인터셉터가 필터보다 더 정교하고 다양한 기능들을 제공하기 때문에, 웹과 관련된 공통로직을 처리해야하고, 내 프로젝트에서 Spring MVC를 사용하고 있으면서, 필터가 꼭 요구되는 상황이 아니라면 인터셉터를 사용하는 것이 좋은 선택이라고 생각합니다.
            다만, 필터를 이용하면, 필터에서 적절하지 않은 요청이라고 판단하여 서블릿을 호출하기 전에 요청로직을 끝내, 이후 로직을 수행하지 않을 수 있다는 장점을 가질 수 있으나, 이것이 필터를 선택해야 한다는 결정적인 요소가 된다고는 생각하지는 않습니다.
        </p>
    </div>
</details>

### Q. Spring AOP가 무엇이고 어떻게 동작하나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            흩어진 관심사를 하나의 aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하는 방식의 프로그래밍 기법을 말합니다.
            Spring AOP는 프록시 패턴을 이용해 동작합니다.
            프록시란 타겟 오브젝트을 감싸서 타겟의 요청을 대신 받아주는 Wrapping 오브젝트 입니다.
            클라이언트에서 타겟 메서드를 호출하게 되면 타겟이 아닌 타겟을 감싸고 있는 프록시가 대신 호출되어, 
            타겟 메서드 실행전에 전처리, 타겟 메소드 실행 후, 후처리를 실행시키도록 구성됩니다.
        </p>
    </div>
</details>

### Q. Spring AOP에서 프록시는 어떻게 생성되나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프록시를 컴파일 시점에 생성하면 직접 프록시의 기능을 추가해야해서 번거롭고 코드가 지저분해 질 수 있다는 단점이 있습니다.
            그래서 스프링에서는 이러한 단점을 해결하기 위해 런타임 시점에 타겟에 대한 프록시를 생성해 주는 2가지 기법을 사용합니다.
            첫번째 기술은 Dynamic proxy입니다.
            다만, Dynamic proxy 기법으로는 클래스 기반의 프록시를 만들지 못하는 한계가 있다.
            즉, 타겟 오브젝트가 interface를 구현하고 있지 않다면 Dynamic proxy 기법으로는 프록시를 만들지 못합니다.
            두번째 기술은 CGLIB 방식입니다.
            CGLIB은 인터페이스만 가능했던 dynamic proxy와는 달리 클래스에 대한 Proxy가 가능합니다.
            CGLIB Proxy는 Target Class를 상속받아 생성됩니다.
            스프링 부트에서는 런타임에 프록시 생성 시 기본적으로 CGLIB 방식을 이용합니다.
        </p>
    </div>
</details>

### Q. spring boot security에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            인증, 권한 처리를 편리하게 관리하도록 도와주는 spring 프로젝트 입니다.
            이로 인해, 보안 문제는 Spring Boot Security에 맡겨 두고 핵심 비즈니스 로직에 집중할 수 있었습니다.
        </p>
    </div>
</details>

### Q. JPA에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자바진영의 ORM 기술 표준, 인터페이스 입니다.
            SQL에 의존되는 개발을 피할수 있도록 도와줍니다.
            ORM은 객체와 관계형 데이터베이스를 매핑한다는 뜻입니다.
            ORM은 Object Relation Mapping의 약자로, 객체와 관계형 데이터베이스의 패러다임 불일치 문제를 개발자 대신 해결해줍니다.
            가령, RDBMS의 컬럼값으로는 list등 다른 구조를 포함할 수 없는 반면, 메모리 내 데이터 구조에서는 이런 제약이 없어 훨씬 복잡한 구조를 사용합니다. 
            그 결과 복잡한 메모리 내 데이터 구조를 데이터베이스에 저장하려면 먼저 관계형 표현으로 변환해야 하는데 
            이때, ORM은 개발자의 별도 코드없이 이를 대신 매핑해줍니다.
        </p>
    </div>
</details>

### Q. Spring data JPA에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Spring에서 JPA를 쉽게 사용할 수 있도록 도와주는 Spring project입니다.
            기본적인 CRUD를 메서드로 제공해주기 때문에 쉽고 빠르게 개발하는데 도움이 되어 생산성을 높일 수 있습니다.
        </p>
    </div>
</details>

### Q. JPA에서 영속성 컨텍스트가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            엔티티를 영구 저장하는 환경이라는 의미입니다.
            애플리케이션과 DB 사이에서 엔티티를 보관하는 가상의 DB 역할을 수행합니다.
            영속성 컨텍스트에 저장된 영속상태의 엔티티들은 플러시 시점에 DB에 반영되는데,
            일반적으로 트랜잭션을 커밋할 때 영속성 컨텍스트가 플러시 됩니다.
            이를통해 캐시, 쓰기 지연, 변경 감지(영속성 컨텍스트가 관리하는 영속 상태의 엔티티에만 적용됨), 
            지연로딩(실제 객체대신 프록시 객체를 로딩해두고 해당 객체를 실제 사용할 때 영속성 컨텍스트를 통해 데이터를 불러오는 방법)
            의 기능을 수행할 수 있습니다.
        </p>
    </div>
</details>

### Q. N+1 문제가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            특정 객체와 연관된 객체를 조회할 때 쿼리가 특정 객체의 수만큼 더 발생하는 문제입니다.
            실제 프로젝트를 진행하면서 N+1 문제가 발생했던 경험이 있습니다.
            상품 테이블과 상품 할인 테이블이 1:N 관계를 갖는 상황에서 상품 데이터를 조회한 후 그와 연관된 상품 할인
            데이터를 조회한 결과, 상품 데이터의 수만큼의 쿼리가 더 발생했습니다.
            이를 해결하기 위해 특정 연관된 엔티티를 SQL 조인을 사용해서 함께 조회하는 fetch join 방식과 연관된 엔티티를 
            조회할 때 지정한 size만큼 IN절을 사용해 조회하는 BatchSize 방식을 고민하였습니다.
            그러나 fetch join은 paging 쿼리를 작성할 수 없다는 제한이 있어 BatchSize 방식을 통해 N+1문제를 해결하였습니다.
        </p>
    </div>
</details>

### Q. Spring boot batch가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스프링 진영에서 배치기능을 쉽게 개발하기 위해 지원하는 프로젝트 입니다.
            실제 프로젝트에서 상품 구매 카운트 데이터를 다루기 위해 spring batch를 사용했습니다.
            처음에는 모든 step을 tasklet으로 개발하였는데, tasklet의 경우 paging 단위의 조회를 지원하지 않았고
            chunk size 기준 commit interval 기능도 지원하지 않았습니다.
            이런이유 때문에, tasklet 구조를 read,process,write 구조로 바꿨습니다.
            그런다음, JpaPagingItemReder를 통해 paging 처리하였고 chunk size도 page size와 동일하게 설정하여
            보다 더 안정적인 batch application 환경을 구축했습니다.
        </p>
    </div>
</details>

### Q. Entity, DTO, VO에 대해서 설명하세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Entity 클래스는 실제 DB의 테이블과 1:1로 매핑 되는 클래스로,
            DB의 테이블내에 존재하는 컬럼만을 속성으로 갖습니다.
            DTO(Data Transfer Object)는 데이터 전송 객체라는 의미를 가지고 있으며,
            계층간 데이터 교환을 위한 객체입니다.
            client에게서 원하는 데이터만을 얻어오거나 client에게 원하는 데이터만을 응답해주기 위해 사용합니다.
            VO(Value Object)는 말 그대로 값 객체라는 의미를 가지고 있습니다.
            VO는 read-only 값을 가지고 있습니다. 즉, 변하지 않는 immutable한 성질을 갖고 있어 중간에 값을 바꿀 수가 없습니다.
        </p>
    </div>
</details>

### Q. spring의 connection pool에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            client 입장에서 DB와의 connection을 생성하는 작업은 많은 비용을 초래하는 작업입니다.
            그래서, 스프링은 DB와의 connection을 connection pool에다가 미리 만들어 놓고 그 connection이 
            필요할 때마다 해당 스레드에게 connection을 할당해주는 전략을 사용합니다.
            이를 통해, 성능적으로 이점을 얻을 수 있습니다.
        </p>
    </div>
</details>

### Q. thread pool에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스프링에서는 스레드풀에 스레드 객체를 미리 생성해놓고, 요청이 들어올 때마다 특정 스레드를 할당해주는 방식으로 요청을 처리합니다.
            이를통해, 엔터프라이즈 환경에서 스레드를 생성하는 작업을 최소화 시켜 애플리케이션의 성능저하를 막을 수 있다.
            다만, 스레드풀에 너무 많은 스레드를 만들어 놓으면 쉬고있는 스레드가 많이 발생해 시스템 자원을 효율적으로 사용하지 못할 수 있으므로 적절하게 생성해야합니다.
        </p>
    </div>
</details>

### Q. UnitTest가 무엇이고 왜 필요한가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            내가 만든 하나의 기능을 테스트 하는 메서드를 유닛테스트라고 합니다.
            단위테스트를 잘 작성해 놓았다면 추후에 변경사항이나 리팩토링을 했을 때 초기에 버그를 발견하기 수월하고
            안정성 있게 코드를 작성할 수 있습니다.
        </p>
    </div>
</details>

### Q. CI(Continuous Integration), CD(Continuous Delivery)에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            현대에는 어떻게 하면 고객의 요구에 빠르게 반응해서 제품을 출시, 업데이트 할 것인가가 중요해졌습니다.  
            CI/CD란 애플리케이션 개발단계부터 배포단계까지 모든 단계들을 자동화해서 조금 더 효율적이고 빠르게 사용자에게 빈번이 배포할 수 있도록 하는 것을 말합니다.
            CI는 지속적인 통합 이고, 버그를 수정하거나 새로 추가한 기능들이 build 되고, test 되어 메인 레파지토리에 주기적으로 merge되는 과정을 말합니다.
            CI는 코드 변경사항을 최대한 작은단위로 나누어서 지속적으로 빈번하게 merge한다는 특징을 가지며, build, test, merge 단계를 자동화한다는 특징을 갖습니다.
            CI를 이용하면, 빈번하게 merge하기 때문에 merge 충돌을 최소화 시켜 개발 생산성을 향상 시킬 수 있습니다. 또한 build, test, merge 과정을 개발자가 직접 수동으로 하지 않고, 자동화시켜 휴먼에러를 최소화시킬 수 있습니다.
            CD는 지속적인 전달이며, ci가 완료된 결과물을 검증하고 배포하는 작업을 자동화 시키는 것을 말합니다.
        </p>
    </div>
</details>

### Q. redirect와 forward 차이에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            둘다 페이지 전환 방식입니다.
            redirect는 서버가 클라이언트의 요청을 처리하고 클라이언트에게 어떤 URL로 이동하라는 요청을 보내는 것을 말합니다.
            URL의 변화여부가 필요하다면 Redirect를 사용하는 것이 좋습니다. 주로 로그인 후에 많이 사용됩니다.
            forward 클라이언트가 요청을 보냈을 때 서버 쪽에서 혼자 처리하는 것이 아니라 또 다른 서버에게 일을 넘기는 것입니다.
            그렇기 때문에 웹 브라우저에는 최초에 호출한 URL이 표시되며 이동한 페이지의 URL 정보는 볼 수 없습니다.
            요청했던 URL이나 request,response 객체를 재사용하거나 공유해야한다면 Forward를 사용하는 것이 좋습니다.
        </p>
    </div>
</details>

### Q. 네이버 쇼핑 플랫폼에서는 왜 Spring 의 WEB FLUX 를 사용하려는 걸까요? 무조건 WEB FLUX가 좋은 걸까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Spring MVC는 Servlet을 기반으로 동작하며, request당 thread가 하나씩 할당되어 요청을 처리하는 구조입니다.
            또한, network I/O 또는 DB I/O 작업 수행 시 해당 작업이 끝날때까지 쓰레드가 대기하는 Blocking I/O 방식으로 동작합니다.
            반면, Spring Webflux는 I/O 작업 수행 시, 해당 작업이 끝날때까지 쓰레드가 대기하지 않고 다른 작업을 수행하다가 I/O 작업이 끝나면 다시 이어서 작업을 수행하는 방식인 Non-Blocking I/O 방식으로 동작합니다.
            그렇기 때문에 Spring Webflux를 이용하면 최소한의 자원으로 대량의 트래픽을 빠르게 처리할 수 있다는 장점이 있습니다.
            그렇다면 무조건 WebFlux를 써야할까요?
            그렇지는 않습니다.
            만약, 트래픽이 적당히 발생하는 서비스라면, thread pool을 튜닝하는 것만으로도 충분히 좋은 성능을 보장받을 수 있을 것입니다.
            또한, Blocking 방식의 코드를 짜는 것은 코드의 동작 과정을 디버깅하기 수월하며, 가독성도 더 좋습니다. 그리고 이는 유지보수 비용과 연결됩니다.
            문제는 네이버 쇼핑 플랫폼 같은 적당하지 않은 트래픽이 발생하는 서비스일 경우입니다.
            Core의 개수는 한정적이며, Thread는 메모리를 소모하는 자원이기 때문에 트래픽이 많이 발생하는 상황에서, 무한정 thread pool size를 늘리는 것에는 한계가 있습니다.
            또한, 쓰레드가 많을수록 Core를 점유하기 위해 대기하고 있던 쓰레드와 Core를 점유하고 있던 쓰레드간의 Switching 작업인 Context Switching으로 인해 Core를 제대로 활용하지 못해 처리량이 저하될 가능성이 큽니다.
            그렇기 때문에, 요청마다 쓰레드를 할당하고 Blocking I/O로 쓰레드를 병렬처리하는 방식으로는 대량의 트래픽을 처리하는데 한계가 생길 수 있습니다.
            이러한 한계를 극복할 수 있는 방법이 Non-Blocking I/O를 이용하는 방식이며, Spring5 부터 Webflux라는 모듈을 통해 Non-Blocking I/O 방식의 프로그래밍을 할 수 있도록 지원하고 있습니다.
            결론적으로, 트래픽이 상대적으로 적은 서비스에서는 Spring MVC를 사용해도 충분하지만, 트래픽이 감당하기 힘들정도로 많아질 경우에는 Spring Webflux를 사용하는 것이 자원과 성능 측면에서 유리합니다.
        </p>
    </div>
</details>

# Database

### Q. INDEX가 뭔가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            테이블의 데이터 조회를 빠르게 하기 위한 기술입니다.
            조회 성능은 빨라지지만 데이터를 추가하는 성능은 느려집니다.
            메모리 상에 index가 저장됩니다.
        </p>
    </div>
</details>

### Q. RDB에서 INDEX가 어떻게 구성되어 있나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            b+트리로 구성되어있습니다.
            b+트리는 root, branch, leaf 노드로 나뉘고 스스로 균형을 맞추는 트리입니다.
            스스로 균형을 맞추기 때문에 데이터의 수에 상관없이 O(logN)의 조회성능을 유지합니다.
        </p>
    </div>
</details>

### Q. RDB에서 쿼리가 어떻게 동작하는지 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            RDB는 크게 connection pool, parser, optimizer, execution egine으로 구성됩니다.
            먼저, connection pool에서 할당받은 connection으로 client와 연결하여 쿼리를 전달받습니다.
            전달받은 쿼리는 parser에 의해 잘게 쪼개지는데 이 과정에서 쿼리가 문법적으로 문제가 있는지 없는지 파악합니다.
            마치 컴파일 단계와 유사한 과정을 수행합니다.
            다음으로, parsing된 쿼리가 optimizer에 전달되고 optimizer는 인덱스의 유무, 데이터 분산 또는 편향 정도 등의
            통계정보를 참고하여 여러 실행계획을 작성합니다. 
            그리고 이들의 비용을 연산한 후, 가장 낮은 비용을 가진 실행계획을 선택합니다.
            execution engine은 optimizer가 생성한 실행계획을 바탕으로 읽어 들여야 할 데이터가 buffer memory에 
            있다면 buffer memory의 데이터를 그대로 읽어들입니다. 만약 읽어 들여야 할 데이터가 buffer memory에 없다면 storage에서 직접 데이터를 
            읽어들이고 buffer memory에 적재시킵니다.
        </p>
    </div>
</details>

### Q. optimizer가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            optimizer는 인덱스의 유무, 데이터 분산 또는 편향 정도 등의 통계정보를 참고하여 여러 실행계획을 작성하고
            이들의 비용을 연산한 후, 최적화된 실행계획을 수립하는 DBMS의 핵심엔진 입니다.
        </p>
    </div>
</details>

### Q. 스토리지 엔진은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            디스크에서 데이터를 어떻게 가져오고 어떻게 최적으로 저장할 것인지 결정하는 역할을 수행하는
            DBMS의 component 입니다.
            Mysql의 스토리지 엔진은 innoDB 입니다.
        </p>
    </div>
</details>

### Q. index scan과 table full scan이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            index scan은 index가 적용될 때 테이블을 scan하는 방식이고 table full scan은 index가 적용되지 않았을때 테이블을 scan하는 방식입니다.
            index scan은 single block I/O로 동작하고, table full scan은 multi block I/O로 동작합니다.
            데이터가 엄청 많은 상태에서 조회하고자 하는 데이터가 적을 경우에는 index scan이 유리하고 그렇지 않으면 table full scan이 유리합니다.
            즉, 어느것이 무조건 좋은 방법인 것이 아니라 상황에 따라 특정 방법이 더 좋을 수 있으니 자신의 환경에 맞게 선택하는 것이 중요합니다.
            (책예시)
        </p>
    </div>
</details>

### Q. hint에 대해 알고계시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            옵티마이저가 잘못된 쿼리 플랜을 생성하는 것을 대비해 hint를 사용하여 직접 쿼리 플랜을 제어할 수 있습니다.
        </p>
    </div>
</details>

### Q. 트랜잭션에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            트랜잭션은 여러 쿼리들을 논리적으로 하나의 작업으로 묶어주는 것을 의미합니다.
            쪼개질 수 없는 작업수행의 논리적 단위를 트랜잭션이라고 합니다.
            데이터의 정합성을 위해 사용하며 원자성(Atomicity), 일관성(Consistency), 고립성(Isolation), 지속성(Durability)의 4가지 특성을 갖습니다.
            원자성(Atomicity)은 트랜잭션은 DB에 모두 반영되거나, 전혀 반영되지 않아야 한다는 특성입니다.
            일관성(Consistency)은 트랜잭션이 성공적으로 수행된 후에도 데이터베이스가 일관성 있는 상태를 유지해야 한다는 특성입니다.
            고립성(Isolation)은 트랜잭션 수행시 다른 트랜잭션의 작업이 끼어들지 못하도록 보장하는 것을 말합니다.
            지속성(Durability)은 트랜잭션이 성공적으로 완료되었으면 결과는 영구히 반영되어야 한다는 것을 말합니다.
            또한 커밋이랑 롤백이라는 개념이 있습니다.
            커밋은 한 트랜잭션 내의 모든 쿼리가 성공하여 결과값을 디비에 적용하는 것을 말합니다.
            롤백은 트랜잭션 수행 시 문제가 발생하여 트랜잭션 이전으로 디비 상태를 변경하는 작업을 말합니다.
        </p>
    </div>
</details>

#### Q. Spring @Transactional의 propagation에 대해 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            특정 트랜잭션 동작 도중 또다른 트랜잭션을 호출하는 상황에서 기존 트랜잭션을 어떻게 동작시킬 것인지 결정하는 방식입니다.
            REQUIRED, REQUIRES_NEW, NOT_SUPPORTED 등이 있습니다.
            REQUIRED는 트랜잭션이 없으면 새로 생성하고, 이미 시작된 트랜잭션이 있으면 해당 트랜잭션을 계속해서 사용하는 옵션입니다.
            REQUIRES_NEW는 항상 새로운 트랜잭션을 시작하는 옵션입니다. 즉, 이전에 시작되어 실행중인 트랜잭션에 상관없이 항상 새로운 트랜잭션을 만들어 시작시킵니다.
            NOT_SUPPORTED는 현재 진행중인 트랜잭션이 있어도 사용하지 않습니다. 여러 메서드 동작 시 특정 메서드만 트랜잭션 적용을 제외시킬때 사용됩니다. (이메일 예시)
        </p>
    </div>
</details>

### Q. 트랜잭션의 Isolation level에 대해 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            여러 트랜잭션을 순차적으로 수행시킨다면 성능이 매우 안좋을 것입니다.
            즉, 여러 트랜잭션들을 동시에 수행시키면서 데이터의 정합성을 유지시킬 수 있는 적절한 격리 수준이 필요합니다.
            이러한 격리 수준으로 READ-UNCOMMITTED, READ-COMMITED, REPEATABLE-READ, SERIALIZABLE 총 4가지 level이 있습니다.
            READ-UNCOMMITTED는 커밋 전의 트랜잭션의 데이터 변경 내용을 다른 트랜잭션이 읽는 것 허용합니다.
            여기서는 dirty read, non-repeatable read, panthom read 발생할 수 있습니다.
            dirty read는 이전 트랜잭션에 의해 수정된 됐지만 아직 커밋되지 않은 데이터를 이후 트랜잭션에서 읽는 것을 말합니다. 
            이 상황에서 이전 트랜잭션이 롤백된다면 이후 트랜잭션에서 읽은 데이터는 비일관된 상태에 놓여 문제가 발생할 수 있습니다.
            READ-COMMITTED는 커밋이 적용된 변경 데이터만 다른 트랜잭션에서 조회 가능합니다.
            커밋이 반영되지 않은 변경 데이터에는 다른 트랜잭션이 접근할 수 없습니다.
            여기서는 non-repeatable read와 panthom read가 발생할 수 있습니다.
            non-repeatable read는 한 트랜잭션 내에서 select 결과가 다르게 나오는 데이터 불일치 문제를 말합니다.
            REPEATABLE-READ는 트랜잭션 범위 내에서 조회한 내용이 항상 동일함을 보장합니다.
            한 트랜잭션이 조회한 데이터는 트랜잭션이 종료될 때까지 다른 트랜잭션이 변경하거나 삭제할 수 없는 격리 수준입니다.
            여기서는 panthom read가 발생할 수 있습니다.
            phantom read는 non-repeatable read의 한 종류로 해당 쿼리 결과에 행이 추가로 읽히는 문제를 말합니다.
            SERIALIZABLE은 한 트랜잭션에서 사용하는 데이터를 다른 트랜잭션에서 접근 불가합니다.
            트랜잭션의 ACID 성질이 모두 엄격하게 지켜지는 level이나 성능저하의 문제가 발생합니다.
        </p>
    </div>
</details>

### Q. mysql의 join의 종류와 각각을 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
           inner, left outer, full outer join이 있습니다.
           inner join은 A테이블과 B테이블이 공통으로 가진 데이터를 조회하는 join 입니다.
           left outer join은 A테이블의 데이터와 A,B 테이블의 공통 데이터를 조회하는 join 입니다.
           full outer join은 A테이블의 데이터와 B테이블의 데이터 그리고 A,B 테이블의 공통 데이터를 조회하는 join 입니다. 
        </p>
    </div>
</details>

### Q. User table에서 pk를 1부터 증가하는 auto_Increment로 설정했을 때 장단점을 설명해주세요. 
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            순차적으로 row가 생성되는 것을 알 수 있다는 장점이 있습니다.
            다만, 유저의 규모가 추측이 가능하고 데이터의 규모가 커졌을 때 불리할 수 있습니다.
            왜냐하면, pk를 기준으로 샤딩 시 부하가 한쪽으로 치우쳐질 수 있고 그로인해 특정 샤드에 부하가
            몰릴 수 있어 샤딩한 의미가 없게 될 수 있습니다. 
        </p>
    </div>
</details>

### Q. MYSQL에서 PK조회 성능은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            O(logN) 입니다.
        </p>
    </div>
</details>

### Q. 샤딩에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            샤딩이란 대량의 데이터를 분산 처리하기 위해 데이터베이스 테이블을 분할하여 물리적으로 서로 다른곳에 분산하여 저장하는 것을 말합니다.
            샤딩키를 기준으로 데이터가 분산되며, 샤딩키를 잘 지정하여 데이터가 한쪽 샤드로 몰리게 하는것을 막는 것이 중요합니다.
        </p>
    </div>
</details>

### Q. NoSQL이 무엇인지 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Not Only SQL의 약자로, 데이터를 처리하는 데에는 SQL 외에 다른 방법들도 있다는 의미 입니다.
        </p>
    </div>
</details>

### Q. RDB 대신 NoSQL을 쓰는 이유는 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            RDB는 트랜잭션을 이용해서 정교한 데이터 처리에 능숙하지만, 이런 정교함은 대량의 데이터를 관리하는데는 걸림돌이 될 수 있습니다.
            반면, NOSQL은 데이터의 일관성을 약간 포기한 대신 여러 대의 서버에 데이터를 분산하여 저장하는 scale out에 용이합니다.
            RDB 내에서는 기본적으로 분산처리, sharding/re-balancing, 데이터 복제/자동 복구와 같은 기능등을 제공하지 않습니다.
            물론, RDB 내에서 서드 파티 도구들로 위의 기능들을 수행할 수도 있겠지만, RDB로 이미 구성된 샤드 클러스터에 샤드를 추가하여 re-balancing 작업을
            수행한다던지, 로드를 분산시키는 작업들은 많은 노력과 고민이 필요할 수 있습니다.
            반면, 대부분의 일반적인 NoSQL은 내부적으로 분산처리, sharding/re-balancing, replica 등의 기능을 제공합니다.
            그러므로, 엄청난 양이 생성되지만 한번 저장되고 난 뒤에는 수정될 일이 거의 없어
            데이터의 일관성을 보장할 필요가 없는 가령, read/write만 수행하는 로그 같은 데이터를 처리한다면, 
            NoSQL은 좋은 대안이 될 수 있습니다.
        </p>
    </div>
</details>

### Q. MongoDB가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            몽고디비는 schema-less한 document 형식의 데이터를 다루는 NoSQL database입니다.
        </p>
    </div>
</details>

### Q. MongoDB의 장점?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            몽고디비의 document는 schema-less 하기 때문에 유연한 동적 데이터 저장이 가능하다는 장점이 있습니다.
            또한, secondary-index를 지원하여 많은 index를 설정할 수 있고, compound-index를 지원합니다.
            compound-index란 document 내의 여러 개의 field를 조합한 index인데 compound-index로 지정한 field의 순서에 맞게 조회 조건을
            걸어주면 index-scan을 할 수 있어 일반적으로, 높은 성능의 read가 가능합니다.
            또한, 기본적으로 Replication을 통한 High Availability를 제공하며 Auto-Sharding을 통한 높은 확장성을 제공합니다.
        </p>
    </div>
</details>

### Q. MongoDB의 단점?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            메모리 사용량이 크며 메모리 양에 따라 성능이 좌지우지 됩니다.
            메모리가 가득 찰 시 page fault가 발생하고 page fault가 발생하면, page를 memory와 disk 사이에 switching하는 
            현상이 일어나기 때문에, disk IO가 발생하고, 성능 저하를 유발하게 됩니다.
            또한, MongoDB는 데이터 write 시 document의 field가 같이 write되어 비효율적으로 데이터가 저장된다는 단점이 있습니다.
            예를들어, name 이라는 field를 가진 document가 10000개 write된다고 가정한다면 name이라는 field가 10000번 중복되어
            저장됩니다. 이처럼 mongodb는 동일 field를 같는 document 저장 시 비효율적인 저장이 될 수 밖에 없다는 단점이 있습니다.
            'ex) ({birthday:19920101} {birthday:19000202} {birthday: 18880303})'
        </p>
    </div>
</details>

### Q. MongoDB에서 schema-less하다는 의미가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            사용할 필드를 미리 정의하지 않고 언제든지 필요한 시점에 데이터를 저장할 수 있는 것을 의미합니다.
            다만, MongoDB는 다른 NoSQL DB들과는 다르게 secondary-index를 생성할 수 있는데, MongoDB의 secondary-index는
            schema-less가 아니라 항상 먼저 해당 인덱스를 구성하는 필드를 정의해야 한다는 특징이 있습니다.
        </p>
    </div>
</details>

### Q. MongoDB의 replica-set은 몇 개로 이루어져 있으며 왜 그렇게 이루어져 있나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
           레플리카셋은 홀수 멤버로 유지하는 것이 좋습니다.
           그 이유는 동일 high-availability 수준을 유지하는데 필요한 멤버의 수가 홀수일 때보다 짝수일 때 더 많이 필요하기 때문입니다.
           예를 들어, 4대로 구성된 레플리카 셋은 두개의 멤버에 장애가 발생하면 프라이머리를 선출하지 못하는데 
           3대로 구성된 레플리카 셋도 마찬가지로 두개의 멤버에 장애가 발생하면 프라이머리를 선출하지 못하기 때문입니다.
           그래서 만약에 짝수 멤버가 필요한 경우라면 아비터를 투입해서 투표 가능 멤버는 홀수가 하는데 좋습니다.
        </p>
    </div>
</details>

### Q. ElasticSearch의 키워드 검색과 RDB의 %LIKE% 검색의 차이점이 뭘까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            elasticsearch는 inverted index 방식으로 데이터를 저장하기 때문에 O(1) 만에 특정 키워드 검색이
            가능합니다. 하지만 RDB의 LIKE는 문자열 전체를 탐색해야 하기 때문에 특정 row에서 특정 키워드를 찾아내는데 
            O(N)의 시간이 걸립니다.
        </p>
    </div>
</details>

### Q. 클러스터링 인덱스, 넌클러스터링 인덱스에 대해 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 낙관적 락과, 비관적 락에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            낙관적인 락은 트랜잭션 내에서 데이터 갱신 시 충돌이 발생하지 않을 것으로 가정하여 별도 락을 걸지 않는 방식입니다.
            낙관적인 락은 DB 수준에서 거는 락이 아닌, 애플리케이션 수준에서 락을 처리하는 방식입니다.
            그래서 트랜잭션을 커밋하기 전까지는 트랜잭션의 충돌 여부를 알 수 없다는 특징이 있습니다.
            또한, 트랜잭션을 커밋하기 직전에 충돌이 났다는 것이 확인되면 이전의 작업을 모두 롤백 해야하는 특징이 있습니다.
            JPA에서는 낙관적인 락을 구현하기 위해 @Version이라는 어노테이션을 제공합니다.
            @Version을 사용하면, 엔티티를 수정할 때마다 버전이 하나씩 자동으로 증가합니다.
            만약, 두 개의 트랜잭션에서 동일한 데이터를 조회한 상황이라고 가정하겠습니다.
            한 트랜잭션이 먼저 조회한 데이터를 수정하고 커밋을 완료하면 버전도 자동으로 증가합니다.
            이후, 또 다른 트랜잭션에서도 마찬가지로 조회한 데이터의 값을 수정하고 커밋을 시도할 때, 버전 정보가 맞지 않아 Exception을 발생시킵니다.
            반면, 비관적인 락은 트랜잭션의 충돌이 발생한다고 가정하고 우선 락을 걸고보는 방식입니다.
            데이터 갱신시 충돌이 발생할 것이라고 미리 예상하기 때문에 조회를 할때부터 우선적으로 락을 거는 방식입니다.
            비관적인 락은 DB 수준에서 거는 락이며 DB가 제공하는 락 기능을 통해 구현할 수 있습니다.
            대표적으로 select for update문이 있습니다.
            select for update문은 한 트랜잭션 내에서 업데이트 대상 row에 접근 할 때마다 lock을 걸어 다른 트랜잭션에서의 접근을 막는 row 수준의 rock 
            방식입니다.
            즉, 비관적인 락은 낙관적인 락보다 데이터 일관성 문제를 잘 해결할 수는 있지만, 오버헤드가 크고 애플리케이션 성능에 치명적인 악영향을 줄 수 있습니다.
            그렇기 때문에 어느 한 방식이 무조건 옳다고 말할 수 없습니다. 
            트랜잭션간의 동시성 문제로 인한 충돌이 자주 일어나는 상황인지, 해당 데이터에 대한 읽기와 수정하기의 비율중 어떤 것이 높은지에 
            따라 상황에 맞게 두 방식 중 적절한 방식을 선택하는 것이 중요합니다.
        </p>
    </div>
</details>

### Q. flyway DB가 무엇이고 왜 사용하는 걸까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            flyway를 사용하는 이유는 무엇일까요?
            먼저 flyway는 오픈소스 데이터베이스 마이그레이션 도구 입니다.
            또한, flyway는 데이터베이스 형상관리 도구 입니다.
            그렇다면 flyway, 왜 쓰는 걸까요?
            첫번째 이유는 실수 방지 입니다.
            배포환경이  local, dev, prod… 등등 다양한 상황에서, 사람이 직접 DB schema 변경사항을 다룬다면 번거롭고 실수하기 딱 좋습니다.
            flayway를 이용하면 DB schema 변경 작업을 자동화(변경사항에 대한 script만  버전업 하여 작성하면 됨)하여 위의 문제를 방지할 수 있습니다. (휴먼에러 방지)
            두번째 이유는 히스토리 관리 입니다.
            각 버전별로 변경 이력들을 남겨놓기 때문에, 언제 어떤 DB 내역이 바뀌었는지 쉽게 파악할 수 있습니다.
            이를 통해, 문제가 생겼을 때 에러의 원인을 보다 쉽게 찾을 수 있을 것입니다.
            세번쨰 이유는 환경 분리 수월 입니다.
            배포환경이 local, dev, prod와 같다고 했을때, local 환경에서만 seed 데이터를 넣는다던지 (repeatable) 각 배포환경마다 배포된 DB 종류에 따라 분리하여 형상관리하는 기능들을 제공합니다.
        </p>
    </div>
</details>

# 운영체제

### Q. 프로세스와 쓰레드는 어떤 차이가 있으며, 쓰레드는 왜 써야 할까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프로세스는 메모리에 적재되어서 실행되고 있는 프로그램 입니다.
            그에반해, 쓰레드는 프로세스 안에서 실행되는 하나의 실행 흐름을 말합니다.
            프로세스는 운영체제로부터 자원을 할당 받아 실행됩니다.
            쓰레드는 한 프로세스 내에서 해당 프로세스의 자원을 공유하면서 병렬적으로 실행됩니다.
            쓰레드는 프로세스에 비해 낮은 컨텍스트 스위칭 비용을 가집니다.
            그리고 프로세스를 여러개 띄우는 것보다, 하나의 프로세스에서 여러 쓰레드를 생성하는 것이 메모리를 더 절약할 수 있습니다.
            또한 프로세스에 비해 작업들 간 통신 비용을 절감시킬 수 있습니다.
            그렇기 때문에 쓰레드를 사용합니다.
        </p>
    </div>
</details>

### Q. 멀티 프로세싱, 멀티 스레딩에 대해서 설명하세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            멀티 프로세싱은 두개 이상, 다수의 프로세서(CPU)가 협력적으로 작업을 동시에 처리하는 것을 의미합니다.
            즉, 여러 개의 프로그램들을 병렬로 처리할 수 있는 것을 말합니다.
            멀티 프로그래밍은 특정 프로세스 A에 대해서 프로세서가 작업을 처리할때 낭비되는 시간동안 다른 프로세스를 처리하도록 하는 것입니다.
            즉, 멀티 프로그래밍 은 프로세서의 자원이 낭비되는 것을 최소화하기 위한 것입니다.
            멀티 태스킹은 다수의 Task를 운영체제의 스케줄링에 의해 번갈아 가면서 수행하는 것입니다.
            프로세서가 각각의 Task를 조금씩 자주 번갈아가면서 처리하기 때문에 사용자는 마치 동시에 여러 Task가 수행되는 것처럼 보이게 됩니다.
            즉, 멀티 태스킹은 일정하게 정해진 시간동안 번갈아가면서 각각의 Task를 처리하는 것입니다.
            멀티 스레딩은 하나의 프로세스를 여러 개의 스레드끼리 공유하는 것을 뜻합니다.
            멀티 쓰레딩의 장점으로는 자원을 공유하여 메모리에 대한 효율성을 가져올 수 있다는 점이 있습니다.
        </p>
    </div>
</details>

### Q. 데드락이란 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            여러개의 스레드 혹은 프로세스가 하나의 자원을 할당받기위해 무한정 대기하는 상태를 말합니다.
        </p>
    </div>
</details>

### Q. 데드락 발생조건은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            상호배제(mutual exclusion), 점유 및 대기(hold-and-height), 비선점(no-preemption), 순환대기(circular-wait) 입니다.
            상호배제는 한번에 한개의 프로세스만이 공유 자원을 사용할 수 있어야 한다는 조건입니다.
            점유 및 대기는 최소한 하나의 자원을 점유하고 있으면서 다른 프로세스에 할당되어 사용되고 있는 자원을 추가로 점유하기 이해 대기하는 프로세스가 있어야 한다는 조건입니다.
            비선점은 다른 프로세스에 할당된 자원은 사용이 끝날 때까지 강제로 빼앗을 수 없어야한다는 조건입니다.
            순환대기는 공유자원과 공유자원을 사용하기 위해 대기하는 프로세스들이 원형으로 구성되어 있어 자신에게 할당된 자원을 점유하면서 앞이나 뒤에 있는 프로세스의 자원을 요구해야 합니다.
        </p>
    </div>
</details>

### Q. 데드락 해결방법은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            예방, 회피, 탐지와 복구의 방법이 있습니다.
            예방은 교착상태의 필요조건을 부정함으로써 교착상태가 발생하지 않도록 예방하는 방법입니다.
            교착상태 발생의 네가지 조건 중에서 어느 하나를 제거함으로써 수행가능합니다.
            회피는 교착상태 가능성을 배제하지 않고 적절하게 피해나가는 방법입니다.
            대표적으로 뱅커스 알고리즘이 있습니다.
            탐지는 교착상태 발견 기법은 시스템에 교착상태가 발생했는지 점검하여 교착상태에 있는 프로세스와 자원을 발견하는 것을 의미합니다.
            대표적으로 자원 할당 그래프가 있습니다.
            복구는 교착상태를 일으킨 프로세스를 종료하거나 교착상태의 프로세스에 할당된 자원을 선점하여 프로세스나 자원을 회복하는 것을 의미합니다.
        </p>
    </div>
</details>

### Q. context switch에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            core를 점유하지 못한 프로세스/스레드들이 queue에서 대기하고 있다가 core를 점유하기 위해 core를 점유하고 있던 
            프로세스/스레드와 core 점유를 바꾸게 되는데 이것을 context switching 이라고 합니다.
            코어점유가 계속 바뀌니까 스레드수가 코어수보다 많아도 동시에 스레드를 처리 할 수 있습니다.
            다만, 스레드가 너무 많아지면 context switching도 많아져서 그에 따른 비용 문제가 발생할 수 있습니다.
        </p>
    </div>
</details>

### Q. 가상 메모리에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프로세스 전체가 메모리 내에 로딩되지 않더라도 실행이 가능하도록 하는 기법을 말한다.
            즉, 프로그램이 CPU에 의해 실제로 사용되는 부분만 메모리로 로드하고, 사용되지 않는 부분은 디스크로 옮겨서 물리 
            메모리를 대체하도록 하는 것을 말합니다.
            가상 메모리로 저장되는 영역을 스왑영역이라 하며, 프로세스를 쪼갠 단위를 페이지 라고 합니다.
            또한, 필요한 페이지만 물리 메모리에 올리는 것을 Demanding Paging(요구 페이징) 이라고 합니다.
            그리고, 물리 메모리가 가득 찬 상황에서 swap 영역의 페이지를 요구하는 상황을 가리켜 페이지 부재라고 하며,
            이때, 물리 메모리에 로딩된 페이지를 가상 메모리의 swap 영역으로 옮기는 작업을 swap out 이라고 합니다.
            페이지 부재 발생 시 어떤 페이지를 swap out 할 것인지 결정하는 알고리즘을 페이지 교체 알고리즘 이라고 하며,
            대표적으로 FIFO, LRU 등이 있습니다.
        </p>
    </div>
</details>

# 네트워크

### Q. 웹이란 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            인터넷에 연결된 컴퓨터를 통해 사람들이 정보를 공유할 수 있는 전 세계적인 정보 공간을 말합니다.
        </p>
    </div>
</details>

### Q. server와 client가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            한 컴퓨터가 네트워크로 연결된 다른 컴퓨터로 무언가 서비스를 해줄때 서비스를 해주는 주체를 server,
            서비스를 받는 주체를 client라고 합니다.
        </p>
    </div>
</details>

### Q. API란 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            API는 Application Programming Interface의 약자로, 애플리케이션에서 일종의 소프트웨어나 플랫폼에서 제공하는 서비스 혹은 기능에 접근하기 위한 수단 입니다.
            즉, API는 누구나 쉽게 사용할 수 있도록 모듈화하여 만들어진, 특정 기능을 제공하는 인터페이스 입니다.
            API는 어떤 소프트웨어에서 다른 소프트웨어를 제어하기 위해 미리 약속된 규약을 의미합니다.
        </p>
    </div>
</details>

### Q. URI와 URL의 차이는 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            URI는 네트워크 상의 리소스를 식별하기 위한 문자열 전반을 나타냅니다.
            URL은 네트워크 상의 구체적인 리소스 위치를 나타냅니다.
            즉, URL는 URI의 한 형태로, 바꿔 말하면 URI는 URL을 포함 하는 개념입니다.
            예를들어 https://www.abcd.com/group는 URI 혹은 URL 입니다.
            https://www.abcd.com/group?groud_id=3는 URI 입니다.
        </p>
    </div>
</details>

### Q. 프로토콜이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            네트워크 상의 기기가 상호간에 통신하기 위해서는 서로 같은 방법으로 통신해야 합니다.
            즉, 서로 다른 플랫폼을 가지고 네트워크를 통해 서로 통신하기 위해서는 
            규칙이 필요하게 되는데 이러한 규칙을 프로토콜이라고 합니다.
        </p>
    </div>
</details>

### Q. http가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            인터넷상에 존재하는 서버와 클라이언트간에 데이터를 교환하기 위한 프로토콜, 통신규약입니다.
            HTTP는 TCP/IP 기반으로 한 지점에서 다른 지점(보통 클라이언트와 서버)로 요청과 응답을 전송합니다.
            HTTP는 먼저 클라이언트가 request를 서버에 보내면, 서버는 클라이언트에게 요청에 맞는 
            response를 보내고 접속을 끊는 connectionless한 특성이 있습니다.
            또한, 연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보는 유지하지 않는 stateless한 특성이 있습니다.
        </p>
    </div>
</details>

### Q. 인터넷 상에서 클라이언트/서버의 통신과정에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            1. 클라이언트는 DNS 서버를 통해서 www.naver.com의 IP 주소를 얻습니다.
            2. 클라이언트는 애플리케이션(HTTP) 계층에서 얻은 IP주소를 목적지로 하여 알맞는 HTTP 요청 메세지를 작성합니다. (이때, HTTP 메서드는 get 방식)
            3. 클라이언트는 서버와 TCP connection을 만들기 위해 3-way-handshaking 작업을 수행합니다.
            4. connection이 만들어 지면 클라이언트는 서버에게 HTTP 요청 메세지를 보내는데 해당 메세지는 패킷단위로 쪼개져서 인터넷을 라우팅하며 서버로 전송됩니다.
            5. 서버는 전송계층(TCP)에서 패킷을 수신하고 조립합니다.
            6. 서버는 클라이언트의 요청에 맞는 자원이 존재하는지 파악하여 존재한다면 200 상태코드 존재하지 않는다면 
               404 상태코드를 넣어 HTTP 응답 메세지를 작성합니다.
            7. 서버는 클라이언트에게 역방향으로 HTTP 응답 메세지를 전송합니다.
            8. 클라이언트에서 서버의 응답 메세지를 받으면 TCP connection을 끊기위해 4-way-handshaking 작업을 수행하여 connection을 끊습니다.
            9. 클라이언트는 서버로부터 받은 HTTP 응답 메세지를 브라우저에 띄웁니다.
        </p>
    </div>
</details>

### Q. 쿠키와 세션에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            쿠키와 세션모두 http의 stateless한 한계를 극복하기 위한 기술입니다.
            쿠키는 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일입니다.
            클라이언트 로컬에 저장되기 때문에 변조하거나 request에서 스나이핑당할 우려가 있어서 보안이 취약합니다.
            만료시간은 있지만 파일로 저장되기 때문에 브라우저를 종료해도 계속해서 정보가 남아 있을수 있습니다.
            세션이란 서버에 저장하는 상태 정보입니다.
            세션 아이디는 웹 브라우저 당 1개씩 생성되며 서버내에 저장됩니다.
            세션은 만료기간을 정할수는 있지만 브라우저가 종료되면 그에 상관없이 삭제됩니다.
            쿠키를 이용해서 세션id만 로컬에 저장하고 그것으로 구분해서 서버에서 처리하기 때문에 
            쿠키보다는 비교적 안전합니다.
            (쿠키/세션 동작방식 그림설명)
        </p>
    </div>
</details>

### Q. 서버간 세션 불일치를 해결할 수 있는 방법에는 어떤 것들이 있으며, 각각의 장단은 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Sticky Session, 톰캣의 Session Clustering, 별도의 세션 저장소를 두는 방법이 있습니다.
            Sticky Session은 처음 클라이언트의 요청을 처리한 서버가 이후에도, 그 클라이언트의 요청을 담당하는 방식입니다. 특정 서버에 트래픽이 몰리는 이슈가 발생할 수 있습니다.
            톰캣의 Session Clustering 방법이 있습니다. all-to-all 방식으로 해당 서버에 저장된 session을 다른 서버에 전파하는 방식입니다. 
            트래픽이 분산되는 효과가 있습니다.
            모든 서버에 동일한 세션 리스트가 저장되기 때문에, 메모리를 효율적으로 사용하는 방식이 아닙니다.
            세션 변경이 일어날 때마다 세션을 전파하는 작업이 일어나므로 네트워크 트래픽 비용이 추가적으로 발생합니다.
            별도의 세션 저장소를 두는 방법이 있습니다.
            세션을 저장할 저장소를 별도로 구축하는 방법입니다.
            트래픽이 한 서버로 몰리는 문제를 해결할 수 있으며, 저장 공간을 효율적으로 사용할 수 있습니다.
            또한, 각 서버들 간의 동기를 맞추기 위한 추가적인 네트워크 비용도 발생하지 않습니다.
            다만, 별도의 저장소를 구축해야 한다는 점에서 관리포인트가 늘어날 수 있고, SPOF이 되어 해당 저장소에 이슈가 생길 시 해당 이슈가 모든 서버로 전파될 우려가 있습니다.
        </p>
    </div>
</details>

### Q. TCP/IP에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            인터넷과 관련된 프로토콜을 모은 집합입니다.
            애플리케이션, 트랜스포트, 데이터링크, 링크 계층 이렇게 4계층으로 나뉘어져 있습니다.
            애플리케이션 계층은 유저에게 제공되는 애플리케이션에서 사용하는 통신의 움직임을 결정합니다. FTP, DNS, HTTP 등이 여기 포함됩니다.
            트랜스포트 계층은 애플리케이션 계층에 네트워크로 접속되어 있는 2대의 컴퓨터 사이의 데이터 흐름을 제공합니다.
            여기에는 TCP가 있습니다.
            네트워크 계층은 네트워크 상에서 패킷의 이동을 다룹니다.
            여기서 패킷이란 전송하는 데이터의 최소단위를 말합니다.
            그리고 어떠한 경로를 라우팅(택배와 비슷)하여 상대의 컴퓨터까지 패킷을 보낼지 결정합니다.
            링크 계층은 네트워크에 접속하는 하드웨어적인 면을 다룹니다.
            디바이스 드라이버와 네트워크 인터페이스 카드(NIC), 케이블 등과 같은 물리적으로 보이는 부분을 포함합니다.
        </p>
    </div>
</details>

### Q. TCP (Transfer Control Protocol)에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            높은 신뢰성을 보장하는 연결형 프로토콜 입니다.
            트랜스포트 계층에 해당하며, 인터넷에서 사용되는 프로토콜 입니다.
            3way,4way handshaking을 통해 client/server 간 연결을 생성하고 종료합니다. (그림설명)
            데이터의 흐름 제어 및 혼잡 제어를 담당합니다.
            흐름제어는 데이터를 송신하는 곳과 수신하는 곳의 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지하는 것입니다.
            혼잡제어는 네트워크 내의 패킷 수가 넘치지 않도록 방지하는 것입니다.
        </p>
    </div>
</details>

### Q. UDP (User Datagram Protocol)에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            TCP와 달리 비연결형 프로토콜입니다. 트랜스포트 계층에 해당합니다.
            신뢰성이 낮지만 TCP보다 속도가 빠릅니다.
            스트리밍 서비스 환경에 유리합니다.
        </p>
    </div>
</details>

### Q. Rest API에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            REST는 Representational State Transfer라는 용어의 약자로서 소프트웨어 프로그램 개발 아키텍처의 한 형식입니다.
            REST는 URI로 잘 표현된 리소스에 대한 행위를 HTTP Method로 정의하는 방식
            rest의 구성 요소로는 자원 (Resource), 행위 (Verb), 표현 (Representations)이 있습니다.
            REST API는 REST 라는 형식의 API 입니다.
            REST가 필요한 이유는 각 요청이 어떤 리소스에 어떤 동작을 위한 것인지 그 요청의 모습 그자체로 추론이 가능하기 때문에 협업에 용이합니다.
            그리고 다양한 클라이언트가 등장함에따라 Backend 하나로 다양한 Device를 대응하기 위해 REST가 더욱 더 필요하게 되었습니다.
            RESTful이란 REST 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭합니다.       
        </p>
    </div>
</details>

### Q. REST의 행위는 http의 어떤 메서드와 매칭되나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            자원에 대한 조회는 GET, 수정은 PUT, 삭제는 DELETE로 표현합니다. 또한 특정 자원의 추가는 POST로 표현합니다.
            이때 멱등성이라는 개념이 적용되는데, 멱등성은 같은 연산을 여러번 적용하더라도 결과가 달라지지 않는 성질을 말합니다.
            GET, PUT, DELETE는 같은 조건으로 연산을 여러번 적용해도 결과가 변하지 않기 때문에 멱등성을 가집니다.
            그러나 POST는 연산을 적용할때마다 결과가 변하기 때문에 멱등성을 갖지 않습니다. 
        </p>
    </div>
</details>

### Q. sync, async, blocking I/O, non blocking I/O에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            두 그룹은 비슷하게 동작하는 것처럼 보이지만, 관심사가 다릅니다. Synchrous, Asynchronous는 호출되는 함수의 작업 완료 여부를 누가 신경 쓰느냐가 관심사 입니다.
            호출하는 함수가 호출되는 함수의 작업 완료 후 리턴을 기다리거나, 또는 호출되는 함수로부터 바로 리턴 을 받더라도 작업 완료 여부를 호출하는 함수 스스로 확인하며 신경쓰면 Synchrous 입니다.
            그런데 호출되는 함수에게 callback을 전달해서, 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 callback을 실행하고, 호출하는 함수는 작업 완료 여부를 신경쓰지 않으면 Asynchrous 입니다.
            반면에 Blocking/NonBlocking은 호출되는 함수가 바로 리턴하느냐 마느냐가 관심사 입니다.
            호출된 함수가 바로 리턴해서 호출한 함수에게 제어권을 넘겨주고, 호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있으면 NonBlocking 입니다.
            그렇지 않고 호출된 함수가 자신의 작업을 모두 마칠 때까지 호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만든다면 Blocking 입니다.
        </p>
    </div>
</details>

### Q. latency, bandwidth에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            latency는 요청이 처리되길 기다리는 시간을 의미하며 ms 단위를 사용합니다.
            bandwidth는 네트워크나 데이터 전송 매체의 데이터 운반 능력을 말하며 단위 시간동안 한 지점에서 다른 지점으로 
            전달될 수 있는 최대 데이터 양을 의미합니다. bps 단위를 사용합니다.
        </p>
    </div>
</details>

### Q. https가 무엇이며 어떻게 동작하나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            https는 http의 보안문제를 보완하기 위해 나온 프로토콜입니다.
            먼저, client는 임의의 랜덤값을 생성해 server로 보내줍니다.
            다음으로, server는 임의의 랜덤값을 생성해 CA의 개인키로 암호화돼있는 인증서와 함께 client에게 응답합니다.
            다음으로, clienet는 server로 부터 받은 인증서를 브라우저에 내장돼있는 CA의 공개키로 복호화 하여 server의 공개키를 얻습니다.
            다음으로, client는 자신이 생성했던 랜덤값과 서버로 부터 응답받은 랜덤값을 조합해 새로운 대칭키를 만듭니다.
            다음으로, client는 새로 만든 대칭키를 server의 공개키로 암호화하여 server에게 보내줍니다.
            다음으로, server는 자신의 개인키로 client로 부터 받은 암호문을 복호화하여 대칭키를 얻습니다.
            다음으로, client는 http 메세지를 새로만든 대칭키로 암호화 하여 server에게 보내줍니다.
            마지막으로, server는 암호화된 http 메세지를 client로 부터 받은 대칭키로 복호화하여 http 메세지를 얻고 연결을 종료합니다.
        </p>
    </div>
</details>

### Q. keepAlive에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            TCP connection을 끊지않고 유지시켜 재사용하는 기법입니다.
            즉, Handshake 과정이 생략되므로 성능 향상을 기대 할 수 있습니다.
            그러나 요청이 많은 서버 환경에서 Keep Alive 기능을 사용할 경우 모든 요청 마다 연결을 유지해야 하기 때문에
            오히려 connection을 유지하는데 드는 비용이 커져 서버의 부하가 커지고, 성능이 하락할 수 있습니다.
            그렇기 때문에 요청이 많이 발생하는 대용량 서비스에서는 사용 시 문제가 발생할 수 있습니다.
            ex) timeout=5, max=100 - 하나의 연결을 5초 동안 유지. 최대 100개의 connection 까지 허용
        </p>
    </div>
</details>

### Q. 로드밸런싱 알고리즘 아시는 거 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            알고있는 로드밸런싱 방식으로는 round-robin, hashing by source IP, least connections이 있습니다.
            round-robin은 순차적으로 돌아가며 골고루 여러 서버에 부하를 분산시키는 방법입니다.
            hashing by source IP는 사용자의 IP를 Hashing하여 부하를 분배하는 방식으로 동일한 IP라면 항상 같은 서버로 연결되는 것을 
            보장하는 기법입니다.
            least connections는 현재 각 서버들에서 open된 세션을 고려한 다음, open된 세션이 가장 적은 서버쪽으로 세션을 연결 하는 기법입니다.
        </p>
    </div>
</details>

### Q. OSI 7계층에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
          OSI 7계층은 네트워크에서 통신이 일어나는 과정을 7계층으로 나눈 것을 말합니다.
          1계층인 물리계층은 데이터를 0, 1의 비트단위를 전기 신호로 바꾸어 신호를 주고받는 역할을하는 계층입니다.
          대표적인 장비로 통신 케이블, 허브 등이 있습니다.
          2계층인 데이터 링크계층은 물리계층을 통해 송수신되는 데이터의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할을 합니다.
          물리주소인 MAC 주소가 데이터 링크계층에 속합니다.
          이 계층에서 전송되는 단위를 프레임이라고 하고, 대표적인 장비로 스위치가 있습니다.
          3계층인 네트워크 계층은 IP주소를 제공하는 계층입니다. 데이터를 목적지까지 최적의 경로로 전달하는 라우팅 기능을 수행합니다. 
          데이터 전송 단위는 패킷입니다. 대표적인 장비로 라우터가 있습니다.
          4계층인 전송 계층은 종단 간(End to End) 데이터를 주고 받을 수 있게 하는 계층입니다.
          데이터 전송단위는 세그먼트 입니다.
          대표적으로 TCP, UDP 프로토콜이 전송계층에 포함됩니다.
          5계층인 세션 계층은 세션 생성, 유지, 종료 등의 기능을 수행합니다.
          세션은 데이터를 통신하기 위한 논리적인 연결을 말합니다.
          6계층인 표현 계층은 데이터의 변환, 압축, 암호화가 이루어지는 계층입니다.
          7계층인 응용 계층은 사용자 또는 애플리케이션이 네트워크에 접근할 수 있도록 사용자를 위한 인터페이스를 제공합니다.
          대표적으로 HTTP, FTP, SMTP, TELNET 등의 프로토콜이 응용 계층에 속합니다.
          이렇게 계층을 나누는 이유는 통신이 일어나는 과정을 단계별로 파악할 수 있기 때문입니다.
          또한, 7계층 중 특정한 곳이 이상이 생기면 다른 단계의 물리 장비 혹은 소프트웨어는 신경쓰지 않고 이상이 생긴 계층만 고치면 되기 때문입니다.
        </p>
    </div>
</details>

### Q. Connection Timeout과 Read Timeout에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            Connection Timeout은 종단 간에 3-way-handshaking을 통해 Connection을 생성 하는데 소요되는 최대 시간을 의미합니다. 이 시간을 넘기게 되면 연결 할 수 없는 것으로 판단하고 에러가 발생 합니다.
            Read Timeout은 연결된 종단 간에 데이터를 주고 받을 때 소요되는 최대 시간을 의미 합니다. 이 시간을 넘기게 되면 데이터를 받을 수 없는 것으로 판단하고 에러가 발생 합니다.
            이로 인해 클라이언트와 서버 간 싱크가 맞지 않아 문제가 발생할 확률이 높습니다.
        </p>
    </div>
</details>

### Q. 소켓이란 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            소켓이란 네트워크상에서 서버와 클라이언트가 특정 포트를 통해 양방향 통신이 가능하도록 만들어주는 소프트웨어 장치입니다.
            소켓 통신이란 클라이언트와 서버 양쪽에서 서로에게 데이터 전달을 하는 방식의 양방향 통신을 말합니다.
            스트리밍이나 실시간 채팅 등 실시간으로 데이터를 주고 받아야 하는 경우 connection을 끊는 HTTP 통신보단 소켓 통신이 적합합니다.
            단, 소켓 통신은 Connection을 지속적으로 유지하기 때문에 HTTP 통신에 비해 많은 리소스가 소모됩니다.
        </p>
    </div>
</details>

# 보안
### 대칭키와 공개키,개인키가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            대칭키는 암호화와 복호화 하는데 동일하게 사용되는 키입니다.
            다만, 대칭키는 해커가 가로채면 문제가 발생합니다.
            공개키(비대칭키)는 공개키로 암호화 한 암호문은 개인키로 복호화 하고 개인키로 암호화한 암호문은 
            공개키로 복호화 하는 기법입니다.
        </p>
    </div>
</details>

### CORS가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            CORS는 SOP로 인해 발생하는 불편함을 해소하기 위해 서로 다른 도메인간의 요청과 응답을 허용하는 것입니다.
            SOP(Same Origin Policy)란 브라우저가 스크립트에서 시작한 서로 다른 출처의 HTTP 요청을 제한하는 정책입니다.
            동일 출처라는 것은 Protocol, Host, Port가 같다는 것을 의미합니다.
            기존에는 하나의 출처/도메인에서 비즈니스로직을 처리하고 html을 렌더링하는 작업을 같이 하는것이 일반적이었다.
            그래서 SOP에 위배되지 않았습니다.
            하지만, 최근에는 frontend와 API서버간 서로 다른 도메인을 사용하는 상황이 늘었습니다.
            그래서 SOP때문에 불편한점들이 생기기 시작했습니다.
            이러한 불편함을 해결하기 위해 나온 기법이 CORS (Cross Origin Resource Sharing) 입니다.
        </p>
    </div>
</details>

### XSS가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            client가 조회하는 웹페이지에 악성 script를 심어놓아 client의 쿠키/세션 정보를 탈취하는 해킹기법입니다.
            client를 노리는 기법입니다.
            XSS 필터를 통해 예방할 수 있습니다.
        </p>
    </div>
</details>

### CSRF가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            client의 의도와는 무관하게 해당 client가 의도치 않은 요청을 server로 보내도록 하는 해킹기법입니다.
            server를 노리는 기법입니다.
            예를들어, 해커가 특정 웹사이트의 관리자에게 관리자의 비밀번호를 수정하는 URL을 심어놓은 메일을 전송합니다.
            웹사이트의 관리자는 의심없이 해당 메일을 열어보고 자기도 모르게 비밀번호를 수정하는 URL을 server로
            요청합니다. 이 과정에서 발생하는 해킹이 CSRF 입니다.
            서버로부터 CSRF 토큰을 client에게 발급해준 후, client는 DB 상태를 변경시킬 수 있는 POST, PUT, DELETE 요청 시 http 헤더에
            CSRF 토큰을 넣고, 그 토큰을 서버에서 검증함으로서 예방할 수 있습니다.
        </p>
    </div>
</details>

### SQL Injection이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            client가 요청으로 보낸 파라미터가 DB 쿼리에 이용되도록하여 쿼리를 조작하는 해킹기법입니다.
            JDBC preparedstatement를 사용하던가 JPA에서 native query를 이용할 때 parameter 바인딩을 하면 예방가능 합니다.
        </p>
    </div>
</details>

### 해시함수가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            해시 함수란 데이터의 효율적 관리를 목적으로 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수입니다.
            매핑 전 데이터 값을 key, 매핑 후 데이터 값을 hash value라 하고, 매핑하는 과정을 해싱이라고 합니다.
            또한 저장된 데이터의 양에 상관없이 데이터 하나를 저장하고 검색하는 것을 상수시간에 처리 하기위한 기법을 해시 테이블이라고 합니다.
            해시를 사용하면 데이터 조회, 추가 시 O(1) 성능을 보장받을 수 있습니다. 
            그리고 동일 key에 대한 해시값은 무조건 같습니다.
            다만, key가 달라도 해시값은 같을 수 있는데 이를 충돌이라고 합니다.
        </p>
    </div>
</details>

# 인프라/클라우드

### 무중단 배포 어떤거 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            blue-green과 rolling update에 대해 알고 있습니다.
            blue-green은 서버그룹을 쌍으로 구축하여 LB의 proxy_pass를 업데이트 버전의 서버그룹으로 번갈아가며 배포하는 방식
            이전 버전으로의 rollback이 쉽다는 장점이 있습니다.
            하지만 서버 구축 비용이 많이 든다는 단점이 있습니다.
            rolling-updates는 기존에 운영하던 서버를 하나씩 중단시키고 버전 업데이트 후 다시 배포하는 방식
            추가적인 서버 구축 비용이 없다는 장점이 있습니다.
            하지만 업데이트 시점에 배포되어있는 서버가 줄어들어 부하가 몰릴 수 있으며 버그 발생 시 이전 버전으로의 rollback이 어렵습니다.
            또한, 동일한 시점에 여러 버전이 공존할 수 있어 응답 결과가 요청마다 달라질 수 있습니다.
        </p>
    </div>
</details>

### devops가 무엇인지 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            소프트웨어 개발 방법론의 하나로, 개발(development)과 운영(operation)을 결합한 혼성어입니다.
            개발 담당자와 운영 담당자가 연계하여 협력하는 개발 방법론을 말합니다.
        </p>
    </div>
</details>

# Git

### rebase 무엇인지 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
          git에서 한 브랜치에서 다른 브랜치로 합치는 방법으로는 merge, rebase가 있습니다.
          그 중 rebase를 이용하면, 커밋 히스토리를 깔끔하게 유지하면서 브랜치를 병합할 수 있습니다.
          rebase는 말 그대로 브랜치 히스토리들의 베이스를 변경하는 방법입니다.
          베이스란, 브랜치가 분기되기 시작하는 시점의 마스터 브랜치의 HEAD를 베이스라고 합니다.
          리베이스는 기존의 커밋을 그대로 사용하는 것이 아니라 내용은 같지만 다른 커밋을 새로 만듭니다.
          그렇기 때문에, 모든 변경사항에 대한 히스토리를 남기고 싶다면 merge를, 그렇지 않고 커밋 히스토리를 깔끔하게 유지하고 싶다면 rebase를 사용하는 것이 좋습니다.
        </p>
    </div>
</details>

# 프로젝트

### 프로젝트 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            개인적으로 스프링 부트를 이용해 쇼핑몰 서비스를 제공하는 프로젝트를 개발하였습니다. 
            또한, 서비스를 개발하는 것으로 끝내는 것이 아니라 내가 만든 서비스에 대해 어떻게 하면 성능과 안정성을
            더 높일 수 있을 지에 대해 주도적으로 고민하였습니다. 결과적으로, 스프링 단일 서버 기준 약 900tps 까지 처리
            하는 서비스를 구축하였고, cloud 환경에서 auto scale out 할 수 있는 architecture를 구축하여 초당 
            수만 건의 요청도 처리할 수 있는 환경을 구축했습니다. 
            또한 테스팅 환경을 실시간으로 모니터링 할 수 있는 환경을 구축했으며, 
            서비스 내에서 발생하는 Log들을 실시간 모니터링 할 수 있는 환경을 구축했습니다.
        </p>
    </div>
</details>

### java, spring을 선택한 이유가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            spring은 기본적으로 IOC/DI, AOP, PSA 등을 지원하여 코드를 유연하고 확장성 있게 개발할 수 있도록 도와주고,
            개발자가 자신의 비즈니스 로직에만 집중하여 생산성을 높일 수 있도록 도와주기 때문에 사용했습니다.
            또한, java와 스프링은 검증된 다양한 기능들과 오픈소스 생태계를 지원합니다. 
            예를들어 spring은 다양한 하위 프로젝트들을 제공하며, spring batch나 spring security 등과 같은 spring의 
            하위 프로젝트들을 사용하게 되면 개발자 입장에서 신경써야 할 부분들이 훨씬 줄어들고 이를 통해 비즈니스 로직에 보다 
            더 집중하여 생산성을 높일 수 있습니다.
            이러한 장점들을 이용하기 위해 스프링을 선택했습니다.
        </p>
    </div>
</details>

### 서버가 느리다는 피드백을 받았을 때 어떻게 대처할 것인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            만약 특정 API에서 성능 저하가 발생했다면 해당 API에서 수행하던 쿼리의 실행계획
            을 파악한 후, index를 적용시키기 좋은 상황이라면 적용시킬 것 같습니다. 만약 이미 index가 적용돼있는 상황이라면 
            index가 의도한대로 잘 타고있는지 확인한 후 잘 타지 않는다면 index 설계를 다시 할 것 같습니다.
            또한, 해당 API에서 수행하는 쿼리가 캐싱을 하기 적절하다고 판단되는 쿼리가 있다면 메모리 캐시나 로컬 캐시를 적용해서 성능을 높일 것입니다.
            또한 만약 대량의 트래픽으로 인해 latency가 갑자기 높아진 상황이라면 서버를 scale out 하여 트래픽을 분산시킬 것입니다.
        </p>
    </div>
</details>

### 서버의 트래픽이 과도하게 많을 때 어떻게 대처할 것인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            캐싱할 수 있는 데이터를 memory db나 local에 캐싱하여 요청들을 빠르게 처리할 것입니다.
            그래도 트래픽이 과도하게 많다면, 서버를 scale out 시켜 트래픽을 분산시킬 것입니다.
            그리고 서버의 laytency와 tps를 파악할 수 있는 모니터링 시스템을 구축한 후
            한대 서버 기준 최대 tps를 파악해 scale out 시켜줘야 할 임계점을 찾을 것입니다.
            그 후 그 임계점을 초과하면 자동으로 서버를 scale out하는 auto scale out 시스템을 구축할 것입니다.
        </p>
    </div>
</details>

### TDD가 뭔지 아시나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            말그대로 테스트가 주도하는 개발 방법론을 의미합니다.
            TDD는 먼저 요구되는 새로운 기능에 대한 테스트를 작성하고 
            해당 테스트를 통과하는 가장 간단한 코드를 작성합니다.
            그리고 테스트가 통과되면 해당 코드를 리팩토링 하는 과정을 수행합니다.
            TDD를 행함으로써 개발하고 있는 코드의 문제점을 빠르게 잡아낼 수 있어 디버깅 시간을 줄일 수 있다는 장점이 있습니다.
            다만, 코딩량이 늘어나면서 생산성의 관점에서는 의문점이 발생할 수 있다는 단점이 있습니다.
        </p>
    </div>
</details>

### 단위 테스트를 왜 작성해야 할까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            단위테스트는 개발단계 초기에 버그를 발견할 수 있게 도와줍니다.
            또한, 단위 테스트는 개발자가 나중에 코드를 리팩토링하거나 라이브러리를 업그레이드 시킬 때
            기존 기능이 올바르게 동작하는지를 보장해줍니다.
        </p>
    </div>
</details>

### 왜 MQ로 kafka를 선택했나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            kafka는 메세지를 저장하는 하나의 토픽에 대해 여러 용도로 사용할 수 있기 때문입니다.
            일반적인 메세지 큐는 특정 컨슈머가 메세지를 소비하면 큐에서 메세지가 삭제되어 다른 컨슈머에서는
            가져갈 수 없는데, 카프카는 컨슈머가 메세지를 소비해도 해당 메세지를 삭제하지 않기 때문입니다.
            프로젝트에서 이런 카프카의 특징을 이용해서 하나의 메세지를 여러 컨슈머가 다른 용도로 사용할 수 있도록 시스템을 구성했습니다.
        </p>
    </div>
</details>

### 왜 Load Balancer로 nginx를 선택했나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            nginx는 event-driven 방식의 single thread process로 구성되어 가볍고, 
            비동기 처리를 통해 높은 성능을 보장합니다.
            즉, nginx는 적은 자원을 이용해 빠른 서비스를 보장해주기 때문에 선택했습니다.
        </p>
    </div>
</details>

### 비동기의 장점에는 무엇이 있을까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            장애나 과부하 등이 발생해 응답 속도가 느려지면, 동기 방식은 문제가 발생한 백엔드를 거치지 않는 요청까지도 
            함께 피해를 볼 수 있기 때문에 시스템 전반적인 장애로 번지게 되는 경우가 많습니다. 
            반면 비동기 방식은 문제가 발생한 백엔드를 거치지 않는 요청은 특별한 튜닝 없이도 깔끔하게 처리해 낼 수 있어 
            장애가 크게 번지지 않습니다.
        </p>
    </div>
</details>

### redis에서 key * 명령어를 사용하면 안되는 이유가 무엇일까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            redis의 keys는 모든 키의 내용을 출력하는 커맨드인데, 키가 많아지면, 키를 찾는데 시간 소요가 커질 수 있습니다.
            또한, redis는 single thread로 동작하기 때문에 keys * 명령 수행중에는 다른 작업을 하지 못하게 됩니다.
            그렇기 때문에, 성능적으로 keys * 명령어는 좋은 선택이 아닐 가능성이 높습니다.
            이런 문제를 해결하기 위한 방법이 scan 명령어를 사용하는 방법입니다.
            scan 명령어는 Keys처럼 한번에 모든 레디스 키를 읽어오는 것이아니라 count 값을 정하여 그 count값만큼 여러번 레디스의 모든 키를 읽어오는 것입니다.
            따라서 count의 개수를 낮게잡으면 count만큼 키를 읽어오는 시간은 적게 걸리고, 모든 데이터를 읽어오는데 시간이 오래걸리지만 그 사이사이 시간에 다른 요청들을 레디스에서 처리해줄 수 있을 것입니다.
        </p>
    </div>
</details>

# 손코딩
### Q. 스택
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 링크드리스트
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>

        </p>
    </div>
</details>

### Q. for문을 안쓰고 1-100까지 더하기
```java
package algorithm;

public class Test {

    private int sum(int n) {
        if (n == 100) {
          return n;
        }
        return n + sum(n + 1);
    }

    private int sum2(int n) {
        if (n == 1) {
          return 1;
        }
        return n + sum2(n - 1);
    }

    public static void main(String[] args) {
        Test test = new Test();
        System.out.println(test5.sum(1));
        System.out.println(test5.sum2(100));
    }
}
```

### Q. *, / 연산자 없이 곱하기, 나누기 연산 수행하기
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>