# [Kotlin] Useful Features
코틀린의 유용한 기능들
* 확장 함수 : 원래 있던 클래스에 기능을 추가하는 함수
* 형변환 : 숫자형 자료형끼리 쉽게 형변환 가능
* 형 체크 : 변수의 형이 무엇인지 체크하는 기능
* 고차 함수 : 인자로 함수를 전달하는 기능
* 동반 객체 : 클래스의 인스턴스 생성 없이 사용할 수 있는 객체
* let() 함수 : 블록에 자기 자신을 전달하고 수행된 결과를 반환하는 함수
* with() 함수 : 인자로 객체를 받고 블록에서 수행된 결과를 반환하는 함수
* apply() 함수 : 블록에 자기 자신을 전달하고 이 객체를 반환하는 함수
* run() 함수 : 익명함수처럼 사용하거나, 블록에 자기 자신을 전달하고 수행된 결과를 반환하는 함수

## 확장 함수 
```kotlin
// 기존 클래스에 함수 추가
fun Int.isEven() = this % 2 == 0 // 확장 함수 내부에서 객체를 this로 접근, 이러한 객체를 리시버 객체라고 함

val a = 5
val b = 6

println(a.isEven()) // false
println(b.isEven()) // true
```
## 형변환 
```kotlin
// 숫자형 자료형 끼리는 to자료형() 메서드를 사용하여 형변환 가능
val a = 10L
val b = 20

val c = a.toInt() // Long -> Int
val d = b.toDouble() // Int -> Double
val e = a.toString() // Long -> String

// <숫자 형태 문자열 -> 숫자>의 경우 자바와 마찬가지로 Integer.parseInt() 메서드 사용
val intStr = "10"
val str = Integer.parseInt(intStr);

// 일반 클래스 간 형변환은 as 키워드 사용
open class Animal

class Dog: Animal()

val dog = Dog()

val animal = dog as Animal // Dog -> Animal
```
## 형 체크
is 키워드 사용, 자바의 instanceOf에 대응
```kotlin
val str = "hello"

if(str is String)
    println(str.toUpperCase())
```
## 고차 함수
코틀린에서는 함수의 인수로 함수를 전달하거나 함수를 반환할 수 있다. 이렇게 다른 함수를 인수로 받거나 반환하는 함수를 고차 함수라고 한다.
```kotlin
fun add(x: Int, y: Int, callback: (sum: Int) -> Unit) {
    callback(x + y)
}

add(5, 3, { println(it) }) // 8
``` 
자바에서는 주로 인터페이스를 사용하지만 코틀린은 함수를 활용한다.
## 동반 객체 
프래그먼트는 특수한 제약 때문에 팩토리 메서드를 정의하여 인스턴스를 생성해야 한다. 팩토리 메서드는 생성자가 아닌 메서드를 사용해 객체를 생성하는 코딩 패턴을 말하는데 클래스와 별개로 보며 포함 관게도 아니다. 코틀린에서는 자바에서의 static과 같은 정적 메서드를 만들 수 있는 키워드를 제공하지 않고 대신 동반 객체로 이를 구현한다.
```kotlin
class Fragment {
    companion object { // 동반 객체
        fun newInstance(): Fragment {
            println("생성됨")
        }
    }
}

val fragment = Fragment.newInstance()
```
## let() 함수
코틀린 기본 라이브러리는 몇 가지 유용한 함수를 제공한다. let() 함수는 블록에 자기 자신을 인수로 전달하고 수행된 결과를 반환한다. 인수로 전달한 객체는 it로 참조한다.
```kotlin
// fun <T, R> T.let(block: (T) -> R): R
val result = str?.let { // Int
    Integer.parseInt(it);
}
```
## with() 함수
with() 함수는 인수로 객체를 받고 블록에 리시버 객체로 전달한다. 그리고 수행된 결과를 반환한다. 리시버 객체로 전달된 객체는 this로 접근할 수 있다. this는 생략이 가능하다. 안전한 호출이 불가능하여 객체가 null이 아닐 때만 사용해야 한다.
```kotlin
// fun <T, R> with(receiver: T, block: T.() -> R): R
with(str) {
    println(toUpperCase())
}
```
## apply() 함수 
apply() 함수는 블록에 객체 자신이 리시버 객체로 전달되고 이 객체가 반환된다. 객체의 상태를 변화시키고 그 객체를 다시 반환할 때 주로 사용한다.
```Kotlin
// fun <T> T.apply(block: T.() -> Unit): T
val result = car?.apply {
    car.setColor(Color.RED)
    car.setPrice(1000)
}
```
## run() 함수 
run() 함수는 익명 함수처럼 사용하는 방법과, 객체에서 호출하는 방법을 모두 제공한다. 익명 함수처럼 사용할 때는 블록의 결과를 반환한다. 블록안에 선언된 변수는 모두 임시로 사용되는 변수이다.
```kotlin
// 익명 함수처럼 호출
// fun <R> run(block: () -> R): R
val avg = run {
    val korean = 100
    val english = 80
    val math = 50

    (korean + english + math) / 3.0
}

// 객체에서 호출
// fun <T, R> run(block: T.() -> R): R
// 안전한 호출이 가능해서 with() 함수보다 유용
str?.run {
    println(toUpperCase())
}
```