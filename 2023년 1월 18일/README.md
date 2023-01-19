# [백준1789](https://www.acmicpc.net/problem/1789)
[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/1789.%E2%80%85%EC%88%98%EB%93%A4%EC%9D%98%E2%80%85%ED%95%A9)

# [백준 2003](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/2003.%E2%80%85%EC%88%98%EB%93%A4%EC%9D%98%E2%80%85%ED%95%A9%E2%80%852)
[풀이](https://github.com/stockmanager1/baejoon-study--TIL/tree/main/%EB%B0%B1%EC%A4%80/Silver/2003.%E2%80%85%EC%88%98%EB%93%A4%EC%9D%98%E2%80%85%ED%95%A9%E2%80%852)

여기서 투포인터에 대한 개념을 짚고 넘어갸야한다.

졍렬 알고리즘 중에서 포함되는 알고리즘이다.

투포인터 알고리즘이란? 1차원 배열에서 두개의 포인터(start,end)를 조작하는 알고리즘이다. 다른말로 말하자면, 리스트에 순차적으로 접근 해야 할때, 두개의 점의 위치를 기록하면서, 처리하는 알고리즘을 말한다.

좀 말이 어려운데, 좀 쉽게 이야기 하자면, 배열의 인덱스를 가르키는 2개의 포인터를 설정하고, 이를 옮겨가면서 내가 원하는 값을 찾는 알고리즘이다.

예를 들어보자.

배열 [4,6,-2,9,2,5]가 있다.

이때 우리는(문제 조건마다 front = 0, rear =1로 시작하는 조건도 당연히 존재한다.) 우선 front=0, rear=0으로 시작점과 끝점을 설정한다.

이때 front와 rear를 움직여서 front와 rear의 범위(범위가 아닐때도 있다.) 만큼 더해서 15가 되는 경우의 수를 찾아보자.

첫 경우의 수인 front == 0, rear == 0일때 arr[0:0]이므로 그 합은 4다.

이때 코드로
```
if sum(arr[front:rear]) < target: 
  rear = rear + 1
```
을 추가해준다. 그럼 rear가 0에서 1로 이동한다.

다시 그럼 배열은 arr[0:1]로 그 합은 10이다. 이때 역시  target인 15보다 작으니까 rear = rear + 1이 성립한다.

그럼 다시 rear = 2가 되고, arr[0:2]가 되는데, 이때는 4+6-2로 역시 target보다 작다.

rear = 3이 되고 합은 4+6-2+9 = 17로 target보다 커진다. 
이때는 front를 한칸 땡긴다. (문제마다 front랑 rear가 같이 땡겨야 할 때도 있다.)
```
front = front + 1
```
그럼 arr[1:3]으로 드디어 합이 15가 되었다. 그럼 이제 
```
rear = rear +1, cnt = cnt +1
```
을 해서 경우를 더하고, 다음 경우를 탐색한다.

이런 흐름으로 이루어 지는데 전체 코드를 정리하면 다음과 같다.
|front|rear|합|
|------|---|---|
|0|0|4|
|0|1|10|
|0|2|8|
|0|3|17|
|1|3|15|
|1|4|19|
.
.
.
(계속 이어짐)

### 전체코드
```
arr = [4,6,-2,9,2,-5]
front = 0
rear = 0
target = 15

while rear < len(array):
  if sum(arr[front:rear]) < target:
    rear = rear + 1
  elif sum(arr[front:rear]) > target:
    front = front + 1
  elif sum(arr[front:rear]) == target:
    print(arr[front:rear])
    rear = rear + 1
```

앞으로 투포인터를 생각할때 이 알고리즘의 베이스라인을 떠올리면서 구현해보자.
   
