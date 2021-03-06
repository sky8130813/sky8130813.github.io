---
emoji: ๐ช
title: (์๊ณ ๋ฆฌ์ฆ) ์์ ์ ๋ ฌ Topological Sort + C++ ์์ 
date: '2019-07-02 03:00:00'
author: ์ค์ฝ๋ฉ
tags: algorithm
categories: ์๊ณ ๋ฆฌ์ฆ
---

## ์์ ์ ๋ ฌ(Topological Sort)์ด๋?

์ฌํ๊น์ง ์ ๋ ฌ ๊ธฐ์ค์ด ์๋ค๋ฉด **์์์ ๋ ฌ์ ์ ๋ ฌ ๊ธฐ์ค์ '์์'**์ด๋ค.
์ฌ๊ธฐ์ **์์์ด๋ incoming edge์ ์**๋ฅผ ์๋ฏธํ๋ค.

- ์์ ์ ๋ ฌ์ Directed Acyclic Graph(DAG)์์๋ง ๊ฐ๋ฅํ ์ ๋ ฌ๋ฐฉ๋ฒ์ด๋ค.
- DAG๋ ๊ฐ edge๊ฐ ๋ฐฉํฅ์ ๊ฐ์ง๊ณ  ์๋๋ฐ cycle์ด ๋ฐ์ํ์ง ์๋ ๊ฒฝ์ฐ๋ฅผ ๋งํ๋ค.
- **Cycle์ด ์์ผ๋ฉด ๋ฌดํ ๋ฃจํ๋ฅผ ๋ฐ์์ํฌ ๊ฒ์ด๋ค!!**
- ๋ณดํต ์ผ์ ์์๋ฅผ ์ ํ๋ ์๊ณ ๋ฆฌ์ฆ์์ ๋ง์ด ์ฌ์ฉ๋๋ค.

## Topological Sorting ์๊ณ ๋ฆฌ์ฆ

์๊ณ ๋ฆฌ์ฆ์ ๊ณผ์ ์ ๋ค์๊ณผ ๊ฐ๋ค.

1. ๊ฐ vertex์ ์์(incoming edge์ ์)๋ฅผ ์ ์ฅํ๋ค.
2. ์ ์ (์์์ด 0์ธ ๋ธ๋)์ ๋ค ํ์ ๋ฃ์ด์ค๋ค.
3. ํ์์ ๋ธ๋๋ฅผ ํ๋์ฉ ๊บผ๋ด์ ์์์ ๋ ฌ์ ๋ฃ์ด์ค๋ค.
4. ๊บผ๋ธ ๋ธ๋์ ์ฐ๊ฒฐ๋ ๋ธ๋์ ์์์ ํ๋์ฉ ๋ฎ์ถฐ์ฃผ๊ณ  ์ฃ์ง๋ฅผ ์์ ์ค๋ค.
5. ์์์ด 0์ธ ๋ธ๋๋ฅผ ํ์ ๋ค์ ๋ฃ์ด์ค๋ค.
6. 3๋ฒ๋ถํฐ 5๋ฒ์ ํ๊ฐ ๋น ๋๊น์ง ๋ฐ๋ณตํ๋ค.

## ์์

๋ค์๊ณผ ๊ฐ์ ๊ทธ๋ํ์ ๋ํด ์์ ์ ๋ ฌ์ ์งํํด๋ณด์.

### ์์ 0์ธ ์น๊ตฌ ํ์ ๋ฃ๊ธฐ

![์ฌ์ง](https://raw.githubusercontent.com/zoomKoding/zoomKoding.github.io/source/assets/_posts/topological-sort-0.png)

### ํ์์ 1 ๊บผ๋ด๊ธฐ

![์ฌ์ง](https://raw.githubusercontent.com/zoomKoding/zoomKoding.github.io/source/assets/_posts/topological-sort-1.png)

์ด ๋๋ ์์์ด 0์ธ ์น๊ตฌ๊ฐ ์์ผ๋ฏ๋ก ํ์ ์๋ฌด ๊ฐ๋ ๋ค์ด๊ฐ์ง ์๋๋ค.

### ํ์์ 3 ๊บผ๋ด๊ธฐ

![์ฌ์ง](https://raw.githubusercontent.com/zoomKoding/zoomKoding.github.io/source/assets/_posts/topological-sort-2.png)

### ํ์์ 2 ๊บผ๋ด๊ธฐ

![์ฌ์ง](https://raw.githubusercontent.com/zoomKoding/zoomKoding.github.io/source/assets/_posts/topological-sort-3.png)

**์ด์  ํ์ ์๋ฌด๊ฒ๋ ์์ผ๋ฏ๋ก ์ต์ข ์์ ์ ๋ ฌ๋ ๊ฒฐ๊ณผ(1,3,2,4)๋ฅผ ์ป์ ์ ์๋ค.**

## ์์์ ๋ ฌ ๊ด๋ จ ๋ฌธ์  (๋ฐฑ์ค 2252๋ฒ ์ค์ธ์ฐ๊ธฐ)

[๋ฐฑ์ค 2252๋ฒ ์ค์ธ์ฐ๊ธฐ ๋งํฌ](https://www.acmicpc.net/problem/2252)

### ๋งํฌ๋ ๋ฆฌ์คํธ ์ฌ์ฉ

```cpp
#include <cstdio>
#include <queue>

using namespace std;

int* in;
queue<int> q;


struct Node {
    int data;
    Node* next, * prev;
    Node() {
        next = prev = NULL;
        data = 0;
    }
    Node(int i, Node* ptr){
        data = i;
        prev = ptr;
        next = ptr->next;
        next->prev = prev->next = this;
    }
};

struct LinkedList {
    Node *head;
    Node *tail;
    LinkedList() {
        head = new Node();
        tail = new Node();
        head->next = tail;
        tail->prev = head;
    }
    void insert(int i) {
        new Node(i, tail->prev);
    }
};


int main(){
    int N, M, v1, v2;
    scanf("%d %d", &N, &M);
    LinkedList **list = new LinkedList*[N+1];
    for(int i = 0; i < N + 1; i++)list[i] = new LinkedList();
    in = new int[N+1];
    for(int i = 0; i < N + 1; i++)in[i] = 0;
    for(int i = 0 ; i < M; i++){
        scanf("%d %d", &v1, &v2);
        list[v1]->insert(v2);
        in[v2] ++;
    }
    for(int i = 1; i <N+1; i++){
        if(in[i] == 0) q.push(i);
    }

    while(!q.empty()){
        int temp = q.front();
        printf("%d ", temp);
        q.pop();
        Node* tmp = list[temp]->head;
        while (tmp->next != NULL) {
            in[tmp->data] --;
            if(in[tmp->data] == 0) q.push(tmp->data);
            tmp = tmp->next;
        }
    }
}
```

### ์ด์ค ๋ฒกํฐ๋ฅผ ์ด์ฉํ ์ฝ๋

```cpp
#include <cstdio>
#include <queue>
#include <vector>

using namespace std;

int* in;
queue<int> q;

int main(){
    int N, M, v1, v2;
    scanf("%d %d", &N, &M);
    vector<vector<int> > v;
    for(int i = 0; i < N + 1; i++)v.push_back(vector<int>());
    in = new int[N+1];
    for(int i = 0; i < N + 1; i++)in[i] = 0;
    for(int i = 0 ; i < M; i++){
        scanf("%d %d", &v1, &v2);
        v[v1].push_back(v2);
        in[v2] ++;
    }
    for(int i = 1; i <N+1; i++){
        if(in[i] == 0) q.push(i);
    }

    while(!q.empty()){
        int temp = q.front();
        printf("%d ", temp);
        q.pop();
        for(int i = 0; i < v[temp].size(); i++){
            if(--in[v[temp][i]] == 0)q.push(v[temp][i]);
        }
    }
}
```

### ๊ฒฐ๊ณผ

![์ฌ์ง](https://raw.githubusercontent.com/zoomKoding/zoomKoding.github.io/source/assets/_posts/topological-sort-4.png)

**์ด์ค ๋ฒกํฐ ์จ๋ ๊ฐ ๋ฒกํฐ๋ง๋ค ์ฌ์ด์ฆ๋ฅผ ๋ฌ๋ฆฌํ  ์ ์๋ค. ๊ทธ๋ ๋ค๋ฉด ํ์คํ ๋ฐ๋ก ๋งํฌ๋ ๋ฆฌ์คํธ ์ฐ๋ ๊ฒ๋ณด๋ค ๊ทธ๋ฅ ๋ฒกํฐ๋ฅผ ์ฐ๋ ๊ฒ ์ข๋ค!!**

## ๋๋์ 

- ์ ๋ฆฌํ๊ธฐ ์ ๊น์ง ์ ์์์ ๋ ฌ์ด ์ผ์ ์์๋ฅผ ์ ํด์ฃผ๋ ์ค ๋ชฐ๋๋ค.
- ์์์ ๋ ฌ์ ์์กด์ฑ์ด ์๋ ์ผ๋ถํฐ ์์ํด์ ์์กด์ฑ์ด ๋ฎ์ ์ ๋ค๋ถํฐ ํ๋์ฉ ์ฒ๋ฆฌํด๊ฐ๋ ์๊ณ ๋ฆฌ์ฆ์ด๋ค.
- ๋์ค์ ๋ถ๋ชํ ์ฐ์ผ ์ผ์ด ์์ํ๋ฐ ๊ณต๋ถํ  ์ ์๊ฒ ๋์ ์ข์๋ค ใใ
- ์์์ ๋ ฌ ๋ชจ๋ฅด๋ฉด ๋ชปํ ๋ฌธ์ ๋ค์ด ์์๊ฑฐ ๊ฐ๋ค. ์ด์ ๋ ๋ฌด์์ ํ์ง ๋ง๊ณ  ๋ฌ๋ ค๋ณด์ ใใ
