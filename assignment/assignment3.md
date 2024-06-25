# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by ==赵策 数学科学学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11

Python编程环境：Visual Studio Code 1.86.2



## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
# 
def f(missile):
    global k
    dp=[1]*k
    for i in range(k):
        for j in range(i):
            if missile[j]>=missile[i]:
                dp[i]=max(dp[i],dp[j]+1)
    return max(dp)

k=int(input())
missile=list(map(int,input().split()))
print(f(missile))
```



代码运行截图 ==（至少包含有"Accepted"）==

![1709985553696](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709985553696.png)



**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：



##### 代码

```python
# 
def Move(a,b,c,n):
    if n==1:
        print(str(n)+':'+a+'->'+c)
    else:
        Move(a,c,b,n-1)
        print(str(n)+':'+a+'->'+c)
        Move(b,a,c,n-1)

n,a,b,c=input().split()
n=int(n)
Move(a,b,c,n)
```



代码运行截图 ==（至少包含有"Accepted"）==

![1709985660912](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709985660912.png)



**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：



##### 代码

```python
# 
import queue
def josephus(n,m,p):
    q=queue.Queue()
    ans=[]
    for i in range(1,n+1): 
        q.put((i+p-1)%n)
    while q.qsize() > 0:
        for _ in range(m - 1):
            q.put(q.get())
        ans.append(q.get())
    for i in range(n):
        if ans[i]==0:
            ans[i]=n
            break
    ans=[str(i) for i in ans]
    print(','.join(ans))

while True:
    n,p,m=map(int,(input().strip('/r')).split())
    if n==0 and m==0:
        break
    josephus(n,m,p)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709985516940](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709985516940.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python
# 
n=int(input())
s=[]
t=list(map(int,input().split()))
for i in range(1,n+1):
    s.append((t[i-1],i))
s.sort(key=lambda x: x[0])
ans=[]
for i in range(1, n+1):
    ans.append(s[i-1][1])
ans=[str(i) for i in ans]
print(' '.join(ans))
sum=0
for i in range(1, n+1):
    sum+=s[i-1][0]*(n - i)
print("{:.2f}".format(sum/n))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1709985872970](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1709985872970.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
# 
def median(lst):
    lst0=sorted(lst)
    l=len(lst0)
    a=int(l/2)
    if l%2==0:
        return (lst0[a-1]+lst0[a])/2
    if l%2!=0:
        return lst0[a]

n=int(input())
pairs=[i[1:-1] for i in input().split()]
distance=[sum(map(int,i.split(','))) for i in pairs]
expense=list(map(int,input().split()))
ratio=[]
cnt=0
for i in range(n):
    ratio.append(distance[i]/expense[i])
a,b=map(median,(expense,ratio))
for i in range(n):
    if expense[i]<a and ratio[i]>b:
        cnt+=1
print(cnt)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1710050547251](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1710050547251.png)



**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
# 
from collections import defaultdict
n=int(input())
dic=defaultdict(list)
for _ in range(n):
    a,b=input().split('-')
    dic[a].append(b)
d=sorted(dic)
for i in d:
    l1=[]
    l2=[]
    for j in dic[i]:
        if j[-1]=='M':
            l1.append(j[:-1])
        else:
            l2.append(j[:-1])
    l1.sort(key=lambda x:eval(x))
    l2.sort(key=lambda x:eval(x))
    l1=[i+'M' for i in l1]
    l2=[i+'B' for i in l2]
    if l1==[]:
        print(i+': '+', '.join(l2))
    elif l2==[]:
        print(i+': '+', '.join(l1))
    else:
        print(i+': '+', '.join(l1)+', '+', '.join(l2))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1710058545045](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1710058545045.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

整体不难，要注意解题速度，其二是积累重点算法（类似于建立思维模型），判断题目需要使用什么比如dp、递归、queue、greedy等等，需要投入时间加强练习



