# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by Hongfei Yan==（张子明，2400090106）==



**说明：**

1）Oct⽉考： AC6==（1）== 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：15分钟 每个字母的顺序减去k就是原来的字母，为了不超过26字母需要前去a的取模再加回a的顺序



代码

```python

a = int(input())
b = input()
for char in b:
    if 'a' <= char <= 'z':
        new_char = chr((ord(char)-ord('a')-a)%26+ord('a'))
    elif 'A' <= char <= 'Z':
        new_char = chr((ord(char)-ord('A')-a)%26+ord('A'))
    print(new_char,end='')
```



代码运行截图 ==（![image-20241015165354471](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241015165354471.png))==





### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：5分钟 用[:2]取字符串的前两个数字



代码

```python
a,b=input().split()
x=int(a[:2])
y=int(b[:2])
print(x+y)

```



代码运行截图 ==（![image-20241015170317201](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241015170317201.png))==





### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：25分钟 将每个数字的系数和余数列为两个序列，根据题意用每个数字乘以系数在除以11取余数和最后一位对比

代码

```python
n=int(input())
list1 = [7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
list2 = ['1','0','X','9','8','7','6','5','4','3','2']
for _ in range(n):
    s=input()
    x=0
    for i in range(17):
        x+=int(s[i])*list1[i]
    y=x%11
    if list2[y] == s[17].upper():
        print('YES')
    else:
        print('NO')

```



代码运行截图 ==（![image-20241015180312408](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241015180312408.png))==





### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：15分钟 



代码

```python
n=int(input())
if n==1:
    print('End')
else:
    while n!=1:
        if n%2==0:
            m=n//2
            print(f'{n}/2={m}')
        else:
            m=n*3+1
            print(f'{n}*3+1={m}')
        n = m
    print('End')
```



代码运行截图 ==（![image-20241015183005261](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241015183005261.png))==





### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：只有一点想法，但是不知道用什么语法靠代码实现，依靠ai和答案做出的代码



##### 代码

```python
def roman_to_integer(s):
    roman_values = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    }

    total = 0
    prev_value = 0

    for char in reversed(s):
        value = roman_values[char]
        if value < prev_value:
            total -= value
        else:
            total += value
        prev_value = value

    return total


def integer_to_roman(num):
    value_to_roman = [
        (1000, 'M'),
        (900, 'CM'),
        (500, 'D'),
        (400, 'CD'),
        (100, 'C'),
        (90, 'XC'),
        (50, 'L'),
        (40, 'XL'),
        (10, 'X'),
        (9, 'IX'),
        (5, 'V'),
        (4, 'IV'),
        (1, 'I')
    ]

    result = ""

    for value, roman in value_to_roman:
        while num >= value:
            result += roman
            num -= value

    return result


input_str = input()

if input_str.isdigit():
    num = int(input_str)
    if 1 <= num <= 3999:
        print(integer_to_roman(num))
else:
    print(roman_to_integer(input_str))

```



代码运行截图 ==（![image-20241015184403845](C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20241015184403845.png))==





### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：



代码

```python


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==对于完全没有语法储备的新人来说离开了网络查询代码真的什么都不会了，但将本次月考作为作业来的话除了罗马数字这题其他题目都没有特别依靠ai，但是几乎每道题还是需要网上查询语法以应对以往题目没有使用过的代码。==











