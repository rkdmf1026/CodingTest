## 섬 연결하기(프로그래머스)

## 목차
- 문제 설명
- 코드 및 설명
- 느낀 점
- 링크

## 문제 설명
### 문제
n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.
다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

### 제한사항
섬의 개수 n은 1 이상 100 이하입니다.
costs의 길이는 ((n-1) * n) / 2이하입니다.
임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
연결할 수 없는 섬은 주어지지 않습니다.
### 입출력 예
|n|costs|return|
|------|---|---|
|4|[ [0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8] ]|4|
costs를 그림으로 표현하면 다음과 같으며, 이때 초록색 경로로 연결하는 것이 가장 적은 비용으로 모두를 통행할 수 있도록 만드는 방법입니다.
![f2746a8c-527c-4451-9a73-42129911fe17](/assets/f2746a8c-527c-4451-9a73-42129911fe17.png)

## 코드 및 설명

### 접근 방법
이동기 머리로 풀 수 없다고 판단하여 블로그를 보았다.
먼저 weight가 작은 순서로 정렬 후, 가장 작은 weight를 가진 간선의 섬 중 하나를 방문한 상태로 시작한다.
그 후 weight를 기준으로 정렬된 배열에서 작은 가중치를 갖고 있는 간선의 섬들이 방문가능한지 체크하고, 가능하다면 answer에 weight를 추가하고, visited에 방문한 섬을 추가한다. 그렇게 모든 섬을 방문할때까지 위의 과정을 반복한다.

### 코드
```kotlin
class Solution {
    fun solution(n: Int, costs: Array<IntArray>): Int {
        val sortedCosts = costs.sortedBy { it[2] }
        val visited = mutableSetOf(sortedCosts[0][0])
        var answer = 0

        while(visited.size <n){
            for((first: Int, second : Int, cost : Int) in sortedCosts) {
                if(visited.any{it==first || it == second}){
                    if(visited.contains(first) && visited.contains(second))
                    continue

                    visited.add(first)
                    visited.add(second)
                    answer+=cost
                    break
                }

            }
        }

        return answer
    }
}
```
## 느낀점
Greedy 알고리즘을 공부하기 위해서 풀었지만, 정확히 Greedy 알고리즘에 대해서 잘 이해하지 못한 것 같다. 일단 쉬운 Greedy 문제부터 풀면서 이해해야겠다.

## 링크
https://school.programmers.co.kr/learn/courses/30/lessons/42861

## Reference
https://codeinleonis.tistory.com/22
