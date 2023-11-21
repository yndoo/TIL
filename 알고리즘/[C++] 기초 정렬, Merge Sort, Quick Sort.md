# 기초 정렬
## 선택 정렬
책장의 크기가 뒤죽박죽인 책들을 정렬할 때 모두가 찾게되는 방법
`큰 책부터 뒤로 보내기`
가장 큰 책을 찾고 그 책을 뒤로 보내야하므로 `O(N^2)`의 시간복잡도 걸림
```cpp
	int arr[10] = { 6, 2, 99, 24, 80, 130, 5, 62, 1, 301 };
	int n = 10;
	for (int i = n - 1; i > 0; i--) {
		int mxidx = 0;
		for (int j = 1; j <= i; j++) {
			if (arr[mxidx] < arr[j]) mxidx = j;
		}
		swap(arr[mxidx], arr[i]);
	}
```

내용은 같은데 코드의 길이를 줄이면

```cpp
	int arr[10] = { 6, 2, 99, 24, 80, 130, 5, 62, 1, 301 };
	int n = 10;
	for (int i = n - 1; i > 0; i--) {
		swap(*max_element(arr, arr + i + 1), arr[i]);
	}
```

## 버블 정렬
구현하기 가장 편한 건 버블 정렬
앞뒤 비교해서 큰게 뒤로가도록 계속 교환, 그 과정을 N-1회 반복
```cpp
int arr[5] = { 2, 6, 13, -2, 4 };
int n = 5;
for (int i = 0; i < n; i++) {
	for (int j = 0; j < n - 1 - i; j++) {
		if (arr[j] > arr[j + 1]) swap(arr[j], arr[j + 1]);
	}
}
```

# Merge Sort 합병 정렬
재귀적으로 수열을 나눠 정렬한 후 합치는 정렬법
시간복잡도 `O(NlgN)`  

### 단계
1. 주어진 리스트 2개로 나눈다.
2. 나눈 리스트 2개를 각각 정렬한다.
3. 정렬된 두 리스트를 합친다.

2번에서 나눈 리스트 정렬은 어떻게 할건지? => `재귀` 활용 정렬  
> 길이 8인 리스트 정렬할 수 있으려면 길이가 4인 리스트 정렬할 수 있어야하고
길이 4인 리스트 정렬할 수 있으려면 길이가 2인 리스트 정렬할 수 있어야하고
길이 2인 리스트 정렬할 수 있으려면 길이가 1인 리스트 정렬할 수 있어야하고
길이가 1인 리스트는 정렬하기 매우 쉽다!

나눌 때 O(N), 합칠 때 O(NlgN) 이므로 O(NlgN) 걸린다고 볼 수 있다.

### 코드
`merge()` : 정렬된 두 리스트를 합치는 함수  
`merge_sort()` : [st, en) 범위로 정렬하는 함수  

```cpp
#include<bits/stdc++.h>
using namespace std;

int n = 10;
int arr[10] = { 2, 131, -8, 80, 41, 13, -13, 99, 214, 94 };
int tmp[10];

void merge(int st, int en) {
	int mid = (st + en) / 2;
	int lidx = st, ridx = mid;
	for (int i = st; i < en; i++) {
		if (lidx == mid) tmp[i] = arr[ridx++];
		else if (ridx == en) tmp[i] = arr[lidx++];
		else if (arr[lidx] <= arr[ridx]) tmp[i] = arr[lidx++];
		else tmp[i] = arr[ridx++];
	}
	for (int j = st; j < en; j++) arr[j] = tmp[j];
}

void merge_sort(int st, int en) {
	if (en == st + 1) return;
	int mid = (st + en) / 2;
	merge_sort(st, mid);
	merge_sort(mid, en);
	merge(st, en);
}

int main() {
	ios::sync_with_stdio(0);
	cin.tie(0);
	merge_sort(0, n);
	for (int i = 0; i < n; i++) cout << arr[i] << ' ';
	return 0;
}
```

#### Stable sort 성질
Stable sort 성질은 우선순위가 같은 원소들끼리는 원래의 순서를 따라가도록 하는 정렬 성질이고, Merge sort는 Stable sort임  

위 코드에서 
```cpp
else if (arr[lidx] <= arr[ridx]) tmp[i] = arr[lidx++];
```
에서 우선순위가 같다면 왼쪽 리스트의 원소 먼저 보내줬기 때문에 Stable sort 성질을 만족하도록 구현됐음
