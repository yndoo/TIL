### 상황
안드로이드에서 Postman의 Mock서버로 Post 통신을 테스트 중이었다.

### retrofit2 failure 로그
안드로이드에서 통신 실패 로그가 떴다! 하지만 서버로그에는 통신이 잘 완료된 것으로 떴다.
아래는 안드로이드의 로그 내용이다.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/4127e0ae-b5b0-4bc4-bb0f-dbf87b4a13d7/image.png)
로그는 다음과 같다.
```
com.google.gson.stream.MalformedJsonException: Unterminated object at line 4 column 6 path $.username
````

### 해결 과정
후.. 당황하지 않고 차근차근 읽어보고 서버 응답을 요리조리 바꿔보고 구글링도 해봤다.
이 에러는 서버의 응답 메시지에 문제가 있는 것으로 보인다!!
![](https://velog.velcdn.com/images/kuronuma_daisy/post/01912224-389d-4086-80fb-a329f2ec665d/image.png)

알고보니 서버의 응답 데이터에 쉽표 하나를 빼먹었다!!!!
Mock 서버에서는 응답의 타입이 Json이 아닌 Text로 설정되어있어 오류가 나지 않았었다😓
```json
{
    "result": "GREAT",
    "username": "John"
    "age": "24"
}
```
(찾아보세요)

### 결과
![](https://velog.velcdn.com/images/kuronuma_daisy/post/351373b0-b2a1-41e8-8649-8cd19452d86b/image.png)
결국 마지막엔 서버의 응답을 정상적으로 로그에서 볼 수 있었다!
