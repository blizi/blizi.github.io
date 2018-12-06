---
layout: post
title: "校内选拔赛"
date: 2018-12-06 18:40:06 
description: "蓝桥 校内题"
tag: java
---



**1.输入一个自然数n，求小于等于n的素数之和**

 	遍历一遍....

```c
#include <stdio.h>
int judge(int);
int main(void) {
	int n,i,count = 3;
	scanf("%d",&n);
	if(n==1){
		printf("1");
	}
	else if(n==2){
		printf("3");
	}else{
		for(i = 3;i<=n;i++){
			if(judge(i)){
				count+=i;
			}
		}
		printf("%d",count);
	}
	return 0;
}
//判断是否为素数
int judge(int n){
	int i;
	for(i = 2;i<n;i++){
		if(n%i==0){
			break;
		}
	}
	if(i==n){
		return 1;
	}
	return 0;
}
```

**2.从小到大输出所有满足每一位的立方和等于自己的十进制三位数（一行一个）**

​	遍历......

```c
#include <stdio.h>
int main(){
	int i,a,b,c;
	for(i =100;i<999;i++){
		a = i%10;
		b = (i/10)%10;
		c = i/100;
		if(a*a*a+b*b*b+c*c*c==i){
			printf("%d\n",i);
		}
	}
	return 0;
}
```

**3.寻找数组中的最大值（限制了用数组做  那还能用啥 hhhaO(∩_∩)O ）**

**第一行输入n，然后输入n个数字。**

**输出：第一行输出输入的n个数字，第二行输出n个数字中的最大值**

​	......

```c
#include <stdio.h>
int main(){
	int i,n,a[10000],max=0;
	scanf("%d",&n);
	for(i=0;i<n;i++){
		scanf("%d",&a[i]);
		printf("%d ",a[i]);
		if(a[i]>max){
			max = a[i];
		}
	}
	printf("\n%d",max);
	return 0;
}
```

**4.输入一个字符串（长度100以内），统计其中数字字符出现的次数。**

```c
#include <stdio.h>
int main() {
	char str[100];			//100的字符串
	int i = 0,count=0;
	scanf("%s",str);
	while(str[i]){			//到字符串尾时结束
        if(str[i]>'0'&&str[i]<='9'){
            count++;
        }
        i++;
	}
	printf("%d",count);
}
```

**5.输出一个3行4列中绝对值最大的数并换行输出其所在的行和列。（注意绝对值最大的数为负数时的输出也为负数）**

​	这题和上面那个找最大值大同小异。需要注意的是如果你是把负数换位正数比较的话，输出时记得输出原有的数字。

```c
#include <stdio.h>
int main(){
	int i,j,max=0,a,b,c=0; //a，b存所在位置的下标（输出时记得加1）
	int arr[3][4];
	for(i=0;i<3;i++){
		for(j =0;j<4;j++){
			scanf("%d",&arr[i][j]);
			if(arr[i][j]<0){
				arr[i][j]=0-arr[i][j];
				c = 1;
				if(arr[i][j]>max){
					max = arr[i][j];
					a = i;
					b =j;
					c = 1;       //用c来表示取绝对值前是否为负数
				}
			}
			else{
				if(arr[i][j]>max){
					max = arr[i][j];
					a = i;
					b =j;
					c = 0;
				}
			}

		}
	}
	if(c == 1){               //为负数。
		printf("%d\n",-max);
	}else{
		printf("%d\n",max);
	}
	printf("%d %d",a+1,b+1);  //下标加1后输出
	return 0;
}

```

6.**有m个还鞋的，n个借鞋的（排成一队），要保证每次借鞋的都有鞋可借，**

**输入m，n分别表示还鞋和借鞋的，输出所有可以满足的排队个数。（两个还鞋的的位置不加以区别）**

​	以前做过的题，当时百度到答案也看不懂...

递归实现：

```c
#include <stdio.h>
int judge(int m ,int n){
	if(n==0){
		return 1;
	}
	if(m<n||m==0){
		return 0;
	}
	return judge(m-1,n)+judge(m,n-1);
}
int main(){
	int m,n;
	scanf("%d%d",&m,&n);
	printf("%d",judge(m,n));
	return 0;
}
```

另一种写法

```c
#include<stdio.h>
#define x 18
int main()
{
    int dp[x][x]={0};
    for(int i=1;i<x;++i)
    {
        dp[i][0]=1;
        for(int j=1;j<=i;++j)
        {
            dp[i][j]=dp[i-1][j]+dp[i][j-1];
        }
    }
    int n,m;
    scanf("%d%d",&n,&m);
    printf("%d",dp[n][m]);

    return 0;
}
```





​	

<br>

转载请注明：[blizi的博客](http://blizi.github.io) » 