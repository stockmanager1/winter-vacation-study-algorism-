# [백준 1463](https://www.acmicpc.net/problem/1463) 

해결 유무 : 아직 3트에서 막힘


# 문제 설명
case가 총 3가지가 있다. 3으로 나누는 경우, 2로 나누는 경우, 1로 빼는 경우가 있다. 이때 n을 1로 만들어야 하는데, 최소한의 연산 횟수로 n을 1로 만들어야 한다.

# 1트 (제일 큰수를 먼저 나누고 안되면 2로 나누기)
제일 큰수로 나누어 지면 값이 최솟값이 될거라는 가정

![Screenshot 2023-01-04 at 16 49 18](https://user-images.githubusercontent.com/95357946/210507809-8c571837-d53b-4760-bf9b-7c1f00d43ed2.JPG)


근데 예제부터 틀려서 x

# 2트(반복문으로 제곱수를 사용)

예제 2번인 10을 보고 느낀건데, 제곱수를 사용하면 더 빠르게 소거가 가능할거라고 생각해서 반복문을 통해 구현하려고 했다.

![Screenshot 2023-01-04 at 16 54 20](https://user-images.githubusercontent.com/95357946/210508609-76fcf7f4-41b5-4648-a7e8-dac71038c609.JPG)

시간초과가 남

# 3트(재귀를 사용해서 풀어보자.)

위 발상을 하나로 좀 생각해보면, 일단 2의 개입을 최소화 해야 한다고 생각한다. 우선 당장 10만 해도 2가 먼저 개입되어버리면 경우의 수가 4지만 -1로 3의 배수를 만들어 버리면 바로 3번만에 가능하니까..

![Screenshot 2023-01-04 at 16 57 44](https://user-images.githubusercontent.com/95357946/210509160-6e11a1af-9530-466d-b2f0-cd1daf509b7b.JPG)

얼추 재귀로 2의 개입을 최소화하고, 3으로 안나누어 떨어지면 -1을 하는 형식으로 코드를 짰는데 왜 재귀가 return에서 안멈추는지 모르겠다,;;; 이건 좀 생각도 못했는데..

