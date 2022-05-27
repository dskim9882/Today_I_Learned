# ***[Kotlin] Collection***
컬렉션은 개발에 유용한 자료구조를 말한다.
## List
List는 배열처럼 같은 자료형의 데이터을 순서대로 가지고 있는 자료구조이다. 중복된 elemenet를 가질 수 있고 추가, 삭제, 교체 등이 쉽다.
```kotlin
val foods: List<String> = listOf("라면", "갈비", "밥") // listOf() : 읽기 전용, 요소 변경 불가
```
```kotlin
val foods = listOf("라면", "갈비", "밥") // 형추론 가능
```
```kotlin
val foods = mutableListOf("라면", "갈비", "밥")

foods.add("초밥")       // 맨 뒤에 초밥 추가
foods.removeAt(0)       // 라면 삭제
foods[1] = "부대찌개"   // 밥을 부대찌개로 초기화

println(foods)      // [갈비, 부대찌개, 초밥]
println(foods[0])   // 갈비
```
## Map
Map은 key와 value의 쌍으로 이루어진 key가 중복될 수 없는 자료구조이다.
```kotlin
// 읽기 전용
val map = mapOf("a" to 1, "b" to 2, "c" to 3)

// 변경 가능
val citiesMap = mutableMapOf("한국" to "서울", "일본" to "동경", "중국" to "북경")

citiesMap["한국"] = "서울특별시"  // 덮어쓰기
citiesMap["미국"] = "워싱턴"      // 추가

// Map의 key와 value를 탐색
for((k, v) in citiesMap){
    println("$k -> $v")
}
```
## Set
Set은 중복되지 않는 요소들로 구성된 자료구조이다.
```kotlin
// 읽기 전용
val citySet = setOf("서울", "수원", "부산")

// 변경 가능
val citySet2 = mutableSetOf("서울", "수원", "부산")
citySet2.add("안양")        // 뒤에 추가
citySet2.remove("수원")     // 삭제

// Set의 크기
println(citySet2.size) // 3
// "서울"이 Set안에 있는 지 여부
println(citySet2.contains("서울")) // true
```