# [백준 7568](https://www.acmicpc.net/problem/7568)

결국 못풀었는데, 너무 어렵게 생각함. 좀 나름 쉽게 생각한다고 했지만, 그 틀을 깨지 못함.

# 1트
각 키와 몸무게 값을 비교해서 제일 큰 값을 찾자.

나도 처음에 풀이처럼 풀었는데 나는 왜 틀린거지...


### 답안
```
n  = int(input())
 
data = [] # 입력받은 정보를 저장할 리스트 data
ans = [] # 등수정보를 저장할 리스트 ans
for i in range(n):
    a, b = map(int, input().split())
    data.append((a, b)) # 몸무계와 키를 묶어서 append 해줌
 
for i in range(n):
    count = 0
    for j in range(n):
        if data[i][0] < data[j][0] and data[i][1] < data[j][1]: # 몸무게와 키 모두 자신보다 큰 사람의 수를 센다
            count += 1 
    ans.append(count + 1) # 덩치 등수는 자신보다 몸무계 키 모두 큰 사람의 수 + 1 이므로 count + 1을 ans에 append한다.
 
for d in ans:
    print(d,end=" ")
```

블로그에서 긁어온 풀이다.

그리고 아래는 내가 처음으로 시도했던 풀이다.

### 내꺼 1트
```
n = int(input())
list_A = []

for i in range(5):
  k = input().split()
  k = list(map(int,k))
  list_A.append(k)

list_A_height = sorted(list_A,key=lambda x:x[1],reverse=True)

rank = 1

for i in range(len(list_A_height)):
  if i == len(list_A_height) -1:
    rank = i
    list_A_height[i].append(rank+1)
  else:
    if list_A_height[i][0] > list_A_height[i+1][0] and list_A_height[i][1] > list_A_height[i+1][1]:
      list_A_height[i].append(rank)
      rank = rank + 1
      pass
    elif list_A_height[i][0] >= list_A_height[i+1][0] or list_A_height[i][1] >= list_A_height[i+1][1]:
      list_A_height[i].append(rank)
      rank = rank
    elif list_A_height[i][0] < list_A_height[i+1][0] and list_A_height[i][1] < list_A_height[i+1][1]:
      list_A_height[i].append(rank)
      rank = rank + 1
        
final = []

for i in list_A:
  final.append(i[2])

final

```

나는 키 순으로 우선 정렬을 하고 남은 몸무게끼리 비교하면 답이 나올거라 생각함. 하지만 답이 틀리다. 여기 블로그 답안은 그냥 바로 
새로운 리스트를 만들어서 순서를 받아서, 출력했는데... 솔직히 내가 왜 틀린지 모르겠다. 

# 2트
조금더 간단하게 코드를 작성했는데, 생각하는 방법은 1트와 동일하다. 좀 방법이 변경됨.

```
n = int(input())
list_A = []

for i in range(5):
  k = input().split()
  k = list(map(int,k))
  list_A.append(k)

list_A_height = sorted(list_A,key=lambda x:x[1],reverse=True)
for i in range(n):
  if i == 0:
    list_A_height[i].append(1)
  else:
    if list_A_height[i][0]<= list_A_height[i-1][0]:
      rank = i + 1
      list_A_height[i].append(rank)
    else:
      list_A_height[i].append(rank)
 final = []
 for i in list_A:
  final.append(i[2])
  
 print(*final)
 ```
 
