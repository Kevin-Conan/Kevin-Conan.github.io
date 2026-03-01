---
title: hash
date: 2026-03-01 14:28:07
categories:
    - 学习
    - 算法
tags:
mathjax: true  <-- 加上这一行
---

## 普通Hash：

使用C++内置的 Map 以及 UnorderedMap类来实现Hash映射

### 应用场景：
- 快速查找数列中是否出现某数字

## 字符串Hash

先可以看我2020年写的cpp代码

```cpp
#include<bits/stdc++.h>
using namespace std;
inline int read(){
	int s=0,w=1;
	char ch=getchar();
	while(ch<'0'||ch>'9'){
		if(ch=='-')w=-1;
		ch=getchar();
	}
	while(ch>='0'&&ch<='9'){
		s=(s<<1)+(s<<3)+(ch^48);
		ch=getchar();
	}
	return s*w;
}
typedef unsigned long long ULL;
const int P=131;
ULL h[1000005];
char str[1000005];
int ans;
int main(){
	int n=read();
	for(int i=1;i<=n;i++){
		scanf("%s",str+1);
		int len=strlen(str+1);
		for(int j=1;j<=len;j++){
			h[i]=h[i]*P+str[j];
		}
	}
	sort(h+1,h+1+n);
	for(int i=1;i<=n;i++){
		if(h[i]!=h[i-1]){
			++ans;
		}
	}
	cout<<ans;
	return 0;
}
```

有两个关键点：
- 使用unsigned long long来做自然溢出实现mod；
- 取模数一般P取131 或者 13331

核心计算公式就是

$$
H(s)=\sum_{i} H(s)*P^{len-i}+s[i]
$$

字符串hash的主要作用在于可以使得容易判断这个字符串是否出现过

- 替代方案：直接使用`map<string,bool>`应该也是可行的