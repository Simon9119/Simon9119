# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：15min 先将数列由小到大排列，再取最左边的就行了



代码

```python
a,b=map(int,input().split())
c=list(map(int,input().split()))
c.sort()
x=0
for i in range (b):
    if c[i] < 0:
        x -= c[i]
    else:
        break
print(x)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022221936936](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241022221936936.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：40min 将硬币大小从大到小排列，通过比较拿走的和剩下的大小知道拿走的多再停止



代码

```python

n=int(input())
m=list(map(int,input().split()))
sum = 0
for i in range(n):
    sum += m[i]
m.sort(reverse=True)
a = 0
x = 0
for i in range(n):
    a += m[i]
    x += 1
    if a > sum - a:
        break
print(x)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241022224925088](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241022224925088.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：40min 用序列A中最小的数加上所有序列B中的数，再反过来用B中最小的加上A，取最小值



代码

```python
t = int(input())
for _ in range(t):
    n = int(input())
    A = list(map(int, input().split()))
    B = list(map(int, input().split()))
    a = min(A)
    b = min(B)
    x = sum(a + b for b in B)
    y = sum(b + a for a in A)
    print(min(x,y))


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：4人组一辆车，3人组可以和1人拼车，2人组两两拼车，剩下的可以和两个1人组拼车，最后算剩下来的1人组要几辆车



代码

```python
n = int(input())
groups = list(map(int, input().split()))

def x(n, groups):
    count = [0] * 5

    for size in groups:
        count[size] += 1

    taxis = count[4]

    taxis += count[3]
    count[1] = max(0, count[1] - count[3])

    taxis += count[2] // 2
    if count[2] % 2 == 1:
        taxis += 1
        count[1] = max(0, count[1] - 2)

    taxis += (count[1] + 3) // 4

    return taxis

print(x(n, groups))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241022235253536](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241022235253536.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

本次作业中除了最后一题都没有很平凡的使用ai辅助和查答案，特别是完成第一题后在第二题中融会贯通，还是挺有趣的。有些错误自己盯着看是真的想不出问题的来源，总的来说也能感受到自己的进步，希望有一天能彻底的独立完成那些困难一点的题目吧。



