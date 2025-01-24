# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>张子明 2400090106</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：30min



代码：

```python
n=int(input())
I = [(n,'A','B','C')]
print(2**n-1)
while I:
    n, A, B, C = I.pop()
    if n == 1:
        print(f'{A}->{C}')
    else:
        I.append((n-1,B,A,C))
        I.append((1,A,B,C))
        I.append((n-1,A,C,B))
```



代码运行截图 <mark>（![image-20241105201536350](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105201536350.png))</mark>





### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：30min



代码：

```python
n = int(input())

sequence = list(range(1, n + 1))
result = []

stack = [(sequence, [])]

while stack:
    nums, path = stack.pop()
    if not nums:
        result.append(path)
    else:
        for i in range(len(nums)):
            new_nums = nums[:i] + nums[i+1:]
            new_path = path + [nums[i]]
            stack.append((new_nums, new_path))
for perm in sorted(result):
    print(" ".join(map(str, perm)))
```



代码运行截图 ==（![image-20241105202540834](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105202540834.png))==





### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：20min



代码：

```python
k = int(input())
heights = list(map(int, input().split()))

dp = [1] * k

for i in range(1, k):
    for j in range(i):
        if heights[i] <= heights[j]:
            dp[i] = max(dp[i], dp[j] + 1)
print(max(dp))
```



代码运行截图 <mark>（![image-20241105203129389](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105203129389.png))</mark>





### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：30min



代码：

```python
N, B = map(int, input().split())
values = list(map(int, input().split()))
weights = list(map(int, input().split()))

dp = [[0] * (B + 1) for _ in range(N + 1)]

for i in range(1, N + 1):
    for w in range(B + 1):
        if weights[i-1] <= w:
            dp[i][w] = max(dp[i-1][w], dp[i-1][w - weights[i-1]] + values[i-1])
        else:
            dp[i][w] = dp[i-1][w]

print(dp[N][B])
```



代码运行截图 <mark>（![image-20241105203455874](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105203455874.png))</mark>





### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：45min 不会做，看的答案理解了下代码；-；



代码：

```python
list1 = []

def queen(s):
    if len(s) == 8:
        list1.append(s)
        return
    for i in range(1, 9):
        if all(str(i) != s[j] and abs(len(s) - j) != abs(i - int(s[j])) for j in range(len(s))):
            queen(s + str(i))

queen('')
samples = int(input())
for k in range(samples):
    print(list1[int(input()) - 1])
```



代码运行截图 <mark>（![image-20241105204038704](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105204038704.png))</mark>





### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：25min



代码：

```python
n, a, b, c = map(int, input().split())

dp = [-1] * (n + 1)
dp[0] = 0 

for x in range(1, n + 1):
    if x >= a and dp[x - a] != -1:
        dp[x] = max(dp[x], dp[x - a] + 1)
    if x >= b and dp[x - b] != -1:
        dp[x] = max(dp[x], dp[x - b] + 1)
    if x >= c and dp[x - c] != -1:
        dp[x] = max(dp[x], dp[x - c] + 1)

print(dp[n])
```



代码运行截图 <mark>（![image-20241105204837049](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241105204837049.png))</mark>





## 2. 学习总结和收获

感觉作业也是越来越难了，本次作业题目大部分都是看答案和问ai再尝试理解的，好在也感觉到自己确实有学到解答这些题目的方法。





