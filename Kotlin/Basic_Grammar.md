# ***코틀린 기본 문법***
## 변수와 상수
코틀린에서 변수는 var, 상수는 val(자바의 final 키워드에 대응)로 선언한다.
```kotlin
var a: Int = 10     // var 변수명: 자료형 = 값
val b: Int = 20     // val 상수명: 자료형 = 값
```
자료형을 따로 지정하지 않더라도 형추론을 지원하므로 생략 가능하다.
```kotlin
var c = 10      // var c: Int = 10
val d = 20      // val d: Int = 20
```
## 함수
코틀린의 함수는 자바의 메서드에 해당된다.
* fun 함수명(인수1 : 자료형1, 인수2 : 자료형2, ...): 반환자료형

반환자료형 Unit은 자바의 void에 대응한다. 반환값이 Unit이면 반환자료형을 생략할 수 있다.
```kotlin
fun func1(str : string){
    println(str)
}
```
## 기본 자료형
코틀린의 기본 자료형은 모두 객체이다.
### 숫자형
* Double : 64-bit 부동소수점
* Float : 32-bit 부동소수점
* Long : 64-bit 정수
* Int : 32-bit 정수
* Short : 16-bit 정수
* Byte : 8-bit 정수

#### 리터럴
자료형을 알 수 있는 표기 형식으로, 리터럴에 따라 컴파일러가 자료형을 추론한다.
```Kotlin
val a = 10      // Int
val b = 10L     // Long
val c = 10.0    // Double
val d = 10.0f   // Float
```
### 문자형
* String : 문자열
* Char : 문자

#### 리터럴
```Kotlin
val str = "안녕하세요"   // " ": String 
val c = 'H'             // ' ': Char

// 여러 줄에 걸친 문자열을 표현할 때, 큰따옴표 3개를 리터럴로 사용한다.
val strs = """여러 줄
    문자열
    표현
    """
```
#### 문자열 비교
== 을 사용하고, 자바의 equal() 메서드와 대응한다.
</br>참고로 오브젝트 비교시에는 ===를 사용한다.

#### 문자열 템플릿
```kotlin
val str = "반갑"        // 출력 :
println(str + "습니다") // 반갑습니다
println("$str 습니다")  // 반갑 습니다
println("${str}습니다") // 반갑습니다
```
### 논리형
* Boolean : true or false
### 배열
Array라는 별도의 타입으로 표현한다. arrayOf()를 사용해서 배열의 생성과 초기화를 함께 수행한다. 컴파일러가 자료형을 유추할 수 있을 때는 이를 생략할 수 있다.
```kotlin
val numbers: Array<Int> = arrayOf(1, 2, 3, 4, 5)

println(numbers[0]) // 1
```
## 제어문
### if
일반적인 if - else 사용 방법과 같다. if문을 식처럼 사용할 수 있다.
```kotlin
val max = if(a > b) a else b
```
### when
자바의 switch문에 대응한다.
```kotlin
val x = 1

when (x) {
    1 -> println("x == 1")
    2, 3 -> println("x == 2 or 3") // , 사용해서 범위지정
    in 4..7 -> println("4 이상 7 이하") // in .. 연산자로 범위 지정
    !in 8..10 -> println("8 ~ 10이 아님") // 범위에 벗어난 값에 대해 처리 
    else -> {                       // else로 나머지 경우에 대해 처리, {}으로 코드 감싸기 가능
        println("8 ~ 10")
    }
}
```
if문처럼 식처럼 사용이 가능하다. 또한 함수의 반환값으로 사용할 수 있다.
```kotlin
val number = 1
fun isEven(num: Int) = when(num%2) {
    0 -> "짝"
    1 -> "홀"
}
```
### for
```kotlin
var arr: Array<Int> = arrayOf(1,2,3,4,5)
for (num in arr){       // 자바의 for each문과 비슷하다. 배열을 순회하며 각 요소를 변수 num를 통해 사용할 수 있다.
    println(num)
}

for (i in 1..3)     // in a..b(a이상 b이하)혹은 in a until b(a이상 b미만) 로 범위를 지정한다.
    println(i)      // 1; 2; 3;
for (i in 1..10 step 2) // step을 통해 i가 증가/감소 하는 폭을 조절한다.
    println(i) // 1; 3; 5; 7; 9;
for (i in 10 downTo 1 step 3) // downTo를 통해 i를 감소시킬 수 있다.
    println(i) // 10; 7; 4; 1;
```
### while
주어진 조건이 참일 때, 반복한다. while, do-while문은 자바와 완전히 동일하다.
## 클래스
### 클래스 선언
```kotlin
// 클래스 선언
class Person{

}

// 인스턴스 생성
val person = Person()
```
### 생성자
```kotlin
// 빈 생성자를 가지는 클래스
class Person(var name: String){

}

// 생성자 작성
class Person{
    constructor(name: String){
        println(name)
    }
}

// init 블록을 통해 인스턴스 생성시 가장 먼저 초기화
class Person(var name: String){
    init {
        println(name)
    }
}
```
### Property
클래스의 필드와 접근자 (getter/setter)를 통칭하여 코틀린에서는 프로퍼티(property)라고 한다.
</br>다음과 같은 자바 코드가 있다.

```java
class Person {
    private String name;

    public Person(String name){
        this.name = name;
    }

    public String getName(){
        return name;
    }

    public void setName(String name){
        this.name = name;
    }
}
```
코틀린에서는 다음과 같은 한줄의 코드로 동일한 코드를 작성할 수 있다.
```kotlin
class Person(var name: String)
```
setter와 getter 메서드 없이 .을 통하여 name 프로퍼티에 접근할 수 있다.
```kotlin
class Person(var name: String)
val p = Person("오태식")
println(p.name) // 오태식;
p.name = "뒤지기싫으면"
println(p.name) // 뒤지기싫으면;
```
setter와 getter를 작성해서 사용할 수도 있다.
```kotlin
class Person(name: String){
    var name: String = ""
        get(){
            println("getter 커스텀")
            return field
        }
        set(name: String){
            println("setter 커스텀")
            field = name
        }
    init{
        this.name = name
    }
}
val p = Person("오태식") // setter 커스텀;
println(p.name)         // getter 커스텀; 오태식;
p.name = "뒤지기싫으면"  // setter 커스텀;
println(p.name)         // getter 커스텀; 뒤지기싫으면;
```
### 접근 제한자
* public : 생략 가능, 전체 공개이다.
* private : 현재 파일 내부에서만 사용할 수 있다.
* internal : 같은 모듈 내에서만 사용할 수 있다.
* protected : 상속받은 클래스에서 사용할 수 있다.
### 상속
코틀린에서 기본적으로 클래스의 상속이 금지된다. 상속이 가능하게 하기 위해서는 open 키워드를 추가해야 한다.
```kotlin
open class Animal {}

class Dog : Animal() {}

//생성자가 있는 경우
open class Animal(val name: String) {}

class Dog : Animal(name: String) : Animal(name) {}
```
### 내부 클래스
내부 클래스 선언에는 inner 키워드를 사용한다.
```kotlin
class OuterClass {
    var a = 10

    inner class OuterClass2{
        fun something() {
            a = 20 // inner 키워드로 외부 클래스 접근 가능
        }
    }
}
```
### 추상 클래스
추상 클래스는 미구현 메서드(추상 메서드)가 포함된 클래스를 말한다. 직접 인스턴스화할 수 없고 다른 클래스가 상속하여 미구현 클래스를 구현해야 한다.
```kotlin
abstract class A {
    abstract fun func()

    fun func2(){

    }
}

class B: A(){
    override fun func(){
        println("hello")
    }
}

val a = A() // 에러 발생
val b = B() // 인스턴스 생성
```
## 인터페이스
인터페이스는 미구현 메서드를 포함하여 클래스에서 이를 구현한다. 추상 클래스와 비슷하지만 클래스가 단일 상속만 되는 반면 인터페이스는 다중 구현이 가능하다. 주로 클래스에 동일한 속성을 부여해 같은 메서드라도 다른 행동을 할 수 있게 하는 데 사용한다.
```kotlin
interface Runnable{
    fun run() // abstract 생략
}

class Human: Runnable{
    override fun run(){ // 인터페이스의 추상 메서드를 구현해서 사용
        println("달린다")
    }
}

interface Eatable{
    fun eat()
}

open class Animal {}

class Dog : Animal(), Runnable, Eaterable{ // 상속은 하나만, 인터페이스는 여러 개 동시에 구현 가능
    override fun eat(){
        println("먹는다")
    }

    override fun run(){
        println("달린다")
    }
}
```
## null 가능성
코틀린의 모든 객체는 생성과 동시에 값을 대입하여 초기화해야 한다.
```kotlin
val a: String // 초기화하지 않아서 에러 발생

val a: String = null // 코틀린은 기본적으로 null을 허용하지 않음 -> 에러 발생

val a: String? = null // 성공 : 자료형 옆에 ?를 붙여서 null 허용
```
초기화를 나중에 진행해야 할 경우, 이때는 lateinit 키워드를 추가하면 된다. 단 사용할 수 있는 조건이 존재한다.
* var 변수에만 사용
* null 값으로 초기화 불가
* 초기화 전에는 변수 사용 불가
* Int, Long, Double, Float에서는 사용 불가
```kotlin
lateinit var a: String 
a = "hello"
```
val 상수가 늦은 초기화가 필요할 경우 by lazy를 사용한다. 늦은 초기화로 앱이 시작될 때의 연산을 분산시킬 수 있어서 빠른 실행에 도움이 된다.
```kotlin
val str: String by lazy{
    println("초기화")
    "hello"
}

println(str) // 초기화; hello;
println(str) // hello;
```
null 값을 허용하는 변수의 값을 허용하지 않는 변수에 담을려면 null값이 아니라는 보증이 필요한데 이를 위해 대입하는 변수뒤에 !!를 붙인다.
```kotlin
val name: String? = "null 아닌데ㅋㅋ"

val name2: String = name        // 에러
val name2: String? = name       // 성공

val name2: String = name!!      // 성공
```
메서드 호출 시 .연산자 대신 ?.연산자를 사용하여 null이 아닌 경우에만 호출하도록 한다.
</br>
안전한 호출(?.) 시에 null이 아닌 기본값을 반환하고 싶으면 엘비스 연산자 ?: 를 함께 사용한다.
```kotlin
val str: String? = null

var upperCase = if(str != null) str else null // 복잡한 if문을
upperCase = str?.toUpperCase // ?.연산자로 다이어트 가능
upperCase = str?.toUpperCase ?: "초기화하세요" // null 대신 초기화하세요 대입
```
