# Assignment #8: 图论：概念、遍历，及 树算

Updated 1150 GMT+8 Apr 8, 2024

2024 spring, Complied by ==赵策 数学科学学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows 11

Python编程环境：Visual Studio Code 1.86.2

## 1. 题目

### 19943: 图的拉普拉斯矩阵

matrices, http://cs101.openjudge.cn/practice/19943/



思路：



代码

```python
# 
n,m=map(int,input().split())
arr=[[0]*n for _ in range(n)]
for _ in range(m):
    i,j=map(int,input().split())
    arr[i][j]=arr[j][i]=-1
for i in range(n):
    for j in range(n):
        if arr[i][j]==-1:
            arr[i][i]+=1
for i in range(n):
    print(' '.join(map(str,arr[i])))
```



代码运行截图 ==（至少包含有"Accepted"）==

![1712659536896](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1712659536896.png)



### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：



代码

```python
# 
def dfs(x,y):
    if x<0 or x>=n or y<0 or y>=m or board[x][y]=='.' or visited[x][y]:
        return 0
    visited[x][y]=True
    area=1
    directions=[(x,y) for x in [-1,0,1] for y in [-1,0,1]]
    for dx,dy in directions:
        area+=dfs(x+dx,y+dy)
    return area

def find_largest_area(board):
    max_area=0
    for i in range(n):
        for j in range(m):
            if board[i][j]=='W' and not visited[i][j]:
                max_area=max(max_area,dfs(i,j))
    return max_area

for _ in range(int(input())):
    n,m=map(int,input().split())
    board=[input() for _ in range(n)]
    visited=[[False for _ in range(m)] for _ in range(n)]
    print(find_largest_area(board))
```



代码运行截图 ==（至少包含有"Accepted"）==

![1712661679613](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1712661679613.png)



### sy383: 最大权值连通块

https://sunnywhy.com/sfbj/10/3/383



思路：



代码

```python
# 
def dfs(v):
    visited[v]=True
    wgt=weights[v]
    for nbr in neighbor[v]:
        if not visited[nbr]:
            wgt+=dfs(nbr)
    return wgt

n,m=map(int,input().split())
weights=list(map(int,input().split()))
visited=[False]*n
neighbor=[[] for _ in range(n)]
for _ in range(m):
    u,v=map(int,input().split())
    neighbor[u].append(v)
    neighbor[v].append(u)
dp=[0]*n
for v in range(n):
    if not visited[v]:
        dp[v]=dfs(v)
print(max(dp))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1713173134970](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1713173134970.png)



### 03441: 4 Values whose Sum is 0

data structure/binary search, http://cs101.openjudge.cn/practice/03441



思路：



代码

```python
# 
def count(arr):
    sum_counts={}
    for a in arr[0]:
        for b in arr[1]:
            sum1=a+b
            sum_counts[sum1]=sum_counts.get(sum1,0)+1
    cnt=0
    for c in arr[2]:
        for d in arr[3]:
            sum2=-(c+d)
            if sum2 in sum_counts:
                cnt+=sum_counts[sum2]
    return cnt

arr=[[] for _ in range(4)]
for _ in range(int(input())):
    quadruplet=input().split()
    for _ in range(4):
        arr[_].append(int(quadruplet[_]))
print(count(arr))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1713174785303](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1713174785303.png)



### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/



思路：



代码

```python
# 
for _ in range(int(input())):
    n=int(input())
    phone_numbers=sorted([input() for _ in range(n)])
    sgn=0
    for i in range(n-1):
        u,v=phone_numbers[i],phone_numbers[i+1]
        if len(u)<=len(v) and u==v[:len(u)]:
                sgn=1
                break
        if sgn==1:
            break
    print('YES' if sgn==0 else 'NO')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1713182568628](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1713182568628.png)



### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：



代码

```python
# 
from collections import defaultdict
n=int(input())
preorder=input().split()
root,type=list(preorder[0])
dic={}
nodes=[root]
dic[root]=type
tier=defaultdict(list)
tier[0].append(root)
level=0
for i in range(1,n):
    name,type=list(preorder[i])
    dic[name]=type
    if dic[nodes[-1]]=='1':
        level-=1
    else:
        level+=1
    nodes.append(name)
    if name!='$':
        tier[level].append(name)
res=''
for i in sorted(tier.items()):
    res+=''.join(i[1])[::-1]
print(' '.join(res))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1713192955809](D:\HuaweiMoveData\Users\Chaun\Documents\WeChat Files\wxid_43vf8wixfcpq22\FileStorage\Temp\1713192955809.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

居然没有一道题写了树（×）

最后一题写的还是比较满意的

电话号码那道题时间卡的还是挺死的,最开始用了一个双重循环就超时了：

```python
#
for _ in range(int(input())):
    n=int(input())
    phone_numbers=sorted([input() for _ in range(n)],key=lambda x:int(x))
    sgn=0
    for i in range(n-1):
        for j in range(i+1,n):
            u,v=phone_numbers[i],phone_numbers[j]
            if u==v[:len(u)]:
                    sgn=1
                    break
        if sgn==1:
            break
    print('YES' if sgn==0 else 'NO')
```
