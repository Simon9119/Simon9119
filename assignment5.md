# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>张子明 数学科学学院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。

非常抱歉，我之前在复习专业课的期中考试，有点昼夜颠倒，作业的截止日期记错了。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：25min 通过逐天递增就可以找到下一个共同高峰日



代码：

```python
case=0
while True:
    p,e,i,d=map(int,input().split())
    if [p,e,i,d]==[-1,-1,-1,-1]:
        break
    case+=1
    p%=23
    e%=28
    i%=33
    s=d+1
    while s%23!=p or s%28!=e or s%33!=i:
        s+=1
    print(f'Case {case}: the next triple peak occurs in {s-d} days.')
```



代码运行截图 <mark>（![image-20241030103020289](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030103020289.png))</mark>





### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：40min 将价格从小到大排序，有钱就买便宜的，没钱就把最贵的卖了



代码：

```python
p=int(input())
costs=list(map(int,input().split()))
costs.sort()
my=0
enemy=0
i=0
j=len(costs)-1
while i<=j:
    if p>=costs[i]:
        p-=costs[i]
        my+=1
        i+=1
    elif my>enemy:
        p+=costs[j]
        enemy+=1
        j-=1
    else:
        break
print(my - enemy+(costs[i] <= p))
```



代码运行截图 ==（![image-20241030143147667](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030143147667.png))==





### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：40min 让需要时间越少的人先做实验就能保证用时最少，使用lambda排列顺序



代码：

```python
n=int(input())
time=list(map(int,input().split()))
order=sorted(range(1,n+1),key=lambda x:time[x-1])
time.sort()
avg=sum((n-i-1)*time[i]for i in range(n))/n
print(*order)
print(f'{avg:.2f}')
```



代码运行截图 <mark>（![image-20241030200530230](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030200530230.png))</mark>





### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：题目就没怎么看懂，跟着答案的思路敲了一遍代码，用ai解释了几个不会的语法QAQ



代码：

```python
Haab = {"pop": 0, "no": 1, "zip": 2, "zotz": 3, "tzec": 4, "xul": 5, "yoxkin": 6, "mol": 7, "chen": 8, "yax": 9, "zac": 10, "ceh": 11, "mac": 12, "kankin": 13, "muan": 14, "pax": 15, "koyab": 16, "cumhu": 17, "uayet": 18}
Tzolkin = {0: "imix", 1: "ik", 2: "akbal", 3: "kan", 4: "chicchan", 5: "cimi", 6: "manik", 7: "lamat", 8: "muluk", 9: "ok", 10: "chuen", 11: "eb", 12: "ben", 13: "ix", 14: "mem", 15: "cib", 16: "caban", 17: "eznab", 18: "canac", 19: "ahau"}
n = int(input())
print(n)
for _ in range(n):
    day, month, year = input().split()
    day = int(day.rstrip("."))
    total = int(year) * 365 + Haab[month] * 20 + day
    print(total % 13 + 1, Tzolkin[total % 20], total // 260)
```



代码运行截图 <mark>（![image-20241030202051517](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030202051517.png))</mark>





### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：40min 让每颗树能往左倒就倒，不然就往右倒，都不行就不砍。砍完后变动坐标以确定下一个树能倒的位置。



代码：

```python
n = int(input())
tree = [tuple(map(int, input().split())) for _ in range(n)]

if n == 1:
    print(1)
else:
    trees = 1
    position = tree[0][0]

    for i in range(1, n - 1):
        x, h = tree[i]
        if x - h > position:
            trees += 1
            position = x
        elif x + h < tree[i + 1][0]:
            trees += 1
            position = x + h
        else:
            position = x

    trees += 1

    print(trees)
```



代码运行截图 <mark>（![image-20241030205404328](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030205404328.png))</mark>





### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：对新手来说好像有点困难，看的答案尝试理解了一下代码;-;



代码：

```python
import math

def solve(n, d, islands):
    if d < 0:
        return -1

    ranges = []
    for x, y in islands:
        if y > d:
            return -1
        delta = math.sqrt(d * d - y * y)
        ranges.append((x - delta, x + delta))

    if not ranges:
        return -1

    ranges.sort(key=lambda x:x[1])

    number = 1
    r = ranges[0][1]
    for start, end in ranges[1:]:
        if r < start:
            r = end
            number += 1

    return number

case_number = 0
while True:
    n, d = map(int, input().split())
    if n == 0 and d == 0:
        break

    case_number += 1
    islands = []
    for _ in range(n):
        islands.append(tuple(map(int, input().split())))

    result = solve(n, d, islands)
    print(f"Case {case_number}: {result}")
    input()
```



代码运行截图 <mark>（![image-20241030205914871](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241030205914871.png))</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

本次作业感觉比之前的困难了好多，光看题目就需要理解一会才有思路，有一点想法也无从下手，大部分题目需要答案和ai的辅助，但自己也啃了两道题，还是能感受到一点成长。（蛮多时候想用会的语法去尝试题目，后来才发现需要使用其他语法才能跟好的完成）



