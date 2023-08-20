`엘비스 연산자를 보고 삼항 연산자인줄 알았던 사람의 널 안전성 (? .? ?: !! 연산자) 기록. 🪄`  

# 널 안전성?
널`null`은 객체가 선언되었지만 초기화되지 않은 상태를 의미한다. 객체는 데이터가 저장된 주소가 저장되고, 이 주소로 메모리에 접근해서 데이터를 이용한다. 그런데 널은 객체가 주소를 가지지 못한 상태를 나타낸다.  

널인 객체를 이용하면 널인 상태릐 객체를 이요할 수 없다는 의미의 `널 포인트 예외`가 발생한다. 이때 널 안전성이란 널 포인트 예외가 발생하지 않도록 코드를 작성하는 것을 말한다.

kotlin에서 널 안전성을 지원한다는 것은 객체가 널인 상황에서 널 포인트 예외가 발생하지 않도록 연산자를 비롯해 여러 기법을 제공한다는 의미이다.

# 널 안전성 연산자
## 널 허용 - ? 연산자
코틀린에서 변수 타입을 널 허용`nullable`과 불허`not null`로 구분한다. ? 연산자로 널 허용 변수를 만들 수 있다.

```kotlin
var data1: String = "kkang"
data1 = null //오류!

var data2: String? = "kkang"
data2 = null //성공!
```
data2 변수는 String 타입 뒤에 ? 연산자를 추가했으므로 널 허용 변수가 되어 null을 대입할 수 있다.

## 널 안전성 호출 - ?. 연산자
널 허용 변수는 변수가 널인 상황을 고려해 프로그램을 작성해야한다.
```kotlin
var data: String = "kkang"
var length = data.length //오류!
```
null이 대입될 수 있는 data 변수를 널 안전성을 고려하지 않고 작성하여 오류가 발생한다. 따라서 널 허용으로 선언한 변수의 멤버에 접근할 때는 반드시 `?.` 연산자를 이용해야 한다.  

```kotlin
var data: String? = "kkang"
var length = data?.length //성공!
```
?. 연산자는 변수가 null이 아니면 멤버에 접근하지만 null이면 멤버에 접근하지 않고 null을 반환한다.

## 엘비스 - ?: 연산자
엘비스 연산자란 `?:` 기호를 말한다. (처음에 삼항연산자인줄 알았다..ㅋㅋ)  
이 연산자는 변수가 널이면 널을 반환한다. 변수가 널일 때 대입해야 하는 값이나 실행해야 하는 구문이 있을 때 사용한다.
```kotlin
fun main() {
   var data: String? = "kkang"
   println("data = $data : ${data?.length ?: -1}")
   data = null
   println("data = $data : ${data?.length ?: -1}")
}
```
🪄실행 결과
```
data = kkang : 5
data = null : -1
```

## 예외 발생 - !! 연산자
`!!`는 객체가 널일 때 예외를 일으키는 연산자이다. 객체가 널일 때 널 포인트 예외가 발생하지 않게 작성할 수도 있지만, 널 포인트 예외를 발생시켜야 할 때도 있다. 그럴 때 !! 연산자를 사용한다.
```kotlin
fun some(data: String?): Int {
   return data!!.length
}
fun main() {
   println(some("kkang"))
   println(some(null))
}
```
🪄실행 결과
```
5
Exception in thread "main" java.lang.NullPointerException
```
some() 함수에 문자열을 전달하면 오류 없이 length를 출력하며 정상 실행되고, null을 전달하면 data!!.length 코드로 예외 메시지를 출력한다.


