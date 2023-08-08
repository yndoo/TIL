8x8 체스판에 서로 위협하지 않는 8개의 퀸을 놓는 `여덟 퀸 문제`가 있다.
이를 일반화한 `N-Queens` 문제는 NxN 체스판에서 N개의 퀸을 서로 위협이 되지 않게 두는 경우의 수를 찾는 문제이다. 알고리즘 문제로 자주 등장하며, 백트래킹으로 해결할 수 있다.

백준에서 [N-Queens](https://www.acmicpc.net/problem/9663) 문제를 풀어볼 수 있다.

## 이해 과정 (풀이 과정)
### 1. 퀸의 행마법 - 같은 열 체크
![](https://velog.velcdn.com/images/kuronuma_daisy/post/342a70fb-7e9e-4eda-8f0b-8790530a7f40/image.png)
* 퀸은 위 그림처럼 같은 열이나 행, 또는 대각선으로 움직일 수 있다.
* 그래서 N-Queens 문제에서 또다른 퀸을 놓을 수 있는지 확인할 때 첫 조건으로 `같은 열에 있지 않은 지`를 먼저 확인한다.
* col[i] : i번째 행에 퀸이 몇번째 열에 있는지 저장

### 2. 대각선 체크
* 대각선에 있는 퀸끼리는 |행의 차|와 |열의 차|가 같다.
* 절대값으로 대각선 위협 판단
* abs(i-k) == abs(col[i]-col[k])

## Python 코드

`col` = `[0, 0, 0, 0, ..., 0]` = `배열 인덱스 i번째의 행에 퀸이 있는 열 인덱스를 저장`
`isokay(i, col)` : 퀸 위치 저장된 col배열로 `(i, col[i])`위치에 퀸을 놔도 okay인지 체크하는 함수
`finding(i, col)` : i번째 행에서 1~N 열에 퀸을 놓아보며 맞는 경우의 수를 찾으면 카운트하는 함수

### 최적화 전 코드 (PyPy3 제출, 30768ms)
```python
import sys
myinput = sys.stdin.readline
N= int(myinput())
col = [0] * (N+1)
answer = 0

def isokay(i,col):
    k = 1
    while k<i: # 같은 행은 안 봄
        #대각선이거나 같은 열에 있는지 체크
        if abs(col[i]-col[k])==abs(i-k) or (col[i]==col[k]): 
            return False
        k+=1
    return True

def finding(i, col):
    global answer
    if isokay(i,col): # i번째 행이 유망한지 체크
        if i == N: # N번째 행의 기물까지 okay되면 경우의 수를 하나 찾은 것!
            answer += 1
        else:
            for j in range(1,N+1):  # 1~N번째 열까지 하나씩 놓아보며 재귀로 확인
                col[i+1]=j
                finding(i+1,col)

finding(0, col) # 0행부터 탐색 시작
print(answer)
```

### 3초정도 시간 줄인 Python 코드  (PyPy3 제출, 27404ms)
* 함수 매개변수로 배열 주고 받는 것 제거
* 로직 순서 조정
```python
import sys
myinput = sys.stdin.readline

N= int(myinput())
col = [0] * (N)
answer = 0

def isokay(i):
    k = 0
    while k<i:
        if abs(col[i]-col[k])==abs(i-k) or (col[i]==col[k]):
            return False
        k+=1
    return True

def finding(i):
    global answer
    if i==N: # 마무리된 것 확인
        answer+=1
    else: 
        for j in range(N):
            col[i] = j 		# 1~N(0~N-1)열에 넣어보며
            if isokay(i):	# 즉시 확인 후 재귀
                finding(i+1)

finding(0)
print(answer)
```

## C++ 코드 (4248ms)
함수 매개변수 변경, 로직 순서 변경, 배열을 2차원 아닌 1차원 배열 사용 등 최적화할 수 있도록 노력했으나 파이썬이 느려 시간초과가 난다. 하지만 PyPy3으로 제출하면 통과가 된다. 질문게시판을 보면 다른 파이썬 풀이자들도 파이썬이 느려 PyPy3으로 제출하는데 시간이 거의 턱걸이로 걸리기 때문에 운이 좋으면 통과, 안 좋으면 시간초과가 뜬다(3초 줄이게 되어 이제 항상 통과되긴 함). 경험상 C++로는 노가다 풀이법을 사용해도 파이썬보다 시간 여유가 있을 정도로 빨랐던 것 같아 비교삼아 C++로도 풀어봤다.

```cpp
#include <iostream>
#define MAX 15
using namespace std;

int col[MAX];
int N, answer=0;


bool isokay(int i){
    int k=0;
    while (k<i){
        if (col[i]==col[k] || abs(col[i]-col[k])==i-k){
            return false;
        }
        k++;
    }
    return true;
}

void finding(int i){
    if (i==N){
        answer ++;
    } else {
        for (int j=0; j<N; j++) {
            col[i] = j;
            if (isokay(i))
                finding(i+1);
        }
    }
}

int main() {
    cin >> N;
    finding(0);
    cout<<answer;
}
```


## 설명이 좋은 강의 영상
[N Queens 이해에 큰 도움이 된 영상](https://youtu.be/HRwFgtiqHH0)

## 두 코드와 문제 깃허브
[깃허브](https://github.com/yndoo/algorithm-study/tree/main/%EB%B0%B1%EC%A4%80/Gold/9663.%E2%80%85N%EF%BC%8DQueen)
