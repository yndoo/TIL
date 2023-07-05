> 에러 해결 기록

# 문제와 원인
## string 리소스 에러
`"is translated here but not found in default locale"`
새 프로젝트를 생성하자마자 string 리소스에 새로운 문자를 등록했는데 이런 에러가 떴다.
찾아보니 이 에러는 다국어 지원에 대한 처리가 제대로 되어 있지 않다는 오류로, 일반적으로 다국어 지원을 위한 별도의 처리를 한 적이 없다면 이 오류는 발생하지 않는다고 한다. 
## layout 리소스를 못 찾는 에러
`"Unresolved reference: activity_main"`
잘만 있는 activity_main.xml 파일을 안드로이드 스튜디오가 못 찾고 있다.
새 프로젝트를 생성할 때마다 이 에러를 본 것 같다.. 다른 개발자들도 같은 고민이 많았던 것 같다.

# 해결
* `Build 탭` > `Clean Project` 
두 에러 모두 Clean Project를 통해 해결되었다.
또는 안드로이드 스튜디오를 껐다 키는 것으로도 해결된다.
