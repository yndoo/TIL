`벨로그 올리기 전 정리중`
## 람다 함수
* 익명 함수 정의 기법
* 함수를 간단하게 정의할 때 이용, 람다식이라고도 함
---
### 람다 함수 선언과 호출
* 일반 함수는 fun 키워드 사용하지만 람다함수는 `중괄호 { }`로 표현
* 람다 함수`{매개변수 -> 함수 본문}`
* 일반 함수`fun 함수명(매개변수) {함수 본문}`

> #### 람다 함수 사용 규칙
* 람다 함수는 {}로 표현
* {} 안에 화살표(->)가 있으며 화살표 왼쪽은 매개변수, 오른쪽은 함수 본문
* 함수 반환값은 함수 본문의 마지막 표현식

#### 람다 함수 선언
```kotlin
val sum = {no1: Int, no2: Int -> no1 + n02}
```
#### 람다 함수 호출문
```kotlin
sum(10, 20)
```
#### 람다 함수 선언, 호출 동시에
```kotlin
{no1: Int, no2: Int -> no1 + n02} (10, 20)
```
---
### 매개변수 없는 람다 함수
* 함수에 매개변수가 없어도 가능
* 화살표 왼쪽의 매개변수 정의 부분을 비워 두면 됨
* 화살표를 생략해도 됨
```kotlin
{-> println("function call")}
{println("function call")}
```
---
### 매개변수가 1개인 람다 함수
* 매개변수가 1개일 때 매개변수를 선언하지 않아도 함수로 전달된 값을 쉽게 이용할 수 있음
#### it 키워드 사용
```kotlin
fun main() {
   val some: (Int) -> Unit = {println(it)}
   some(10)
}
```
#### 실행 결과
```
10
```
* 람다 함수 안에 화살표가 없어 매개변수가 없는 것처럼 보이지만 함수 앞에 `(Int) -> Unit`이 매개변수가 1개인 람다 함수임을 알려줌
* 람다 함수에서 `it 키워드`를 이용해 매개변수를 사용하는 것은 해당 매개변수의 `타입을 식별할 수 있을 때`만 가능
---
### 람다 함수의 반환
* 람다 함수는 return 문 없음
* `마지막 줄의 실행 결과`가 람다 함수의 반환값
* 
#### 람다 함수의 반환문
```kotlin
fun main() {
   val some = {no1: Int, no2: Int ->
      println("in lambda function")
      no1 * no2
   }
   println("result : ${some(10,20)}")
}
```
#### 실행 결과
```
in lambda function
result : 200
```
* 람다 함수 안에 화살표가 없어 매개변수가 없는 것처럼 보이지만 함수 앞에 `(Int) -> Unit`이 매개변수가 1개인 람다 함수임을 알려줌
* 람다 함수에서 `it 키워드`를 이용해 매개변수를 사용하는 것은 해당 매개변수의 `타입을 식별할 수 있을 때`만 가능
---
## 함수 타입과 고차 함수
* 코틀린에서는 함수를 변수에 대입해서 사용 가능
* 앞에서 본 람다 함수도 주로 변수에 대입해서 사용했음
* 그런데 변수는 타입을 가지며 타입을 유추할 수 있을 때를 제외하곤 생략 불가능
* 그래서 변수에 함수를 대입하려면 변수를 함수 타입으로 선언해야 함

### 함수 타입 선언
* 함수 타입이란 함수 선언할 때 나타내는 매개변수와 반환 타입을 의미
> Int형 매개변수 2개 받아 결괏값을 Int로 반환하는 함수 선언
fun some**(no1: Int, no2: Int): Int** {
   return no1 + no2
}

* 이를 `(Int, Int) -> Int`로 표현 가능
```kotlin
val some: (Int, Int) -> Int = {no1: Int, no2: Int -> n01 + no2}
```
### 타입 별칭 - typealias
* 타입의 별칭을 선언하는 키워드 `typealias`
* 함수 타입뿐만 아니라 데이터 타입 선언할 때도 사용 (_함수 타입 선언에 주로 사용_)
#### 타입 별칭 선언과 사용 예시
* 코틀린의 정수 타입인 Int를 MyInt라는 새로운 별칭으로 선언
```kotlin
typealias MyInt = Int
fun main() {
   val data1: Int = 10
   val data2: MyInt = 10
}
```
#### 함수 타입 별칭 예시
* (Int, Int) -> Boolean 타입을 MyFunType 이라는 별칭으로 선언하면,
* MyFunType으로 선언한 변수에는 (Int, Int) -> Boolean 타입에 맞는 함수를 대입해야 함
``` kotlin
typealias MyFunType = (Int, Int) -> Boolean

fun main() {
   val someFun: MyFunType = {no1: Int, no2: Int ->
      no1 > no2
   }
   println(someFun(10, 20))
   println(someFun(20, 10))
}
```
⬇️ 실행 결과
```
false
true
```
### 매개변수 타입 생략
* 매개변수의 타입을 유추할 수 있다면 타입 선언 생략 가능
* 타입 유추 가능한 상황이라면 어디서든 통함
#### 매개변수 타입을 생략한 함수 선언
##### 예시 1
``` kotlin
typealias MyFunType = (Int, Int) -> Boolean

val someFun: MyFunType = {no1, no2 ->
   no1 > no2
}
```
##### 예시 2
```kotlin
val someFun: (Int, Int) -> Boolean = {no1, no2 ->
   no1 > no2
}
```
#### 변수 선언 시 타입 생략
* 또한 함수의 타입을 유추 가능하다면 변수를 선언할 때 타입을 생략 가능
```kotlin
val someFun = {no1: Int, no2: Int ->
   no1 > no2
}
```

### 고차 함수(high order function)
* 고차 함수란 `함수`를 매개변수로 전달받거나 반환하는 함수
* 함수를 매개변수로 이용할 수 있는 것은 함수를 변수에 대입할 수 있기 때문!
#### 고차 함수 예시
* 고차 함수 `hofFun` : 매개변수로 (Int) -> Boolean 함수를 받음, () -> String 함수로 반환함
```kotlin
fun hofFun(arg: (Int) -> Boolean):() -> String {
   val result = if(arg(10)) {
      "valid"
   } else {
      "invalid"
   }
   return {"hofFun result : $result"}
}
fun main() {
   val result = hofFun({no -> no > 0})
   println(result())
}
```
⬇️ 실행 결과
```
hofFun result : valid
```
