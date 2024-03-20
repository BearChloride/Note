#   库

```c++
#include<bits/stdc++.h>//万能
#include<iostream>//cin输入 cout输出
#include<cstdlib>//system()，system("pause")=getchar用于显示暂停
#include<cstdio>//scanf,printf
#include<math.h>//调用常用库函数
#include<algorithm>//sort(begin,end,cmp)排序
#include<algorithm>//priority_queue
```



![image-20230908152633323](TY/img/image-20230908152633323.png)

# 程序结构

hello world

```c++
#include<iostream>//cin cout
#include<cstdlib>//system()
using namespace std;

int main() {
	cout << "hello world" << endl;//endl换行
	system("pause");//暂停，调用cstdlib库，不必加
	return 0;
}
```

计算x个人的票价

```c++
#include<iostream>

using namespace std;

int main() {
	int x, y;
	cin >> x;
	y = x * 10;
	cout << x << " " << y << endl;

	return 0;
}
```

计算圆柱表面积

```c++
#include<iostream>
#include<cstdio>
using namespace std;

int main() {
	const double pi = 3.1415926;
	double r, h, s1, s2, s;
	cin >> r >> h;//自动存为double
	s1 = pi * r * r;
	s2 = 2 * pi * r * h;
	s = 2*s1 + s2;
	printf("%0.3lf\n", s);

	return 0;
}
```

## 数据输入输出

### getchar字符输入

```c++
char ch;
ch=getchar();
```

只能接受单个字符，按回车键结束，同时读入两个，要先输入，否则会读入回车键

### putchar字符输出

```c++
char c='B'
putchar(c);
putchar('\x42');//用转义字符输出B
putchar(0x42);//用16进制输出B
putchar(66);//用10进制输出B
```

### scanf

![image-20230908170113068](TY/img/image-20230908170113068.png)

![image-20230908170140988](TY/img/image-20230908170140988.png)

### printf

![image-20230908170229669](TY/img/image-20230908170229669.png)

**short 用%hd输出**



![image-20230908170312044](TY/img/image-20230908170312044.png)

![image-20230908170330847](TY/img/image-20230908170330847.png)

### 字符char

```c++
char a[5]={'a','b','c','d','e'}//字符组
char b[5]={'a','b','c','d','、0'}//字符串
char c[5]="abcd";//长度应小于字符数组长度
```

![image-20230908190747752](TY/img/image-20230908190747752.png)

### gets语句

![image-20230908190817445](TY/img/image-20230908190817445.png)

### printf

```c++
printf("%s",a);
//不是printf("%s",a[]);
```

### puts

=`printf("%s",a/n);`

fputs不自带换行符

#### 字符替换

```c++
#include<cstdio>
#include<iostream>

using namespace std;

int main() {
	char st[200];
	char a, b;
	int i, n = 0;
	while ((st[n++] = getchar()) != '\n');
    //同时读入与判断
	a = getchar(); getchar(); b = getchar();
	for (i = 0; i < n; i++)
		if (st[i] == a)cout << b;
		else cout << st[i];
	cout << endl;

	return 0;
}
```

#### 过滤空格

```c++
#include<cstdio>
#include<iostream>

using namespace std;
char st[100];
int main() {

	while (scanf("%s", &st) == 1)
        //scanf只能一个一个读单词，while(scanf("%s", &st) == 1)循环读入数据，读不到时停止循环
		printf("%s ",st);

	return 0;
}

```

### strlen

strlen所作的仅仅是一个计数器的工作，它从内存的某个位置（可以是字符串开头，中间某个位置，甚至是某个不确定的内存区域）开始扫描，直到碰到第一个字符串结束符’\0’为止，然后返回计数器值。

```c++
#include <iostream>
#include <cstring>
int main(void)
{
    char s[] = "Golden Global View";
    std:: cout << s << " has " << strlen(s) << " chars";
    return 0;
}
// Golden Global View has 18 chars

```

##### 与sizeof（）区别

strlen(char*）函数求的是字符串的实际长度，它求得方法是从开始到遇到第一个’\0’，如果你只定义没有给它赋初值，这个结果是不定的，它会从aa首地址一直找下去，直到遇到’\0’停止。
**注意**：当使用strlen时一定要注意是否赋值

```c++
char aa[10];cout<<strlen(aa)<<endl; //结果是不定的
char aa[10]={'\0'}; cout<<strlen(aa)<<endl; //结果为0
char aa[10]="jun"; cout<<strlen(aa)<<endl; //结果为3
sizeof(aa)// 返回10
int a[10]; 
sizeof(a) // 返回40 （根据语言int型 c 是两个字节 c++是四个）

```

#### gets与strlen()的使用

```c++
#include<cstdio>
#include<iostream>
#include<cstring>

using namespace std;
char st[100];
int main() {

	char st[100];
	gets(st);//读取一行字符串
	for(int i=0;i<strlen(st);++i)
        cout<<st[i];
	

	return 0;
}

```

### 字符串处理函数

![image-20230909104150861](TY/img/image-20230909104150861.png)

strcmp比较第一对不相等的字符的大小

# 函数

## 传址调用

```c++
#include<cstdio>
#include<iostream>
#include<cstring>

using namespace std;
void swap(int&a,int&b){
    //将实参的地址值传给形参
int c=a;a=b;b=c;}
int main() {

	int d=1,e=2;
	swap(d,e);
	cout<<d<<' '<<e<<endl;


	return 0;
}

```

```c++
#include <stdio.h>
#include <stdlib.h>
//斐波那契数列

int main()
{  int n;
    scanf("%d",&n);
    int i;
    int a[100]={1,1,2};
    for(i=3;i<100;i++){
        a[i]=a[i-1]+a[i-2];
    }
    for(i=0;i<n;i++){
        printf("%d ",a[i]);
    }
    return 0;
}

```

## 数组排列：冒泡法

```c++
#include<cstdio>
#include<iostream>
#include<cstring>
//冒泡排序
using namespace std;

void bub(int[],int);
int i=0;
int main()
{
    int a[10]={11,4,55,6,77,8,9,0,7,1};
    cout<<"排序前";

    for(i=0;i<10;i++)
        cout<<a[i]<<',';
    cout<<endl;
    bub(a,10);
    cout<<"排序后"<<',';
    for(i=0;i<10;i++)
        cout<<a[i]<<',';
    cout<<endl;

    return 0;
}
void bub(int a[],int n)//将数组地址传入相当于直接干部数组
{
    for(i=1;i<n;i++){
        for(int j=0;j<n-i;j++){//第一轮：比9次；第二轮：8次……
            if(a[j]>a[j+1]){
                int k=a[j];
                a[j]=a[j+1];
                a[j+1]=k;
            }
        }
    }
}

```

## 全局变量与局部变量

![image-20230911063830244](TY/img/image-20230911063830244.png)

## 判断素数

```c++
#include<cstdio>
#include<iostream>
#include<cstring>
#include<math.h>
using namespace std;

int prime(int x)
{
    int j;
    if(x==2)return 1;
    for(j=2;j<sqrt(x)&&x%j!=0;j++)
       if(x%j==0)
         return 0;
    return 1;
}

int main()
{
    int x=19;
    if (prime(x))
        cout<<"true"<<endl;
    else
        cout<<"false"<<endl;
}

```

## 将十进制转换为十六进制

```c++
#include <bits/stdc++.h>
using namespace std;

void turn(int);
char ch[6]={'A','B','C','D','E','F'};
int main()
{
    int n;
   cin>>n;

   turn(n);


return 0;
}
void turn(int a)
{
    if(a<0){
        a=-a;cout<<'-';}
    int num[10]={0};
    int t=a;
    int i=0;
    while(t%16!=0){

        num[i]=t%16;
        i++;
        t/=16;
    }
    num[i]=t;
    //cout<<num[0]<<endl;

    while(num[i]!=0)
    {
        i++;
    }
    i--;

    for(i;i>=0;i--)
    {
        if(num[i]>9)
        {
            cout<<ch[num[i]-9];
        }
        else cout<<num[i];
    }

}

```

## gets函数

[gets函数，C语言gets函数详解 (biancheng.net)](http://c.biancheng.net/view/233.html)

```c
##include<stdio.h>
char a[10];
gets(a);
```

## point类

Point类数据结构表示了二维坐标系的点，即由其图像坐标x和y指定的点，用法如下：

```c++
    Point point;
    point.x = 10;
    point.y = 5;
    cout << point << endl;
```



# 函数递归

```c++
#include <bits/stdc++.h>
using namespace std;

int xn(int);
int x;
int main()
{
    int n;
    cin>>x>>n;poin
    cout<<xn(n);
}
int xn(int n)
{
    if(n==0)return 1;
    else return x*xn(n-1);
}

```

# 结构体

![屏幕截图 2023-09-14 145500](TY/img/屏幕截图 2023-09-14 145500.png)

![image-20230914145538432](TY/img/image-20230914145538432.png)

![image-20230914145652800](TY/img/image-20230914145652800.png)

```c++
#include <bits/stdc++.h>
using namespace std;

struct student
{
    string name;
    int chinese,math;
    int total;
};
student a[100];
int n;

int main()
{
   cin>>n;
   for(int i=0;i<n;i++)
   {
       cin>>a[i].name;
       cin>>a[i].chinese>>a[i].math;
       a[i].total=a[i].chinese+a[i].math;
   }
   for(int i=n-1;i>0;i--)
   {
       for(int j=0;j<i;j++)
       {
           if(a[j].total<a[j+1].total)swap(a[j],a[j+1]);
       }

   }
   for(int i=0;i<n;i++)
   {
       cout<<a[i].name<<' '<<a[i].chinese<<' '<<a[i].math<<' '<<a[i].total<<endl;

   }
   return 0;
}


```

## 结构体使用方式

1. struct 结构体名 变量名

2. struct 结构体名 变量名={成员1，成员2}

3. 定义结构体时自动创建变量

   ```c++
   #include<iostream>
   #include<string>
   using namespace std;
   
   struct student
   {
       string name;
       int score;
   };
   void print(const student* s)//传指针节省空间，加const防止误改
   {
       cout << s->name << s->score << endl;
   }
   int main()
   {
       student a = { "张三",15};
      return 0;
   }
   
   
   ```

# 内存分区模型

- 代码区
- 全局区
- 栈区
- 堆区

## 程序运行前

代码区，全局区

## 运行后

栈区：自动释放，不要返回局部变量地址

堆区：手动分配，释放，new

## new，delete用法

```c++
#include<iostream>
using namespace std;
int* func()
{
	int* p=new int(10);//创建堆区数据，返回指针，地址名称储存在栈区
    int* arr=new int[10];//创建数组，10代表数组有十个元素
	for (int i = 0; i < 10; i++)
	{
		 arr[i] = i + 100;
		 cout << arr[i]<<endl;
	}
	delete[]arr;//释放数组
	return p;
}
int main()
{
	int* p = func();
	cout << *p << endl;
	return 0;
}
```



# 引用

## 基本语法

数据类型 &别名=原名

## 注意事项

- 必须初始化

- 一旦初始化就不可以更改

# 函数重载

##   概述

函数名可以相同，提高复用性

满足条件：

- 同一个作用域

- 函数名相同

- 函数参数类型不同，或个数不同，或顺序不同

- 函数的返回值不可以作为函数重载的条件

```c++
#include<iostream>
using namespace std;
void func()
{
	cout << "func的调用" << endl;
}
void func(int a)
{
	cout << "func(int a)的调用" << endl;
}
int main()
{
	func();//调用函数1
	func(10);//调用函数2
}
```

## 注意事项

#### 函数碰到默认参数,出现二一性

#### 有const

```c++
int a=10;
func(1);//调用有const
func(a);//调用无const
    
```

# 函数指针

```c++
int (*fpIntInt)(int,int);
fpIntInt=min;//将指针指向函数min
```

用typedef简化

```c++
typedef int (*fpIntInt)(int,int);
fpIntInt fp=min;
fpIntInt fp=max;//更改指向
```

# 可变参数

包含<stdarg.h>

```c++
float avg(int size,...)
{
    float sum=0.0;
    va_list valist;//创建参数列表
    va_start(valist,size);//初始化
    for(int i=0;i<size;i++)
    {
        sum+=va_arg(valist,int);//用va_arg依次取得参数
    }
    va_end(valist);//清空内存
}
```





# 数据结构

## 堆与栈的区别

### 1. C++中，内存分成5个区

根据《C++内存管理技术内幕》一书，在C++中，内存分成5个区，分别是：堆、栈、自由存储区、全局/静态存储区、常量存储区。

##### a)栈

内存**由编译器在需要时自动分配和释放**。通常用来存储局部变量和函数参数。

为运行函数而分配的局部变量、函数参数、返回地址等存放在栈区。

栈运算分配内置于处理器的指令集中，效率很高，但是分配的内存容量有限。

##### b)堆

内存使用new进行分配，使用delete或delete[]释放。

**如果未能对内存进行正确的释放，会造成内存泄漏**。

但在程序结束时，会由操作系统自动回收。

##### c)自由存储区

使用malloc进行分配，使用free进行回收。
和堆类似。

##### d)全局/静态存储区

全局变量和静态变量被分配到同一块内存中，C语言中区分初始化和未初始化的，C++中不再区分了。

全局变量、静态数据、常量存放在全局数据区；使用静态关键字static声明，在静态存储区申请一个静态变量。

##### e)常量存储区

存储常量，不允许被修改。

### 2. C++中，内存分成3个区

这里，在一些资料中是这样定义C++内存分配的，可编程内存在基本上分为这样的几大部分：静态存储区、堆区和栈区。他们的功能不同，对他们使用方式也就不同。

##### a)静态存储区

内存在程序编译的时候就已经分配好，这块内存在程序的整个运行期间都存在。它主要存放静态数据、全局数据和常量。

##### b)栈区

在执行函数时，函数内局部变量的存储单元都可以在栈上创建，函数执行结束时这些存储单元自动被释放。

栈内存分配运算内置于处理器的指令集中，效率很高，但是分配的内存容量有限。

##### c)堆区

亦称动态内存分配。

程序在运行的时候用malloc或new申请任意大小的内存，程序员自己负责在适当的时候用free或 delete释放内存。

动态内存的生存期可以由我们决定，如果我们不释放内存，程序将在最后才释放掉动态内存。

但是，良好的编程习惯是：**如果某动态内存不再使用，需要将其释放掉，否则，我们认为发生了内存泄漏现象**。

### 堆和栈究竟有什么区别？

> 管理方式不同：
>
> - 对于栈来讲，是由编译器自动管理，无需我们手工控制；
> - 对于堆来说，释放工作由程序员控制，容易产生memory leak。

> 空间大小不同：
>
> - 一般来讲在32位系统下，堆内存可以达到4G的空间，从这个角度来看堆内存几乎是没有什么限制的。
> - 对于栈来讲，一般都是有一定的空间大小的。默认的栈空间大小是1M了。不过可以修改其大小。

> 能否产生碎片不同：
>
> - 对于堆来讲，频繁的new/delete势必会造成内存空间的不连续，从而造成大量的碎片，使程序效率降低。
> - 对于栈来讲，则不会存在这个问题，因为栈是先进后出的队列，他们是如此的一一对应，以至于永远都不可能有一个内存块从栈中间弹出，在他弹出之前，在他上面的后进的栈内容已经被弹出。

> 生长方向不同：
>
> - 对于堆来讲，生长方向是向上的，也就是向着内存地址增加的方向；
> - 对于栈来讲，它的生长方向是向下的，是向着内存地址减小的方向增长。

> 分配方式不同：
>
> - 堆都是动态分配的，没有静态分配的堆。
> - 栈有2种分配方式：静态分配和动态分配。静态分配是编译器完成的，比如局部变量的分配。动态分配由allocal 函数进行分配，但是栈的动态分配和堆是不同的，他的动态分配是由编译器进行释放，无需我们手工实现。

> 分配效率不同：
>
> - 栈是机器系统提供的数据结构，计算机会在底层对栈提供支持：分配专门的寄存器存放栈的地址，压栈出栈都有专门的指令执行，这就决定了栈的效率比较高。
> - 堆则是C/C++函数库提供的，它的机制是很复杂的，例如为了分配一块内存，库函数会按照一定的算法（具体的算法可以参考数据结构/操作系统）在堆内存中搜索可用的足够大小的空间，如果没有足够大小的空间（可能是由于内存碎片太多），就有可能调用系统功能去增加程序数据段的内存空间，这样就有机会分到足够大小的内存，然后进行返回。显然，堆的效率比栈要低得多。

### 总结

可以看到，堆和栈相比，由于大量new/delete的使用，容易造成大量的**内存碎片**；由于没有专门的系统支持，效率很低；由于可能**引发用户态和核心态的切换**，内存的申请，代价变得更加昂贵。所以栈在程序中是应用最广泛的，**就算是函数的调用也利用栈去完成，函数调用过程中的参数，返回地址，EBP和局部变量都采用栈的方式存放**。所以，推荐大家尽量用栈，而不是用堆。

虽然栈有如此众多的好处，但是由于和堆相比不是那么灵活，有时候**分配大量的内存空间，还是用堆好**。

------

内存使用规则：
【规则1】用malloc或new申请内存之后，应该立即检查指针值是否为NULL。防止使用指针值为NULL的内存。
【规则2】不要忘记为数组和动态内存赋初值。防止将未被初始化的内存作为右值使用。
【规则3】避免数组或指针的下标越界，特别要当心发生“多1”或者“少1”操作。
【规则4】动态内存的申请与释放必须配对，防止内存泄漏。
【规则5】用free或delete释放了内存之后，立即将指针设置为NULL，防止产生“野指针”。

```c++
void fn(){ 
   int* p = new int[5];
}
```

看到new，首先应该想到，我们分配了一块堆内存，那么指针p呢?
　　它分配的是一块栈内存，所以这句话的意思就是：在栈内存中存放了一个指向一块堆内存的指针p。程序会先确定在堆中分配内存的大小，然后调用 operator new分配内存，然后**返回这块内存的首地址，放入栈中**。
　　
　　注意：这里为了简单并没有释放内存，那么该怎么去释放呢? 是`delete p`么? NO，错了，应该是`delete [ ]p`，这是告诉编译器：删除的是一个数组。

## 栈stack函数用法

[c++ stack用法详解_斯文～的博客-CSDN博客](https://blog.csdn.net/weixin_52341477/article/details/119250698)

在c++ 中,stack的[头文件](https://so.csdn.net/so/search?q=头文件&spm=1001.2101.3001.7020)是`#include<stack>`

```c++
stack<int> q;	//以int型为例
int x;
q.push(x);		//将x压入栈顶
q.top();		//返回栈顶的元素
q.pop();		//删除栈顶的元素
q.size();		//返回栈中元素的个数
q.empty();		//检查栈是否为空,若为空返回true,否则返回false
```

```c++
#include<iostream>
#include<stack>
using namespace std;
int main()
{
	stack<int>  q;
	q.push(1);
	q.push(2);
	q.push(3);
	q.push(4);
	q.push(5);
	
	cout<<"q.size "<<q.size()<<endl;
	cout<<"q.top "<<q.top()<<endl;   //输出栈顶元素 
	
	q.pop();	//删除栈顶元素
			
	cout<<"q.size "<<q.size()<<endl;  
	cout<<"q.top "<<q.top()<<endl;
	
	return 0; 
}

```

![image-20230924043416345](TY/img/image-20230924043416345.png)

```c++
#include<cstdio>
#include<cstdlib>
#include<string>
#include<cstring>
#include<iostream>
using namespace std;

int stack[101];
char s[256];
int comp(char s[256])
{
    int i = 0, top = 0, x, y;
    while (i <= strlen(s) - 2)
    {
        switch (s[i])
        {
        case'+':stack[--top] += stack[top + 1]; break;
        case'-':stack[--top] -= stack[top + 1]; break;
        case'*':stack[--top] *= stack[top + 1]; break;
        case'/':stack[--top] /= stack[top + 1]; break;
        default:x = 0;
            while (s[i] != ' ')x = x * 10 + s[i++] - '0';
            stack[++top] = x; break;
        }
        i++;
    }
    return stack[top];
}
int main()
{
    printf("input a string(@_over):");
    cin>>s;//gets(s);cin不能输入空格
    printf("result=%d", comp(s));

    return 0;
}
16 9 4 3 +*-@
```

# 类和对象

c++三大特性：封装，继承，多态

## 封装

将属性和行为作为一个整体

语法：class 类名{访问权限：属性/行为}；

```c++
#include <iostream>

using namespace std;
const double PI = 3.14;
class Circle//类 类名称
{
	//访问权限
	//公共权限
public:
    //类中的属性和行为，统称为成员
		//属性  成员属性 成员变量
		//半径
		int m_r;

		//行为  成员函数 成员方法
		//获取园的周长
		double C()
		{
			return 2 * PI * m_r;
		}
};
int main()
{
	//通过圆类，创建具体对象
	Circle c1;
	//赋值
	c1.m_r = 10;
	cout << "周长为：" << c1.C() << endl;

	return 0;
}
```

### 封装的意义

#### 访问权限

1. public 公共权限          成员类内可访问，类外也可以
2. protected 保护权限   类内可以，类外不可以，儿子可以访问父亲中的保护内容
3. private 私有权限        类内可以，类外不可以，儿子不可以访问父亲中的私有内容

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	string m_Name;
protected:
	string m_Car;
private:
	int m_Password;
public:
	void func()
	{
		m_Name = "张三";
		m_Car = "拖拉机";
		m_Password = 123456;
	}
};
int main()
{
	Person p1;
	p1.m_Name = "李四";//通过
	p1.m_Car = "奔驰";//报错
}
```

#### struct和class区别

struct默认权限是公共，class默认为私有

#### 成员属性设为私有

- 可以自己控制读写权限
- 对于写权限，可以自己检查数据有效性

```c++
//通过成员函数访问私有权限
class Person
{
private:
    int m_Age;
public:
    void segAge(int age)
    {
        if(age<0||age>150)
        {
            m_Age=0;
            cout<<"wrong"<<endl;
            return;
        }
        m_Age=age;
    }
}
```

### 封装案例

求立方体的表面积和体积

```c++
#include<iostream>
using namespace std;
class Cube
{
private:
	int m_L, m_H, m_W;
public:
	void setL(int l)
	{
		m_L = l;
	}
	int getL()
	{
		return m_L;
	}
	void setW(int w)
	{
		m_W = w;
	}
	int getW()
	{
		return m_W;
	}
	void setH(int h)
	{
		m_H = h;
	}
	int getH()
	{
		return m_H;
	}
	int calculateS()
	{
		return 2 * m_L * m_W + 2 * m_H * m_W + 2 * m_L * m_H;
	}
	int calculateV()
	{
		return m_L * m_H * m_W;
	}
	bool isSameByClass(Cube& c)
	{
		if (c.getL() == m_L)
		{
			return true;
		}
	}
};
bool isSame(Cube& c1, Cube& c2)
{
	if (c1.getL() == c2.getL() && c1.getW() == c2.getW() && c2.getH() == c1.getH())
	{
		return true;
	}
}
int main()
{
	Cube c1;
	c1.setL(10);
	c1.setH(10);
	c1.setW(10);
	cout << c1.calculateS() << endl;
	Cube c2;
	c2.setL(10);
	c2.setH(10);
	c2.setW(10);
	bool ret = isSame(c1, c2);
	bool rett = c1.isSameByClass(c2);
	if (ret)
	{
		cout << "c1和c2是相同的" << endl;
	}
	else
	{
		cout << "c1和c2不相等" << endl;
	}
}
```

在一类中可以包含另一类

## 对象的初始化和清理

### 构造函数和析构函数

#### 构造函数

类名（）{}

1. 构造函数，没有返回值也不用写void
2. 函数名与类名相同
3. 可以有参数，可以发生重载
4. 程序在调用对象前会自动调用构造，无需手动调用，只会调用一次

#### 析构函数

~类名（）{}

1. 构造函数，没有返回值也不用写void

2. 函数名与类名相同，前加~

3. 无参数，不能重载

4. 无需手动调用

   ```c++
   #include<iostream>
   using namespace std;
   class Person
   {
   public:
   	Person()
   	{
   		cout << "构造函数的调用" << endl;
   	}
   	~Person()
   	{
   		cout << "析构函数的调用" << endl;
   	}
   };
   void test()
   {
   	Person p;
   }
   int main()
   {
   	test();
   }
   ```

   

### 构造函数的分类和调用

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	int age;
	//无参函数
	Person()
	{
		cout << "构造函数的调用" << endl;
	}
	//有参函数
	Person(int a)
	{
		age = a;
		cout << "有参构造函数的调用" << endl;
	}
	//拷贝构造函数,以引用的方式传进来
	Person(const Person &p)
	{
		age = p.age;
	}
	~Person()
	{
		cout << "析构函数的调用" << endl;
	}
};
//调用
void test()
{
	//1.括号法
	Person p1();//默认构造函数的调用
	//注意：不要加小括号，因为编译器认为是函数声明
	Person p2(10);//有参
	Person p3(p2);//拷贝
	cout << "p2的年龄：" << p2.age << endl;
	cout << "p3的年龄：" << p3.age << endl;
	//2.显示法
	Person p5 = Person(10);
	Person p6 = Person(p5);
	Person(10);//匿名对象，当前执行结束后，系统立即销毁匿名对象
	//3.隐式转换法
	Person p7 = 10;//相当于Person p4=Person(10);有参构造
}
int main()
{
	test();
}
```

# c++对象模型和this指针

#### this指针

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	Person(int age)
	{
		//this指针指向被调用的成员函数所属的对象
		this->age = age;

	}
	Person& PersonAddPerson(Person& p)
	{
		this->age += p.age;
		return *this;
	}
	int age;
};
void test1()
{
	Person p1(18);
	cout << "p1的年龄是：" << p1.age << endl;
}
void test2()
{
	Person p1(10);
	Person p2(10);
	p2.PersonAddPerson(p1).PersonAddPerson(p1);
	cout << "p2的年龄是：" << p2.age << endl;
}
int main()
{
	test1();
	test2();
}
```

## 友元

### 1.全局函数做友元

```c++
#include<iostream>
using namespace std;

class Building
{
	friend void Friend(Building* building);//全局函数做友元
public:
	string m_Sittingroom;
	Building()
	{
		m_Sittingroom = "客厅";
		m_Bedroom = "卧室";
	}
private:
	
	string m_Bedroom;
};
void Friend(Building* building)
{
	cout << "正在访问：" << building->m_Bedroom << endl;
}
int main()
{
	Building building;
	Friend(&building);
	return 0;
}
```

### 2.类做友元

```c++
friend class aFriend;
```

### 3.成员函数做友元

```c++
	friend void GoodGay::visit();
```



# 重载

## 加号重载

```c++
#include<iostream>
using namespace std;
class Person
{
public:
	
	//编译器给了一个通用名称
	//通过成员函数重载加号，
	Person operator+(Person& p)
	{
		Person temp;//创建一个临时变量
		temp.m_A = this->m_A + p.m_A;
		temp.m_B = this->m_B + p.m_B;
		return temp;
	}
	
	int m_A;
	int m_B;
	
};
//通过全局函数重载加号
Person operator+(Person& p1, Person& p2)
{
	Person temp;
	temp.m_A = p1.m_A + p1.m_A;
	temp.m_B = p1.m_B + p1.m_B;
	return temp;
}

int main()
{
	Person p1;
	p1.m_A = 10;
	p1.m_B = 10;
	Person p2;
	p2.m_A = 10;
	p2.m_B = 10;
	//Person p3 = p1.operator+(p2);
	// 或Person p3=(p1,p2);
	//简化为
	Person p3 = p1 + p2;

}
```

## 递增重载

```c++
#include<iostream>
using namespace std;
class MyIntrger
{
	friend ostream& operator<<(ostream& cout, MyIntrger myint);
public:
	MyIntrger()
	{
		m_Num=0;
	}
	//重载前置++运算符 返回引用是为了对一个数据递增
	MyIntrger& operator++()
	{
		//先进性++运算
		m_Num++;
		//再将自身返回
		return*this;
	}
	MyIntrger operator++(int)
	{
		//先记录当时结果
		MyIntrger temp = *this;
		//后递增
		m_Num++;
		//最后将记录结果返回
		return temp;
	}
private:
	int m_Num;
};
//通过全局函数重载<<
ostream & operator<<(ostream&cout,MyIntrger myint)
{
	cout  << myint.m_Num ;
	return cout;
}

int main()
{
	MyIntrger myint;
	cout << ++(++myint) << endl;//前置递增
	cout << myint++ << endl;//后置递增
}
```

前置递增返回引用，后置递增返回值

## 拷贝构造

重载operator=

# 继承

## 基本语法

继承好处：减少重复代码

语法：class 子类：继承方式 父类

子类（派生类）

父类（基类）

```c++
#include<iostream>
using namespace std;

class BasePage//基类
{
	public:
	void header()
	{
		cout << "头部" << endl;
	}
	void footer()
	{
		cout << "脚部" << endl;
	}

};
class Java :public BasePage//子类1
{
public:
	void content()
	{
		cout << "Java视频" << endl;
	}
};

class CPP :public BasePage//子类2
{
public:
	void content()
	{
		cout << "CPP视频" << endl;
	}
};
int main()
{
	Java ja;
	ja.header();
	ja.content();
	ja.footer();
	CPP c;
	c.header();
	c.content();
	c.footer();
		
}
```

## 继承方式

1. 公共继承,访问public
2. 保护继承,访问public,protect
3. 私有继承,访问全部

### 同名成员处理

子类：直接访问

父类：加作用域

```c++
s.m_A;//son下的m_A
s.Base::m_A;//父类下的m_A
```



## 利用开发人员命令提示工具

- 跳转盘符 D：
- 跳转文件路径 cd 具体路径下
- 查看命名
- cl /d1 reportSingleClassLayout类名 文件名

![image-20230930164513299](TY/img/image-20230930164513299.png)

# 多态

## 基本概念

- 静态多态：函数重载，运算符重载

- 动态多态：派生类和虚函数

  ```c++
  #include<iostream>
  using namespace std;
  class Animal
  {
  public:
  	//虚函数
  	virtual void speak() 
  	{
  		cout << "谁在说话？" << endl;
  	}
  };
  class Cat:public Animal
  {
  public:
  	//重写：函数返回值类型，函数名，参数列表完全相同
  	void speak()
  	{
  		cout << "猫在说话" << endl;
  	}
  };
  class Dog :public Animal
  {
  public:
  	void speak()
  	{
  		cout << "狗在说话" << endl;
  	}
  };
  //动态多态满足条件
  //1.有继承关系
  //2.子类重写父类虚函数
  //动态多态使用
  //父类指针或引用执行子类对象
  void doSpeak(Animal& animal)//Animal & animal =cat;
  {
  	animal.speak();
  	//根据传入对象不同，进入不同的类
  }
  void test01()
  {
  	Cat cat;
  	doSpeak(cat);
  	Dog dog;
  	doSpeak(dog);
  }
  int main()
  {
  	test01();
  	return 0;
  }
  ```


## 案例一：计算器类

基本写法

```c++
#include<iostream>
#include<string>
using namespace std;
class Calculator
{
public:
	int m_Num1;
	int m_Num2;
	int getResult(string op)
	{
		if (op == "+")return m_Num1 + m_Num2;
		if (op == "-")return m_Num1 - m_Num2;
		if (op == "*")return m_Num1 * m_Num2;
		if (op == "/")return m_Num1 / m_Num2;
	}
};
void test01()
{
	Calculator c;
	c.m_Num1 = 10;
	c.m_Num2 = 10;
	cout << c.m_Num1 << "+" << c.m_Num2 << "=" << c.getResult("+") << endl;
}
int main()
{
	test01();
	return 0;
}
```

多态写法

```c++
#include<iostream>
#include<string>
using namespace std;
class AbstractCalculator
{
public:
	int m_Num1;
	int m_Num2;
	virtual int getResult()
	{
		return 0;
	}
};
//加法计算器类
class AddCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 + m_Num2;
	}
};
//减法
class SubCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 - m_Num2;
	}
};
//乘法
class MulCalculator :public AbstractCalculator
{
public:
	int getResult()
	{
		return m_Num1 * m_Num2;
	}
};
void test02()
{
	AbstractCalculator* abc = new AddCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << "+" << abc->m_Num2 << "=" << abc->getResult() << endl;
	delete abc;
	abc = new SubCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;
	cout << abc->m_Num1 << "-" << abc->m_Num2 << "=" << abc->getResult() << endl;
	delete abc;
}
int main()
{
	test02();
	return 0;
}
```

## 纯虚函数和抽象类

通常父类虚函数实现无意义，可改为纯虚函数

语法：virtual 返回值类型 函数名 （参数列表）=0；

当类中有纯虚函数，这个类成为抽象类

### 抽象类特点

- 无法实例化对象
- 子类必须重写纯虚函数，否则也属于抽象类

# 模板

## 函数模板

建立一个通用函数，返回值类型和形参类型可不具体指定

语法：

```c++
template<typename T>

void swapT(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}
SwapT(a,b);//自动
SwapT<int>(a,b);//手动
```

template：声明创建模板

typename：表明后面是一种数据类型，可以用class代替

T：虚拟的数据类型

## 类模板

```c++
#include<iostream>
using namespace std;
template <class NameType,class AgeType>

class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->name = name;
		this->age = age;
	}
	void Showperson()
	{
		cout << this->name << " " << this->age;
	}
	NameType name;
	AgeType age;
};
int main()
{
	Person<string, int>p1("小明",12);//没有自动类型推导，必须写出
	p1.Showperson();
	return 0;
}
```

## 类模板对象做函数参数

```c++
//1.指定传入类型(最常用)
void func(Person<string,int>&p);
//2.参数模板化
template <class T1,class T2>
void func(Person<T1,T2>&p);
//3.整个类模板化
template <class T>
void func(T &p);//自动推导出来
```

## 看类型名称

```c++
typeid(T1).name()//显示数据类型
```

## 类模板与继承

要声明父类类型

```c++
class Son :public Father<int>
```

## 类外实现

```c++
//构造函数
template<class T1,class T2>
Person::Person(T1 name,T2 name)
{}
//成员函数
template<class T1,class T2>//告诉它是一个类模板
void Person::func(T1 name,T2 name)
{}
```

## 类模板分文件编写

由于调用时才创建类模板，

1. 第一种解决方式，直接包含原文件.cpp
2. 将.h与.cpp写在一起，改为.hpp文件（约定俗成）

# 标准模板库STL

## vector



### 初始化

```c++
#include<vector>//包含头文件
vector<int>vec1;//空
vector<int>vec2(3);//有3个元素
vector<char>vec3(3,'a');//3个元素全为a
vector<char>vec4(vec3);//复制
```

### 添加元素

```c++
vec1.empty()//判断vec1是否为空
vec1.push_back(1);//将1入栈
vec1.pop_back();//弹出一个元素
vec1==vec2;//可直接比较
```

## 通过迭代器访问数组数据

```c++
vector<int>::iterator itBegin=v.begin();//起始迭代器，指向第一个数据
vector<int>::iterator itEnd=v.end();//结束迭代器，指向最后一个数据的下一个数据
//遍历方法
//1
while (itBegin!=itEnd)
	{
		cout << *itBegin << endl;
		itBegin++;
	}
//2
for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
	{
		cout << *it << endl;
	}
//3
for_each(v.begin(), v.end, myPrint);
```

## 嵌套

```c++
int main()
{
	//text01();
	vector <vector<int>>v;
	vector<int>v1;
	vector<int>v2;
	vector<int>v3;
	vector<int>v4;
	for (int i = 0; i < 4; i++)
	{
		v1.push_back(i + 1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
		v4.push_back(i + 4);
	}
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	v.push_back(v4);
	vector<int>::iterator vit;
	for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++)
	{
		//(*it)是vector容器
		for (vit = (*it).begin(); vit != (*it).end(); vit++);
		{
			cout << *vit << " ";
			cout << endl;
		}
	}
	return 0;
}
```



## string

等于vector<char>

```c++
#include<string>//包含
```

#### 接受不确定个数的读入

```c++
int main()
{
    vector<string> strVec;
    string s;
    while(cin>>s)//读取到了才进入
    {
        strVec.push_back(s);//入栈
    }
    
    return 0;
}
```

#### 可以直接比较’=‘，连接’+‘

# 文件操作

头文件<fstream>

操作文件三大类：

- ofstream:写(outputfile)
- ifstream: 读(input)
- fstream: 读写

## 文本文件

1. 包含头文件

2. 创建流对象

   ==ofstream ofs;==(fstream也行)

3. 打开文件

   ofs.open(“文件路径”，打开方式)；

4. 写数据

   ofs<<“写入的数据”；

5. 关闭文件

   ofs.close();

   ## 文件打开方式

   ![image-20231120210310685](img/image-20231120210310685.png)

配合使用：|

`ios::binary|ios::out`

### 读文件

1. 包含头文件

2. 创建流对象

   ==ifstream ofs;==(fstream也行)

3. 打开文件,判断是否打开

   ifs.open(“文件路径”，打开方式)；

   ```c++
   if(!ifs.is_open())
   
   {
       cout<<“文件打开失败”<<endl;
       return;
   
   }
   ```

   ### 读取方式

   ```c++
   //第一种，暂存于字符数组中
   //注意：>>遇空格会读取结束
   char buf[1024]={0};
   while (ifs>>buf)
   {
       cout<<buf<<endl;
   }
   //第二种,一次读一行ifs中getline
   char buf[1024]={0};
   whlie(ifs.getline(buf,sizeof(buf)))
   {
       cout<<buf<<endl;
   }
   //第三种,全局函数getline
   #include<string>
   string buf;
   while(getline(ifs,buf))
   {
       cout<<buf<<endl;
   }
   //第四种(慢)
   char c;
   while(c=(ifs.get())!=EOF)
   {
       cout<<c;
   }
   ```
   
   ## 二进制文件
   
   打开方式：ios::binary
   
   ```c++
   #include<iostream>
   #include<fstream>
   #include<string>
   using namespace std;
   class Person
   {
   public:
   	char m_Name[64];
   	int m_Age;
   };
   void Write()
   {
   	fstream ofs("person.txt", ios::out|ios::binary);
   	Person p = { "张三",18 };
   	//写的时候要强制类型转换
   	ofs.write((const char*)&p, sizeof(Person));
   	ofs.close();
   }
   void Read()
   {
   	fstream ifs("person.txt", ios::in | ios::binary);
   	if (!ifs.is_open())
   	{
   		cout << "文件打开失败" << endl;
   		return;
   	}
   		Person p;
   		ifs.read((char*)&p, sizeof(Person));
   		cout << p.m_Name << " " << p.m_Age << endl;
   	
   
   }
   int main()
   {
   	Write();
   	Read();
   	return 0;
   }## queue
   ```
   
   #include<algorithm>
   
   ### queue
   
   queue<Type>q 定义
   
   push() 在队尾插入一个元素
   
   top() 返回队列第一个元素
   
   pop() 删除队列第一个元素
   
   size() 返回队列中元素个数
   
   empty() 如果队列空则返回true
   
   front() 返回队列中的第一个元素
   
   back() 返回队列中最后一个元素

### priority_queue

priority_queue<Type, Container, Functional>

Type 就是数据类型，Container 就是容器类型（Container必须是用数组实现的容器，比如vector,deque等等，但不能用 list。STL里面默认用的是vector），Functional 就是比较的方式，当需要用自定义的数据类型时才需要传入这三个参数，使用基本数据类型时，只需要传入数据类型，默认是大顶堆

```c++
priority_queue<int,vector<int>,greater<int>>q;//由大到小排列
```

```text
deque.size();//返回容器中元素的个数
deque.empty();//判断容器是否为空 
deque.resize(num);//重新指定容器的长度为num,若容器变长，则以默认值填充新位置。如果容器变 短，则末尾超出容器长度的元素被删除。 
deque.resize(num, elem); //重新指定容器的长度为num,若容器变长，则以elem值填充新位置,如果 容器变短，则末尾超出容器长度的元素被删除
push_back(elem);//在容器尾部添加一个数据 
push_front(elem);//在容器头部插入一个数据 
pop_back();//删除容器最后一个数据 
pop_front();//删除容器第一个数据
```