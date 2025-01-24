# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>张子明 数学科学学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：50min



代码：

```python
def dfs(board, visited, i, j, N, M):
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1), (-1, -1), (-1, 1), (1, -1), (1, 1)]
    stack = [(i, j)]
    visited[i][j] = True
    area = 0
    
    while stack:
        x, y = stack.pop()
        area += 1
        for dx, dy in directions:
            nx, ny = x + dx, y + dy
            if 0 <= nx < N and 0 <= ny < M and not visited[nx][ny] and board[nx][ny] == 'W':
                visited[nx][ny] = True
                stack.append((nx, ny))
    
    return area

def solve():
    T = int(input())
    for _ in range(T):
        N, M = map(int, input().split())
        board = [input().strip() for _ in range(N)]
        visited = [[False] * M for _ in range(N)]
        max_area = 0
        
        for i in range(N):
            for j in range(M):
                if board[i][j] == 'W' and not visited[i][j]:
                    area = dfs(board, visited, i, j, N, M)
                    max_area = max(max_area, area)
        
        print(max_area)

if __name__ == "__main__":
    solve()

```



代码运行截图 <mark>（![image-20241126231807129](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241126231807129.png))</mark>





### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：50min



代码：

```python
from collections import deque

def bfs(m, n, grid):
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    queue = deque([(0, 0)])
    visited = [[False] * n for _ in range(m)]
    visited[0][0] = True
    steps = 0
    
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            if grid[x][y] == 1:
                return steps
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n and not visited[nx][ny] and grid[nx][ny] != 2:
                    visited[nx][ny] = True
                    queue.append((nx, ny))
        steps += 1
    
    return "NO"

def solve():
    m, n = map(int, input().split())
    grid = [list(map(int, input().split())) for _ in range(m)]
    result = bfs(m, n, grid)
    print(result)

if __name__ == "__main__":
    solve()

```



代码运行截图 ==（![image-20241126233820605](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241126233820605.png))==





### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：50min



代码：

```python
directions = [(-2, -1), (-1, -2), (1, -2), (2, -1),
              (2, 1), (1, 2), (-1, 2), (-2, 1)]

def backtrack(n, m, x, y, visited, count, total):
    if count == total:
        return 1
    result = 0
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < m and not visited[nx][ny]:
            visited[nx][ny] = True
            result += backtrack(n, m, nx, ny, visited, count + 1, total)
            visited[nx][ny] = False
    return result

def solve():
    T = int(input())
    for _ in range(T):
        n, m, x, y = map(int, input().split())
        total = n * m
        visited = [[False] * m for _ in range(n)]
        visited[x][y] = True
        result = backtrack(n, m, x, y, visited, 1, total)
        print(result)

if __name__ == "__main__":
    solve()

```



代码运行截图 <mark>（![image-20241126234056711](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241126234056711.png))</mark>





### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：50min



代码：

```python
def dfs(x, y, now_value):
    global max_value, opt_path
    if x == n - 1 and y == m - 1:
        if now_value > max_value:
            max_value = now_value
            opt_path = temp_path[:]
        return
    
    visited[x][y] = True
    
    for dx, dy in directions:
        next_x, next_y = x + dx, y + dy
        if 0 <= next_x < n and 0 <= next_y < m and not visited[next_x][next_y]:
            next_value = now_value + maze[next_x][next_y]
            temp_path.append((next_x, next_y))
            dfs(next_x, next_y, next_value)
            temp_path.pop()
    
    visited[x][y] = False

n, m = map(int, input().split())
maze = [list(map(int, input().split())) for _ in range(n)]

max_value = float('-inf')
opt_path = []
temp_path = [(0, 0)]
visited = [[False] * m for _ in range(n)]
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

dfs(0, 0, maze[0][0])

for x, y in opt_path:
    print(x + 1, y + 1)

```



代码运行截图 <mark>（![image-20241126235323603](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241126235323603.png))</mark>







### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：50min



代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        f = [[1] * n] + [[1] + [0] * (n - 1) for _ in range(m - 1)]
        print(f)
        for i in range(1, m):
            for j in range(1, n):
                f[i][j] = f[i - 1][j] + f[i][j - 1]
        return f[m - 1][n - 1]

```



代码运行截图 <mark>（![image-20241127000138565](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241127000138565.png))</mark>





### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：50min



代码：

```python
import math

def is_square(num):
    root = int(math.sqrt(num))
    return root * root == num

def check_blessed_number(s):
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True
    
    for i in range(1, n + 1):
        for j in range(i):
            num = int(s[j:i])
            if num != 0 and is_square(num) and dp[j]:
                dp[i] = True
                break
    
    return "Yes" if dp[n] else "No"

s = input().strip()
print(check_blessed_number(s))

```



代码运行截图 <mark>（![image-20241127000343606](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241127000343606.png))</mark>





## 2. 学习总结和收获

还是借助了答案和ai才顺利完成了这此作业，但是通过这样集中的训练新的语法，也能感受到自己的进步。





