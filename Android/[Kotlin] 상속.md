## 상속 Inheritance
클래스를 선언할 때 다른 클래스를 참조해서 선언하는 것
* 상위 클래스에 정의된 멤버(변수, 함수)를 하위 클래스에서 자신의 멤버처럼 사용할 수 있음.
* 코틀린의 클래스는 기본적으로 다른 클래스가 상속할 수 없음 
  * `open` 키워드를 사용해야 함
* 하위 클래스를 선언할 때는 이름 뒤에 콜론`:`을 입력하고 상속받을 클래스명 입력  

🌳 예시
```kotlin 
open class Super { // 상속할 수 있게 open 키워드 사용
}
class Sub: Super() { // Super를 상속받아 Sub 클래스 선언
}
```
### 상속과 생성자
* 상속을 받은 하위 클래스의 생성자에서는 상위 클래스의 생성자를 호출해야 함
* `class Sub: Super() { }` 코드에서는 Super 클래스를 상속받으려 이 클래스의 매개변수가 없는 생성자를 호출  
* 상위 클래스의 생성자 호출문을 꼭 클래스 선언부에 작성할 필요 X

🌳 매개변수가 있는 상위 클래스의 생성자 호출
```kotlin 
open class Super(name: String) {
}
class Sub(name: String): Super(name) {
}
```

🌳 하위 클래스에 보조 생성자만 있는 경우 상위 클래스의 생성자 호출 
```kotlin 
open class Super(name: String) {
}
class Sub: Super {
   constructor(name: String): super(name) {
   }
}
```

### 오버라이딩 - 재정의
상위 클래스에 정의된 멤버를 하위 클래스에서 재정의
* 상위 클래스에서 오버라이딩을 허용할 변수나 함수 선언 앞에 `open` 키워드를 추가
* 하위 클래스에서 재정의할 때는 선언문 앞에 `override` 키워드 추가

🌳 예시
```kotlin 
open class Super { 
   open var someData = 10
   open fun someFun() {
      println("i am super class function : $someData")
   }
}
class Sub: Super() {
   override var someData = 20
   override fun someFun() {
      println("i am sub class function : $someData")
   }
}
fun main() {
   val obj = Sub()
   obj.someFun()
}
```
👇실행 결과
```
i am sub class function : 20
```

### 접근 제한자
클래스의 멤버를 외부의 어느 범위까지 이용하게 할 것인지를 결정하는 키워드
* 코틀린 제공 접근 제한자 : public, internal, protected, private

| 접근 제한자 | 최상위에서 이용 | 클래스 멤버에서 이용 
|:----:|:----:|:----:
| public | 모든 파일에서 가능 | 모든 클래스에서 가능
| internal | 같은 모듈 내에서 가능 | 같은 모듈 내에서 가능
| protected | 사용 불가 | 상속 관계의 하위 클래스에서만 가능
| private | 파일 내부에서만 이용 | 클래스 내부에서만 이용

🌳 예시
```kotlin 
open class Super {
      var publicData = 10
      protected var protectedData = 20
      private var privateDate = 30
   }
}
class Sub: Super() {
      fun subFun() {
         publicData++		//성공!
         protectedData++	//성공!
         privateData++		//오류!
      }
   }
}
fun main() {
   val obj = Super()
   obj.publicData++		//성공!
   obj.protectedData++	//오류!
   obj.privateData++	//오류!
}
```
