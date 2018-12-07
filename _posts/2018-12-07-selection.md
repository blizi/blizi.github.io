---
layout: post
title: "校内选拔赛"
date: 2018-12-07 09:40:06 
description: "蓝桥 校内题"
tag: c
---



**1.输入一个自然数n，求小于等于n的素数之和**

 	遍历一遍





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

​	遍历

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

​	

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
        if(str[i]>='0'&&str[i]<='9'){
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

​	

针对每一次排列：

- ​	当还鞋的人数少于借鞋的人数时，无法满足，返回0
- ​	当借鞋的人数为0时，只有一种排法。
- ​	从m+n个人中，出来一个人放在第一个位置，对剩下m+n-1个人进行排队。
- ​	当出来的人为 借鞋的的时候``f(m,n-1)``
- ​	为还鞋的的时候 ``f(m-1,n)``
- ​	所以m+n个人的排法为``f(m-1,n)+f(m,n-1)``.

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
    int arr[x][x]={0};
    for(int i=1;i<x;++i)
    {
        arr[i][0]=1;
        for(int j=1;j<=i;++j)
        {
            arr[i][j]=arr[i-1][j]+arr[i][j-1];
        }
    }
    int n,m;
    scanf("%d%d",&n,&m);
    printf("%d",arr[n][m]);
    return 0;
}
```

7.**李白喝酒**（题目太长...）

深度搜索....用递归。

- ​	分两种情况：遇到花或者遇到店。 
- ​	当遇到花的次数和遇到店的次数都满足题意时且酒也满足题意，结束递归，计数加一。
- ​	在酒不足或者遇到店和花的次数不满足题意时 return。（递归结束条件）

```c
#include <stdio.h>
int count=0;
void judge(int a ,int b , int w){
	if(a==0&&b==1){  //店为0 花为1（最后一次遇到花）
		if(w==1){     //酒为1
			count++;   
		}
		return;     
	}
	if(a<0||b<0||w<0){ //不满足 return
		return;
	}
	judge(a-1,b,2*w);  //遇到店
	judge(a,b-1,w-1);  //遇到花
}
int main(){
	judge(5,10,2);
	printf("%d",count);
	return 0;
}

```

8.**学炒菜**

​	这道题就比较简单了（相比前两道题O(∩_∩)O），很好理解

​	从第一个菜开始依次过一遍，找到它所需要的材料，要是每一个材料都满足（>0），菜数加一，有一个材料	不满足则进行下一道菜的扫描



```c
#include<stdio.h>

int main () {
	int a,b,c,d;
	scanf("%d%d%d%d", &a, &b, &c, &d);
	int s = 0;
	switch(1){
		case 1:
			while(1){
				if(a >= 2 && b >= 1 && d >= 2){
					a -= 2;
					b -= 1;
					d -= 2;
					s ++;
				} else {
					printf("%d\n",s);
					s = 0;
					break;
				}
			}
		case 2:
			while(1){
				if(a >= 1 && b >= 1 && c >=1 && d >= 1){
					a -= 1;
					b -= 1;
					c -= 1;
					d -= 1;
					s ++;
				} else {
					printf("%d\n",s);
					s = 0;
					break;
				}
			}
		case 3:
			while(1){
				if(c >= 2 && d >= 1){
					c -= 2;
					d -= 1;
					s ++;
				} else {
					printf("%d\n",s);
					s = 0;
					break;
				}
			}
		case 4:
			while(1){
				if(b >= 3){
					b -= 3;
					s ++;
				} else {
					printf("%d\n",s);
					s = 0;
					break;
				}
			}
		case 5:
			while(1){
				if(a >= 1 && d >= 1){
					a -= 1;
					d -= 1;
					s ++;
				} else {
					printf("%d\n",s);
					s = 0;
					break;
				}
			}
	}
	return 0;
}
```

​	**其实**



<p/>

</p>



最后一道题，的c代码，复制，的。。。。。

由于一开始是用java写的，加之这道题也很友好，就。懒得。嗯，就这样了哈(主要还是c的的水平太低了O(∩_∩)O)。

贴一下我用java写的：

```java
import java.util.Scanner;

public class Test {
	public static void main(String[] args) {
		
		String[]str = {"aabdd","abcd","ccd","bbb","ad"};
		int[]result = new int[5];
		int[]arr = new int[4];
		Scanner sc = new Scanner(System.in);
		for(int i=0;i<4;i++) {
			arr[i] = sc.nextInt();
		}
		
		for(int i =0;i<str.length;i++) {
			char[] ch = str[i].toCharArray();
			arr = judge(ch,arr);
			if(judge(arr)) {
				result[i]++;
			}
			else {
				arr = plus(ch,arr);
			}
		}
		for(int i =0;i<result.length;i++) {
			System.out.println(result[i]);
		}
		sc.close();
	}
	
	static int[] judge(char[]ch,int[]arr) {
		for(int i =0;i<ch.length;i++) {
			if(ch[i]=='a') {
				arr[0]--;
			}
			if(ch[i]=='b') {
				arr[1]--;
			}
			if(ch[i]=='c') {
				arr[2]--;
			}
			if(ch[i]=='d') {
				arr[3]--;
			}
		}
		return arr;
	}
	static int[] plus(char[]ch,int[]arr) {
		for(int i =0;i<ch.length;i++) {
			if(ch[i]=='a') {
				arr[0]++;
			}
			if(ch[i]=='b') {
				arr[1]++;
			}
			if(ch[i]=='c') {
				arr[2]++;
			}
			if(ch[i]=='d') {
				arr[3]++;
			}
		}
		return arr;
	}
	static boolean judge(int[]arr) {
		for(int i=0;i<arr.length;i++) {
			if(arr[i]<0) {
				return false;
			}
		}
		return true;
	}

}
```

- 

- 

- 
- 

- 

======================================分割线============================================

- 

- 

- 

- 

- 



​	最难的题的头衔颁给第六道！！ 后三到题还是有难度的，但是能做出前五道题的你们都是最胖的！。

#**结束！**





<br>

转载请注明：[blizi的博客](www.blizi.club) » 