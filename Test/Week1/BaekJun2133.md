## 타일 채우기(백준2133)

## 목차
- 문제 설명
- 코드 및 설명
- 느낀 점
- 링크

## 문제 설명
### 문제
3×N 크기의 벽을 2×1, 1×2 크기의 타일로 채우는 경우의 수를 구해보자.

### 입력
첫째 줄에 N(1 ≤ N ≤ 30)이 주어진다.

### 출력
첫째 줄에 경우의 수를 출력한다.

## 코드 및 설명

### 접근 방법
김옥지

### 코드
```kotlin
val N = readLine()!!.toInt()
val dpTable = Array(1001) { 0 }

fun main() {
    if(N%2!=0) print(0)
    else print(dp(N))
}

fun dp(n: Int) :Int {
    if(n == 0) return 1
    if(n == 1) return 0
    if(n == 2) return 3
    if(dpTable[n] != 0) return dpTable[n]

    var res = 3 * dp(n-2)
    for (i in 3..n){
        if (i % 2 == 0) res += 2 * dp(n - i)
    }

    dpTable[n] = res
    return dpTable[n]
}
```
## 느낀점
그냥 죽을래

## 링크
https://www.acmicpc.net/problem/2133
