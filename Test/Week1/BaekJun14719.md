## 빗물(백준14719)

## 목차
- 문제 설명
- 코드 및 설명
- 느낀 점
- 링크

## 문제 설명
### 문제
2차원 세계에 블록이 쌓여있다. 비가 오면 블록 사이에 빗물이 고인다.
![1](/assets/1.png)![2](/assets/2.png)
비는 충분히 많이 온다. 고이는 빗물의 총량은 얼마일까?

### 입력
첫 번째 줄에는 2차원 세계의 세로 길이 H과 2차원 세계의 가로 길이 W가 주어진다. (1 ≤ H, W ≤ 500)
두 번째 줄에는 블록이 쌓인 높이를 의미하는 0이상 H이하의 정수가 2차원 세계의 맨 왼쪽 위치부터 차례대로 W개 주어진다.
따라서 블록 내부의 빈 공간이 생길 수 없다. 또 2차원 세계의 바닥은 항상 막혀있다고 가정하여도 좋다.

### 출력
2차원 세계에서는 한 칸의 용량은 1이다. 고이는 빗물의 총량을 출력하여라.
빗물이 전혀 고이지 않을 경우 0을 출력하여라.

## 코드 및 설명

### 접근 방법
고인 빗물의 총량을 구하는 구현 문제로 한 열당 최대 어느정도로 물이 찰 수 있는지 찾는 식으로 접근하였다.
한 열을 기준으로 왼쪽과 오른쪽 각각 최대 높이의 블록을 구하고, 왼쪽과 오른쪽을 비교하여 적은 블록의 수만큼 물이 찰 수 있기 때문에 둘의 값을 비교하여 작은 값에 현재 열의 블록 높이만큼 빼 sum에 합해줬다. 

### 코드
```kotlin
class Baek14719 {
    fun solution(h: Int, w: Int, arr: Array<Int>) : Int {
        var sum =0

        for(i in arr.indices){
            var leftMax = 0
            var rightMax = 0
            for(l in 0 until i)
                leftMax = max(leftMax,arr[l])

            for(r in i+1 until arr.size)
                rightMax = max(rightMax,arr[r])

            sum += max(min(leftMax,rightMax) -arr[i],0)
        }
        return sum
    }
}

fun main() {
    val ob = Baek14719()
    val br = BufferedReader(InputStreamReader(System.`in`))
    val (h, w) = br.readLine().split(" ").map { it.toInt() }
    val arr = br.readLine().split(" ").map { it.toInt() }.toTypedArray()

    print(ob.solution(h, w, arr))
}
```
## 느낀점
따로 특별한 알고리즘을 사용한 것은 아닌 구현 문제였고, 아이디어만 잘 생각한다면 쉽게 풀 수 있는 문제이다.

## 링크
https://www.acmicpc.net/problem/14503
