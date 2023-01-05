# [백준 1260](https://www.acmicpc.net/problem/1260)

[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/1260.%E2%80%85DFS%EC%99%80%E2%80%85BFS)

# 1트
이코테에 있는 예제 코드를 참고하고 문제를 해결함.

무조건 이건 암기해야 한다. 암기를 바탕으로 한 응용이 필요한 부분이다.

문제 해설 이전에 개념을 한번씩 잡고가자
## dfs
dfs는 깊이 탐색으로 최대한 깊이 들어간다. 따라서 이친구는 stack을 사용해서 구현한다.
```
def dfs(graph,v,visited):
  visited[v] = True
  for i in graph[v]:
    if not visited[i]:
      dfs(graph,i,visited)
```

이때 선행되어야 하는게 visited를 총 노드의 갯수 +1한만큼의 이중 리스트를 만들어야 한다.

+1을 하는 이유는 graph = [[],[2,3,4]...]이런 식으로 제일 처음을 비워주기 위해서다.

## bfs
bfs는 넓이 탐색으로 한 노드애서 깊이 들어가는 것이 아니라 가능한 경우의 수를 모두 가보면서 탐색한다. 따라서 queue로 구현한다.

```
from collection import deque 

def bds(graph,start,visited):
   queue = deque([start])
  visited[v] = True
  
  while queue:
    v = queue.popleft()
    print(v)
    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True
```

매일 코드를 짜보면서 baseline을 암기하자.

## 풀이
우선 우리는 문제에서 주어진 그래프 형식을 우리 입맛에 맞는 그래프로 바꾸어야 한다.

여기는 예를 들어 (1,3),(1,4)면 1번노드에 3번 노드와 4번노드가 이어져있다고 말하지만, 우리가 필요한 노드는 [3,4],[1],[1]식으로 1번 노드에는 [3,4]가 이어지고, 3번노드에는 1이, 4번노드에도 1이 이어지는 그래프로 변경해야 한다.

따라서 
```
for i in range(m):
  input_list = input().split()
  input_list = list(map(int,input_list))
  list_A[input_list[0]].append(input_list[1])
  list_A[input_list[1]].append(input_list[0])

for i in range(len(list_A)):
  list_A[i] = sorted(list_A[i])

```
이 코드를 사용해서 우리에게 맞는 그래프를 만들었다.

이후 갯수 +1만큼 visited리스트를 만들었고, dfs,bfs코드를 순서대로 집어넣으면 문제가 해결된다.
