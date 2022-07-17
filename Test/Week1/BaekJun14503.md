## 로봇청소기(백준14503)

## 목차
- 문제 설명
- 코드 및 설명
- 느낀 점
- 링크

## 문제 설명
### 문제
로봇 청소기가 주어졌을 때, 청소하는 영역의 개수를 구하는 프로그램을 작성하시오.
로봇 청소기가 있는 장소는 N×M 크기의 직사각형으로 나타낼 수 있으며, 1×1크기의 정사각형 칸으로 나누어져 있다. 각각의 칸은 벽 또는 빈 칸이다. 청소기는 바라보는 방향이 있으며, 이 방향은 동, 서, 남, 북중 하나이다. 지도의 북쪽에서부터 r번째, 서쪽에서부터 c번째로 위치한 칸은 (r, c)로 나타낼 수 있다.
로봇 청소기는 다음과 같이 작동한다.

1. 현재 위치를 청소한다.
2. 현재 위치에서 다음을 반복하면서 인접한 칸을 탐색한다.
  a. 현재 위치의 바로 왼쪽에 아직 청소하지 않은 빈 공간이 존재한다면, 왼쪽 방향으로 회전한 다음 한 칸을 전진하고 1번으로 돌아간다. 그렇지 않을 경우, 왼쪽 방향으로 회전한다. 이때, 왼쪽은 현재 바라보는 방향을 기준으로 한다.
  b. 1번으로 돌아가거나 후진하지 않고 2a번 단계가 연속으로 네 번 실행되었을 경우, 바로 뒤쪽이 벽이라면 작동을 멈춘다. 그렇지 않다면 한 칸 후진한다.
### 입력
첫째 줄에 세로 크기 N과 가로 크기 M이 주어진다. (3 ≤ N, M ≤ 50)
둘째 줄에 로봇 청소기가 있는 칸의 좌표 (r, c)와 바라보는 방향 d가 주어진다. d가 0인 경우에는 북쪽을, 1인 경우에는 동쪽을, 2인 경우에는 남쪽을, 3인 경우에는 서쪽을 바라보고 있는 것이다.
셋째 줄부터 N개의 줄에 장소의 상태가 북쪽부터 남쪽 순서대로, 각 줄은 서쪽부터 동쪽 순서대로 주어진다. 빈 칸은 0, 벽은 1로 주어진다. 지도의 첫 행, 마지막 행, 첫 열, 마지막 열에 있는 모든 칸은 벽이다.
로봇 청소기가 있는 칸의 상태는 항상 빈 칸이다.

### 출력
로봇 청소기가 청소하는 칸의 개수를 출력한다.

로봇 청소기가 있는 칸의 상태는 항상 빈 칸이다.

## 코드 및 설명

### 접근 방법
청소기가 정해진 규칙으로 끝까지 탐색하는 구현문제라고 생각하여 dfs로 구현하는게 적합하다고 생각하였고, dfs 탐색의 시간복잡도를 계산했을 때, O(N*M)으로 N,M ≤ 50 조건에 따라 무리가 없다고 생각하여 dfs로 구현하였다.
구현에서는 회전할 때마다 청소기의 나아갈 방향을 정해주는 dx1과 dy1 이라는 각각의 리스트를 만들어 사용하였고, 배열의 인덱스에 접근할 때, Null 인지 체크해주는 함수를 만들어 사용하였다.
dfs 함수는 현재 위치(x,y)와 방향(d)을 받아 규칙대로 탐색하도록 구현하였다.

### 코드
```kotlin
class Baek14503(val n: Int, val m: Int) {
    val dx1 = intArrayOf(0, 1, 0, -1)
    val dy1 = intArrayOf(-1, 0, 1, 0)
    lateinit var array: Array<IntArray>
    var count = 0

    fun solution(r: Int, c: Int, d: Int, array: Array<IntArray>) : Int {
        this.array = array
        count++
        array[r][c] = 2
        dfs(c,r,d)
        return count
    }

    fun isNullCheck(x: Int, y: Int) =
        x in 0 until m && y in 0 until n

    fun dfs(x: Int, y: Int, d: Int) {
        var xCount = 0
        for (i in 3 downTo 0) {
            var x1 = x + dx1[(d + i) % 4]
            var y1 = y + dy1[(d + i) % 4]

            if (isNullCheck(x1, y1)) {
                if (array[y1][x1] == 0) {
                    array[y1][x1] = 2
                    count++
                    dfs(x1, y1, (d + i) % 4)
                    return
                } else {
                    xCount++
                }
            } else {
                xCount++
            }
        }
        if (xCount == 4 && array[y + dy1[(d + 2) % 4]][x + dx1[(d + 2) % 4]] != 1) {
            dfs(x + dx1[(d + 2) % 4],y + dy1[(d + 2) % 4],d)
        }else{
            return
        }
    }
}

fun main() {
    val br = BufferedReader(InputStreamReader(System.`in`))
    val (n, m) = br.readLine().split(" ").map { it.toInt() }
    val (r, c, d) = br.readLine().split(" ").map { it.toInt() }
    val array = Array(n) { IntArray(m) }
    for (i in 0 until n) {
        array[i] = br.readLine().split(" ").map { it.toInt() }.toIntArray()
    }
    val ob = Baek14503(n, m)
    print(ob.solution(r, c, d, array))
}
```
## 느낀점
따로 특별한 알고리즘을 사용한 것은 아닌 구현 문제였지만, 예외사항이 있어 까다로웠고, 방향에 대한 dx1,dxy 라는 리스트를 만들어 사용한다는 접근방법이 없었다면 꽤 복잡하게 풀었을 것 같다. 이런 접근방법과 isNullCheck와 같은 함수는 앞으로도 자주 사용될 것 같으니 잘 기억해야겠다.

## 링크
https://www.acmicpc.net/problem/14503
