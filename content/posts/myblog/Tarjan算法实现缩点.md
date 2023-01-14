---
title: "Tarjan+缩点"
summary: 
date: 2023-01-14
weight: 2
tags: ["tarjan","有向图"]
author: "CHuSeng"
isCJKLanguage: true
---
# Tarjan算法实现缩点

### [强连通分量]

在有向图G中，如果两点之间至少存在一条路径，称两个顶点强连通。

如果有向图G中任意两点连通，称图G为强连通图。

有向非强连通图的极大强连通子图，称为强连通分量。



### [Tarjan算法]

赋予每个节点DFN和LOW两个属性，分别表示节点的时间次序和能追溯到的栈中最早节点。

通过`dfs`从初始节点开始遍历，将每一个未处理的节点加入栈中，并给该节点赋值DFN（时间戳），再赋值LOW等于当前的DFN，等待后续更新。当`dfs`搜素到已经在队列中的节点S时，则将该节点的LOW值赋值为DFN(s)。`dfs`返回到某节点时，若该节点DFN=LOW则弹出栈顶元素直到该节点弹出，弹出的点为同一强连通分量。



### [Tarjan算法的c++实现]

```c++
void tarjan(int u){
    DFN[u]=LOW[u]=++index;
    instack[u]=true;
    stack[++top]=u;
    for(int i=head[u];i;i=e[i].next){
        int v=e[i].to;
        if(!DFN[v]){
            tarjan(v);
            low[u]=min(low[u],low[v]);
        }
        else if(instack(v))
            low[u]=min(low[u],low[v]);
    }
    if(DFN[u]==LOW[u]){
        dcnt++;
        do{
            int tmp=stack[top--];
            belong[tmp]=dcnt;
            instack[tmp]=false;
        }while(j!=i)
    }
}

void solve(){
    //top是栈顶；dcnt是组编，index是时间戳
    int top=0,dcnt=0,index=0;
    menset(DFN,0,sizeof(DFN));
    for(int i=1;i<=N;i++)
        if(!DFN[i])
            tarjan[i]; 
}
```



### [缩点]

```c++
void add(int u,int v){
    edge[++ecnt].to=v;
    edge[ecnt].next=head[u];
    head[u]=ecnt;
}
void suodian(){
    menset(edge,0,sizeof(edge));
    ecnt=0;
    //x[i],y[i]分别是原边的起点和终点，N是原边数
    for(int i=1;i<=N;i++){
        if(belong[x[i]]==belong[y[i]]) continue;
        else add(belong[x[i],belong[y[i]]);
    }
}
```

