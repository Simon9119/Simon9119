# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>张子明 数学科学学院</mark>



**说明：**

1）⽉考： AC6<mark>（）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：



代码：

```python
n = int(input())

elderly = []
non_elderly = []

for _ in range(n):
    patient_id, age = input().split()
    age = int(age)
    if age >= 60:
        elderly.append((patient_id, age))
    else:
        non_elderly.append((patient_id, age))

elderly.sort(key=lambda x: -x[1])

sorted_patients = elderly + non_elderly

for patient in sorted_patients:
    print(patient[0])
```



代码运行截图 <mark>（![image-20241112210426581](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112210426581.png))</mark>





### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：



代码：

```python
n, m1, m2 = map(int, input().split())
a = [[0] * n for _ in range(n)]
b = [[0] * n for _ in range(n)]
for _ in range(m1):
    x, y, v = map(int, input().split())
    a[x][y] = v
for _ in range(m2):
    x, y, v = map(int, input().split())
    b[x][y] = v
c = [[0] * n for _ in range(n)]
for i in range(n):
    for j in range(n):
        c[i][j] = sum(a[i][k] * b[k][j] for k in range(n))
        if c[i][j] != 0:
            print(i, j, c[i][j])
```



代码运行截图 ==（![image-20241112205900313](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112205900313.png))==





### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：



代码：

```python
from collections import defaultdict

cases = int(input())

for _ in range(cases):
    situation = "alive" 
    n, m, b = map(int, input().split())
    a = defaultdict(list) 
    
    for _ in range(n):
        x, y = map(int, input().split())
        a[x].append(y)
    
    for x in sorted(a):
        if m >= len(a[x]):
            b -= sum(a[x])
        else:
            a[x].sort(reverse=True)
            b -= sum(a[x][:m])
        
        if b <= 0:
            situation = x
            break
    
    print(situation)

```



代码运行截图 <mark>（![image-20241112210325395](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112210325395.png))</mark>





### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：



代码：

```python
def coinChange(coins, m):
    dp = [float('inf')] * (m + 1)
    dp[0] = 0
    
    for coin in coins:
        for i in range(coin, m + 1):
            dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[m] if dp[m] != float('inf') else -1

n, m = map(int, input().split())
coins = list(map(int, input().split()))

print(coinChange(coins, m))

```



代码运行截图 <mark>（![image-20241112210718237](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112210718237.png))</mark>





### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：



代码：

```python
def word_to_number(word):
    num_map = {
        'zero': 0, 'one': 1, 'two': 2, 'three': 3, 'four': 4, 'five': 5, 'six': 6, 'seven': 7, 'eight': 8, 'nine': 9,
        'ten': 10, 'eleven': 11, 'twelve': 12, 'thirteen': 13, 'fourteen': 14, 'fifteen': 15, 'sixteen': 16, 'seventeen': 17,
        'eighteen': 18, 'nineteen': 19, 'twenty': 20, 'thirty': 30, 'forty': 40, 'fifty': 50, 'sixty': 60, 'seventy': 70,
        'eighty': 80, 'ninety': 90, 'hundred': 100, 'thousand': 1000, 'million': 1000000
    }
    
    words = word.split()
    result = 0
    temp = 0
    sign = 1
    
    if 'negative' in words:
        sign = -1
        words.remove('negative')
    
    for w in words:
        if w in num_map:
            num = num_map[w]
            
            if num == 100:
                temp *= num
            elif num == 1000 or num == 1000000:
                temp *= num
                result += temp
                temp = 0
            else:
                temp += num
    
    result += temp
    return result * sign

input_str = input().strip()
print(word_to_number(input_str))

```



代码运行截图 <mark>（![image-20241112210815438](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112210815438.png))</mark>





### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：



代码：

```python
def max_activities(n, activities):
    activities.sort(key=lambda x: x[1])
    count = 0
    last_end_time = -1
    for start, end in activities:
        if start > last_end_time:
            count += 1
            last_end_time = end
    return count

n = int(input())
activities = []
for _ in range(n):
    start, end = map(int, input().split())
    activities.append((start, end))

print(max_activities(n, activities))
```



代码运行截图 <mark>（![image-20241112211016882](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241112211016882.png))</mark>





## 2. 学习总结和收获

平时都是不会的可以问ai和查答案养成了习惯，并没有认真的背一些语法，本次闭卷做题顿时丢了底气，好多语法都要一个一个试才行。能感受到我的真实水平离题目的难度还差的远，希望在期末来临前能努力跟上吧。





