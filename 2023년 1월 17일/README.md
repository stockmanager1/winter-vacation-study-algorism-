# [백준 11656](https://www.acmicpc.net/problem/11656)

[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/11656.%E2%80%85%EC%A0%91%EB%AF%B8%EC%82%AC%E2%80%85%EB%B0%B0%EC%97%B4)

# [백준 1946](https://www.acmicpc.net/problem/1946)

[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/1946.%E2%80%85%EC%8B%A0%EC%9E%85%E2%80%85%EC%82%AC%EC%9B%90)

## 1트

```
import sys

n = int(sys.stdin.readline())

cnt = 1

list_A = []

for i in range(n):
  a = int(sys.stdin.readline())
  for i in range(a):
    k = map(int,sys.stdin.readline().split())
    k = list(map(int,k))
    list_A.append(k)
  list_A = sorted(list_A, key = lambda x : (x[0]))
  cnt = 1
  for i in range(len(list_A)-1):
    if list_A[i][1] > list_A[i+1][1]:
      cnt = cnt + 1
    else:
      pass
  print(cnt)
  list_A.clear()
  cnt = 1
```

그리디--- **현재**최선의 경우를 알아내는 것에 입각해서 문제를 풀었다.

처음 코드를 짤때 막연히 딱 이전경우, 그러니까 i번째와 i+1번째만 비교했다.

예제는 운 좋게 모두 통과했지만 틀렸고, 반례를 찾아보다가 찾았다.

7

1 4

2 3

3 2

4 1

5 7

6 6

7 5

나의 정답:6

실제 정답 4

첫번째 경우인 1,4에 대해서 선발이 되기 위해서는 4보다 작아야 한다. 이미 첫번쨰가 크기 때문이다.

그러면 (5,7),(6,6),(7,5)를 제외해야 하지만 난 제외가 안됨.

따라서 코드를 수정했다.
## 2트
```
list_A = []
for i in range(n):
  a = int(input())
  for i in range(a):
    k = input().split()
    k = list(map(int,k))
    list_A.append(k)
  list_A = sorted(list_A, key = lambda x : (x[0]))
  cnt = 1
  for i in range(len(list_A)):
    if i == 0:
      value = list_A[i][1]
    else:
      q = list_A[i][1]
      if q < value:
        value = q
        cnt = cnt + 1
      else:
        pass
  print(cnt)
  list_A.clear()
  cnt = 1

```
그리디를 좀 더 보충해야한다는 생각이 든 문제다.

# [백준1931](https://www.acmicpc.net/problem/1931)

오답... 그리디의 개념을 너무 대충 생각하고 있었는데, 이걸 공부하면서 배운걸 신입사원 문제에 적용했더니 잘 풀렸다.

## 1트
dfs식으로 풀려고 했다. 

false를 최대시간대를 기준으로 리스트를 만든다.

그리고 이걸 각 시간의 차이에 집중해서 작은 순으로 정렬후 이걸 false를 true로 바꾸어서 최댓값이 되는 방법을 찾으려고 했는데...

망했다.

일단 최댓값을 구하는 것에서 그리디를 떠올려야 하고, 그리디 == 지금 최고의 경우의 수 를 떠욜려야 한다.

옛날에는 이게 무슨 말인지 몰랐는데, 이제는 얼추 이해했다.

[인터넷에서 찾은 코드](https://jokerldg.github.io/algorithm/2021/03/11/meeting-room.html)

```
N = int(input())
time = []

for _ in range(N):
  start, end = map(int, input().split())
  time.append([start, end])

time = sorted(time, key=lambda a: a[0]) # 시작 시간을 기준으로 오름차순
time = sorted(time, key=lambda a: a[1]) # 끝나는 시간을 기준으로 다시 오름차순

last = 0 # 회의의 마지막 시간을 저장할 변수
conut = 0 # 회의 개수를 저장할 변수

for i, j in time:
  if i >= last: # 시작시간이 회의의 마지막 시간보다 크거나 같을경우
    conut += 1
    last = j

print(conut)
```

이 코드를 설명해보자.

start, end를 time이라는 리스트에 집어 넣는다.

그리고 lambda를 통해 start로 정렬 한번, end를 기준으로 정렬한번을 하는데 이부분이 이해가 안됬다.

이렇게 생각해보자.

내가 지금 회의실을 사용하고 있다고 가정하고, 나의 회의가 끝난후에 회의실에서 가장 많은 회의가 열리기 위해서는 나의 회의가 빨리 끝나야 한다.---> 즉 종료시간이 빨라야 한다.

그리디는 현재 최고의 경우를 뽑기 때문이다.

따라서 종료시간을 기준으로 값을 구한다.

그럼 start를 기준으로 왜 정렬하는가? 끝나는 값이 중복이 될 경우, 끝나는 값이 동일하다면, 우리는 회의가 빨리 끝나기 위해서는 빨리 시작해야 한다. 따라서 먼저 start를 기준으로 정렬했다.
