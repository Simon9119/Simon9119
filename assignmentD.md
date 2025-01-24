# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：50min



代码：

```python
n = int(input())

def check(coins, case):
    for item in case:
        left, right, res = item.split()

        left_total = sum(coins[i] for i in left)
        right_total = sum(coins[i] for i in right)

        if left_total == right_total and res != 'even':
            return False
        elif left_total < right_total and res != 'down':
            return False
        elif left_total > right_total and res != 'up':
            return False

    return True

for _ in range(n):
    case = [input().strip() for _ in range(3)]

    for counterfeit in 'ABCDEFGHIJKL':
        found = False
        for weight in [-1, 1]:
            coins = {coin: 0 for coin in 'ABCDEFGHIJKL'}
            coins[counterfeit] = weight

            if check(coins, case):
                found = True
                tag = "light" if weight == -1 else "heavy"
                print(f'{counterfeit} is the counterfeit coin and it is {tag}.')
                break
        if found:
            break
```



代码运行截图 <mark>（![image-20241224214426536](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224214426536.png))</mark>





### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：55min



代码：

```python
def longest_slide(R, C, heights):
    dp = [[-1] * C for _ in range(R)]
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]

    def dfs(x, y):
        if dp[x][y] != -1:
            return dp[x][y]
        
        max_length = 1
        for dx, dy in directions:
            nx, ny = x + dx, y + dy
            if 0 <= nx < R and 0 <= ny < C and heights[x][y] > heights[nx][ny]:
                max_length = max(max_length, dfs(nx, ny) + 1)
        
        dp[x][y] = max_length
        return dp[x][y]

    result = 0
    for i in range(R):
        for j in range(C):
            result = max(result, dfs(i, j))
    
    return result

R, C = map(int, input().split())
heights = [list(map(int, input().split())) for _ in range(R)]
print(longest_slide(R, C, heights))

```



代码运行截图 ==（![image-20241224215506135](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224215506135.png))==





### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：65min



代码：

```python
from collections import deque

def can_reach(n, maze):
    start_positions = []
    target_position = None
    for i in range(n):
        for j in range(n):
            if maze[i][j] == 5:
                start_positions.append((i, j))
            elif maze[i][j] == 9:
                target_position = (i, j)
    
    start_positions = tuple(sorted(start_positions))
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    visited = set()
    queue = deque([start_positions])
    visited.add(start_positions)
    
    while queue:
        current = queue.popleft()
        if target_position in current:
            return "yes"
        
        for dx, dy in directions:
            new_positions = []
            for x, y in current:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n and maze[nx][ny] != 1:
                    new_positions.append((nx, ny))
            
            if len(new_positions) == 2 and (new_positions[0][0] == new_positions[1][0] or new_positions[0][1] == new_positions[1][1]):
                new_positions = tuple(sorted(new_positions))
                if new_positions not in visited:
                    visited.add(new_positions)
                    queue.append(new_positions)
    
    return "no"

n = int(input())
maze = [list(map(int, input().split())) for _ in range(n)]
print(can_reach(n, maze))

```



代码运行截图 <mark>（![image-20241224220228584](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224220228584.png))</mark>





### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：50min



代码：

```python
limit = int(input())
n = int(input())
lst = list(map(str, input().split()))

lst.sort(key=lambda x: x * 20, reverse=True)

dp = [0] * (limit + 1)
temp = [0] * (limit + 1)

for num in lst:
    num_len = len(num)
    for i in range(limit, num_len - 1, -1):
        dp[i] = max(dp[i], int(str(temp[i - num_len]) + num))
    temp[:] = dp

print(dp[limit])
```



代码运行截图 <mark>（![image-20241224221401342](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224221401342.png))</mark>





### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：60min



代码：

```python
from copy import deepcopy
from itertools import product
rmap = {0:1, 1:0}
matrix_backup = [[0] * 8] + [[0, *map(int, input().split()), 0] for i in range(5)] \
    + [[0] * 8]
    
for test in product(range(2), repeat=6):
    matrix = deepcopy(matrix_backup)
    triggers = [list(test)]  
    for i in range(1, 6):         
        for j in range(1, 7):
            if triggers[i - 1][j - 1]:
                matrix[i][j] = rmap[matrix[i][j]]
                matrix[i - 1][j] = rmap[matrix[i - 1][j]]
                matrix[i + 1][j] = rmap[matrix[i + 1][j]]
                matrix[i][j - 1] = rmap[matrix[i][j - 1]]
                matrix[i][j + 1] = rmap[matrix[i][j + 1]]
        triggers.append(matrix[i][1:7])
    if matrix[5][1:7] == [0, 0, 0, 0, 0, 0]:
        for trigger in triggers[:-1]:
            print(' '.join(map(str, trigger)))   
```



代码运行截图 <mark>（![image-20241224221500785](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224221500785.png))</mark>





### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：60min



代码：

```python
def can_jump(rocks, L, M, min_distance):
    rocks = [0] + rocks + [L]
    removed = 0
    last_position = 0
    
    for i in range(1, len(rocks)):
        if rocks[i] - last_position < min_distance:
            removed += 1
            if removed > M:
                return False
        else:
            last_position = rocks[i]
    
    return True

def longest_min_jump(L, N, M, rocks):
    left, right = 1, L
    best = 0
    
    while left <= right:
        mid = (left + right) // 2
        if can_jump(rocks, L, M, mid):
            best = mid
            left = mid + 1
        else:
            right = mid - 1
    
    return best

L, N, M = map(int, input().split())
rocks = [int(input()) for _ in range(N)]

print(longest_min_jump(L, N, M, rocks))

```



代码运行截图 <mark>（![image-20241224221813255](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241224221813255.png))</mark>





## 2. 学习总结和收获



面对困难的题目有时连答案都看不懂，考试在即，现在就专注2E2M的题目了，希望不要挂科



