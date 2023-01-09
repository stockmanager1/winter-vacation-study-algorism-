# [백준 1260](https://www.acmicpc.net/problem/10816)

[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/10816.%E2%80%85%EC%88%AB%EC%9E%90%E2%80%85%EC%B9%B4%EB%93%9C%E2%80%852)

# 1트
이전에 풀었을때 해에 대한 개념이 없어서 풀지 못했다.

해쉬란 다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 맵핑하는 것이다.

좀 더 간단하게 설명하자면, 

![image](https://user-images.githubusercontent.com/95357946/211262024-e59de987-d1df-41d8-99ed-787f1a021015.png)

이렇게 파이썬의 딕셔너리처럼 키와 value로 구성되어 있다.

파이썬의 경우 구현이 매우 간편하다.
```
hash_set = set()
hash_map = {}
```

근데 나는 해시함수를 직접적으로 구현해 문제를 풀기보다는 collections의 couters를 사용해서 딕셔너리를 통해 풀었다.

```
n = int(input())
list_A = input().split()
list_A = list(map(int,list_A))

m = int(input())
list_B = input().split()
list_B = list(map(int,list_B))

from collections import Counter

cnt = Counter(list_A)


for i in range(len(list_B)):
  if list_B[i] in cnt.keys():
    list_B[i] = cnt[list_B[i]]
  else:
    list_B[i] = 0
    
print(*list_B)
```

이런식으로 풀었다.
