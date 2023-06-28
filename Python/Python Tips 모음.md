# Python3 Tips  
`알고리즘을 공부하며 유용했던 내장함수, 자료구조 등을 정리합니다.`

## 자료구조
#### Dictionary 딕셔너리
* 선언
   * number = {"zero":0}
   * number["zero"] = 0
* 검색 및 활용
   * number.keys()
   * number.values()
   * number.items() //key,val 쌍
   * if 딕셔너리.get(키값) == None: //키값이 이 딕셔너리에 없으면 None

#### Set 집합
* 선언
   * num = set()
* 추가
   * num.add(i)
* 삭제
   * num.discard(i) //삭제하려는 원소가 없어도 에러발생 X
   * num.remove(i) //삭제하려는 원소가 없으면 에러발생

#### List 리스트
* 리스트 정렬
   * list.sort() //원본이 정렬됨, 기본은 오름차순
      * list.sort(reverse=True) //내림차순 정렬
      * list.sort(key=len) //len함수를 key로 두고 정렬, 길이 순으로 정렬됨
   * sorted(list) //정렬된 리스트를 반환, 원본은 변하지 X
   * 2차원리스트.sort(key = lambda x:(-x[1],x[0])) //리스트 두 번째 열 기준으로 역정렬, 같으면 첫번째 원소 기준으로 내림차순
   
#### List to Dict 하는 법
   * from collections import Counter //O(n), 짱편함
   * mydict = dict(zip(키 리스트, 밸류 리스트))
   * mydict = dict.fromkeys(키 리스트, 0) //val 모두 0으로 초기화 하는 느낌쓰

#### deque
   * deque(iterable, maxlen)
   * cache = deque(maxlen=cacheSize)
      * maxlen 정하면 그 이상 개수의 원소를 append하면 가장 왼쪽 원소 삭제 후 오른쪽에 추가
      * 같은 상황 appendleft() 하면 가장 오른쪽 원소 삭제 후 왼쪽에 추가
  
  
 ---
## ETC
#### String 관련
* string.replace('0','') //string에 있는 0문자를 모두 없애줌, 시간복잡도 O(N)
* string += "a" 가능

#### 변수 치환
* num1, num2 = num2, num1 //완전 편리한 치환 가능!

#### for-else 문
```python
for i in ragne(n):
	if i%10==0:
    	break
else:
	print("10으로 나눠 떨어지는 수가 없을 경우")
```

#### 파이썬에서 아스키코드 변환
* ord('A')
* chr(65)

#### is타입()
* isdigit() //숫자로만?
* isalpha() //알파벳으로만?

#### try-except
```python
try:
	실행할 코드
except IndexError:
	예외 발생시 실행할 코드
```
