> 이전 게시물 보기 
[Koltin 기초 - 조건문과 반복문](https://velog.io/@kuronuma_daisy/Kotlin-%EA%B8%B0%EC%B4%88-%EC%A1%B0%EA%B1%B4%EB%AC%B8%EA%B3%BC-%EB%B0%98%EB%B3%B5%EB%AC%B8#%EC%A1%B0%EA%B1%B4%EB%AC%B8)  

## 클래스와 생성자
### 클래스 선언
* class User 부분이 클래스 선언부, 중괄호 {} 영역이 본문
```kotlin
class User {}
```
* 클래스의 멤버는 생성자, 변수, 함수, 클래스로 구성
* 코틀린의 생성자는 constructor 라는 키워드로 선언하는 함수
* 클래스 안에 다른 클래스를 선언할 수 있음

🌼 예시
```kotlin
class User {
   var name = "daisy"
   constructor(name: String) {
      this.name = name
   }
   fun someFun() {
      println("name : $name")
   }
   class SomeClass { }
}
```
### 주 생성자
* 코틀린 클래스는 생성자를 주 생성자와 보조 생성자로 구분
* 한 클래스 안에 주 생성자, 보조 생성자 각각만 선언할 수도 있고 둘다 선언할 수도 있음
* 주 생성자 선언은 한 클래스에 하나만 가능
* constructor 키워드 생략 가능
* 만약 주 생성자를 선언하지 않으면 컴파일러가 매개변수가 없는 주 생성자를 자동으로 추가
* 주 생성자는 클래스 선언부에 있기 때문에 본문을 구현하고 싶으면 init 키워드를 이용

🌼 예시
```kotlin
class User (name: String, count: Int) {
   init {
      println("i am init....")
   }
}
fun main() {
   val user = User("daisy", 300)
}
```
#### 생성자의 매개변수를 클래스의 멤버 변수로 선언하는 방법
* 생성자의 매개변수는 기본적으로 생성자에서만 사용할 수 있는 지역 변수
##### 방법 1. 클래스 멤버 변수에 생성자 매개변숫값 대입
```kotlin
class User (name: String, count: Int) {
   // 클래스 멤버 변수 선언
   var name: String
   var count: Int
   init {
      // 클래스 멤버 변수에 생성자 매개변숫값 대입
      this.name = name
      this.count = count
   }
   fun someFun() {
      println("name : $name, count : $count")	// 성공
   }
   fun main() {
      val user = User("daisy", 300)
      user.someFun()
   }
}
```
👇실행 결과
```
name : daisy, count : 300)
```
##### 방법 2. 매개변수를 var나 val 키워드로 선언
* 원래 함수는 매개변수를 선언할 때 var나 val 키워드를 추가할 수 없음
* 주 생성자에서만 유일하게 var나 val 키워드로 매개변수 선언 가능
```kotlin
class User (val name: String, val count: Int) {
   fun someFun() {
      println("name : $name, count : $count")	// 성공
   }
   fun main() {
      val user = User("daisy", 300)
      user.someFun()
   }
}
```
👇실행 결과
```
name : daisy, count : 300)
```
### 보조 생성자 
* 보조 생성자는 클래스의 본문에 constructor 키워드로 선언하는 함수
* 클래스 본문에 선언하므로 여러 개 추가 가능
* init 없이 중괄호 { }로 묶어서 객체 생성과 동시에 실행 영역 지정 가능
```kotlin
class User {
   constructor(name: String) {
      println("constructor(name: String) call...")
   }
   constructor(name: String, count: Int) {
      println("constructor(name: String, count: Int) call...")
   }
   fun main() {
      val user1 = user("kuronuma")
      val user2 = user("daisy", 300)
   }
}
```
👇실행 결과
```
constructor(name: String) call...
constructor(name: String, count: Int) call...
```
#### 보조 생성자에 주 생성자 연결
* 주 생성자, 보조 생성자 모두 선언한다면 반드시 생성자끼리 연결해야 함
* 보조 생성자로 객체를 생성할 때 보조 생성자에서 주 생성자를 호출해야 함
* this()구문 이용
🌼 예시
```kotlin
class User (name: String) {
   constructor(name: String, count: Int): this(name) { 	// 보조 생성자로 객체 생성할 때 주 생성자도  함께 호출됨
   (...생략...)
   }
}
fun main() {
   val user = User("daisy", 300)
}
```
* 보조 생성자가 여러 개라면 이때에도 보조 생성자로 객체를 생성할 때 주 생성자가 호출되게 해야 함
🌼 예시
```kotlin
class User (name: String) {
   constructor(name: String, count: Int): this(name) { 	
   // ⑶ 보조 생성자에서 주 생성자 호출
   (...생략...)
   }
   constructor(name: String, count: Int, emial: String): this(name, count) { 	// ⑵ 보조 생성자에서 다른 보조 생성자 호출
   (...생략...)
   }
}
fun main() {
   val user = User("daisy", 300,"abs123@aaa.com") // ⑴ 두 번째 보조 생성자 호출
}
```
