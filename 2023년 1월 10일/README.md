# [백준 1158](https://www.acmicpc.net/problem/1158)


# 1트
n을 전체 리스트 길이로 나누어서 몇개를 빼야 하는지 구해야 한다. 그리고 이중반복문으로 그 길이만큼 빼준다.

```
m,n = input().split()

m= int(m)
n= int(n)


list_A = []

for i in range(1,m+1):
  list_A.append(i)
  
list_A_range = len(list_A) // n

while True:
  if len(list_A) < n:
    for i in list_A:
      list_B.append(i)
      break
  else:
    list_A_range = len(list_A) // n
    for i in range(1,list_A_range+1):
      del_index = n-1
      list_B.append(list_A[i*del_index])
      list_A.remove(list_A[i*del_index])
```
이거는 3-6 사이클을 돌고 그다음 숫자로 가야하는데, 이코드는 3-6사이클을 돌고 초기화가 되버림.

예를 들어 3과6이 삭제되고 그 다음 숫자 7부터 시작해야 하지만 1부터 시작해버림

#2트
리스트를 옮기면 어떨까?

1 2 3 4 5 6 7에서 3,6을 뺴면

1 2 4 5 7인데 여기서 다음 숫자인 7뒤에 1 2 4 5가 오는 새로운 리스트로 만드는 거다.


```
m = 7 
n = 3

list_A = [1, 2, 3, 4, 5, 6, 7]

list_B = []
i = 1
while True:
  del_index = n-1
  if del_index*i >= len(list_A):
    k = list_A[-1]
    k_index = list_A.index(list_A[-1])
    list_A.append(k)
    list_A[-1:] = list_A[:i+1]
    del list_A[0:k_index]
    i = 1
  else:
    list_B.append(list_A[del_index*i])
    list_A.remove(list_A[del_index*i])
    i = i + 1

```

이거 71245다음에 4571로 넘어가야 하는데 여기서 막힘.

계속 5714로 넘어감

# 솔루션
총 2가지 솔루션이 있다.

1. 배열로 푸는 방법

2. 원형큐를 사용해서 푸는 방법

총 2가지가 있다.

## 1. 배열로 푸는 방법


```
N, K = map(int,input().split())
ans= []
arr = [i for i in range(1,N+1)] 
num = 0
for i in range(N):
    num+=(K-1)
    if num >= len(arr):
        num %= len(arr)
    ans.append(str(arr[num]))
    arr.pop(num)

print("<",', '.join(ans),">", sep="")
```

나처럼 배열로 푼 문제다. 나와 좀 차이점이 있는데, 나는 배열을 꼭 만드는 것에 집중했다. 3,6이 날라가면 남은 숫자로 7,1,2,4,5 배열을 만드는 등 이런 시도를 했는데, 이 문제는 나처럼 배열을 하나하나 만들기 보다 그 순번을 나머지로 나누어서 초기화 시키는 방법으로 순서를 맞추었다.

## 2. 원형큐

원형큐에 대해 생전 처음 듣게 되었다. 찾아보니까 fifo특성을 가지는 큐가 fifo를 실행하기 위해 때로는 과도한 시간복잡도가 들기때문에 고안된 방법이라고 한다. 

![image](https://user-images.githubusercontent.com/95357946/211488508-365441ad-6a1f-4441-92d7-6871bbc84de3.png)


이때 우리는 deque라이브러리에서 지원하는 rotate 함수로 간편하게 원형큐를 구현 할 수 있다.

```
import sys
input = lambda : sys.stdin.readline().rstrip()
from collections import deque

n, k = map(int, input().split())
cq = deque()
for i in range(1, n + 1):
    cq.append(i)

result = []
while cq:
    # 양수값은 시계방향, 음수값은 반시계방향
    cq.rotate(1 - k)
    result.append(str(cq.popleft()))

print(f"<{', '.join(result)}>")
```
