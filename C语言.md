# 库

```c
#include<stdio.h>

#include<stdlib.h>
	rand//产生随机数
    malloc//动态内存分配(int*)malloc(n*sizeof(int))
    free//释放内存
    atoi(char*)//将字符串转化为整形

#include<cstdlib>
    itoa(int num,char*location,int jinzhi)//将整形化为字符型

#include<time.h>
	srand(time(NULL));//为随机数设置种子

#include<math.h>

#include<ctype.h>
//使用字符处理函数
	isalpha,isdigit

#include<string.h>
//使用字符串处理函数
    stcpy//赋值,
    strcmp//比较
    strcat//连接
    strlen//长度

#include<stdbool.h>
    bool,true,false//真为一
```

# 附录

## 库函数

![image-20231116143416822](TY/img/image-20230908152633323.png)

fabs小数绝对值

abs整数绝对值

## 字符处理函数

![image-20231008211217496](TY/img/image-20231008211217496.png)



## 字符串处理函数

![image-20231018115004658](TY/img/image-20231018115004658.png)

![image-20231018115019745](TY/img/image-20231018115019745.png)



# 基本数据类型

## 补码与反码

### 无符号整数

最高位为数据位

### 有符号整数

最高位为符号位

假设Int为一个字节

-1：10 00 00 01

反码：11 11 11 10

补码=反码+1：11 11 11 11

但-128表示为-127-1，其补码为10 00…… 00 00

127：01 11…… 11 11



## 内存

### 位bit

0或1

### 字节byte

8bit 可表示0到255

## 单位

![image-20230906111509629](TY/img/image-20230906111509629.png)

### 地址

八位16进制00000001到FFFFFFFF

前1024个字节为启动程序，256个中断服务程序

32位计算机的内存地址编码是32位，从0x00000000到0xFFFFFFFF

<img src="TY/img/image-20230902212749335.png" alt="image-20230902212749335" style="zoom:50%;" />

如定义Int计算机分配4个字节

（在codeblock中longint也占4个字节）

## 数据类型

![image-20230906105018512](TY/img/image-20230906105018512.png)

### 变量长度

![image-20230906111731342](TY/img/image-20230906111731342.png)

#### 浮点数：

float范围：-3.4到3.4

一般用double

a=5.5——101.1存储为.0 00 00 00….10 11*2^10^

​               b=5.7——101.1110101…….无法精确描述

​              故用%f读一个整形变量2，读数为0，因为2被存为00 00 00 …10

#### 字符型：

a=’5‘
a=’53‘错   a=“5”错

#### 字符串：

“sum”

### 如何给变量赋值

不能连续赋值如int a=b=0；
但可以int b；
int a=b=0；

int a=5;if(a=0.5)结果为false
因为a是int

### 变量的储存类型

- auto自动变量，一般变量自动储存为自动变量
- static静态变量
- extern外部变量，编译器不为其分配内存
- register寄存器变量

## 常见符号

### 关键字（保留字）

CB里变蓝的：int return 

## 标识符

CB 里变红的

系统预定义：printf,scanf,main

用户自定义

## 宏常量与宏运算

宏定义：

`#define PI 3.14159`
#define 标识符 字符串（不加冒号，分号）
标识符：宏名，一般用全大写表示

## 自动类型转换与强制类型转换

`int x=10;`

`float y;`

`y=(float)x;`
`//y=10.000000`

## exit

exit（0）：正常运行程序并退出程序；

exit（1）：非正常运行导致退出程序；

return（）：返回函数，若在主函数中，则会退出函数并返回一值。

# 运算

% 符号与被除数相同

## scanf用法

![image-20230913105218427](TY/img/image-20230913105218427.png)

![image-20230919194948426](TY/img/image-20230919194948426.png)

![image-20230913105245506](TY/img/image-20230913105245506.png)

输入short %hd

输入long long %I64d

![image-20230913105314435](TY/img/image-20230913105314435.png)

```c
scanf("%d%*c%d",&a,&b);
//输入1 2
//1*2等都读入1 2
```

## rand用法

rand():产生[0，RAND_MAX]间的随机数

RAND_MAX在#include<stdlib>中定义，不大于32767

产生[0,b-1]间的随机数
`MAGIC=rand()%b;`

产生[a,a+b-1]之间的随机数
`MAGIC=rand()%b+a;`



```c++
#include<stdlib>
#include<stdio.h>
#include<time.h>
srand(time(NULL));//调取现在时间生成随机数
int magic=rand()%100+1;//生成一个1到100的随机数

```

### 随机函数srand()

为rand（）设置随机数种子使随机数随机化

scanf(“%u”,&seed);

srand(seed);

magic=rand()%100+1;

```c++
for(i=1;i<10;i++)
{
    srand(i);
    for(j=0;j<5；j++)
    {
        printf("%d\t",rand());
    }
}
```

## 检验非法输入

**scanf的返回值是以成功读入数据的项数**，非法字符的输入会导致无法读入

### 函数fflush() 清除缓冲区中错误数据

`fflush(stdin);`清除缓冲区中错误数据

或者`while(getchar()!=‘\n’);``while(getchar()!=‘\0’);`等

### 用getchar()

![image-20230925152240077](TY/img/image-20230925152240077.png)

# 调试

![image-20231008141716921](TY/img/image-20231008141716921.png)

![image-20231008141743434](TY/img/image-20231008141743434.png)![image-20231008141806037](TY/img/image-20231008141806037.png)

# 一，循环

```c++
int price = 0;

	printf("请输入：");//提示输入
	scanf("%d", &price);  //读取

	int change = 100 - price;

	printf("%d", change);
	return 0;
```



 

## **if语句**

```c++
#include<studio.h>
int a, b;
	printf("请输入两个整数");
	scanf_s("%d,%d", &a, &b);

	int max = 0;
	if (a < b) {
		max = a;
	}if (b > a) {
		max = b;
	}
```



## **Switch-case语句：多路分支**

```c++
	#include<studio.h>
    int type;

	scanf_s("%d", &type);

​	switch (type)

​	{

​	case 1:

​		printf("你好\n");

​		break;

​	case 2:

​		printf("晚上好\n");

​		break;

​	default://不符合任意情况

​		printf("中午好\n");

​		break;

}
```





 

## **while循环**

```c++
 //计算数的位数
	int x;
	int n = 0;

	scanf_s("%d", &x);
	n++;
	x /= 10;
	while (x > 0) {
		n++;
		x /= 10;
	}
	printf("%d\n", n);

	
	return 0;
```



 

## **Do while循环**

```c++
 //计算数的位数
	int x;
	int n = 0;

	scanf_s("%d", &x);
	n++;
	x /= 10;
	while (x > 0) {
		n++;
		x /= 10;
	}
	printf("%d\n", n);

	
	return 0;
```



### **猜数游戏**

```c++
#include <stdio.h>
#include<stdlib.h>
#include<time.h>
int main()
{  
	srand(time(0));//使产生的数像随机数
	int number = rand()%100+1;//产生100以内随机数
	int count = 0;
	int a;
	printf("我已经想好了一个1到100之间的数。");
		do {
			printf("请猜猜这个数：");
			scanf_s("%d", &a);
			count++;
			if (a > number) {
				printf("你猜的数大了,");

			}
			else if (a < number) {
				printf("你猜的数小了,");
				}
			} while (a != number);
			printf("你用了%d次.\n", count);
```



### **算平均数**

```c++
int number;
	int count = 0;
	int sum = 0;

	do {
		scanf_s("%d", &number);
		if (number != -1) {
			count++;
			sum += number;
		}
	} while (number != -1);//读到-1时结束
	printf("%f\n", 1.0 * sum / count);
	return 0;

```



### **整数求逆**

```c++
int x;
    scanf_s("%d", &x);
	
	int digit;
	int ret = 0;

	while (x > 0) {
		digit = x % 10;
		printf("%d", digit);
		ret = ret * 10 + digit;
		x /=10;
	}
```



## **for循环**

```c++
int n, x=1;
	int y=1;
	scanf_s("%d", &n);
	for (x = 1; x <= n; x++) {//初始值；循环条件；操作
		y *= x;
	}
	printf("%d", y);

```



**有固定次数：for**

*1.判断初始值*，若不满足条件则不进入循环

*2.进入循环*

*3.进行操作*

*4.判断循环条件*

**必须执行一次：do while**

**其他：while**

 

### **判断素数**

```c++
	int x;

	scanf_s("%d", &x);

	int i;
	int isPrime = 1;//x是素数；
	for (i = 2; i < x; i++) {
		if (x % i == 0) {
			isPrime = 0;
			break;//离开循环
			//continue:结束该循环到下一轮循环
		}
	}
	if (isPrime == 1) {
		printf("是素数\n");
	}
	else {
		printf("不是素数\n");
	}

int x;

	for(x=2;x<100;x++)

	{
		int i;
		int isPrime = 1;//x是素数；
		for (i = 2; i < x; i++) {
			if (x % i == 0) {
				isPrime = 0;
				break;//离开循环
				//continue:结束该循环到下一轮循环
			}
		}
		if (isPrime == 1) {
			printf("%d ",x);
		}
		
	}printf("\n");
```



### **前50个素数**

```c++
int x=2;
	int cnt = 0;
	while (cnt < 50)

	{
		int i;
		int isPrime = 1;//x是素数；
		for (i = 2; i < x; i++) {
			if (x % i == 0) {
				isPrime = 0;
				break;//离开循环
				//continue:结束该循环到下一轮循环
			}
		}if (isPrime == 1) {
			printf("%d ", x);
			cnt ++;
		}
		x++;

	}printf("\n");
```



### **凑钱**

```c++
	int x;
	scanf_s("%d", &x);
	int a, b, c;
	for (a = 1; a < x * 10; a++) {
		for (b = 1; b * 2 < x * 10; b++) {
			for (c = 1; c * 5 < x * 10; c++) {
				if (a + b * 2 + c * 5 == x * 10) {
					printf("可以用%d个1角加%d个2角加%d个5角得到%d元\n", a, b, c, x);
				}
			}
		}
	}
```



### **接力break**

```c++
	int x;
	int exit = 0;
	scanf_s("%d", &x);
	int a, b, c;
	for (a = 1; a < x * 10; a++) {
		for (b = 1; b * 2 < x * 10; b++) {
			for (c = 1; c * 5 < x * 10; c++) {
				if (a + b * 2 + c * 5 == x * 10) {
					printf("可以用%d个1角加%d个2角加%d个5角得到%d元\n", a, b, c, x);
					exit = 1;
					break;
				}
			}if (exit)break;
		}if (exit)break;
	}
```



## **Goto**

```c++
	int x;
	int exit = 0;
	scanf_s("%d", &x);
	int a, b, c;
	for (a = 1; a < x * 10; a++) {
		for (b = 1; b * 2 < x * 10; b++) {
			for (c = 1; c * 5 < x * 10; c++) {
				if (a + b * 2 + c * 5 == x * 10) {
					printf("可以用%d个1角加%d个2角加%d个5角得到%d元\n", a, b, c, x);
					exit = 1;
					goto out;//直接跳到out
				}
			}
		}
	}
out:	
```

## 练习

### **正序输出**

```c++
	int x;
	scanf_s("%d", &x);
	int mask = 1;
	int t = x;
	while (t > 9) {
		mask *= 10;
		t /= 10;
	}
	do {
		int d = x / mask;
		printf("%d",d);
		if (mask > 9) {
			printf(" ");

		}x %= mask;
		mask /= 10;
	} while (mask > 0);
	printf("\n");
```



 

### **辗转相除法**

```c++
	int a, b,t;
	scanf_s("%d,%d", &a, &b);
	while (b != 0) {
		t = a % b;
		a = b;
		b = t;
	}
	printf("gcd=%d\n", a);
```



 

### **输出数阵**

```c++
	int a;
	scanf_s("%d", &a);
	int i, j, k;
	int cnt = 0;

	i = a;
	while (i <= a + 3) {
		j = a;
		while (j <= a + 3) {
			k = a;
			while (k <= a + 3) {
				if (i != j) {
					if (i != k) {
						cnt++;
						printf("%d%d%d", i, j, k);
						if (cnt == 6) {
							printf("\n");
							cnt = 0;

						}
						else {
							printf(" ");
						}

					}
				}
				k++;
			}
			j++;
		}
		i++;
	}
```



### **水仙花数**

```c++
	int n;
	scanf_s("%d", & n);
	int a = 1,b=1;
	while (b < n) {
		a *= 10;
		b++;
	}
	b = a;
	while (b < a * 10) {
		int t = b;
		int sum = 0;
		do{
			int d = t%10;
			t /= 10;

			int p = d;
			int j = 1;
			while (j < n) {
				p *= d;
				j++;
			}
			sum += p;
		} while (t > 0);
		if (sum == b) {
			printf("%d\n", b);
		}
		b++;
	}
```



### **打印九九乘法表**

```c++
	int a = 1;
	int b;
	scanf_s("%d", &b);
	while (a <= b) {
		int c = 1;
		while (c <= a) {
			printf("%d*%d=%d", c, a, a * c);
			if (a*c<10) {
				printf("   ");
			}
			else {
				printf("  ");
			}
			
			c++;
		}
		printf("\n");
		a++;
	}
```



### **统计素数求和（存疑）**

```c++
	int m, n;
	scanf_s("%d %d", &m, &n);
	if (m == 1)
		m = 2;
	int i=m, j, k=1;
	int cnt=0, sum=0;
	for (i = m; i <=n; i++) {
		for (j = 2; j < i; j++) {
			if (i%j == 0) {
				k = 0;
				break;
			}
		}
		if (k) {
			cnt++;
			sum += i;
		}
	}
	printf("%d %d", cnt, sum);
```



 

### **猜数游戏6.1.5(存疑）**

```c++
	int number, n, inp, finished = 0, cnt = 0;
	scanf_s("%d", &number, &n);
	do {
		scanf_s("%d" ,&inp);
		cnt++;
		if (inp < 0) {
			printf("Game over\n");
			finished = 1;
		}else if (inp > number) {
			printf("To big\n");
		}else if (inp < number) {
			printf("To small\n");
		}else {
			if (cnt == 1) {
				printf("Bingo\n");
			}else if (cnt <= 3) {
				printf("Lucky you\n");
			}else {
				printf("Good guess\n");
			}
			finished = 1;

		}
		if (cnt == n) {
			if (!finished) {
				printf("Game over\n");
				finished = 1;
			}
		}
	} while (!finished);
```



 

### **最简分数**

```c++
	int a, b;
	scanf_s("%d/%d", &a, &b);
	int t;
	int c = a, d = b;
	while (d > 0) {
		t = c  d;
		c = d;
		d = t;
	}
	printf("%d/%d\n", a/c, b/c);
```



### 5-2读数



``` c++
#include<stdio.h>

int main()
{
	int mask = 1;
	int x;
	scanf_s("%d", &x);

	if (x < 0) {
		printf("fu");
			x = -x;//将负化正
	}
	int t = x;
	
	while (t > 9) {
		t /= 10;
		mask *= 10;//计算位数
	}
	do {
		int d = x / mask;
		switch (d) {
		case 0:printf("ling"); break;
		case 1:printf("yi"); break;
		case 2:printf("er"); break;
		case 3:printf("san"); break;
		case 4:printf("si"); break;
		case 5:printf("wu"); break;
		case 6:printf("liu"); break;
		case 7:printf("qi"); break;
		case 8:printf("ba"); break;
		case 9:printf("jiu"); break;
		}
		if (mask > 9)printf(" ");
		x %= mask;
		mask /= 10;
	} while (mask > 0);
	printf("\n");
	
	return 0;
}
```

### 5-3求a的连续和

 ``` c++
 #include<stdio.h>
 
 int main()
 {
 	int a, n;
 	int s = 0;
 	int t = 0;
 	scanf_s("%d %d", &a, &n);
 	for (n; n > 0; n-- ) {
 		s = a * n;
 		a *= 10;
 		t += s;
 	
 	}
 	printf("%d", t);
 
 	
 	return 0;
        
     
 ```



# 二，函数

### 1.求和函数



```c++
#include<stdio.h>

void sum(int begin, int end) {//定义函数
	int i;
	int sum = 0;
	for (i = begin; i <= end; i++) {
		sum += i;
	}
	printf("%d和%d的和为%d\n",begin, end, sum);
}
int main()
{
	sum(1, 10);
	sum(20, 30);
	sum(35, 45);
	return 0;
}
```

### 2.从函数中返回

void无返回值 
int有return，带值

### 3.函数声明

```c++
#include<stdio.h>

void sum(int begin, int end);//函数原型声明：函数名，类型，可以不用参数名称
int main()
{
	sum(1, 10);
	sum(20, 30);
	sum(35, 45);
	return 0;
}
void sum(int begin, int end) {//定义函数
	int i;
	int sum = 0;
	for (i = begin; i <= end; i++) {
		sum += i;
	}
	printf("%d和%d的和为%d\n",begin, end, sum);
}
```

1.调用最好不要使用void swap(),数据类型可能与实际不符(默认int);

2.无参数，使用void swap(void).

### 4.布尔值

true:1  false:0

### 5.条件操作符

int max = a>b ? a : b;     问号后：正确取冒号前；错误取后      

### 6.输入

只有int ,long long

**%d:int**

**%u:unsigned**

**%ld:long long(c是%I64d)**

**%lu:unsigned long long**

**%hd:short**

### 7.字符类型

char 整数，字符
用单引号‘a’
“也是一个字符
**用%c输入输出**

### 8.**逃逸字符**

**\b 回退一格**

**\t到下一个表格位**

**\n换行**

**\r回车**

**\\"双引号**

### 9.自动类型转换

printf:小于int变为int，float变为double

scanf不会，要输入short,需要%hd

### 10.bool用来判断真假命题

`#include<stdbool.h>`
之后可以使用bool,true,false
真为1

### 11.逻辑运算

!非   1变为0，0变为1

&&与    x>4&&x<6   x属于4到6

||或   一边为true即为true

### 12.逗号表达式

1.即逗号后面的表达式为结果

2.用于for循环

3.优先级低于=

> 题目：以下程序的输出结果是：
> main()
> {
> int x,y,z;
> x=1;
> y=1;
> z=x++,y++,++y;
> printf(“%d,%d,%d\n”,x,y,z);
> }
> [A]2，3，3 [B]2，3，2 [C]2，3，1 [D]1，1，1
> 解析：
> x和y的值经过自增以后分别为2和3，D可以排除。剩下3个选项选择什么呢？
> 如果是（x++,y++,++y）实际上可以看成（1,1,3）整个逗号表达式的值应该是3，那么选A。
> 如果是（x++,++y,y++）实际上可以看成（1,2,2）整个逗号表达式的值应该是2，那么选B。
> 但这是错的，这儿还有赋值运算符。赋值运算符的优先级是14，而逗号表达式的优先级是15，也就是说上面的表达式中应该等价于这样的结合：(z=x++),y++,++y;如果这样写的话，则答案很清晰，为：2，3，1
> 正确答案选C。

### 13.自加与自减

a++:先输出a，再把a加一

++a：先把a加一，再输出加后a

### 14.运算优先级

[c++运算符优先级归纳_赵民勇的博客-CSDN博客](https://blog.csdn.net/zhaominyong/article/details/126268983)

### 15.格式化输入与输出

**%d      int             有符号10进制整数**
**%u      unsigned int    无符号10进制整数**
**%h      短型前缀，后接d(10进制整形)、x(16进制整形)、o(8进制整形)**
%hd     short           有符号10进制短整形
%hu     unsigned short  无符号10进制短整形
%ld     long            
%lu     unsigned long   
%lld    long long
%llu    unsigned long long   
        
        
%o                      有符号8进制整数
%x 　　                 无符号的16进制数字，并以小写abcdef表示
%X 　                   无符号的16进制数字，并以大写ABCDEF表示
**%f　　                  输入输出为浮点型 （%lf双精度浮点型）**
**%c                      输入输出为单个字符** 
**%s                      输入输出为字符串**

### 16.大小写字母转换

大、小写字母都是按顺序进行存储的，大写字母的ASCII值区间为：65//90，对应的字母为：'A'-'Z'；小写字母的ASCII值区间为：97//122，并应的字母为：'a'-'z'，因此，将小写字母转差谨化为大写字母，可以**直接将该变量减32即可得到对应的大写字母**，如：
`char ch='a';`
`printf("upper case '%c'='%c'\n", ch, ch-32 );`
如果记不清，大小字母谁大谁小，则可以采用如下方法进行转换：
``char ch='x';`
`printf("upper case '%c'='%c'\n", ch, ch-'a'+'A' );`` //减a得到偏移值，加A得到相应的大写字母

### 17.浮点数

(double)(10/4*4)=8.0

(double)10/4*4=10.0

它是先将整数10转为double，成为10.0，然后再除以整数4；C系统会自动将4转为4.0再相除，得到2.5，再与4.0相乘，最后得到10.0。

### 18.变量定义类型

<img src="TY/img/image-20230902212611364.png" alt="image-20230902212611364" style="zoom:50%;" />

static int 不管在函数内还是函数外，都作为一个全局变量可以保存它被修改以后的值。

而 int 则没有这一功能，只有作为全局变量时能保存修改。放在函数内部时，每次调用都用的是一个新的数。

### 19，使用内存的情况

<img src="TY/img/image-20230902212749335.png" alt="image-20230902212749335" style="zoom:50%;" />

# 三，数组

## 1.初试数组

```c++
#include<stdio.h>

int main(){
	int x;
	double sum = 0;
	int cnt = 0;
	int num[100];//定义数组
	scanf_s("%d", &x);
	while (x != -1) {
        num[cnt]=x;//对数组中元素赋值
		sum += x;
		cnt++;
		scanf_s("%d", x);
	}
	if (cnt > 0) {
		printf("%f\n", sum / cnt);
		int i;
		for (i = 0; i < cnt; i++) {
			if (num[i] > sum / cnt) {
				printf("%d\n", num[i]);//遍历数组
			}
		}
	}
	return 0;
}
```

下标：从0开始到个数减一

如 int a[10];

a[9]=0;//赋值

## 2.数组运算

int a[10]={1,2,2,4}

未赋值时为随机数；任意赋值后其余为0

或int a[]={[1]=2,4,[4]=3}//{0,2,4,0,4}

### 计算0-9数字的个数

```c++
#include<stdio.h>

int main(){
	const int number = 10;//const不可变常量
	int i, x;
	int count[number];//数组内不可键入变量
	for (i = 0; i < number; i++) {
		count[i] = 0;//初始化，也可以count[0]=0;默认全为0
	}
	scanf_s("%d", &x);
	while (x != -1) {
		if (x >= 0 && x <= 9) {
			count[x]++;
		}
		scanf_s("%d", & x);
	}
	for (i = 0; i < number; i++) {
		printf("%d:%d\n", i, count[i]);
	}
	return 0;
}
```

### 找出key在数组中的位置

```c++
#include<stdio.h>
int search(int key, int a[], int length) {//数组做参数要再定义一个参数来传入数组大小
	int t = -1;
	int i = 0;
	for (i; i < length ; i++) {
		if (a[i] == key) {
			t = i;
			break;
		}
	}
	return t;
}
int main(){
	int a[] = { 2,4,6,7,1,3,5,9,11,13,23,14,32 };
	int x;
	int loc;
	printf("请输入一个数字:");
	scanf_s("%d", &x);
	loc = search(x, a, sizeof(a) / sizeof(a[0]));//目标数，数组，数组长度
	if (loc != -1){
		printf("%d在%d的位置上", x, loc);

	}
	else {
		printf("不存在\n");
	}
	return 0;
}
```

## 3.寻找素数

### 从一到根号x

### 素数表

```c++
#include<stdio.h>
int isprime(int x, int knownprimes[], int count) {
	int i;
	int ret = 1;
	for (i = 0; i < count; i++) {
		if (x % knownprimes[i] == 0) {
			ret = 0;
			break;
		}
	}
	return ret;
}
int main(void){
	const int number = 100;
	int prime[number] = { 2 };
	int count = 1;
	int i = 3;
	for (count; count < number; count++) {
		if (isprime(i, prime, count)) {
			prime[count++] = i;
		}
		i++;
	}
	for (i = 0; i < number; i++) {
		printf("%d", prime[i]);
		if ((i + 1) % 5) {
			printf("\t");
		}
		else {
			printf("\n");
		}
	}
	return 0;
}
```

### 构造素数表:标记非素数

素数的倍数不是素数

```c++
#include<stdio.h>

int main(void){
	const int max = 25;
	int prime[max];
	int i;
	for (i = 0; i < max; i++) {
		prime[i] = 1;

	}
	int x = 2;
	for (x = 2;  x < max; x++) {
		if (prime[x]) {
			for (i = 2; i *x< max; i++) {
				prime[i * x] = 0;
			}
		}
	}
	for (i = 2; i < max; i++) {
		if (prime[i]) {
			printf("%d\t", i);
		}
	}
	return 0;
}
```

### 二维数组

```c++
#include<stdio.h>
//-1都没赢；0 o赢了；1 x赢了

int main(void){
	const int size = 3;
	int broad[size][size];
	int i, j, X, O;
	int result = -1;
	for (i = 0; i < size; i++) {
		for (j = 0; j < size; j++) {
			scanf_s("%d", &broad[i][j]);
		}
	}
    //检查横行
	for (i = 0; i < size; i++) {
		X, O = 0;
		for (j = 0; j < size; j++) {
			if (broad[i][j] == 1) {
				X++;
			}
			else { O++; }
		}
		if (O == size) {
			result = 0;
		}
		else if(X==size){result = 1; 
		}
	return 0;
}
```

若定义全部元素，二维数组不能省略，一维数组可以省

## 4.初始化数组

### memset函数

```c
void *memset(void *str, int c, size_t n)
```



- 解释：复制字符 c（一个无符号字符）到参数 str 所指向的字符串的前 n 个字符。
- 作用：是在一段内存块中填充某个给定的值，它是对较大的结构体或数组进行清零操作的一种最快方法
- 头文件：C中`#include<string.h>`，C++中`#include<cstring>`

```c
#include<string.h>
int a[100];
memset(a,0,sizeof(a));
```

按字节赋值，只能最好赋值0



### memcpy函数

```c
memcpy(b,a,sizeof(a));
```



# 四，指针

## 1.&：取地址运算

## 2.指针

用来记录地址

*用来访问那个地址上的变量

如int k=*p

## 3.用途

### 用于交换变量

```c++
void swap(int* pa, int* pb)
{
	int t = *pa;
	*pa = *pb;
	*pb = t;
}
```



### 函数返回运算的状态，结果通过指针返回

易犯错误：定义指针变量，不指向任何变量

如 int *p;
*p=12;

```c++
#include<iostream>
void minmax(int a[], int len, int* min, int* max);
int main(void) {
	int a[] = { 54,87,87,545,12,25 };
	int min, max;
	minmax(a, sizeof(a) / sizeof(a[0]), &min, &max);
	printf("%d %d", min, max);
	return 0;
}
void minmax(int a[], int len, int* min, int* max)
{
	int i;
	*min = *max = a[0];
	for (i = 1; i < len; i++) {
		if (a[i] < *min) {
			*min = a[i];
		}
		if (a[i] > *max) {
			*max = a[i];
		}
	}
}
```



## 4.函数中的数组

函数头中“a[]”实际是指针

数组变量本身表达地址，所以 int a[10];int p=a;无需用&取地址

但数组单元是变量，要用&

a==&a[0],a这个地址就是a[0]

数组变量是常量指针（const）不能在被赋值

## 5.指针与const

### 所指是const

表示不能通过这个指针去修改那个变量（不能使那个变量成为const)

不能通过指针干坏事了

```c++
const int*p=&i;
*p=26;//ERROR(*是const)
i=26;//OK
p=&j//OK
```

`const int*p1=&i;`

`int const *p1=&i;//const在*前面，如上`

 `int*const p1=&i;//const在*后面，所指的对象不能被修改`

### const数组

const int a[]={1,2,3};

里面都是int

## 6.数组运算

给char数组地址加一，就是地址加一

给int数组地址加一，就是地址加四

### *p++

取出p所☞的数据，顺便把p移到下一个数去

### 0地址

NULL 用0地址表示特殊的事情：返回指针无效，指针没有被真正初始化，此时不能直接malloc

### void*p

暂不确定类型



## 7.动态内存分配

### malloc

#include<stdlib.h>

向malloc申请的空间是以字节为单位的

返回的结果是void*,需要类型转换为自己需要的类型

`(int*)malloc(n*sizeof(int))`

**申请后的空间要用free还**

```c++
#include<stdio.h>
#include<stdlib.h>
int main()
{
	int num;
	int* a;
	printf("输入数量");
	scanf("%d", &num);
	a = (int*)malloc(num * sizeof(int));
	for (int i = 0; i < num; i++) {
		scanf("&d", &a[i]);
	}
	for (int i = num - 1; i >= 0; i--) {
		printf("%d", a[i]);
	}
	free(a);
	return 0;
}

```

### calloc

`a=(int*)calloc(num,sizeof(int));`

与malloc不同：自动将内存初始化为0

### free()与realloc（）

![image-20231011202352130](TY/img/image-20231011202352130.png)

### 必须确保是非空指针

![image-20231011202708235](TY/img/image-20231011202708235.png)

## 8.指针与二维数组

### 行指针

![image-20231011195557956](TY/img/image-20231011195557956.png)

### 列指针

列数未知时应用动态内存分配

![image-20231011195659668](TY/img/image-20231011195659668.png)

![image-20231011195712850](TY/img/image-20231011195712850.png)

### 指针数组

#### 字符串排序

![image-20231011200127146](TY/img/image-20231011200127146.png)

![image-20231011200149306](TY/img/image-20231011200149306.png)

# 五，字符串

## 1.字符串

char word[]{‘H’,’e’,’l’,’l’,’o’,’\0’};

- 以0结尾的一串字符

- 0和‘\0’一样，与‘0’不同，标志字符串结束，但不是字符串一部分

- 计算长度不包含0

- 字符串以数组形式存在，以数组或指针的形式访问

- 更多以指针

- string.h中有很多处理字符串的函数
## 2.字符串常量

  char* s=“hello,world”;

- s是一个指针，初始化为一个字符串常量
- 不能修改
- 如果要修改应用char s[]=“hello,world”;

## 3.字符串输入输出

- char string[8];
- `scanf(“%s”,string);`
- `printf(“%s”,string);`
- scanf读入一个单词（到空格，tab或回车为止）
- 不能超出定义的数组范围，用`scanf(“%7s”,string);`
- 用`fgets(a,sizeof(a),stdin);`会把回车也读入，与原密码比较必不同
- 方法：将\n改为\0  `str[strlen(str)]=‘\0’;`

### 空字符串

char buffer[100]=“”;

buffer[0]==‘\0’长度只有1

## 4.整形与字符串的转换函数

[【C语言】 itoa()函数 和 atoi()函数（字符串与整型数的转换）_itoa函数-CSDN博客](https://blog.csdn.net/qq_44524918/article/details/114679985)

atoi()是C语言中的字符串转换成整型数的一个函数

（1）【头文件】#include <stdlib.h>

（2）【函数原型】int atoi (const char * str);

（3）【函数说明】atoi() 函数会扫描参数 str 字符串，跳过前面的空白字符（例如空格，tab缩进等），直到遇上数字或正负符号才开始做转换，而再遇到 非数字 或 字符串结束时(’\0’) 才结束转换，并将结果返回。函数返回转换后的整型数；如果 str 不能转换成 int 或者 str 为空字符串，那么将返回 0。

```c++
#include <iostream>
#include <cstdlib>
using namespace std;

int main(){
	const char *s = " 134";
	int num = atoi(s);
	cout << num; //输出：134 
	return 0;
}

```



二、itoa()函数
itoa()函数是C语言中的整型数转换成字符串的一个函数

（1）【头文件】#include <cstdlib>

（2）【函数原型】char *itoa(int value, char *string, int radix);

（3）【参数说明】
            value：要转换的数据。
            string：目标字符串的地址。
            radix：转换后的进制数，可以是10进制、16进制等，范围必须在 2-36。

```c++
#include <iostream>
#include <cstdlib>
using namespace std;

int main(){
	int num = 100;
	char str[25];
	itoa(num, str, 10);
	cout << str; //输出100 
	return 0;
}

```



# 六，结构体

## typedef

![image-20231016062048122](TY/img/image-20231016062048122.png)![image-20231016062107099](TY/img/image-20231016062107099.png)

## 箭头运算符

![image-20231016070859686](TY/img/image-20231016070859686.png)

## 共用体

![image-20231016081510042](TY/img/image-20231016081510042.png)

![image-20231016081601592](TY/img/image-20231016081601592.png)![image-20231016081617866](TY/img/image-20231016081617866.png)![image-20231016081636860](TY/img/image-20231016081636860.png)

## 枚举类型

![image-20231016082615212](TY/img/image-20231016082615212.png)

![image-20231016082632497](TY/img/image-20231016082632497.png)



# 七，文件操作

## 文件打开与关闭

### FILE*fp;

定义一个FILE类型的指针变量

### fopen()

![image-20231025023609954](TY/img/image-20231025023609954.png)



格式：`FILE *fopen( const char *filename, const char *mode);`

FILE *fp;//返回打开/生成文件的文件指针

`fp = fopen("test.txt", "r");`

`fp = fopen(“..\\test.txt", "r");`上一级路径

`fp = fopen(“bin\\test.txt", "r");`

filename是文件名包含路径。如果不含路径，表示打开当前目录下的文件(CB是.cbp文件所在目录)

`fp = fopen("D:\newproject\test.txt", "r");`

`编译器会将’\’看成转义字符，例如：\n和\t，为此“\\”`

`fp = fopen("D:\\newproject\\test.txt", "r");`

### fclose()

![image-20231025023735303](TY/img/image-20231025023735303.png)

![image-20231025031904862](TY/img/image-20231025031904862.png)

- 若文件不存在，w新建一个文件，若文件存在，w会将原文件内容覆盖
- 用a打开文件，如果文件不存在则创建，文件存在则保留原文件内容，在文件末尾添加
- 若文件不存在：r+打开会失败，w+则会新建一个文件
- 若文件存在：r+不清空文件，w+则清空文件，因此当文件存在时要慎用w+
  - 文本文件字符读写： 
  -  fgetc(), fputc()字符         
  -  fgets(), fputs()字符串
  - 格式化读写: fscanf(), fprintf()
  - 二进制文件数据块读写: fread(), fwrite()



## 按字符读写文件

### fgetc（）与fputc()

![image-20231025024358620](TY/img/image-20231025024358620.png)

## 判断是否读到末尾EOF或feof（）

![image-20231025025022771](TY/img/image-20231025025022771.png)

### feof（）

![image-20231025025204733](TY/img/image-20231025025204733.png)

## 按字符串读写文件fgets与fputs



![image-20231025035625466](TY/img/image-20231025035625466.png)

![image-20231025035636274](TY/img/image-20231025035636274.png)

## 按格式读写文件fscanf与fprintf

![image-20231025035920261](TY/img/image-20231025035920261.png)![image-20231025035928777](TY/img/image-20231025035928777.png)

### 按数据块读写文件fread与fwrite

通常用于二进制文件的输入，输出

![image-20231025040005079](TY/img/image-20231025040005079.png)![image-20231025040021603](TY/img/image-20231025040021603.png)

【例13.7】在前几个实例基础上，计算每个学生的4门课程的平均分，将学生的各科成绩及平均分输出到文件student.txt中，然后再从文件中读出数据并显示到屏幕上

应该用rb：防止误读使读取结束

![image-20231025040459909](TY/img/image-20231025040459909.png)

![image-20231025040506632](TY/img/image-20231025040506632.png)
