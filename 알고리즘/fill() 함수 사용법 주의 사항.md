백준 문제 중 유명한 [상어 초등학교](https://www.acmicpc.net/problem/21608) 문제를 풀다가 고생을 했다. 아무리 봐도 로직에 문제가 없고, 모든 테스트케이스와 인터넷 상의 반례를 모두 통과하는데 백준에 제출만 하면 1%만에 '틀렸습니다'가 떴다. 로직에 대해서도 진짜 (진~~~짜) 한참을 고민했으나 잘못 설정한 부분이 없다고 판단되었고, 테스트케이스는 모두 잘 통과하는데 백준에서는 1%만에 틀린다는 점에서 `메모리상의 오류`를 의심하게 되었다.

메모리 오류를 의심하고서는 로직에 대해 고민하던 것보다 빠르게 범인을 찾을 수 있었다.
바로 `fill`함수 사용에 오류가 있었던 것이다.

#### fill() 함수 헤더
```cpp
#include<algorithm>
```

#### 고친 점
```cpp
int likedArr[20][20];
int blanks[20][20];	
```
이렇게 선언된 배열이 있고, 나는 아래와 같이 초기화 하였다.
```cpp
fill(&likedArr[0][0], &likedArr[20][20], 0);
fill(&blanks[0][0], &blanks[20][20], 0);
```
여기서 다양하게 고쳐보았으나 아래 참고 블로그를 보고 다시 변경해서 AC를 받을 수 있었다..
```cpp
fill(&likedArr[0][0], &likedArr[19][20], 0);
fill(&blanks[0][0], &blanks[19][20], 0);
```

## 그 이유는?
[해당 링크](https://cplusplus.com/reference/algorithm/fill/)에서 보면
`The range filled is [first,last)` 라고 한다!! 그러므로 fill함수의 두 번째 매개변수로  1을 더한 이터레이터를 넣어줘야 한다.

## fill() 로 다차원 배열을 초기화하는 방법
```cpp
int arr1[a][b];
int arr2[a][b][c]; 
``` 
arr1, arr2 배열이 있다고 할 때 다음과 같이 사용하면 된다.
```cpp
fill(&arr[0][0], &arr[a-1][b], 초기화 할 숫자);
fill(&arr[0][0][0], &arr[a-1][b-1][c], 초기화 할 숫자);
```


## 오늘의 교훈  
> fill 사용을 조심하자  

### 참고  
https://cplusplus.com/reference/algorithm/fill/  
https://zynar.tistory.com/90  

### 코드 보기
https://github.com/yndoo/algorithm-study/blob/main/%EB%B0%B1%EC%A4%80/Gold/21608.%E2%80%85%EC%83%81%EC%96%B4%E2%80%85%EC%B4%88%EB%93%B1%ED%95%99%EA%B5%90/%EC%83%81%EC%96%B4%E2%80%85%EC%B4%88%EB%93%B1%ED%95%99%EA%B5%90.cc


