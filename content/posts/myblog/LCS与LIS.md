---

title: "LIS与LCS"
summary: 
date: 2023-01-15
weight: 
tags: ["LIS","LCS"]
author: "CHuSeng"
draft: false
isCJKLanguage: true
---

# 最长公共子序列

一个给定序列的**子序列**是在该序列中删去若干个元素后得到的序列。子序列与子串不同，子序列在原序列中可以是不连续的，而子串必须是连续的。

最长公共子序列（longest common subsequence）问题：对给定的两个序列，找出他们的最长公共子序列。
$$
L[i][j]=
\begin{cases}
L[i-1][j-1]&(X_i=y_j)
\\
max(L[i-1][j],L[i][j-1])&(X_i\not=y_j)
\end{cases}
$$

```c++
int LCS(){
    memset(dp,0,sizeof(dp));
    for(int i=1;i<=str1.length();i++){
        for(int j=1;j<=str2.length();j++){
            if(str1[i-1]==str2[j-1])
                dp[i][j]=dp[i-1][j-1]+1;
            else
                dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
        }
    }
    return dp[str1.length()][str2.length()];
}
```



# 最长递增子序列

最长递增子序列（longest increasing subsequence）问题：给定一个长度为N的数组，找出一个最长的单调递增子序列。

### 方法一：用LCS求解
------

先对序列进行排序X‘，将X'和原序列X取最长公共子序列，即为最长递增子序列。



### 方法二：直接使用DP

------



$$
DP[i]=max\{DP[j],0\}+1 \quad(0<j\leq i-1)
$$

### 方法三：使用数组O（nlgn）

---

逐个处理原序列中的数，如果比辅助数组的最后一个数大，则在辅助数组的最后加入该数；否则替换掉原数组中的第一个大于该数的数字。

```c++
int LIS(){
    int len = 0;
    int d[maxn];
    d[1]=arr[1];
    for(int i=1;i<=n;i++){
        if(arr[i]>d[len])
            d[++len]=arr[i];
        else {
            //int j=lower_bound(d+1,d+1+len,arr[i]) - d;
            //或者二分查找
            int l=1,r=len+1;
            while(l<r){
                mid=(r+l)/2;
                if(d[mid]<arr[i])
                    l=mid+1;
                else r=mid+1;
            }
            j=l;
            d[j]=arr[i];
        }     
    }
    return len;
}
```

