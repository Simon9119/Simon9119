# Assignment #A: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>张子明 数学科学学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：40min



代码：

```python
def count_ways(n):
    if n == 1:
        return 1
    elif n == 2:
        return 2
    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2
    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]

n = int(input())
print(count_ways(n))

```



代码运行截图 <mark>（![image-20241204100130369](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204100130369.png))</mark>





### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：35min



代码：

```python
def count(n):
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = sum(dp[1:i]) + 1
    return dp[n]

n = int(input())
print(count(n))
```



代码运行截图 ==（![image-20241204101257090](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204101257090.png))==





### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：50min



代码：

```python
MOD = 1000000007

def solve_flower_dinner(t, k, queries):
    max_n = max(b for _, b in queries)
    f = [0] * (max_n + 1)
    f[0] = 1
    for i in range(1, max_n + 1):
        f[i] = f[i - 1]
        if i >= k:
            f[i] = (f[i] + f[i - k]) % MOD
    S = [0] * (max_n + 1)
    for i in range(max_n + 1):
        S[i] = (S[i - 1] + f[i]) % MOD if i > 0 else f[0]
    results = []
    for a, b in queries:
        results.append((S[b] - S[a - 1]) % MOD)
    return results

t, k = map(int, input().split())
queries = [tuple(map(int, input().split())) for _ in range(t)]
results = solve_flower_dinner(t, k, queries)
print("\n".join(map(str, results)))

```



代码运行截图 <mark>（![image-20241204102359915](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204102359915.png))</mark>





### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：60min



代码：

```python
class Solution:
    def expandAroundCenter(self, s, left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return left + 1, right - 1

    def longestPalindrome(self, s: str) -> str:
        start, end = 0, 0
        for i in range(len(s)):
            left1, right1 = self.expandAroundCenter(s, i, i)
            left2, right2 = self.expandAroundCenter(s, i, i + 1)
            if right1 - left1 > end - start:
                start, end = left1, right1
            if right2 - left2 > end - start:
                start, end = left2, right2
        return s[start: end + 1]
```



代码运行截图 <mark>（![image-20241204103719515](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204103719515.png))</mark>







### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：80min



代码：

```python
import sys

sys.setrecursionlimit(300000)
input = sys.stdin.read

def is_valid(x, y, m, n):
    return 0 <= x < m and 0 <= y < n

def dfs(x, y, water_height_value, m, n, h, water_height):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]

    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        if is_valid(nx, ny, m, n) and h[nx][ny] < water_height_value:
            if water_height[nx][ny] < water_height_value:
                water_height[x][y] = water_height_value
                dfs(nx, ny, water_height_value, m, n, h, water_height)

def main():
    data = input().split()
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []

    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        h = []
        for i in range(m):
            h.append(list(map(int, data[idx:idx + n])))
            idx += n
        water_height = [[0] * n for _ in range(m)]

        i, j = map(int, data[idx:idx + 2])
        idx += 2
        i, j = i - 1, j - 1

        p = int(data[idx])
        idx += 1

        for _ in range(p):
            x, y = map(int, data[idx:idx + 2])
            idx += 2
            x, y = x - 1, y - 1
            if h[x][y] <= h[i][j]:
                continue

            dfs(x, y, h[x][y], m, n, h, water_height)

        results.append("Yes" if water_height[i][j] > 0 else "No")

    sys.stdout.write("\n".join(results) + "\n")

if __name__ == "__main__":
    main()

```



代码运行截图 <mark>（![image-20241204104412088](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204104412088.png))</mark>





### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：80min



代码：

```python
from collections import deque
from collections import defaultdict

def bfs(start, end, grid, h, w):
    queue = deque([start])
    in_queue = defaultdict(lambda: float('inf'))
    dirs = [(0, -1), (-1, 0), (0, 1), (1, 0)]
    min_x = float('inf')
    while queue:
        x, y, d, seg = queue.popleft()

        for i, (dx, dy) in enumerate(dirs):
            nx, ny = x + dx, y + dy

            new_seg = seg if i == d else seg + 1
            if (nx, ny) == end:
                min_x = min(min_x, new_seg)
                continue

            if (0 <= nx < h + 2 and 0 <= ny < w + 2 and new_seg<in_queue[(nx,ny,i)]
                    and grid[nx][ny] != 'X'):
                    in_queue[(nx, ny, i)] = new_seg
                    queue.append((nx, ny, i, new_seg))

    return min_x


board_num = 1
while True:
    w, h = map(int, input().split())
    if w == h == 0:
        break

    grid = [' ' * (w + 2)] + [' ' + input() + ' ' for _ in range(h)] + [' ' * (w + 2)]
    print(f"Board #{board_num}:")
    pair_num = 1
    while True:
        y1, x1, y2, x2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0:
            break

        start = (x1, y1, -1, 0)
        end = (x2, y2)

        seg = bfs(start, end, grid, h, w)
        if seg == float('inf'):
            print(f"Pair {pair_num}: impossible.")
        else:
            print(f"Pair {pair_num}: {seg} segments.")
        pair_num += 1

    print()
    board_num += 1
```



代码运行截图 <mark>（![image-20241204104539898](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241204104539898.png))</mark>





## 2. 学习总结和收获

前两题掌握了套路还是可以掌握的，但是后面几个大题属实复杂只能根据答案一步一步复原理解





