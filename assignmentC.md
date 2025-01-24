# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>张子明 数学科学学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：



代码：

```python
def dfs(a, b, memo):
    if (a, b) in memo:
        return memo[(a, b)]
    if a == 0 or b == 0:
        return False
    if a < b:
        a, b = b, a
    k = a // b
    if k >= 2:
        memo[(a, b)] = True
        return True
    for i in range(1, k + 1):
        new_a = a - i * b
        if not dfs(new_a, b, memo):
            memo[(a, b)] = True
            return True
    memo[(a, b)] = False
    return False

def main():
    while True:
        a, b = map(int, input().split())
        if a == 0 and b == 0:
            break
        memo = {}
        if dfs(a, b, memo):
            print("win")
        else:
            print("lose")

if __name__ == "__main__":
    main()

```



代码运行截图 <mark>（![image-20241217221830812](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217221830812.png))</mark>





### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
n = int(input())
buffer = [0] * ((n+1)//2+1)
for i in range(1, n+1):
    line = [0]+list(map(int, input().split()))
    for j in range(1, n+1):
        k = min(i, j, (n+1)-i, (n+1)-j)
        buffer[k] += line[j]
print(max(buffer))
```



代码运行截图 ==（![image-20241217222546197](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217222546197.png))==





### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
a=int(input())
potions=list(map(int,input().split()))
dp=[-float('inf')]*(1+a)
dp[0]=0
for i in range(1+a):
	for j in range(i,0,-1):
		temp=max(dp[j],dp[j-1]+potions[i-1])
		if temp>=0:
			dp[j]=temp
for i in range(a,-1,-1):
	if dp[i]>=0:
		print(i)
		break
```



代码运行截图 <mark>（![image-20241217222701219](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217222701219.png))</mark>





### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
def main():
    stack = []
    min_stack = []
    
    while True:
        try:
            command = input().strip()
            if command.startswith('push'):
                _, n = command.split()
                n = int(n)
                stack.append(n)
                if min_stack:
                    min_stack.append(min(n, min_stack[-1]))
                else:
                    min_stack.append(n)
            elif command == 'pop':
                if stack:
                    stack.pop()
                    min_stack.pop()
            elif command == 'min':
                if min_stack:
                    print(min_stack[-1])
        except EOFError:
            break

if __name__ == "__main__":
    main()

```



代码运行截图 <mark>（![image-20241217222812536](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217222812536.png))</mark>





### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python
import heapq
m, n, p = map(int, input().split())
martix = [list(input().split())for i in range(m)]
dir = [(-1, 0), (1, 0), (0, 1), (0, -1)]
for _ in range(p):
    sx, sy, ex, ey = map(int, input().split())
    if martix[sx][sy] == "#" or martix[ex][ey] == "#":
        print("NO")
        continue
    in_queue, heap, ans = set(), [], []
    heapq.heappush(heap, (0, sx, sy))
    in_queue.add((sx, sy, -1))
    while heap:
        tire, x, y = heapq.heappop(heap)
        if x == ex and y == ey:
            ans.append(tire)
        for i in range(4):
            dx, dy = dir[i]
            x1, y1 = dx+x, dy+y
            if 0 <= x1 < m and 0 <= y1 < n and martix[x1][y1] != "#" and (x1, y1, i) not in in_queue:
                t1 = tire+abs(int(martix[x][y])-int(martix[x1][y1]))
                heapq.heappush(heap, (t1, x1, y1))
                in_queue.add((x1, y1, i))
    print(min(ans) if ans else "NO")
```



代码运行截图 <mark>（![image-20241217225135472](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217225135472.png))</mark>





### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
from collections import deque

def bfs(x, y):
    visited = {(0, x, y)}
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]
    queue = deque([(0, x, y)])
    while queue:
        time, x, y = queue.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            temp = (time + 1) % k
            if 0 <= nx < r and 0 <= ny < c and (temp, nx, ny) not in visited:
                cur = maze[nx][ny]
                if cur == 'E':
                    return time + 1
                elif cur != '#' or temp == 0:
                    queue.append((time + 1, nx, ny))
                    visited.add((temp, nx, ny))
    return 'Oop!'


t = int(input())
for _ in range(t):
    r, c, k = map(int, input().split())
    maze = [list(input()) for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if maze[i][j] == 'S':
                print(bfs(i, j))
```



代码运行截图 <mark>（![image-20241217225402942](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241217225402942.png))</mark>





## 2. 学习总结和收获

快到期末了，作业的题目还是需要ai和答案的辅助，虽然反思一下自己在这学期确实没有把很多精力放在编程上，希望能及格吧；-；





