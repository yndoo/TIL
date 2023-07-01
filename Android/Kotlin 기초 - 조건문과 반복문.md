## 조건문
### 조건문 if~else
* 다른 언어들과 마찬가지로 else if(혹은 elif) 문법이 존재함.
* kotlin은 else if.
```kotlin
fun main() {
   var data = 10
   if (data > 10) {
      println("data > 10")
   } else if (data > 0 && data <= 10) {
      println("data > 0 && data <= 10")
   } else {
      println("data <= 0")
   }
}
```
👇실행 결과
```
data > 0 && data <= 10
```
#### 표현식 
* if~else 문은 표현식으로도 사용할 수 있음.
* 표현식으로 사용하려면 항상 else 구문이 있어야 함.
* if~else 표현식이 반환하는 결괏값은 각 영역의 마지막 줄에 해당함.
```kotlin
fun main() {
   var data = 10
   val result = if (data > 0) {
      println("data > 0")
      true // 참일 때 반환값
   } else {
      println("data <= 0")
      false // 거짓일 때 반환값
   }
   println(result)
}
```
👇실행 결과
```
data > 0
true
```
### 조건문 when
* when 문 사용 예시
```kotlin
fun main() {
   var data = 10
   when(data) {
      10 -> println("data is 10")
      20 -> println("data is 20")
      else -> {
         println("data is not valid data")
      }
   }
}
```
👇실행 결과
```
data is 10
```
* 다양한 유형 조건
* 데이터를 제시하지 않는 것도 가능하다.
```kotlin
fun main() {
   var data: Any = 10
   when(data) {
      is String -> println("data is String")
      20, 30 -> println("data is 20 or 30")
      in 1..10 -> println("data is 1..10")
      else -> {
         println("data is not valid data")
      }
   }
}
```
👇실행 결과
```
data is 1..10
```
#### 표현식 
```kotlin
fun main() {
   var data = 10
   val result = when {
      data <= 0 -> "data is <= 0"
      data > 100 -> "data is > 100"
      else -> "data is valid"
   }
   println(result)
}
```
👇실행 결과
```
data is valid
```
### 반복문 for
* for 문의 조건에 주로 범위 연산자인 in을 사용
```kotlin
fun main() {
   var sum: Int = 0
   for (i in 1..10) {
      sum += i
   }
   println(sum)
}
```
👇실행 결과
```
55
```
* for (i in 1..10) { ... } // 1부터 10까지 1씩 증가
* for (i in 1 until 10) { ... } // 1부터 9까지 1씩 증가(10은 미포함)
* for (i in 2..10 step 2) { ... } // 2부터 10까지 2씩 증가
* for (i in 10 downTo 1) { ... } // 10부터 1까지 1씩 감소
* for (i in data.indices) { ... } // data 배열의 인덱스 0, 1, 2, ...
* for ((index, value) in data.withIndex()) { ... } // data 배열의 인덱스와 값
  * python으로 치면 enumerate()

### 반복문 while
```kotlin
fun main() {
   var x = 0
   var sum1 = 0
   while (x<10) {
      sum1 += ++x
   }
   println(sum1)
}
```
👇실행 결과
```
55
```
