# Assignment #1: 拉齐大家Python水平

Updated 0940 GMT+8 Feb 19, 2024

2024 spring, Complied by ==赵策 数学科学学院==



**编程环境**


操作系统：Windows 11

Python编程环境：Visual Studio Code 1.86.2



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/



思路：



##### 代码

```python
# 
n=int(input())
a,b,c=0,1,1
for i in range(n-2):
    a,b,c=b,c,a+b+c
print(c)
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](5ef58a348bb4aa08b784e8329595933.png)




### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A



思路：
##### 代码

```python
# 
s=input()
dp=[0]*5
s0='hello'
count=0
for l in s:
    if l==s0[count]:
        dp[count]=1
        count+=1
    if count==5:
        break
if sum(dp)==5:
    print('YES')
else:
    print('NO')
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](55eeaa0feba1a48b7cf9b06f65f0b60.png)




### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A



思路：
##### 代码

```python
# 
s=input().lower()
l=['a','e','i','o','u','y']
ans=''
for a in s:
    if a in l:
        continue
    else:
        ans=ans+'.'+a
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](e3274cc1198850ce0ee8cad0ce5cf42.png)




### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/



思路：



##### 代码

```python
# 
from math import sqrt
def isPrime(a):
    b=int(sqrt(a))+1
    lst=[]
    for i in range(2,b):
        if a%i==0:
            lst.append(i)
    if lst==[]:
        return True
    else:
        return False
    
n=int(input())
for i in range(1,n//2):
    if isPrime(i) and isPrime(n-i):
        print(i,n-i)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](1708507097839.png)




### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



思路：



##### 代码

```python
# 
lst=list(input().split('+'))
lst2=[]
for i in lst:
    a,b=i.split('^')
    if a!='0n':
        lst2.append(int(b))
print('n^'+str(max(lst2)))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](1708507126837(1).png)




### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/



思路：



##### 代码

```python
# 
lst=list(map(int,input().split()))
lst2=list(set(lst))
dic={i:0 for i in lst2}
ans=[]
for i in lst:
    dic[i]+=1
for i in dic.keys():
    if dic[i]==max(dic.values()):
        ans.append(i)
ans.sort()
ans=[str(i) for i in ans]
print(' '.join(ans))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](1708507175549(1).png)




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“数算pre每日选做”、CF、LeetCode、洛谷等网站题目。==
本次作业简单，有在OJ、PythonTip等网站练习；下载了Typora，方便编辑使用markdown



