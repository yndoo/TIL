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

##### 🐼 일반 클래스와 데이터 클래스의 차이점을 보기 위해 같은 인자 생성
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
