# [백준 1764](https://www.acmicpc.net/problem/1764)

[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/1764.%E2%80%85%EB%93%A3%EB%B3%B4%EC%9E%A1)

# 1트
그냥 중복 되는 갯수를 구해서 답을 구했다.
```
from collections import Counter

m,n = input().split()
m = int(m)
n = int(n)

list_A = []

for i in range(m+n):
  list_A.append(input())
  
cnt = Counter(list_A)


list_B = []

for i in cnt.keys():
  if cnt[i] >= 2:
    list_B.append(i)
    
list_B = sorted(list_B)

print(len(list_B))
for i in list_B:
  print(i)
```


# [백준 4963](https://www.acmicpc.net/problem/4963)

## 문제 이해

```
def island(graph,i,j):
  graph[i][j] = 0
  if graph[i+1][j] == 1:
    graph[i+1][j] = 0
    island(graph,i+1,j)
  elif graph[i+1][j+1] ==1:
    graph[i+1][j+1] = 0
    island(graph,i+1,j+1)
  elif graph[i][j+1] == 1:
    graph[i][j+1] = 0
    island(graph,i,j+1)

graph = [[1, 0, 1, 0, 0], [1, 0, 0, 0, 0], [1, 0, 1, 0, 1], [1, 0, 0, 1, 0]]
for i in range(4):
  for j in range(5):
    if j <=3 or graph[i][j+1] == 1 or graph[i+1][j+1] == 1 or graph[i+1][j] == 1:
      island(graph,i,j)
      cnt = cnt + 1

```

이런식으로 함수를 짜서 반복문을 돌렸다.

내일 이건 dfs가 아니라서 내일 한번 더 고민해보고 스터디 할때 한번 다 같이 생각해보면 좋을 것 같다.
