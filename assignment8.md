# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by 张子明 数学科学学院

**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：45min



代码：

```python
def calculate(n, m, grid):
    perimeter = 0
    
    for i in range(n):
        for j in range(m):
            if grid[i][j] == 1:
                perimeter += 4
                if i > 0 and grid[i-1][j] == 1:
                    perimeter -= 1
                if i < n-1 and grid[i+1][j] == 1:
                    perimeter -= 1
                if j > 0 and grid[i][j-1] == 1:
                    perimeter -= 1
                if j < m-1 and grid[i][j+1] == 1:
                    perimeter -= 1
                
    return perimeter
n, m = map(int, input().split())
grid = []
for _ in range(n):
    grid.append(list(map(int, input().split())))

print(calculate(n, m, grid))

```



代码运行截图 <mark>（![image-20241119223514851](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119223514851.png))</mark>





### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：45min



代码：

```python
def generate(n):
    matrix = [[0] * n for _ in range(n)]
    top, bottom, left, right = 0, n - 1, 0, n - 1
    num = 1
    
    while num <= n * n:
        for i in range(left, right + 1):
            matrix[top][i] = num
            num += 1
        top += 1
        
        for i in range(top, bottom + 1):
            matrix[i][right] = num
            num += 1
        right -= 1
        
        for i in range(right, left - 1, -1):
            matrix[bottom][i] = num
            num += 1
        bottom -= 1
        
        for i in range(bottom, top - 1, -1):
            matrix[i][left] = num
            num += 1
        left += 1
    
    return matrix

n = int(input())
spiral_matrix = generate(n)
for row in spiral_matrix:
    print(" ".join(map(str, row)))
```



代码运行截图 ==（![image-20241119224652881](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119224652881.png))==





### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：40min



代码：

```python
d = int(input())
n = int(input())
board = [[0] * 1025 for _ in range(1025)]
for _ in range(n):
    x, y, k = map(int, input().split())
    for i in range(max(0, x - d), min(1025, x + d + 1)):
        for j in range(max(0, y - d), min(1025, y + d + 1)):
            board[i][j] += k
maxk = max(max(l) for l in board)
num = sum(l.count(maxk) for l in board)
print(num, maxk)
```



代码运行截图 <mark>（![image-20241119225431598](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119225431598.png))</mark>





### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：55min



代码：

```python
def longest_wiggle_subsequence(nums):
    n = len(nums)
    if n < 2:
        return n

    up = [1] * n
    down = [1] * n

    for i in range(1, n):
        if nums[i] > nums[i - 1]:
            up[i] = down[i - 1] + 1
            down[i] = down[i - 1]
        elif nums[i] < nums[i - 1]:
            down[i] = up[i - 1] + 1
            up[i] = up[i - 1]
        else:
            up[i] = up[i - 1]
            down[i] = down[i - 1]

    return max(up[-1], down[-1])


n = int(input())
nums = list(map(int, input().split()))
print(longest_wiggle_subsequence(nums))

```



代码运行截图 <mark>（![image-20241119230805723](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119230805723.png))</mark>





### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：50min



代码：

```python
def max_points(n, nums):
    max_value = 10**5
    count = [0] * (max_value + 1)

    for num in nums:
        count[num] += 1

    dp = [0] * (max_value + 1)
    dp[1] = count[1]

    for x in range(2, max_value + 1):
        dp[x] = max(dp[x - 1], dp[x - 2] + x * count[x])

    return dp[max_value]


n = int(input())
nums = list(map(int, input().split()))
print(max_points(n, nums))

```



代码运行截图 <mark>（![image-20241119231835141](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119231835141.png))</mark>





### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：50min



代码：

```python
while True:
    n = int(input())
    if n == 0:
        break
    a = sorted([int(x) for x in input().split()], reverse=True)
    b = sorted([int(x) for x in input().split()], reverse=True)
    c = [[0]*(n+1) for _ in range(n+1)]
    for i in range(1, n+1):
        for j in range(1, n+1):
            if a[i-1] > b[j-1]:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1]+2)
            elif a[i-1] == b[j-1]:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1]+1)
            else:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1])
    print((c[n][n]-n)*200)
```



代码运行截图 <mark>（![image-20241119232502961](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241119232502961.png))</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

对我来说作业题还是十分有难度的，需要使用其他的帮助才能完成，感觉自己心态也不太好，总是赶时间完成，发现自己不会或者思路错了就去看解析和问ai，但是也在自己在做题目中学习。希望能赶上课程的进度。



