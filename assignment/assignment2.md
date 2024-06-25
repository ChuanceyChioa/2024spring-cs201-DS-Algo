# Assignment #2: 编程练习

Updated 0953 GMT+8 Feb 24, 2024

2024 spring, Complied by ==赵策 数学科学学院==



**编程环境**


操作系统：Windows 11

Python编程环境：Visual Studio Code 1.86.2



## 1. 题目

### 27653: Fraction类

http://cs101.openjudge.cn/2024sp_routine/27653/



思路：



##### 代码

```python
# 
def gcd(m,n):
    while m%n != 0:
        oldm = m
        oldn = n
        m = oldn
        n = oldm%oldn
    return n
class Fraction:
    def __init__(self,top,bottom):
        self.num=top
        self.den=bottom
    def __str__(self):
        return str(self.num) + "/" + str(self.den)
    def __add__(self, otherfraction):
        newnum = self.num * otherfraction.den + self.den * otherfraction.num 
        newden = self.den * otherfraction.den 
        common = gcd(newnum, newden)
        return Fraction(newnum//common, newden//common)
a,b,c,d=map(int,input().split())
print(Fraction(a,b)+Fraction(c,d))
```



代码运行截图 ==（至少包含有"Accepted"）==

![1709623443018](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709623443018.png)



### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110



思路：



##### 代码

```python
# 
n,w=map(int,input().split())
val=[]
for _ in range(n):
    v,wi=map(int,input().split())
    val_per=v/wi
    for _ in range(wi):
        val.append(val_per)
val.sort(reverse=True)
val_sum=sum(val[:w])
print('{:.1f}'.format(val_sum))
```



代码运行截图 ==（至少包含有"Accepted"）==

![1709623509272](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709623509272.png)



### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/



思路：



##### 代码

```python
# 
from collections import defaultdict
res=[]
for _ in range(int(input())):
    a=defaultdict(list)
    n,m,b=map(int,input().split())
    for _ in range(n):
        t,x=map(int,input().split())
        a[t].append(x)
    for t in sorted(a):
        b-=sum(sorted(a[t],reverse=True)[:m])
        if b<=0:
            res.append(t)
            break
    else:
        res.append('alive')
for _ in res:
    print(_)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709623582735](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709623582735.png)



### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：



##### 代码

```python
# 
from math import sqrt
N=10**6
s=[True]*(N+2)
p=2
s[1]=False
while p<N:
	if s[p]:
		for i in range(2*p,N+1,p):
			s[i]=False
	p+=1

n=int(input())
nums=list(map(int,input().split()))
for i in range(n):
    a=nums[i]
    b=int(sqrt(a))
    if b**2==a and s[b]:
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709984402238](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709984402238.png)



### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A



思路：



##### 代码

```python
# 
for _ in range(int(input())):
    a,b=map(int,input().split())
    s=-1
    A=list(map(lambda x:int(x)%b,input().split()))
    if sum(A)%b!=0:
        print(a)
        continue
    for i in range(a//2+1):
        if A[i] or A[a-i-1]:
            s=a-i-1
            break
    print(s)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709984426007](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709984426007.png)



### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：



##### 代码

```python
# 
from math import sqrt
N = 10005
s=[True]*N
p=2
while p*p<=N:
	if s[p]:
		for i in range(p*2,N,p):
			s[i]=False
	p+=1

m,n=map(int,input().split())
for _ in range(m):
    s0=[int(i) for i in input().split()]
    l=len(s0)
    sum=0
    for a in s0:
        b=int(sqrt(a))
        if b**2==a and s[b]:
            sum+=a
    sum/=l
    if sum==0:
        print(0)
    else:
        print('%.2f'%sum)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709627722843](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709627722843.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本次作业相比第一次提高了一些难度，需要考虑算法时间复杂度，记录常用算法

（如欧拉筛：

from math import sqrt
N=10**6
s=[True]*(N+2)
p=2
s[1]=False
while p<N:
	if s[p]:
		for i in range(2*p,N+1,p):
			s[i]=False
	p+=1

）

需要巩固基础并加强练习
