# 그래프

![1586392313411](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586392313411.png)

<br>

### 가중치 그래프

- 무향 : 최소신장트리
- 유향 : 최단경로

![1586393433118](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586393433118.png)

### DAG

![1586393619646](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586393619646.png)

- 주로 프로세스를 표현하는데 사용

<br>

<br>

### 신장트리

- 사이클이 없으면서 간선을 정점-1 개의 간선을 가지는것
- 가중치가 있으면 MST

![1586393655866](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586393655866.png)

<br>

### 최소신장트리

- 유일하지 않음
- 싸이클이 존재하지 않음
- 대표적 방법 : **Kruskal, Prim**
- 도로망, 통신망, 유통망 등등 여러 분야에서 비용을 최소로 해야 그만큼의 이익을 볼 수 있다

![1586393749950](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586393749950.png)

<br>

<br>

### Kruskal Algorithm

1. 정렬(가중치 오름차순으로)
2. 사이클이 생기면 그 간선은 안 고른다
3. (n-1)개의 간선이 선택될 때까지 반복

![1586394049132](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586394049132.png)

![1586394301250](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586394301250.png)

<br>

<br>

### Prim 

![1586410178368](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586410178368.png)

![1586410243057](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586410243057.png)



### Kruskal vs Prim

- 간적크 간만프 : 간선이 적으면 크루스칼, 간선이 많으면 프림
- 크루스칼의 시간복잡도 : V log V
- 프림의 시간복잡도 : V
- V^2일 때 V^2 <<<<<<<<<< V^2 log V^2







<br>

<br>

# 다익스트라 - 가중치 유향 그래프

![1586479828755](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586479828755.png)

![1586479916922](C:\Users\이수연\AppData\Roaming\Typora\typora-user-images\1586479916922.png)

- 프림과의 유사성 떠올리기



### 다익스트라

- greedy한 알고리즘이기 때문에 음수가중치가 있을경우에는 불리할 수도 잇다
- 음수의 가중치가 있을 경우에는 벨만포드 알고리즘 사용



# 벨만-포드 알고리즘

- 음의 가중치를 포함하는 그래프에서 최단 경로 구할 수 있음
  - 가중치의 합이 음인 사이클은 허용하지 않음
  - Dijkstra로 최단 경로를 구할 수 있다면 벨만- 포드로도 구할 수 있음
  - 하지만 복잡도는 Dijkstra보다 크다 (O(VE))