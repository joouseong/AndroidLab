# AndroidLab
## 9월 22일(6주차)
### 추상화와 인터페이스
인터페이스 연습문제
``` kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        var ki = KotlinImpl()
        ki.get()
        ki.set()
    }
}

class KotlinImpl: InterfaceKotlin{
    override var variable: String = "init value"
    override fun get(){
        Log.e("KotlinImpl", "get() variable: $variable")
    }
    override fun set() {
        variable = "Hello World~!"
        Log.e("KotlinImpl", "set() variable: $variable")
    }
}

interface InterfaceKotlin {
    var variable: String
    fun get()
    fun set()
}
```

### 접근 제한자
* 클래스, 인터페이스, 메서드, 프로퍼티는 모두 접근 제한자(Visibility Modifiers)지정 가능
* default는 public
  - private: 다른 파일에서 접근할 수 없음
  - internal: 같은 모듈에 있는 파일만 접근 가능
  - protected: private와 같으나 상속 관계에서 자식 클래스가 접근 가능
  - public: 제한 없이 모든 파일에서 접근 가능
* 코틀린의 모듈
  - 한 번에 같이 컴파일되는 모든 파일
  - 안드로이드라면 하나의 앱
접근 제한자 연습문제
``` kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        var child = Child()
        child.callVariables()

        var parent = Parent()
        Log.e("MainTest0922", "Parent: default ${parent.defaultVal}")
        Log.e("MainTest0922", "Parent: internal ${parent.internalVal}")

        //Log.e("MainTest0922", "Parent: private: ${parent.privateVal}")
        //0922Log.e("MainTest0922", "Parent: private: ${parent.protectedVal}")
}

open class Parent{
    private val privateVal = 1
    protected val protectedVal = 2
    internal val internalVal = 3
    val defaultVal = 4
}


class Child : Parent(){
    fun callVariables(){
        Log.e("MainTest0922", "Child: protected ${protectedVal}")
        Log.e("MainTest0922", "Child: internal ${internalVal}")
        Log.e("MainTest0922", "Child: default ${defaultVal}")
    }
}
```

### 코틀린의 null 처리
코틀린의 null 처리
* null을 허용하는 nullable 변수
* null을 허용하지 않는 non-nullable 변수
  - non-nullable 변수가 null일 때 property, method를 사용하면 NullPointerException 발생
* NullPointerExcteption 처리
  - java: if문, equals, try ~ catch 등을 활용
  - Kotlin: ?.  ?:  !! 등 활용
nullable 변수 선언
``` kotlin
var nonNullableVar : String = null // null을 허용하지 않는 변수에 null 값을 사용하여 에러
var nullableVar : String? = null
var nullableVar2 : String? = "Nullable Variable"
```
Null Safe Operator
* ?. 객체가 null인지 null이 아닌지 확인
  - null이 아니면 실행
  - null이면 실행하지 않고 null 반환
``` kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        Null Safe Operator 연습문제
        // var nonNullableVar : String = null
        var nullableVar : String? = null
        var nullableVar2 : String? = "Nullable Variable"

        //-------------------------------------------
        var nonNullVar : String = "Hello Kotlin"

        Log.e("NullSafeOperator", nonNullVar.uppercase())
        //Log.e("NullSafeOperator", NullableVar.uppercase())
        Log.e("NullSafeOperator", nullableVar?.uppercase().toString())
        Log.e("NullSafeOperator", nullableVar2?.uppercase().toString())
}
```

### 늦은 초기화 lateinit, lazy
늦은 초기화
* 객체 초기화를 늦게 하는 것
* 객체 선언 시 객체 초기화가 어려울 때 null로 선언하지만 null사용을 지양하고 싶을 때
* 객체 선언 시 초기화할 수 없지만 이후 다른 값들이 정해지면서 초기화해야 할 때
* lateinit, lazy 사용

lateinit
* var(변수 선언)에만 사용
* Primitive Type(Int, Float, Long 등)에는 사용 불가
* non-null 변수로만 사용 가능

by lazy
* val(상수 선언)에서 사용 가능
  - 초기화 후 초기값이 변경되지 않는다면 by lazy를 사용
* Primitive Type(Int, Float, Long등)에도 사용 가능
* non-null, nullable 변수 사용 가능

생명주기 함수와 사용될 때
``` kotlin
class MainActivity : AppCompatActivity() {

    val binding by lazy{
        ActivityMainBinding.inflate(layoutInflater)
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)
}
```
