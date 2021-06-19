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

### Q. 추상클래스와 인터페이스의 차이에 대해 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            추상클래스와 인터페이스의 가장 큰 차이점은 사용용도라고 생각합니다.
            추상 클래스는 서브 클래스에서 슈퍼 클래스의 기능을 그대로 상속받아 확장시키려는 것이 목적입니다.
            이에반해, 인터페이스는 인터페이스를 구현한 객체들은 같은 행위를 한다는 것을 명시하기 위함이 목적입니다.
            추상클래스는 서브클래스와 슈퍼클래스간의 상속의 관계가 필요한 IS-A 관계이며, 하위 상세 클래스에서 공통된 기능은 그대로 
            물려받고 별도의 구현이 필요한 부분이 남아있을때 사용하면 되지만, 꼭 필요한 경우를 제외하고 상속은 피하는게 좋은 디자인이라고 생각합니다.
            상속의 특성상 서브클래스가 슈퍼클래스에 의존하는 관계가 되기 때문에 결합도가 높아 코드의 유연성을 떨어뜨릴 수 
            있다는 단점이 있기 때문입니다.
            그에 반해 인터페이스는 행위의 조건(parmeter)와 결과(return)값만 강제하지 내용은 구현하는 각 클래스에 맡겨져 있기 때문에 
            구현에 종속되지 않습니다.
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
            다만, equals() 메소드가 false 라고해서 두 객체의  hashcode()값이 꼭 다를 필요는 없습니다.
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
            메모리 공간을 훨씬 더 효율적으로 사용할 수  
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
            servlet은 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 자바 클래스입니다.
            servlet은 일반 자바 클래스와 달리 Servlet container 내에서만 실행됩니다.
            servlet container는 client에게 요청을 받아 스레드를 생성하여 servlet을 실행시키고 결과를 client에게 
            전달해주는 기능을 가진 컴포넌트입니다.
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

### Q. spring MVC에 대해서 설명해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            spring mvc는 spring에서 mvc 개발을 편리하게 하기위해 spring 에서 제공하는 프로젝트 입니다.
            MVC는 Model View Controller의 약자로 프로그램 개발 시 세가지 역할로 구분하여 개발하는 방법론입니다.
            이를 사용하는 이유는 완벽한 분업화를 통해 해당 역할의 개발자가 자신의 역할에만 집중하여 개발하기 위함입니다.
            이를 통해 유지보수 비용을 최소화 시킬 수 있습니다.
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
            모두 client의 request를 가로챌 수 있는 기능들이라는 공통점이 있지만, 동작시점에 차이가 있습니다.
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
            CI는 지속적인 통합이라는 뜻으로 VCS 시스템인 git에 코드가 PUSH 되면 자동으로 빌드가 수행되어 안정적인 배포 파일을 만드는 과정입니다.
            CD는 CI를 통해 빌드된 결과를 자동으로 운영서버에 무중단 배포까지 진행하는 과정 입니다.
            개발자가 수동으로 코드를 merge하고 배포하는 과정을 자동화 시켜 생산성을 높이고 협업의 효율성을 높이기 위해 사용합니다.
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

# 운영체제

### Q. 프로세스와 스레드의 차이에 대해서 말해주세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            프로세스는 메모리에 올라와 실행되고 있는 프로그램이며 운영체제로부터 시스템 자원을 할당받는 작업의 단위입니다.
            스레드는 특정 프로세스 내에서 동작되는 여러 실행의 흐름입니다. 스레드는 프로세스로부터 시스템 자원을 할당받습니다.
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
            client/server 간의 통신을 위해 server 쪽에서 정해놓은 약속 입니다.
            (음식점 주문 예)
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

### 프로젝트 하면서 어려웠던 점은 뭐였고 어떻게 해결했나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <div>
            <p>첫번째 무기</p>
            <p>
                결제 성공 API에서 발생했던 문제들을 해결한 경험입니다.
                먼저 상황을 설명드리자면, 결제 성공 시 장바구니 제거, 상품 구매 수량 변경, 적립금 수정, 주문서 작성, 결제완료 메일 전송 작업들을 수행해야 했습니다.
                그런데, 기존에는 이러한 모든 작업들을 결제 성공 API 내에서 수행하고 있었습니다.
                이러한 설계의 문제점은 첫째로, 해당 API가 너무 많은 책임들을 갖고 있었고, 각 작업들의 coupling이 심하다는 문제가 있습니다.
                두번째로, 새로운 작업을 추가할 때마다 계속해서 API내 코드를 추가해야돼서 코드의 유연성과 확장성이 떨어지는 문제가 있습니다.
                세번째로, 일반적으로 메일 전송 기능은 내가 직접 다룰 수 없는 외부 컴포넌트를 많이 사용하는데, 
                그로 인해 외부 컴포넌트의 장애가 내 서비스에 영향을 미칠 수 있는 문제가 발생할 수 있습니다.
                그래서 이 문제를 해결하기 위해 kafka를 이용하였고 기존 API는 결제 성공 event를 전송하는 producer로써의 책임만을 부여했습니다.
                그리고 결제 성공 시 수행하던 각각의 작업들을 consumer group으로 나눠 용도에 맞게 결제 성공 메시지를 사용했습니다.
                결과적으로 기존 결제 성공 API에서 발생했던 coupling 문제나 확장성 문제, 외부 컴포넌트에 의존하게 되는 문제를 해결할 수 있었습니다.
            </p>
        </div>
        <div>
            <p>두번째 무기</p>
            <p>
                상품 구매 카운트 consumer의 scale out 시 발생했던 문제들을 해결했던 경험입니다.
                카프카를 이용해서 pub/sub 구조의 아키텍쳐를 구축하였는데 만약, 카프카에 이벤트가 쌓이는 속도를 consumer에서 따라가지 못하면 어떡하지? 라는 의문이 생겼습니다.
                그렇다면 kafka내 해당 topic의 partition을 2개로 늘리고 consumer를 하나 더 추가시켜 분산처리한다면 문제를 해결할 수 있습니다.
                하지만, 이 과정에서 문제가 발생했습니다. 문제를 말씀드리기 앞서 오른쪽 부분은 product 테이블의 스키마 일부에 대한 부분입니다.
                즉, product 테이블 내에 purchase_count 컬럼이 있는 상황입니다.
                이 상황에서 consumer를 하나 더 늘리게 되면 상품 테이블의 purchase_count 컬럼에서 동시성 문제가 발생합니다.
                이 문제를 해결하기 위해 SELECT FOR UPDATE 쿼리를 사용해 해당 row에 lock을 걸었습니다.
                이를통해, 동시성 문제는 해결했지만, 해당 row에 lock이 걸려 기존에 상품을 조회하는 API 성능에 치명적인 문제가 발생했습니다.
                이 문제를 해결하기 위해, product_purchase_count 테이블을 새로 생성하였고, product_purchase_count 테이블의 데이터를 sum하는 
                배치 job을 생성하여 app server의 API 응답 시간의 영향도 최소화 시켰습니다.
                하지만, 결제 수가 많아질 수록 product_purchase_count 테이블의 크기가 exponentially 하게 커질 가능성이 있었고, 
                product_purchase_count 테이블이 커질수록 sum batch에서 수행하는 작업에 걸리는 시간이 늘어나는 또 다른 문제가 발생했습니다.
                그래서 product_purchase_count 테이블에 time column을 추가하여 논리적으로 young area, old area를 나누었습니다.
                그리고 product_purchase_count 테이블이 커질것을 대비해 count 데이터를 집계하는 테이블인 product_purchase_merge_count 테이블을 생성했습니다.
                또한, young area와 old area를 나눌 기준이 되는 time 데이터를 저장할 product_purchase_count_standart_time 테이블을 생성했습니다.
                그리고 배치에서 기존의 job에 merge, delete step을 추가했습니다.
                sum step 에서는 product_purchase_count 테이블의 young 데이터와 product_purchase_merge_count 테이블의 old 데이터를 합해 product 테이블의 count 데이터를 업데이트 시킵니다.
                merge step 에서는 product_purchase_count 테이블의 young 데이터를 집계하여 product_purchase_merge_count 테이블에 insert 합니다.
                delete step 에서는 product_purchase_count 테이블의 old 데이터를 삭제시킵니다.
                위의 과정들을 통해 결과적으로, 상품 구매 수량 count consumer의 scale-out 상황에서 발생했던 데이터의 정합성 문제와 안정성 문제, 데이터가 많아졌을 때 특정 테이블이 커지는 문제를 해결했습니다. 
                하지만 현재, 상품 결제 시 실시간으로 상품의 구매 수량 데이터를 업데이트 하지 못한다는 한계를 가지고 있습니다. 
                어떻게 하면 위의 문제들을 모두 해결하면서 상품 구매 수량 count를 실시간으로 업데이트 시킬지 정확한 답을 아직 찾지는 못했으나, 
                조사를 통해 대용량 데이터의 실시간 분석이 가능한 lambda architecture에 대해 알게 되어 도입을 고려하고 있습니다.
            </p>
        </div>
        <div>
            <p>세번째 무기</p>
            <p>
                코드 중복, 버전관리, github repository 관리의 어려움을 gradle multi module로 해결한 경험입니다.
                기존에 각 consumer들을 별도의 모듈로 만들었고, 각자의 github repository를 생성해 배포하고 있었습니다.
                그래서 각 consumer들마다 공통으로 사용하는 코드 혹은 redis, kafka 관련 코드들의 중복이 발생했고 consumer들이 추가될 때마다 github repository를 관리하기 어려워졌습니다.
                이를 해결하기위해 gradle multi module을 사용하였고, 이로인해 코드 중복을 최소화 시켰고 확장성도 좋아졌으며, 버전관리가 용이하게 되었고, github repository 관리도 수월해졌습니다.
            </p>
        </div>
        <div>
            <p>네번째 무기</p>
            <p>
                스프링 배치에서 각 스텝을 tasklet으로 구성했을 때 발생했던 문제를 해결한 경험입니다.
                tasklet으로 구성하면 데이터 조회 시 조건에 맞는 모든 데이터를 읽어들이고 처리합니다.
                조회할 데이터의 수가 적다면 문제될 것 없겠지만 조회할 데이터의 매우 많다면 한번에 매우 많은 데이터를 
                메모리상으로 로딩시켜야 할 것이고 이는 서버에 많은 부하를 주게 될 것이다. 최악의 경우 서버가 다운될 우려도 있을 것입니다.
                이를 방지하기 위해 스프링 배치에서는 데이터를 page 단위로 끊어서 읽는 pageItemReader를 제공합니다.
                이를 통해 안정적으로 batch job을 수행할 수 있는 배치 애플리케이션을 개발했습니다.
            </p>
        </div>
        <div>
            <p>다섯번째 무기</p>
            <p>
                ELK 스택에서 Logstash 장애 시 생기는 문제를 kafka를 이용해 해결한 경험입니다.
                filebeat에서 로그 데이터를 보냈는데 logstash가 해당 데이터를 받는 도중에 장애가 나는 경우 또는
                filebeat에서 로그 데이터를 logstash로 보낸 후 logstash에서 로그 데이터를 parsing하는 도중에 장애가 
                나버리면 최악의 경우, 데이터의 손실이 발생할 수 있었습니다.
                왜냐하면, logstash나 filebeat 모두 어디에서도 안정성을 보장해주지 못하기 때문입니다.
                이를 해결하기 위해, 시스템의 중앙에서 신뢰성을 보장하고 확장성 높으며 높은 성능을 보장해주는 kafka를 연동하여 문제를 해결하였습니다.
                즉, kafka에 메시지가 없어지기 전에 logstash의 장애를 해결하고 다시 작동시킨다면 데이터 손실을 막을 수 있습니다.
            </p>
        </div>
        <div>
            <p>여섯번째 무기</p>
            <p>
                성능 테스트 시 발생했던 문제를 scale up을 통해 해결한 경험입니다.
                초기에, 개인 pc에 테스팅 환경을 구축하여 cloud 상에 배포된 애플리케이션의 load test를 진행했습니다.
                하지만 개인 pc에서 테스트를 진행하다보니 일관성있는 결과를 얻을 수 없다는 문제가 발생했습니다.
                그래서 클라우드 상에 새로 테스팅 환경을 구축하여 다시 load test를 진행했습니다.
                하지만, 부하를 많이 주면 줄수록 실패하는 요청이 늘어나는 문제가 발생했습니다.
                application log를 파악한 결과 thread가 CP로부터 connection을 응답받는 시간이 default로 지정된 시간을 초과하여 생기는 문제였습니다.
                이 문제를 해결하기 위해 connection pool size를 늘려서 테스트를 진행하였는데 이번에는 메모리 부족으로 인해 서버가 아예 다운되었습니다.
                AWS 프리티어의 환경으로 애플리케이션을 띄워놓다보니 해당 VM server의 스펙이 너무 낮아 많은 connection 들을 갖고 있을 메모리 공간의 부족이 주요 문제 상황이었습니다.
                그래서, application을 띄울 서버의 사양을 높였고 이를통해, 메모리 부족 문제를 해결했습니다.
            </p>
        </div>
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

### 성능 관련해서 무엇을 하셨나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <div>
            <p>첫번째 무기</p>
            <p>
                redis 캐싱을 통해 메인화면 API의 성능을 높인 경험이 있습니다.
                메인화면 API 호출 시 조회하는 상품 카테고리, 인기상품 조회, 최신상품 조회를 하고 있었고, 이 데이터들은 캐싱하기 용이한 데이터라고 판단했습니다.
                매우 빈번하게 호출 될 가능성이 높고 변경사항이 많더라도 실시간성으로 캐시를 업데이트할 필요가 없다고 판단했기 때문입니다.
                또한, in-memory storage 면서 다양한 자료구조를 지원해주는 redis를 캐시로 선택했습니다.
                그리고 정렬된 데이터를 저장하고 있음을 보장 받을 수 있는 sorted-set 자료구조로 key 설계를 하였습니다.
                (범위 조회 시 O(logN)+M(N은 전체 요소 개수, M은 return할 요소 개수), 데이터 하나 추가 시 O(logN))
                결과적으로, 캐싱을 통해 메인화면 API의 성능을 약 450tps에서 약 870tps로 향상시켰습니다.
            </p>
        </div>
        <div>
            <p>두번째 무기</p>
            <p>
                더 많은 트래픽을 분산 처리하기 위해 애플리케이션 서버를 scale-out하여 성능을 높인 경험이 있습니다.
                부하를 분산시키기 위해 load balancer를 사용하였고 load balancer로 nginx를 사용했습니다.
                그리고 round-robin 방식을 적용시켜 트래픽을 분산시켰습니다.
                결과적으로, scale out을 통해 단일서버 기준 약 900tps의 성능을 약 1300tps로 향상시켰습니다.
            </p>
        </div>
        <div>
            <p>세번째 무기</p>
            <p>
                web server 캐싱을 이용해 정적인 컨텐츠의 응답 성능을 높인 경험이 있습니다.
                nginx 서버 내에 정적인 컨텐츠를 캐싱하여 성능을 높였고 애플리케이션 서버의 부하를 줄였습니다.
            </p>
        </div>
        <div>
            <p>네번째 무기</p>
            <p>
                index 설계를 통해 수십 배 이상의 성능 향상을 보장 받았던 경험이 있습니다.
                인턴 생활을 하면서 약 4억건의 데이터에서 약 250만건의 데이터를 조회하는 쿼리가 있었는데 조회조건으로 사용하고 
                있던 등록시간 컬럼을 index로 잡아 수십 배 이상의 성능 향상을 보장 받은 경험이 있습니다.
                또한, 프로젝트를 하면서 exponentialy하게 커지는 테이블 내에서 고정된 숫자의 데이터를 조회하는 쿼리였던,
                인기 top10 상품 조회 쿼리에서 where 조건 컬럼이었던 purchase_count 컬럼을 대상으로 index를 생성하여 성능을 
                향샹시켰던 경험이 있습니다.
            </p>
        </div>
        <div>
            <p>다섯번째 무기</p>
            <p>
                thread pool size와 connection pool size 증가를 통해 성능을 향상시켰던 경험이 있습니다.
                다만, thread pool을 계속해서 증가시킨다고 해서 dramatic하게 성능이 올라가진 않았습니다.
                thread가 증가함에따라 context switching의 비용이 늘어났기 때문인 것으로 추정됩니다.
            </p>
        </div>
    </div>
</details>

# 인턴생활

### NoSQL도 여러가지가 있는데 왜 MongoDB를 썼나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            조회 쿼리가 다양한 테이블이어서 primary index 외에도 secondary index에 대한 기능이 필요하다고 판단했습니다.
            그래서 다른 nosql storage보다 secondary index를 잘 지원해주는 mongodb를 선택했었습니다.
        </p>
    </div>
</details>

### 왜 떨어진것 같나요? 뭘 배웠나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            인턴을 하기 전에는 그냥 잘 돌아가는 서비스 개발에만 집중했었습니다. 
            하지만 인턴과정의 코드리뷰나 발표과정을 통해 내가 만든 서비스가 어느정도의 트래픽을 감당할 수 있는지, 
            성능은 어떻게 되는지, 그리고 서비스가 커질것을 대비해 어떻게하면 확장성있는 아키텍처를 설계 할 수 있을지에 
            대해 고민할 줄아는 역량이 부족하다는 것을 느꼈고, 결국, 이러한 역량 부족으로 인해 떨어졌다고 생각합니다.
            인턴 과정을 통해 진정한 백엔드 개발자로서 갖추어야 할 역량들에 대해서 알게 되었고, 백엔드 개발에 대한 시야가
            넓어졌다고 생각합니다.
        </p>
    </div>
</details>

# 인성

### Q. 1분 자기소개 해보세요.
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            안녕하세요. 저는 ㅇㅇㅇ 입니다.
            저는 컴퓨터 공학을 전공하였습니다.
            컴퓨터 공학을 전공하다보니 자연스레 개발자가 되는 것을 꿈꾸게 되었습니다.
            개발자 중에서도 사용자의 눈에 직접 보이지는 않지만 내부에서 어떻게하면 더 좋은 서비스를 사용자에게 제공해 줄지
            끊임 없이 고민하며 고군분투하는 백엔드 개발자에 매력을 느껴 백엔드 개발자를 꿈꾸게 되었습니다.
            저는 사용자의 삶의 질을 만족시켜줄 수 있는 백엔드 개발자로 성장하는 것이 앞으로의 목표입니다.
            이러한 목표를 달성하기 위해 끊임없이 노력하고 있는 예비 개발자 입니다.
            또한, 저는 혁신을 이끌어나가는 개발자가 되는 것이 목표입니다.
            혁신을 이끌어나가는 개발자란 특정 기술에 정체되어 안주하는 개발자가 아니라,
            새로운 기술들을 끊임없이 시도하여 보다 더 좋은 시스템을 구축하여 위해 주도적으로 노력하는 개발자를 의미합니다.
            저는 이런 역량들을 키우기위해 개인적으로 쇼핑몰 서비스를 제공하는 프로젝트를 개발하였으며, 
            주요 기능으로는 상품 주문, 장바구니, 결제, 댓글, 리뷰 기능 등이 있습니다.
            또한, 기능 개발로 프로젝트를 끝마치는 것이 아니라, 어떻게 하면 내가 만든 서비스의 성능을 높일지, 
            또 어떻게 하면 보다 더 확장성 있는 아키텍처를 구성할 지에 대해 주도적으로 고민한 경험이 있습니다.
            결과적으로, 서버 한대 기준 약 900tps 정도의 성능을 보장하는 서비스를 개발하였고, 
            더 나아가 cloud 상에 scale out이 가능한 아키텍처를 구성하여 초 당 수만건의 데이터도 처리할 수 있는
            시스템을 구축했습니다.
        </p>
    </div>
</details>

### Q. 지원동기가 뭔가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            ㅇㅇㅇ에서는 특정 기업의 서비스나 솔루션에 의존하지 않고 자체적으로 인프라를 구축하고 서비스나 솔루션을 만든다는 것에 큰 매력을 느꼈기때문입니다.
            또한, ㅇㅇㅇ에서는 끊임없는 새로운 시도를 하고있고, 앞으로의 성장 가능성도 무궁무진할 것으로 판단했기 때문입니다.
            국내 최고의 클라우드와 그룹웨어 서비스를 제공하는 최고의 환경에서
            혼자 빠르게 나아가려는 것이 아닌 함께 멀리 나아가는 것을 중요 가치로 두고 함께 성장하고 싶어서
            지원했습니다.
        </p>
    </div>
</details>

### Q. 이 회사와서 어떤일을 하고싶어요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 이 회사 오면 무엇을 잘할 것 같으세요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 어떤 개발자가 되고 싶은가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            개발만 잘한다고 해서 훌륭한 개발자라고 생각하지 않습니다.
            기계랑만 소통하는 개발자가 아닌 동료분들과 커뮤니케이션을 잘 할 줄 아는 그런 개발자가 되고 싶습니다.
            혼자 빨리 나아가는것이 아니라, 함께 멀리 나아가는 것을 중요 가치로 생각하고 꾸준히 성장하는 개발자가 되고 싶습니다.
        </p>
    </div>
</details>

### Q. 개발하면서 가장 중요하다고 생각하는게 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            코드를 유연성 있게 설계하고 개발하는 것이 가장 중요한 부분이라고 생각합니다.
            그 이유는 프로그램은 살아있는 생명체와 같기 때문입니다.
            만약, 내가 제공하고자 하는 서비스가 웹 서비스라고 가정한다면 해당 서비스를 이용하는 유저들의 
            요구 사항은 수시로 변경될 수 있습니다. 그런데 요구 사항의 변화에 따라 유연성 있는 코드를 
            설계하지 못한다면 점점 더 유지 보수 하는데 많은 비용을 초래하게 될 것입니다.
            그렇기 때문에 코드를 유연성 있게 설계하고 개발하는 것이 가장 중요하다고 생각합니다.
        </p>
    </div>
</details>

### Q. 어떤 방식으로 개발 역량을 키우세요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            내가 공부한 내용을 직접 프로젝트로 만들어 정리하거나 기존 프로젝트에 공부한 내용을 직접 적용 시켜보는 활동입니다.
            저는 주로 인프런 강의나 관련 서적, 공식문서를 보면서 최근 실무자들이 사용하는 기술에는 어떤 것들이 있는지 학습한 후, 
            그것으로 끝내는 것이 아니라, 항상 제 프로젝트에 직접 적용 시켰습니다. 
            예를 들어, JPA, Kafka, ELK stack 등의 기술이 그런 것들 입니다.
            이런 방식의 학습방식을 통해 개발자로서의 역량이 많이 향상되었다고 생각합니다.
        </p>
    </div>
</details>

### Q. 1일 1커밋을 오랫동안 진행하셨는데, 어떤 내용에 대해서 공부하셨나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            주로 프로젝트에 개발했던 커밋이나 알고리즘 문제 푼 내용을 커밋한 내용들이 대부분입니다.
            최근에는 github 블로그를 새로 개설하여 블로그에 관한 커밋들도 늘어나고 있는 상황입니다.
        </p>
    </div>
</details>

### Q. 가장 재밌게 들었던 전공 수업은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 10년뒤 나의 모습이란?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 좋은 회사란 무엇인지?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 갈등 상황을 어떻게 해소하였나요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            갈등 상황이 있는 팀원들이 있다면 최대한 대화를 하려고 노력하였습니다. 각자 시간을 내어 의견을 들어본 후, 
            개인적으로 절충안이 있는지 생각해보았고 적당한 절충안이 나오지 않더라도 갈등있는 팀원끼리 모아서 저의 절충안을 
            제시하고 여기서 각자 양보하고, 양보할 수 없는 선을 결정하라는 식으로 해결을 하는 편이었습니다.
        </p>
    </div>
</details>

### Q. 본인의 강점은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            저의 가장 큰 강점은 꾸준함과 끈기라고 생각합니다.
            최근 1년 동안 거의 매일 개발 혹은 알고리즘 문제 풀이를 꾸준히 진행하고 있고, 이에 대한 과정들은 github 커밋 이력으로 남겨져 있습니다.
            또한, 프로젝트를 개발하면서 끊임없이 문제상황들을 가정하고 끈기있게 주도적으로 해결해 본 경험을 갖고 있습니다.
            속도가 느릴지라도 하루하루 꾸준히 성장하는 개발자가 되는 것이 앞으로의 목표입니다.
        </p>
    </div>
</details>

### Q. 본인의 단점은 무엇인가요?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. 검색 서비스에서 불편했던 점은?
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            해외 전문 지식을 얻기 위해
            다만, 어떤 물건을 사려고 할 때는 굉장히 좋았고     
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
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>

### Q. *, / 연산자 없이 곱하기, 나누기 연산 수행하기
<details>
    <summary style="font-Weight : bold; font-size : 50px; color : #E43914;">답변</summary>
    <div>
        <p>
            
        </p>
    </div>
</details>