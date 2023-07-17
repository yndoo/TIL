`아직 미완성!!`
## 데이터 클래스
* 데이터 클래스는 `data` 키워드로 선언
* VO 클래스를 편리하게 이용할 수 있게 해줌  
```kotlin
class NonDataClass(val name: String, val email: String, val age: Int)

data class DataClass(val name: String, val email: String, val age: Int)
```
### 객체의 데이터를 비교하는 equals() 함수  
* `equals()` 함수로 객체의 데이터가 같은지 확인 가능
* VO 클래스는 데이터를 주요하게 다루므로 데이터가 서로 같은지 비교하는 경우가 많음

#### 일반 클래스와 데이터 클래스의 차이점을 보기 위해 같은 인자 생성
```kotlin
fun main() {
   val non1 = NonDataClass("bae","a@a.com",10)
   val non2 = NonDataClass("bae","a@a.com",10)
   
   val data1 = DataClass("bae","a@a.com",10)
   val data2 = DataClass("bae","a@a.com",10)
}
```
##### 🐼 데이터 비교
```kotlin
println("non data class equals : ${non1.equals(non2)}")
println("data class equals : ${data1.equals(data2)}")
```
##### 🐼 실행 결과
```
non data class equals : false
data class equals : true
```
* equals() 함수로 일반 클래스 객체를 비교하면 `객체 자체`를 비교하므로 false
* 데이터 클래스의 객체를 비교하면 객체 자체가 아닌 `객체의 데이터`를 비교하므로 true

#### 주 생성자에 선언한 멤버 변수 데이터만 비교 대상
##### 🐼 예시
```kotlin
data class DataClass(val name: String, val email: String, val age: Int) {
   lateinit car adress: String
   constructor(name: String, email: String, age: Int, address: String):
      this(name, email, age) {
      this.address = address
   }
}
fun main() {
   val obj1 = DataClass("kim", "a@a.com", 10, "seoul")
   val obj2 = DataClass("kim", "a@a.com", 10, "busan")
   
   println("obj1.equals(obj2) : ${obj1.equals(obj2)}")
}
```
##### 🐼 실행 결과
* 주 생성자의 멤버 변수가 아닌 address 데이터는 비교되지 않아 true가 나옴
```
obj1.equals(obj2) : true
```

### 객체의 데이터를 반환하는 toString() 함수
* 데이터 클래스를 사용하며 객체가 가지는 값을 확인해야 할 때 사용
* 일반 클래스와 데이터 클래스의 toString() 함수 반환값이 다름!
##### 🐼 예시
```kotlin
fun main() {
   class NonDataClass(val name: String, val email: String, val age: Int)
   data class DataClass(val name: String, val email: String, val age: Int)
   
   val non = NonDataClass("k", "a@a.com", 10)
   val data = DataClass("k", "a@a.com", 10)
   
   println("non data class toString : ${non.toString()}")
   println("data class toString : ${data.toString()}")
}
```
##### 🐼 실행 결과
* 일반 클래스 객체의 toString()함수 반환값은 의미 있는 데이터가 아님
* 데이터 클래스의 toString()함수는 객체가 포함하는 멤버 변수의 데이터를 출력
* toString() 역시 주 생성자의 매개변수에 선언된 데이터만 출력 대상
```
non data class toString : com.example.test4.ch2.Test2Kt$main$NonDataClass@61bbe9ba
data class toString : DataClass(name=k, email=a@a.com, age=10)
```
