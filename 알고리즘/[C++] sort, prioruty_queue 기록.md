글 목적 : C++, Python 둘 다 코테언어로 사용하다보니 헷갈린다. 언젠가 또 'C++ sort'와 ;'C++ 최대힙' 등을 검색할 나를 위한 기록  

---  


헤더 : `#include <algorithm>`

## sort 
```cpp
sort(A.begin(),A.end()); 					// 오름차순
sort(B.begin(), B.end(), greater<int>()); 	// 내림차순
```
* sort(arr, arr+n);
* sort(v.begin(), v.end());
* sort(v.begin(), v.end(), compare); //사용자 정의 함수 사용
* sort(v.begin(), v.end(), greater<자료형>()); //내림차순 (Descending order)
* sort(v.begin(), v.end(), less<자료형>()); //오름차순 (default = Ascending order)

### compare
* 정렬 1차 기준 : 길이, 2차 기준 : 사전순
```cpp
bool compare(string a, string b){
    if (a.size()==b.size()){ //문자열 길이가 같으면, 사전 순
        return a < b;
    } else {                 //길이 다르면, 길이 짧은 순
        return a.size() < b.size();
    }
}
//사용 시
sort(v.begin(), v.end(), compare);
```

* vector에 pair로 값 쌍을 넣었더니 알아서 first기준, first가 같으면 second를 기준으로 정렬해준다.
```cpp
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    int N, x, y;
    vector<pair<int,int>> v;
    cin>>N;

    for(int i=0; i<N; i++){
        cin>>x>>y;
        v.push_back({x, y});
    }
    sort(v.begin(), v.end());

    for(int i=0; i<N; i++) {
        cout<<v[i].first <<" "<< v[i].second<<'\n';
    }
    return 0;
}
```

--- 

## priority_queue
* 최소힙 또는 최대힙
* compare을 그냥 함수로 만들면 안 됨
* 아래 예시는 절댓값이 작은 숫자 순으로 정렬, 절댓값이 같다면 작은 숫자 순서
* [해당 백준 문제](https://www.acmicpc.net/problem/11286)
```cpp
#include <iostream>
#include <vector>
#include<queue>

using namespace std;

struct compare {
    bool operator()(int a, int b){
        if (abs(a) == abs(b)){
            return a > b;
        }
        return abs(a) > abs(b);
    }
};

int main() {
    int N, num;
    vector<int> v;
    priority_queue<int, vector<int>, compare> q;
    cin>>N;
    for (int i=0; i<N; i++){
        cin>>num;
        if(num==0){
            if(q.empty()){
                cout<<0<<'\n';
                continue;
            }
            cout<<q.top()<<'\n';
            q.pop();
            continue;
        }
        q.push(num);
    }
    return 0;
}
```
