# Dynamic Programming

## 문제

### 1. 최소 비용으로 계단오르기
계단에서 i번째 계단을 올라갈려면 양수값을 가진 cost[i]가 지불되어야함(계단 배열마다 지불하는 비용이 다름)
또한, 계단 오르기는 한칸 혹은 두칸만 가능하고, 계단 시작점을 0 혹은 1로 선택할 수 있다.
=> 뒤에서 시작해서 경우의 수를 구한다.

<details>
<summary>뮨재퓰이</summary>

```java
public static int minCostStaris(int[] stairCost) {
    int one = 0;
    int two = 0;
    int current;
    for (int i = stairCost.length - 1; i >= 0; i--) {
        // i위치에서 1 ~ 2 칸전에서 내려온 비용중에 최소 비용을 찾음
        current = stairCost[i] + Math.min(one,two);
        two = one; //현재 위치에서 1칸 전(다음 위치와 2칸 차이)
        one = current; // 현재위치(다음위치와 1칸 차이)
    }
    // 시작 위치를 0 혹은 1로 할지 구함
    return Math.min(one,two);
}
```
</details>        
<br>

## 2. 2차원 배열에서 경로
2차원 배열에서 좌측 상단에서 출발하여 우측 하단으로 이동하는 경로를 구해야한다. 이때 true는 장애물이기 때문에 이동하지 못한다. 재귀함수를 통해서 경로를 구하고, 위치는 객체를 통해서 저장한다. 경로를 구하는 문제이므로 출발점이 아닌 도착점에서 시작한다.

<details>
<summary>뮨재퓰이</summary>

```java
class Point{ // 위치를 저장하는 객체
    int row;
    int col;
    Point(int row, int col) {
        this.row = row;
        this.col = col;
    }
}

class Solution{
    public ArrayList<Point> findPath(boolean[][] grid) {
        if (grid == null || grid.length == 0) return null;
        ArrayList<Point> path = new ArrayList<>();
        // 좌측 상단 -> 우측 하단 이므로 우측 하단 (row,col)-> 좌측 상단(0,0)으로 이동
        return findPath(grid, grid.length - 1, grid[0].length - 1, path) ? path : null;
    }

    private boolean findPath(boolean[][] grid, int row, int col, ArrayList<Point> path) {
        // 범위에 벗어나거나, 장애물에 도달 하였을 경우
        if (!isInRange(grid,row,col) || grid[row][col]) return false;

        // 좌측상단(0,0)은 도착점이므로 재귀함수는 멈추어야한다.
        if ((row == 0 && col == 0) || findPath(grid,row, col -1, path) || findPath(grid, row - 1, col, path)){
            Point point = new Point(row,col);
            path.add(point);
            return true;
        }
        return false;
    }

    private boolean isInRange(boolean[][] grid, int row, int col) {
        return row >= 0 && row <= grid.length - 1 && col >= 0 && col <= grid[0].length -1;
    }

}
```
</details>        
<br>
