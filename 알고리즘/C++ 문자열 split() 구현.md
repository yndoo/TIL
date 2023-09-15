Python에 감사하게 되는 C++의 문자열 다루기..  
C++ 코테를 대비하여 나를 위해 남기는 기록이다.  
~~놀랍게도 아래 모든 것들이 파이썬에서는 split() 하나면 된다.~~  

## ',', ':', '-' 와 같은 구분자로 문자열 잘라 벡터에 넣기
* 포인트는 `istringstream`과 `getline` 인 것 같다.
```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

using namespace std;

int main() {
    vector<string> res;
    
    string now, input;
    string strbuffer;
    istringstream ss;

    cin>>input;
    ss.str(input);
    
    while (getline(ss, now, ':')){ //ss에서 ':'를 만날 때까지 now에 담아 배출
        res.push_back(now);
    }
    for(int i=0; i<res.size(); i++){
        cout<<res[i]<<endl;
    }
    
    return 0;
}
```

## ' ' 공백으로 문자열 나누기
* istringstream에 공백으로 자르는 기능이 있다. 사용할 때와 안 할 때를 모두 기록하겠다.
### istringstream.str(); 이용
* 근데 이 기능을 사용할 땐 cin>>str로 받을 수가 없다. cin>>로 입력을 받으면 공백까지만 입력되기 때문이다. 그래서 `getline(cin, input)`으로 받았다.
```cpp
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

int main() {
    string input, output;
    istringstream ss;

    getline(cin, input);
    
    ss.str(input);
    while(ss>>output){
        cout<<output<<endl;
    }
    return 0;
}
```
### cin>> 사용. (개수가 정해져있고 몇 개 안 될 때)
* cin >> a >> b; 로 입력받으면 알아서 공백으로 나뉘어 a, b 각각에 저장된다.
```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string input1, input2, input3;

    cin >> input1 >> input2 >> input3;

    cout << input1 << " " << input2 << " " << input3;
    
    return 0;
}
```
## 구분자가 한 글자가 아닐 수 있다!?
* 바킹독 쓰앵임이 직접 구현해보라고 하셔서 해보았다.
* find() 사용할 때 실수해서 잠깐 먼 길을 돌아왔었다..ㅋ
```cpp
vector<string> split(string& s, string& sep) {
    int pos = 0;
    vector<string> res;

    while (pos < s.size()) {
        int nxt_pos = s.find(sep, pos); //pos부터 찾는 것
        if (nxt_pos == -1) {
            nxt_pos = s.size();
        }
        if (nxt_pos-pos>0) res.push_back(s.substr(pos, nxt_pos-pos));
        pos = nxt_pos + sep.size();
    }
    return res;
}
```
