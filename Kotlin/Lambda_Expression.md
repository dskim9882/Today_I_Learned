# ***[Kotlin] Lambda Expression***
람다식은 하나의 함수를 표현하는 방식으로 익명 클래스나 익명 함수를 간결하게 표현할 수 있어서 매우 유용하다.
</br>람다식으로 코드를 간결하게 할 수 있지만, 디버깅이 어렵고 남발하여 사용하면 코드 가독성이 떨어질 수 있다.

## 사용법
다음과 같은 코드가 있다.
```kotlin
fun add(x: Int, y: Int): Int {
    return x + y
}
```
이 코드는 반환 자료형, 블록, return을 생략할 수 있다.
```kotlin
fun add(x: Int, y: Int) = x + y
```
람다식은 인수 목록을 나열하고 -> 이후에 본문이 위치하게 작성한다.
```kotlin
var add = {x: Int, y: Int -> x + y} // 변수에 저장하여 일반 함수처럼 사용 가능하다.

println(add(2, 5)) // 7
```
## Single Abstract Method (SAM) 변환
추상 메서드 하나를 인수로 사용할 때는 함수를 인수로 전달하면 편하다. **자바로 작성된 메서드가 하나인 인터페이스를 구현할 때**는 대신 함수를 작성할 수 있다. 이를 SAM 변환이라 한다.
```Kotlin
// 안드로이드 버튼에 클릭 이벤트를 구현할 때 onClick() 추상 메서드만을 가지는 View.OnClickListener 인터페이스를 구현한다.

// 익명 클래스를 작성
button.setOnClickListener(object : View.OnClickListener {
    override fun onClick(v: View?) {
        // 클릭 시 처리 코드
    }
})

// 구현할 메서드가 하나뿐일 때 이를 람다식으로 변경 가능
button.setOnClickListener({v: View? ->
    // 클릭 시 처리 코드
})

// 메서드 호출 시 맨 뒤에 전달되는 인수가 람다식인 경우에는 람다식을 괄호 밖으로 뺄 수 있음
button.setOnClickListener() {v: View? -> 
    // 클릭 시 처리 코드
}

// 람다가 메서드의 유일한 인수인 경우 괄호 생략 가능, 컴파일러가 자료형 추론 가능할 때 자료형도 생략 가능
button.setOnClickListener {v: View? ->
    // 클릭 시 처리 코드
}

// 만약 클릭 시 처리 코드에서 v 인수를 사용하지 않으면 _기호로 변경하여 잘못 사용되는 것 방지 가능. 함수형 언어의 특징
button.setOnClickListener { _ ->
    // 클릭 시 처리 코드, v 인수를 사용하지 않음
}

// 람다식에서 인수가 하나이면 아예 생략하고 인수를 it로 접근할 수 있음
button.setOnClickListener {
    it.visibility = View.GONE // it는 View?타입의 v 인수
}
```