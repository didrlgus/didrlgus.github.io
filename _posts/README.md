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
            그 중, 대표적인 영역으로는 Method, Heap, Stack이 있습니다.
        </p>
        <p>
            Method 영역에는 멤버 변수의 이름, 데이터 타입, 접근제어자에 대한 field 정보와 메서드의 이름, 리턴 타입, 파라미터, 접근 제어자에 대한 정보,
            그리고 class 이름과 같이 class 정보들이 저장됩니다. 또한 static 으로 선언된 데이터들이 저장됩니다.
            Method 영역에 저장된 데이터들은 모든 스레드에서 공유할 수 있는 자원입니다.
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
            그다음 JVM 내에 있는 Execution engine이 runtime data area에 적재된 바이트 코드들을 기계어로 변경해 명령어 단위로 실행합니다.
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
            즉, reachable과 unreachable을 판단하는 과정을 의미합니다. 여기서 GC root가 될 수 있는 조건은 stack 영역의 지역변수나 파라미터들, method 영역의 static 변수들입니다.
            그리고 sweep는 unreachable한 객체들을 heap에서 제거하는 과정입니다. 
            sweep과정이 끝나면 compact 과정이 추가될 수 있는데 compact 과정은 heap에서 제거된 객체가 있던 메모리 공간으로 인해 생길 수 있는 메모리 단편화 문제를 막아주는 작업입니다.
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
            그리고 young gen은 다시 eden, survivor1, survivor2 영역으로 나뉩니다.
            GC의 동작과정에 대해서 말씀드리면 먼저 새로운 객체들이 eden 영역에 추가됩니다. 그리고 eden 영역이 가득차면 young gen을 대상으로 mark and sweep 작업이 수행되는데 이를 'minor gc'라고 부릅니다.
            'minor gc' 작업을 통해 reachable 한 객체는 살아남고 unreachable한 객체는 제거됩니다. 그리고 'minor gc' 작업을 통해 살아남은 reachable한 객체는 survivor1 또는 survivor2 영역중 한곳으로 이동합니다.
            이때, 객체가 survivor1과 survivor2에 공존하지 않고 어느 한 영역에만 존재합니다.
            그리고 survivor에 이동된 살아남은 객체는 age가 하나씩 추가됩니다. 위의 과정이 반복되면서 하나의 Survivor 영역이 가득 차게 되면 'minor gc'가 수행되고 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동시킵니다. 
            그리고 가득 이전 Survivor 영역은 아무 객체도 없는 상태로 비워둡니다.
            위의 과정을 반복하다 survivor에 있는 객체의 age가 특정 임계점에 다다르면 해당 객체는 old gen으로 이동되는데 이 과정을 promotion이라고 합니다.
            위의 모든 과정을 반복하면서 old gen이 가득차게 되면 'major gc' 작업이 수행됩니다.
        </p>
    </div>
</details>

### Q. 객체지향이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프로그램을 설계하는 개념이자 방법론입니다. 
            실세계에 존재하는 사물들을 객체라는 기본 단위로 나눕니다. 그리고 그 객체는 상태와 행위를 가지며 각 객체들은 서로 상호작용합니다.
            그리고 객체지향의 주요 특징으로는 클래스/인스턴스, 캡슐화, 상속, 추상화, 다형성이 있습니다.
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
            두번째로, 캡슐화라는 개념이 있습니다. 캡슐화는 외부에서 접근할 필요가 없는 멤버들을 private으로 지정하여 외부에 노출시키지 않는 것을 말합니다.
            세번째로, 상속이라는 개념이 있습니다. 상속은 특정 클래스의 변수와 메소드를 그대로 이어받아 기능을 확장시키는 것을 의미합니다.
            다음으로 추상화라는 개념이 있습니다. 추상화는 서로 연관있는 클래스간의 공통점을 찾아내서 공통의 조상을 만드는 작업을 말합니다.
            다음으로 다형성이라는 개념이 있습니다. 다형성은 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 하는 것을 말합니다. 
            또한 다형성은 여러 객체에게 동일한 명령을 내렸을 때 서로 다르게 반응하는 현상을 의미하기도 합니다.
            객체지향의 여러가지 특징을 잘 활용하면 유연하고 확장성있는 코드를 작성할수 있어 유지보수 비용을 최소화 시킬 수 있습니다.
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
            메서드 오버라이딩은 부모 클래스로부터 상속받은 메서드의 내용을 자식 클래스에서 변경하는 것을 의미합니다.
            오버라이딩은 부모 클래스의 메서드와 매개변수와 리턴타입이 같아야 한다는 조건이 있습니다.
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
            그리고 예외는 내부적으로 CheckedException과 UncheckedException 으로 나뉘는데,
            CheckedException은 프로그래머가 별도의 예외처리를 하지 않으면 컴파일 단계에서 오류를 발생시키는 예외이고,
            대표적으로 OutOfMemoryError가 있습니다.
            그리고 UncheckedException은 프로그래머가 별도의 예외처리를 하지 않아도 컴파일 단계에서 오류를 발생시키지 않는 예외입니다.
            대표적으로 RuntimeException이 있습니다.
            예외는 throws new 를 통해 발생 시킬 수 있으며, 예외를 처리하기 위해서는 try, catch 문이나 throw 키워드를 이용해 처리할 수 있습니다.
        </p>
    </div>
</details>

### Q. 자바의 final은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            final은 클래스나 멤버에 적용할 수 있는 keyword이고 어디에 적용하느냐에 따라 의미가 달라집니다.
            먼저, 클래스에 적용 시 해당 클래스를 상속받을 수 없습니다. 그리고 Primitive 변수에 적용 시 해당 변수의 값을 변경할 수 없습니다.
            그리고 Reference 변수에 적용 시 해당 referenct 변수가 힙(heap) 내의 다른 객체를 참조할 수 없습니다.
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

### Q. equals()와 hashcode()가 뭘까요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            equals()와 hashcode() 모두 Object 클래스에 정의된 메서드입니다.
            일반적으로 equals()는 객체의 내용이 동일한지 확인하는 동등성 비교를 위한 메서드입니다.
            hashcode()는 해싱(hashing) 기법에 사용되는 해시함수(hash function)를 구현한 것이고 메모리 주소에 대한 해시값을 반환합니다.
            HashMap, HashTable, HashSet, LinkedHashSet 등에서 key를 결정할때 hashcode()를 사용합니다. 
            즉, 각 인스턴스의 hashCode()의 결과가 같다면 동일한 key로 간주합니다.
            일반적으로 equals()가 true이면, 두 객체의 hashCode 값은 항상 같아야 한다는 규약이 있습니다.
            다만, equals() 메소드가 false 경우에는 두 객체의  hashCode값이 꼭 다를 필요는 없습니다.
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

### Q. String, StringBuffer, StringBuilder의 차이점에 대해서 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            String 객체는 immutable하기 때문에 지정된 문자열을 변경할 수 없지만 StringBuffer, StringBuilder 클래스는 인스턴스는 변경이 가능합니다.
            또한, StringBuffer, StringBuilder는 문자열을 변경할 수 있기 때문에 많은 문자열 연산을 요구하는 프로그램일 경우 String 클래스보다 
            메모리 공간을 훨씬 더 효율적으로 사용할 수 있다.
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
            mutable의 장점은 메모리 낭비를 막을 수 있다는 것입니다.
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
            또한, 람다식은 일급객체의 역할을 수행할 수 있어 메소드의 매개변수로 전달될 수도 있으며, 변수에 담거나, 메소드의 결과값으로 반환될 수도 있습니다.
            이를 통해, 자바에서도 함수형 프로그래밍이 가능합니다.
            기존의 불필요한 코드를 줄여주고, 작성된 코드의 가독성을 높여주기 위해 사용됩니다.
        </p>
    </div>
</details>

### Q. 스트림 API가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            스트림 API는 컬렉션이나 배열에 함수형 인터페이스 또는 람다식을 적용시켜 저장된 요소를 하나씩 참조하며 반복적으로 
            처리할 수 있도록 해주는 기능입니다.
            stream은 시작, 중간, 최종 연산으로 이루어져 있으며 Immutable 하다는 특징이 있습니다. 즉, 원본의 데이터를 변경하지 않습니다.
            또한, stream은 재사용할 수 없습니다.
            스트림 API 사용하면 for, if와 같은 불필요한 코딩을 걷어낼 수 있고 직관적이기 때문에 가독성이 좋아지고 실수의 여지를 줄여줍니다.
            또한 병렬처리가 가능해 빠른 처리가 가능합니다.
        </p>
    </div>
</details>

### Q. 스트림 API의 연산중에서 map이랑 flatmap의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            map은 단일 스트림 안의 요소를 원하는 특정 형태로 변환시켜주는 중간 연산 메서드입니다.
            flatMap은 스트림의 형태가 배열과 같을 때, 모든 원소를 단일 원소 스트림으로 반환시켜주는 중간 연산 메서드 입니다.
        </p>
    </div>
</details>

### Q. 접근제어자에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            접근 제어자란 클래스나 클래스 멤버의 선언 시 사용하여 부가적인 의미를 부여하는 키워드를 의미합니다.
            자바에서는 객체지향의 정보 은닉을 위해 접근 제어자라는 기능을 제공하며, public, protected, default, private이 있습니다.
            public으로 선언된 클래스 멤버는 외부로 공개되며, 해당 객체를 사용하는 프로그램 어디에서나 해당 멤버에 직접 접근할 수 있습니다.
            protected로 선언된 클래스 멤버는 같은 패키지 혹은 다른패키지에서 해당 클래스를 상속한 객체에서 접근이 가능합니다.
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
            직렬화가 필요한 이유는 메모리상에 저장되는 Object는 네트워크 상에 두 컴포넌트가 통신을 할때 통신선을 통해 직접적으로 전송이 불가해서
            통신선을 통해 전송이 가능한 JSON,XML,YAML,Byte 파일 등으로 바꾸어서 전송해야하기 때문입니다.
            이와 반대로, 직렬화된 데이터를 Object 형태로 변환시키는 작업을 역직렬화라고 합니다.
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
            리플렉션은 애플리케이션 개발에서보다는 프레임워크나 라이브러리에서 많이 사용되는데, 대표적으로 스프링에서 의존성을 주입할때 사용됩니다.
            다만, 런타임 시점에서 객체를 생성하여 해당 멤버에 접근해 조작하는 방식이기 때문에 컴파일 상에서는 잡히지 않았던 버그가 런타임 시점에 생길 수 있다.
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