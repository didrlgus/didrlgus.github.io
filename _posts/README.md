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

### Q. 좋은 객체지향의 설계 5가지인 SOLID에 대해 설명하세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            먼저 S에 해당하는 SRP, single responsibility principle은 한 클래스는 하나의 책임만 가져야 한다는 원칙입니다.
            여기서 중요한 기준은 변경 입니다. 변경이 있을 때 파급 효과가 적으면 SRP를 잘 따른 것이라고 볼 수 있습니다.
            다음으로 O는 OCP, Open Closed Priciple, 개방-폐쇄 원칙을 의미합니다. 소프트웨어 요소는 확장이나 변경에는 열려 있으나 변경에는 닫혀 있어야 한다는 원칙입니다.
            즉, 내가 어떤 코드를 추가 했을 때, 기존 코드에 대한 변경이 없다면 OCP를 잘 따른 것이라고 볼 수 있습니다.
            다음으로, L은 Liskov Substitution Priciple, 리스코프 치환 원칙입니다. 
            이는 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것을 의미합니다.
            단순히 컴파일 성공하는 것을 넘어서는 이야기입니다. 예를들어, 자동차 인터페이스가 있고 엑셀이라는 기능이 선언되어있다고 할때, 
            자동차 인터페이스의 구현체는 엑셀 기능을 앞으로 가는 기능으로 만들어야지 뒤로 가는 기능으로 만들면 안됩니다.
            다음으로, I는 Interface Segregation Principle, 인터페이스 분리 원칙입니다.
            인터페이스 여러 개가 범용 인터페이스 하나보다 낫다는 원칙입니다.
            인터페이스를 분리하면 인터페이스가 명확해지고, 대체 가능성이 높아지기 때문입니다.
            마지막으로 D는 Dependency Inversion Principle, 의존관계 역전의 원칙입니다.
            프로그래머는 추상화에 의존해야지, 구체화에 의존하면 안된다는 원칙입니다.
            즉, 클라이언트가 인터페이스에 의존해야지 유연하게 구현체를 변경할 수 있습니다. 구현체에 의존하게 되면 유연성이 떨어집니다. 
        </p>
    </div>
</details>

### Q. 추상클래스와 인터페이스의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            추상클래스와 인터페이스의 가장 큰 차이점은 사용용도라고 생각합니다.
            추상 클래스는 서브 클래스에서 슈퍼 클래스의 기능을 그대로 상속받아 확장시키려는 것이 목적입니다.
            이에반해, 인터페이스는 결합도가 낮은 코드를 만들어 코드의 유연성과 확장성을 높여 유지보수 비용을 최소화 시키려는 것이 목적입니다.
            추상클래스는 서브클래스와 슈퍼클래스간의 상속의 관계가 필요한 IS-A 관계이며, 하위 상세 클래스에서 공통된 기능은 그대로 물려받고 별도의 구현이 필요한 부분이 남아있을때 사용하면 되지만, 
            꼭 필요한 경우를 제외하고 상속은 피하는게 좋은 디자인이라고 생각합니다.
            상속의 특성상 서브클래스가 슈퍼클래스에 의존하는 관계가 되기 때문에 결합도가 높아 코드의 유연성을 떨어뜨릴 수 있다는 단점이 있기 때문입니다.
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

### Q. HashMap, TreeMap, LinkedHashMap의 차이에 대해서 말씀해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            HashMap은 내부적으로 Hashing을 사용해 데이터를 저장하고 TreeMap은 Red-Black 트리를 사용해 데이터를 저장합니다.
            그렇기 때문에 hashmap은 O(1)의 데이터 조회가 가능한데 반해 treemap은 O(logN)의 데이터 조회가 가능합니다.
            또한, TreeMap은 HashMap과 다르게 데이터 저장 시 데이터의 순서를 보장합니다.
            그리고 LinkedHashMap도 마찬가지로 HashMap과 다르게 데이터 저장 시 데이터의 순서를 보장합니다.
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
            리플렉션은 애플리케이션 개발에서보다는 프레임워크나 라이브러리에서 많이 사용되는데, 대표적으로 스프링에서 bean을 등록하고 의존관계를 주입할때 리플렉션을 사용합니다.
            다만, 런타임 시점에서 객체를 생성하여 해당 멤버에 접근해 조작하는 방식이기 때문에 컴파일 상에서는 잡히지 않았던 버그가 런타임 시점에 생길 수 있습니다.
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
            개발자들이 애플리케이션 개발을 빠르고 효율적으로 할 수 있도록 도움을 주는 틀 입니다.
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
            이를통해, 개발자는 객체의 라이프사이클이나 의존관계를 신경쓸 필요없이 자신의 비즈니스 로직에만 집중하여 생산성을 높일 수 있습니다.
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
           그리고, 필드 주입방식은 테스트 시 application context 없이는 테스트가 불가하다는 단점이 있습니다.
           즉, 프레임워크 없이 순수한 자바 코드로만 단위 테스트를 수행이 불가합니다.
           결과적으로, 생성자 주입은 필드 주입이나 세터 주입과 비교하여 많은 장점을 가지면서 단점은 없으므로 생성자 주입이 권장됩니다.
        </p>
    </div>
</details>

### Q. 프레임워크와 라이브러리의 차이에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프로그램의 흐름. 즉, 제어권을 누가 가지고 있느냐에 따라 프레임워크와 라이브러르를 구분할 수 있습니다.
            프레임워크는 프로그램의 흐름을 자체적으로 갖고 있어서 개발자는 그 안에서 필요한 코드를 작성합니다. 
            반면에 라이브러리는 개발자가 프로그램의 흐름을 갖고 있어서 자신의 비즈니스 로직을 구현할 때 라이브러리에서 
            가져다 사용할 수 있다는 것을 의미합니다.
            프레임워크는 집, 사람은 개발자, TV나 쇼파 등은 라이브러리로 비유를 해볼 수 있습니다.
        </p>
    </div>
</details>

### Q. servlet과 servlet container에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            servlet은 서버쪽에서 실행되며, 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 자바 클래스입니다.
            servlet은 일반 자바 클래스와 달리 Servlet container 내에서만 실행됩니다.
            servlet container는 servlet의 생명주기를 관리하고 요청에 맞는 스레드를 생성합니다.
            servlet container는 client에게 요청을 받아 servlet을 실행시키고 결과를 client에게 전달해주는 기능을 가진 컴포넌트입니다.
            대표적인 servlet container로는 tomcat이 있습니다.
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

### Q. spring container가 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            bean을 생성하고 관리하면서 의존관계를 연결해 주는 역할 수행하는 스프링의 핵심 객체 입니다.
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

### Q. Spring 서버 부팅 시 동작과정에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            먼저 톰캣이 실행됩니다.
            다음으로, application context 즉, spring container가 생성됩니다.
            다음으로, 스프링 bean들이 spring container에 생성됩니다.
            다음으로, bean들의 의존관계가 주입됩니다.
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

### Q. threadLocal이 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            각 스레드마다 갖는 독립적인 지역변수를 말합니다.
            스프링은 bean을 싱글톤으로 관리하기 때문에 공유 필드로 상태값을 가질 시 
            멀티쓰레드 환경에서 큰 장애가 발생할 수 있습니다. 이럴 때 사용할 수 있는 것이 threadLocal 입니다.
            다만, 스프링에서는 thread 또한 thread pool에 저장되는 공유자원이기 때문에 하나의 요청이 끝나는 시점에
            thread local의 초기화 작업을 해주어야 다른 request에 영향을 주지 않습니다.
        </p>
    </div>
</details>

### Q. spring MVC에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            MVC는 기본적으로 Model View Controller의 약자로 프로그램 개발 시 세가지 역할로 구분하여 개발하는 방법론입니다.
            이를 사용하는 이유는 완벽한 분업화를 통해 해당 역할의 개발자가 자신의 역할에만 집중하여 개발하기 위함입니다.
            이를 통해 유지보수 비용을 최소화 시킬 수 있습니다.
            그리고 spring mvc는 spring에서 mvc 개발을 편리하게 하기위해 spring 에서 제공하는 프로젝트
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
            package를 scan하고 @Controller, @RestController을 확인하여 적절한 Handler Method에 위임해주는 역할을 수행합니다.
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

### Q. filter, interceptor, AOP의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            모두 client의 request를 가로챌 수 있는 기능들이나 동작시점에 차이가 있습니다.
            filter는 Dispatcher Servlet 영역에 들어가기 전 범위에서 수행됩니다.
            또한, filter는 스프링 컨텍스트 이전에 실행되어 스프링과 무관합니다.
            일반적으로 인코딩 변환 처리, XSS 방어를 기능을 수행할 때 사용됩니다.
            interceptor는 스프링의 DispatcherServlet이 Controller를 호출하기 전에 
            수행되기 때문에 스프링 내부에서 Controller에 관한 요청과 응답에 관여합니다.
            스프링 내에서 실행되기 때문에 스프링의 모든 bean에 접근이 가능합니다.
            주로 로그인 체크, 권한체크, 프로그램 실행시간 계산작업 로그확인 등에 사용됩니다.
            AOP Controller 처리 이후, 비지니스 로직 수행 전에 동작합니다.
            로깅, 트랜잭션, 캐싱 기능 등을 주로 수행합니다.
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

### Q. spring boot security 인증 과정에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
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
            가령, 다른 객체를 참조하는 걸 RDB에선 표현하기 어려운데 개발자의 별도 코드없이 ORM에서는 이를 대신 매핑해줍니다.
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
            애플리케이션과 DB 사이에서 엔티티를 보관하는 가상의 DB같은 역할을 할 수 있습니다.
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
            이를 해결하기 위해 특정 연관된 엔티티를 SQL 조인을 사용해서 함께 조회하는 fetch join 방식과 연관된 엔티티를 조회할 때 지정한 size만큼 IN절을 사용해 조회하는 
            BatchSize 방식을 고민하였습니다.
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

### Q. Spring AOP가 무엇이고 어떻게 동작하나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            흩어진 관심사를 하나의 Aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하는 방식의 프로그래밍 기법을 말합니다.
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
            CI는 지속적인 통합이라는 뜻으로 VCS 시스템인 git에 코드가 PUSH 되면 자동으로 빌드가 수행되어 안정적인 배포 파일을 만드는 과정입니다.
            CD는 CI를 통해 빌드된 결과를 자동으로 운영서버에 무중단 배포까지 진행하는 과정 입니다.
            개발자가 수동으로 코드를 merge하고 배포하는 과정을 자동화 시켜 생산성을 높이고 협업의 효율성을 높이기 위해 사용합니다.
        </p>
    </div>
</details>

### Q. redirect의 forward 차이에 대해서 설명해주세요.
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
            (전화예시)
        </p>
    </div>
</details>