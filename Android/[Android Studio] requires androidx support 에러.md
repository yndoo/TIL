안드로이드 스튜디오에서 프로젝트를 새로 생성할 때마다 새로운 에러가 뜨는 것 같다. 보통은 `Clean Project`로 해결이 되는데, 오늘은 아니었다. 오늘도 에러 수집-!!

![](https://velog.velcdn.com/images/kuronuma_daisy/post/5416348e-42b5-4133-95f6-c87d3e07ec4d/image.png)
Empty Views Activity를 생성하려고 하는데 위 사진처럼 버튼이 활성화되지 않고 Fragment 등 몇몇의 액티비티 외에는 생성할 수 없는 상태였다. 그리고 버튼 옆에 `Requires AndroidX Support`라고 써있었다.

`gradle.properties` 파일에 다음 두 줄을 추가하라고 한다. AndroidX 라이브러리를 사용하려면 두 플래그를 모두 true로 설정해야 한다.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/f235ef41-e85e-433a-84aa-c699f61fe125/image.png)

```python
android.useAndroidX=true
android.enableJetifier=true
```
나는 android.useAndroidX는 있는데 아래 android.enableJetifier가 없었다. 추가하니 바로 되었다.


* `android.useAndroidX=true`는 쉽게 말하자면 AndroidX를 사용하겠다는 의미이다.   
_공식 문서_ : 이 플래그가 true로 설정되면 Android 플러그인에서 지원 라이브러리 대신 적절한 AndroidX 라이브러리를 사용한다. 지정하지 않으면 플래그는 기본적으로 false다.
* `android.enableJetifier=true`는 쉽게 말하자면 이전 버전 라이브러리를 AndroidX용으로 작성된 것 처럼 변환해주겠다는 의미이다.   
_공식 문서_ : 이 플래그가 true로 설정되면 Android 플러그인에서 자동으로 기존 타사 라이브러리를 이전하여 바이너리를 다시 작성해 AndroidX 종속 항목을 사용한다. 지정하지 않으면 플래그는 기본적으로 false다.

---
참고한 글  
https://developer.android.com/jetpack/androidx?hl=ko  
https://gozz123.tistory.com/9
