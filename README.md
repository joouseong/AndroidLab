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
