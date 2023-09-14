C++로 코테 풀이하며 기억하고 싶은 팁 적어가는 공간  
[벨로그 포스팅](https://velog.io/@kuronuma_daisy/C-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%9E%A1Tips-%EC%A0%81%EB%8A%94-%EA%B3%B5%EA%B0%84)  
---  
### 헤더
*`#include <bits/stdc++.h>` 에 모든 표준 라이브러리가 포함되어 있기 때문에 이 헤더 하나면 충분할 것 (코테볼때 해당 헤더 지원 안 해서 하나씩 씀 ㅠ.ㅠ)
* 해당 헤더는 그냥 자주쓰는 라이브러리 다 선언해놓은 파일
* 시간이나 공간이 낭비될 수 있다.
* [bits/stdc++.h 헤더 추가 방법](https://godog.tistory.com/entry/C-include-bitsstdch-%ED%97%A4%EB%8D%94-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

### 표준입출력
* scanf/printf와는 다르게 cin/cout에서는 입출력으로 인한 시간초과를 방지하기 위해 반드시 ios::sync_with_stdio(0), cin.tie(0)이라는 두 명령을 실행시켜야 합니다. 두 명령을 실행시키지 않으면 입/출력의 양이 많을 때 시간초과가 발생할 수 있습니다.

### STL vector
* insert, erase는 시간복잡도가 O(N). push_back, pop_back은 제일 끝에 원소를 추가하거나 빼는 것이니 O(1)입니다.
* vector에서 =를 사용하면 deep copy가 발생
* ange-based for loop 이용 가능
* int e : v1이라고 하면 복사된 값이 e에 들어가고 int& e : v1이라고 하면 원본이 e에 들어갑니다
* 기본적으로 vector의 size 메소드는 시스템에 따라 unsigned int 혹은 unsigned long long을 반환합니다. 그렇기 때문에 32비트 컴퓨터 기준 3번같이 쓰면 v1이 빈 vector일 때 v1.size() - 1이 unsigned int 0에서 int 1을 빼는 식이 되고, unsigned int와 int를 연산하면 unsigned int로 자동 형변환이 발생하기 때문에 (unsigned int)0 - (int)1은 -1이 아니라 4294967295이 되어버립니다. 4294967295이라는 이상한 값은 unsigned int overflow로 인해 생기게 된 값입니다.
* for(int i=0; i<=v.size()-1; i++) <<이렇게 구현하면 큰일난다는 뜻

### 배열
* 배열을 전역에 선언하면 따로 초기화 안 해도 0으로 초기화 됨.(bool 배열이면 false)
* int arr[10] = {0}; <<0으로 초기화

### 순열과 조합
* next_permutation(a, a+3);  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/deb4cdc2-0589-41b0-92b9-77ece0ab2437/image.png)  
*  next_permutation은 현재의 수열을 사전 순으로 생각했을 때의 다음 수열로 만들고 true를 반환하는 함수, do-while문으로 딱떨어짐
* 조합은 오른쪽처럼 0과 1이용해서 구현하면 됨
```cpp
#include <bits/stdc++.h>
using namespace std;
int main() {
	int arr[3] = { 1, 2, 3 };
	do {
		for (int i = 0; i < 3; i++)
			cout << arr[i] << ' ';
		cout << '\n';
	} while (next_permutation(arr, arr + 3));
	return 0;
}
```

--- 

## 참고
[기초작성요령](https://blog.encrypted.gg/724)  
[p.19,20 vector 관련](https://blog.encrypted.gg/927)  
[bits/stdc++.h 헤더 추가 방법](https://godog.tistory.com/entry/C-include-bitsstdch-%ED%97%A4%EB%8D%94-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)  
