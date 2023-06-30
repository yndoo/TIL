## 글 작성 이유와 계획
![](https://velog.velcdn.com/images/kuronuma_daisy/post/60145ff2-07e2-4927-af73-e7b00a73bc45/image.jpg)  
지금까지는 교내 프로젝트를 통해 안드로이드 프로그래밍을 공부했다. 내가 생각한 프로젝트를 통한 공부의 장점은 일단 부딪혀 실전 감각을 키울 수 있다는 것이다. 단점은 빠르게 필요한 것만 배우게 되기 때문에 기초가 쌓이기 어렵다는 점인 것 같다. 나는 지금 기초가 매우 부족하다고 느끼는 중!!🥲

따라서 현재 상황(대졸백수)의 이점을 살려 차근차근 기초를 다져보려고 한다. 
위 사진의 책을 바탕으로 진도를 나가고 대표적인 내용 또는 배운점 위주로 글을 작성할 계획이다. 같은 책 2022년 개정판이 새로 나왔던데... 내용은 거의 같아보였다. 상관없을듯!  

방학동안(~~취준생은 방학이 없다~~) 기초를 다지고, 예전부터 연습용으로 개발하던 애플리케이션을 다시 기획하여 간단하게나마 완성지어보려고 한다. 화이팅😁 

---  

## 코틀린 소개
* 코틀린으로 안드로이드 앱을 개발할 수 있는 것은 자바의 가상 머신인 JVM에 기반을 둔 언어이기 때문이다.
* 코틀린 컴파일러(kotlinc)가 코틀린 파일을 컴파일하면 자바 바이트 코드가 만들어 지고, 이를 JVM이 실행한다.
### 자바 대비 코틀린 장점
* 표현력과 간결함
* 안전한 코드 
   * 널 안정성을 지원(널 허용과 널 불허용으로 구분해서 선언)
* 상호 운용성
   * 자바와 100% 호환
* 구조화 동시성
   * 코루틴 기법 이용하면 비동기 프로그래밍을 간소화 할 수 있다.
   * 네트워크 연동이나 데이터베이스 갱신과 같은 작업을 할 때 이용하면 프로그램을 더 간단하고 효율적으로 작성할 수 있다.
## 변수
### 변수 선언하기
* var : variable 줄임말, 값을 바꿀 수 있는 변수
* val : value 줄임말, 초깃값이 할당되면 값을 바꿀 수 없는 변수
```kotlin
val data1 = 10
val data2 = 10
fun main() {
   data1 = 20	// 오류!
   data2 = 20	// 성공!
}
```
### 타입 지정과 타입 추론
* 변수명 뒤에 콜론(:)을 추가해 타입 명시
* 타입을 유추할 수 있는 값의 경우 생략 가능
```kotlin
val data1: Int = 10
val data2 = 10
```
### 초깃값 할당
* 최상위에 선언한 변수나 클래스의 멤버 변수는 선언할 때 초깃값 할당
* 함수 내에 선언하는 함수는 선언과 동시에 초기화 안 해도 됨
### 초기화 미루기
* lateinit나 lazy 키워드를 이용해 이후에 초깃값을 나중에 할당할 것을 명시할 수 있음
#### 1. lateinit
```kotlin
lateinit var data1: Int		// 오류!
lateinit val data2: String	// 오류!
lateinit val data3: String	// 성공!
```
lateinit은 아래 2가지 규칙을 지켜야 함
* lateinit은 var 키워드로 선언한 변수에만 사용할 수 있음
* Int, Long, Short, Double, Float, Boolean, Byte 타입에는 사용할 수 없음
#### 2. lazy
* by lazy{ } 형식으로 선언
* 소스에서 해당 변수가 최초 사용되는 순간에 by lazy 내부가 자동으로 실행되어 그 결괏값이 변수의 초깃값으로 할당
* 중괄호 부분을 여러 줄로 작성한다면 마지막 줄의 실행 결과가 변수의 초깃값이 됨
```kotlin
val data4: Int by lazy{
   println("in lazy...")
   10
}

fun main() {
   println("in main...")
   println(data4 + 10)
   println(data4 + 10)
}
```
👇실행 결과
```
in main...
in lazy...
20
20
```
### 데이터 타입
#### 기초 타입 객체
* Int, Short, Long, Double, Float, Byte, Boolean
```kotlin
val a1: Byte = 0b00001011

val a2: Int = 123
val a3: Short = 123
val a4: Long = 10L
val a5: Double = 10.0
val a6: Float = 10.0f

val a7: Boolean = true
```
#### 문자와 문자열
* Char, String
```kotlin
val a: Char = 'a'
if (a == 1) { // 오류!
}

val str1 = "Hello\nWorld!"
val str2 = """Hello
World!"""
```
* 문자열 템플릿 : $
```kotlin
fun main() {
   fun sum(no: Int) {
   var sum = 0
   for (i in 1..no) {
      sum += i
      }
   }
   
   val name: String = "daisy"
   println("name : $name, sum : ${sum(10)}, plus : ${10+14}")
}
```
👇실행 결과
```
name : daisy, sum : 55, plus : 24
```
#### Any - 모든 타입 가능
* 코틀린에서 최상위 클래스
* 모든 코틀린의 클래스는 Any의 하위 클래스
* 모든 타입의 데이터를 할당 가능
```kotlin
val data1: Any = 10
val data2: Any = "hi"

class User
val data3: Any = User()
```
#### Unit - 반환문이 없는 함수
* 다른 타입과 달리 데이터의 형식이 아닌 특수한 상황을 표현하려는 목적으로 사용
* Unit타입 변수에는 Unut 객체만 대입 가능 << 의미 없음
* 함수에서 반환문의 없을을 명시적으로 나타낼 때 사용
* 반환 타입을 생략하면 자동으로 Unit이 적용됨
```kotlin
fun some(): Unit {
   println(10+20)
}
```
#### Nothing - null이나 예외를 반환하는 함수
* Unit과 마찬가지로 의미 있는 데이터가 아니라 특수한 상황을 표현
* Nothing으로 선언한 변수에는 null만 대입할 수 있음
* 어떤 함수의 반환 타입이 Nothing이면 반환은 하지만 의미 있는 값은 아니라는 의미
#### 널 허용과 불허용
* 타입 뒤에 물음표(?)로 null을 대입할 수 있는 변수(nullable)인지 없는 변수(not null)인지 구분
```kotlin
var data1: Int = 10
data1 = null	// 오류!

var data2: Int? = 10
data2 = null	// 성공!
```
### 컬렉션 타입
#### Array - 배열 표현
* 배열의 타입은 제네릭으로 표현
* 배열 데이터 접근은 대괄호([ ])를 이용해도 되고 set()이나 get() 함수를 이용할 수 O
```kotlin
fun main() {
   val data1: Array<Int> = Array(3,{0})	// 0으로 초기화한 데이터를 3개 나열한 정수형 배열 선언
   data1[0] = 10
   data2[1] = 20
   data1.set(2,30)	// 배열에서 2번째 데이터를 30으로 설정
   
   println(
   """
   array size : ${data1.size}
   array data : ${data1[0]}, ${data1[1]}, ${data1.get(2)}
   """
   )
}
```
👇실행 결과
```
array size : 3
array data : 10, 20, 30
```
#### 기초 타입의 배열
* 만약 배열의 데이터가 기초 타입이라면 Array에 제네릭으로 명시하지않고 각 기초 타입의 배열 클래스 사용 가능
* BooleanArray, ByteArray, CharArray, DoubleArray, FloatArray, IntArray, LongArray, ShortArray 클래스 있음
```kotlin
val data1: IntArray = IntArray(3, {0})
val data2: BooleanArray = BooleanArray(3, {false})
```
* arrayOf()라는 함수를 이용해서 배열을 선언할 때 값을 할당할 수 있음
* arrayOf() 함수도 기초 타입을 대상으로 하는 booleanArrayOf(), byteArrayOf(), charArrayOf(), doubleArrayOf(), floatArrayOf(), intArrayOf(), longArrayOf(), shortArrayOf() 함수를 제공함
```kotlin
val data1 = arrayOf<int>(10, 20, 30)
val data2 = intArrayOf(10, 20, 30)
val data3 = booleanArrayof(true, false, true)
```
#### List, Set, Map
* List, Set, Map은 Collection 인터페이스를 타입으로 표현한 클래스이며 통틀어 컬렉션 타입 클래스라고 함
   * List : 순서가 있는 데이터 집합, 데이터 중복 허용
   * Set : 순서가 없음, 데이터 중복 허용하지 않음
   * Map : 키와 값으로 이루어진 데이터 집합, 순서 없음, 키의 중복은 허용하지 않음
* Collection 타입의 클래스는 가변(mutable) 클래스와 불변(immutable) 클래스로 나뉨
* 불변 클래스는 초기에 데이터 대입하면 더 이상 변경 불가
* 가변 클래스는 초깃값 대입 이후 데이터 추가하거나 변경 가능  

|    | 타입 | 함수 | 특징 
|----|:----|:----|:----
|List|List|listOf()|불변, size(), get() 함수만 제공
|    |MutableList|mutableListOf|가변, add(), set() 함수도 제공
|Set|Set|setOf()|불변, size(), get() 함수만 제공
|    |MutableSet|mutableSetOf|가변, add(), set() 함수도 제공
|Map|Map|mapOf()|불변, size(), get() 함수만 제공
|    |MutableMap|mutableMapOf|가변, add(), set() 함수도 제공
##### List 사용 예시
```kotlin
fun main() {
   var list = listOf<Int>(10, 20, 30)
   var mutableList = mutableListOf<Int>(10, 20, 30)
   mutableList.add(3, 44)
   mutableList.set(2, 33)
   println(
   """
   list size : ${list.size}
   list data : ${list[0]}, ${list.get(1)}, ${list.get(2)}
   """
   )

   println(
   """
   mutableList size : ${mutableList.size}
   mutableList data : ${mutableList[0]}, ${mutableList.get(1)}, ${mutableList.get(2)}, ${mutableList.get(3)}
   """
   )
}
```
👇실행 결과
```
list size : 3
list data : 10, 20, 30


mutableList size : 4
mutableList data : 10, 20, 33, 44
```
##### Map 사용 예시  
Map 객체의 키와 값은 Pair 객체를 이용할 수도 있고 '키 to 값' 형태로 이용할 수도 있음
```kotlin
fun main() {
   var map = mapOf<String, String>(Pair("one","hello"), "two" to "world")
   
   println(
   """
   map size : ${map.size}
   map data : ${map.get("one")}, ${map.get("two")}
   """
   )
}
```
👇실행 결과
```
map size : 2
map data : hello, world
```
### 함수 선언하기
* 함수의 매개변수에는 var나 val 키워드를 사용할 수 없음, 무조건 val이 자동으로 적용됨
* 함수 안에서 매개변숫값을 변경할 수 없음
* 함수의 매개변수에 기본값(default value)을 선언할 수 있음. 기본값을 선언했다면 호출할 때 인자를 전달하지 않아도 됨
```kotlin
fun main() {
   fun some(data1: Int, data2: Int = 10): Int {
      return data1 * data2
   }
   println(some(10))
   println(some(10,20))
}
```
👇실행 결과
```
100
200
```
* 매개변수명 지정해서 호출도 가능
* some(data2 = 20, data1 = 10)
