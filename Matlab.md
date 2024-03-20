# 矩阵操作

```matlab
%ctrl+r注释
%ctrl+t取消

%% 条件
disp('大家好')
a=input("输入：");
if(a>=85)
    disp("1")
elseif (a>=60)
    disp("2")
else
    disp("3")
end

%% 字符串
%合并
strcat('1','2');
a=['字符串1' '字符串2'];
%转换字符串
c=100;

disp(['c的取值为',num2str(c)]);

%% sum求和函数

%向量直接求和
E=[1,2,3];
e=sum(E);
Q=[1;2;3];
q=sum(Q);

%矩阵指明按行还是按列求和
E=[1,2;3,4;5,6];
a=sum(E);%默认按列
b=sum(E,1);%按列求和（得行向量）
c=sum(E,2);%按行求和

%对矩阵求和
a=sum(sum(E));
a=(E(:));%把据矩阵转换为一个列向量

%% 矩阵查询
E=[1,2;3,4;5,6];
%查询某个元素
E(2,3)
%查询某行，某列
E(2,:)
E(:,2)
%取某些行元素
E([1,3],:)%一和三行
E(1:3,:)%一到三行

%递增语法
1;3;10; %返回1,4,7,10
E(1:2:3,:)%取1，3行
E(1:end,:)%取第一行到最后一行
E(:)%取全部元素

%% size函数
[r,c]=size(A);

%% repmat函数
B=repmat(A,m,n);%将A作为元素填入m*n的B中

%% 矩阵运算
A*B,A/B%乘和除
inv(A)%求逆
A.*B%对应元素相乘
A*2=A.*2%所有元素乘2
A.^2%每个元素乘方

%% 求特征值和特征向量
E=eig(A)%求特征值，构成列向量
[V,D]=eig(A)%diag特征值构成的对角矩阵，V对应特征值形成列向量构成的矩阵

%% 生成矩阵
ones(a,b)%生成a行b列全为1的矩阵
zeros(a,b)%全为0
rand(a,b)%0或1
```

# 层次分析法

```matlab
%% 层次分析法
%A=[1 2 5;1/2 1 2;1/5 1/2 1]
%% 获取判断矩阵
disp("请输入判断矩阵：");
A=input('A=');
[~,n]=size(A);

%% 特征值法求权重
[V,D]=eig(A);
Max_eig=max(max(D));
[r,c]=find(D==Max_eig,1);
%k = find(X,n) 返回与 X 中的非零元素对应的前 n 个索引。
% 先判断D==1是否成立，若成立返回值为1，find寻找第一个使返回值为1的位置
disp("特征值法求权重结果是：");
w=V(:,c)./sum(V(:,c));
disp(w);

%%计算一致性比例CR
CI=(Max_eig-n)/(n-1);
RI=[0 0.0001 0.52 0.89 1.12 1.26 1.36 1.41 1.46 1.49 1.52 1.54 1.56 1.58 1.59];
%常数，使用要求n<=15
%n=2时为零，取一个较小数代替
CR=CI/RI(n);
disp("最大特征值为：");
disp(Max_eig);
disp('一致化指标：CI=');
disp(CI);
disp('一致性比例：CR=');
disp(CR);
if(CR<0.1)
    disp('A的一致性可以接受');
else
    disp('该判断矩阵需要修改');
end
```

# Topsis优劣解距离法

```matlab
X=[99,0.0100;100,0.0120;98,0.0400;97,0.0330]

%% 正向化
disp('---正在进行正向化---');
[n,m]=size(X);
vec=input('请输入需要正向化的列（若不需要输入-1，按向量格式输入，如[a,b,c]表示a,b,c要正向化）：');
if(vec~=-1)
    for i=1:size(vec,2)
        
        flag=input(['对于第',num2str(vec(i)),'列，极小型输入1，中间型2，区间型3：']);
        if(flag==1)%极小型
            X(:,vec(i))=Min2Max(X(:,vec(i)));
        elseif(flag==2)%中间型
            best=input('best=');
            X(:,vec(i))=Mid2Max(X(:,vec(i)),best);
        elseif(flag==3)%区间型
            arr=input("请输入最好区间（[a,b]形式）：");
            X(:,vec(i))=Int2Max(X(:,vec(i)),arr(1),arr(2));
        end
    end
end
disp("正向化已完成!");

%% 标准化

disp('---正在进行标准化---');
%检查有没有负元素
isNeg=0;
for i=1:n
    for j=1:m
        if(X(i,j)<0)
            isNeg=1;
        end
    end
end
if(isNeg==1)
    X_min=min(X,[],1);
    X_max=max(X,[],1);
   stand_X=X-repmat(min_X,n,1)./(repmat(X_max,n,1)-repmat(X_min,n,1));
else
    X_square=(X.*X);
    X_sum=sum(X_square,1).^0.5;
    X_stand=X./repmat(X_sum,n,1);
end
disp('标准化已完成!储存于X_stand中');

%% 用距离法打分
disp('---正在使用距离法打分---');
X_max=max(X_stand,[],1);
X_min=min(X_stand,[],1);
S=(X-repmat(X_min,n,1))./(X_max-X_min);

%% 用优劣解打分
disp('---正在使用优劣解打分---');
tmp=ones(m);%创建全为一的数组
w_j=tmp(:,1);%默认权值1
is_need_w=input('是否需要指定权值，是请输入1，否请输入0：');
if(is_need_w==1)
    w_j=input('请输入各项权值：（向量列格式,如[0.1;0.2;0.3;0.4]）');
end

Z_plus=repmat(X_max,n,1);
Z_sub=repmat(X_min,n,1);
D_plus=sum(((X_stand-Z_plus).^2)*w_j,2).^0.5;
D_sub=sum(((X_stand-Z_sub).^2)*w_j,2).^0.5;

S=D_sub./(D_sub+D_plus);

%% 将结果归一化
res_topsis=S./sum(S)
writematrix(res_topsis,'res_topsis.xlsx');%写入文件
```

# 熵权法

## shangquanfa.m

```matlab
%%熵权法
%clear,clc
X=readmatrix('D:\Excel文档\Excel01.xlsx');%读取Excel文档

%% 正向化
disp('---正在进行正向化---');
[n,m]=size(X);
vec=input('请输入需要正向化的列（若不需要输入-1，按向量格式输入，如[a,b,c]表示a,b,c要正向化）：');
if(vec~=-1)
    for i=1:size(vec,2)
        
        flag=input(['对于第',num2str(vec(i)),'列，极小型输入1，中间型2，区间型3：']);
        if(flag==1)%极小型
            X(:,vec(i))=Min2Max(X(:,vec(i)));
        elseif(flag==2)%中间型
            best=input('best=');
            X(:,vec(i))=Mid2Max(X(:,vec(i)),best);
        elseif(flag==3)%区间型
            arr=input("请输入最好区间（[a,b]形式）：");
            X(:,vec(i))=Int2Max(X(:,vec(i)),arr(1),arr(2));
        end
    end
end
disp("正向化已完成!");

%% 标准化

disp('---正在进行标准化---');
%检查有没有负元素
isNeg=0;
for i=1:n
    for j=1:m
        if(X(i,j)<0)
            isNeg=1;
        end
    end
end
if(isNeg==1)
    X_min=min(X,[],1);
    X_max=max(X,[],1);
   stand_X=X-repmat(min_X,n,1)./(repmat(X_max,n,1)-repmat(X_min,n,1));
else
    X_square=(X.*X);
    X_sum=sum(X_square,1).^0.5;
    X_stand=X./repmat(X_sum,n,1);
end
disp('标准化完成!');

%% 信息熵
disp('---正在用熵权法确定权值---');
P=X_stand./repmat(sum(X_stand),n,1);
%手动将0改为0.00001
for i=1:n
    for j=1:m
        if(P(i,j)==0)
            P(i,j)=0.00001;
        end
    end
end
X_H=sum(-P.*log(P));%信息熵（以下套公式
e_j=X_H./log(n);
d_j=1-e_j;
%进行归一化，获得熵权
disp('权值为：');
w=d_j./sum(d_j);
disp(w)
```

## Min2Max.m

```matlab
function [res] = Min2Max(X)
%MIN2MAX （熵权法）将极小型正向化
% 传入待正向化的向量，返回正向化后结果
%   用最大值减去每一项
res=max(X)-X;
end

```

## Mid2Max.m

```matlab
function [res] = Mid2Max(X,best)
%（熵权法）将中间型正向化
% MIN2MID X为一个列向量，best是最好中间值
M=max(abs(best-X));
res=1-abs(best-X)/M;

end
```

## Int2Max.m

```matlab
function [res] = Int2Max(X,a,b)
%MINTOMID 将区间型向量正向化
%   此处显示详细说明
M=max(a-min(X),max(X)-b);
for i=1:size(X)
    if(X(i)>=a&&X(i)<=b)
        X(i)=1;
    elseif(X(i)<a)
        X(i)=1-(a-X(i))/M;
    elseif(X(i)>b)
        X(i)=1-(X(i)-b)/M;
    end
end
res=X;
end
```

# 线性规划

![25415fc02fea6580e451a3055604f79e](img/25415fc02fea6580e451a3055604f79e.png)

```matlab
f=[-40;-30];
A=[1 -1 0 240; 1 0 -1 120]';
b=[6;-1;-1;1200];
lb=[0;0];
ub=[+inf;+inf];
[x,val]=linprog(f,A,b,[],[],lb,ub)
```

# 整数规划

![4e8f856a5d0f09f12189b2a6cc7f0e8a](img/4e8f856a5d0f09f12189b2a6cc7f0e8a.png)

```matlab
```

# 非线性规划

![0F2DE644A41C88AFE5BC9F5802854C84](img/0F2DE644A41C88AFE5BC9F5802854C84.png)

# 算法

## 异常值用均值代替

```matlab
for j=7:9
    A=ree(:,j);
    B=filloutliers(A,'nearest','mean');
    ree(:,j)=B;
end
```

## 随机数

`X = randi(imax)` 返回一个介于 `1` 和 `imax` 之间的伪随机整数标量。

`X = randi(imax,n)` 返回 `n`×`n` 矩阵，其中包含从区间 [`1`,`imax`] 的均匀离散分布中得到的伪随机整数。

` `

# Topsis

```matlab
%X=[99,0.0100;100,0.0120;98,0.0400;97,0.0330]

%% 正向化
disp('---正在进行正向化---');
[n,m]=size(X);
vec=input('请输入需要正向化的列（若不需要输入-1，按向量格式输入，如[a,b,c]表示a,b,c要正向化）：');
if(vec~=-1)
    for i=1:size(vec,2)
        
        flag=input(['对于第',num2str(vec(i)),'列，极小型输入1，中间型2，区间型3：']);
        if(flag==1)%极小型
            X(:,vec(i))=Min2Max(X(:,vec(i)));
        elseif(flag==2)%中间型
            best=input('best=');
            X(:,vec(i))=Mid2Max(X(:,vec(i)),best);
        elseif(flag==3)%区间型
            arr=input("请输入最好区间（[a,b]形式）：");
            X(:,vec(i))=Int2Max(X(:,vec(i)),arr(1),arr(2));
        end
    end
end
disp("正向化已完成!");

%% 标准化

disp('---正在进行标准化---');
%检查有没有负元素
isNeg=0;
for i=1:n
    for j=1:m
        if(X(i,j)<0)
            isNeg=1;
        end
    end
end
if(isNeg==1)
    X_min=min(X,[],1);
    X_max=max(X,[],1);
   stand_X=X-repmat(min_X,n,1)./(repmat(X_max,n,1)-repmat(X_min,n,1));
else
    X_square=(X.*X);
    X_sum=sum(X_square,1).^0.5;
    X_stand=X./repmat(X_sum,n,1);
end
disp('标准化已完成!储存于X_stand中');

%% 用距离法打分
disp('---正在使用距离法打分---');
X_max=max(X_stand,[],1);
X_min=min(X_stand,[],1);
S=(X-repmat(X_min,n,1))./(X_max-X_min);

%% 用优劣解打分
disp('---正在使用优劣解打分---');
tmp=ones(m);%创建全为一的数组
w_j=tmp(:,1);%默认权值1
is_need_w=input('是否需要指定权值，是请输入1，否请输入0：');
if(is_need_w==1)
    w_j=input('请输入各项权值：（向量列格式,如[0.1;0.2;0.3;0.4]）');
end

Z_plus=repmat(X_max,n,1);
Z_sub=repmat(X_min,n,1);
D_plus=sum(((X_stand-Z_plus).^2)*w_j,2).^0.5;
D_sub=sum(((X_stand-Z_sub).^2)*w_j,2).^0.5;

S=D_sub./(D_sub+D_plus);

%% 将结果归一化
res_topsis=S./sum(S)
writematrix(res_topsis,'res_topsis.xlsx');%写入文件
```

# 2020C

```matlab
%clc,clear
data=readmatrix("D:\数学建模\2020C\C\表1.xlsx");
result1=zeros(2,11);
for i=1:2
    %原始数据
    m=find(data(:,1)==i);%企业数据位置
    re=data(m(1):max(m),:);%同一公司数据
    %re=sortrows(re,[3 4 5]);%按时间顺序排序
    void=find(re(:,6)==2);%作废记录
    void=size(void,1);
    valid=size(m,1)-void;%有效记录

    %筛除完作废发票与有效发票中小于0的数据
    mm=find(re(:,6)==1&re(:,5)>0);%企业数据位置
    ree=re(mm,:);%筛除完作废发票与有效发票中小于零的数据
    %ree=sortrows(ree,[3,4,5]);%按时间排序

    %计算结果
    smonth(1,:)=ree(1,3:4);%发票起始日期
    smonth(2,:)=ree()


end

```

# 图论



```matlab
%% 绘制数字标号图
s = [1 2 3];%起点（标号从一开始）
t = [4 1 2];%终点
w = [5 2 6];%权重（1到4权重为5）
% 绘制带权重的图
G = graph(s,t,w);
plot(G,'EdgeLabel',G.Edges.Weight,'LineWidth',2);%调用plot绘制带权重的图
G2 =graph(s, t);
plot(G2,'LineWidth',2);%绘制不带权重的图
set( gca,'xtick',[],'YTick',[]);%去掉坐标轴上的数字

%% 绘制字符串标号的图
s = {'北京','上海','广州','深圳','上海'};
t = {'上海','广州','深圳','北京','深圳'};
w = [10 65 3 90 60];
G = graph(s, t, w);
plot(G, 'EdgeLabel',G.Edges.Weight,'linewidth',2);
set( gca,'xtick',[],'YTick',[]);%去掉坐标轴上的数字

%% 重点 绘制邻接矩阵的图
c = [0 15 10 20 0 0 0 0;
     0 0 0 0 7 10 0 0;
     0 0 0 0 0 8 2 0;
     0 0 0 0 0 0 18 0;
     0 0 0 0 0 0 0 6;
     0 0 0 0 0 0 0 6;
     0 0 0 0 0 0 0 16;
     0 0 0 0 0 0 0 20;
     0 0 0 0 0 0 0 0;];
view(digraph(c, [], 'ShowWeights','on'));% 编译错误

%% Dijkstra
% 注意Matlab中图从1开始编号
s = [1 1 2 2 8 8 3 9 3 3 7 4 4 6];
t = [2 8 8 3 9 7 9 7 4 6 6 6 5 5];
w = [4 8 3 8 1 6 2 6 7 4 2 14 9 10];
G = graph(s,t,w);
plot(G,'EdgeLabel',G.Edges.Weight,'LineWidth',2);
set( gca,'xtick',[],'YTick',[]);%去掉坐标轴上的数字
[P,d] = shortestpath(G,1,5)%求解由1到5的最短路径

%% 将邻接矩阵转化为图对象graph格式
c = [0 15 10 20 0 0 0 0;
     0 0 0 0 7 10 0 0;
     0 0 0 0 0 8 2 0;
     0 0 0 0 0 0 18 0;
     0 0 0 0 0 0 0 6;
     0 0 0 0 0 0 0 6;
     0 0 0 0 0 0 0 16;
     0 0 0 0 0 0 0 20;
     0 0 0 0 0 0 0 0;];
G = digraph(c);%转化为有向图
G2 = graph(c);%转化为无向图（必须为对称矩阵）
```

## Dijkstra算法（最短路径）

![285e08b6ace39efe583662d9a525d61e](img/285e08b6ace39efe583662d9a525d61e.png)

```matlab
%% Dijkstra
% 注意Matlab中图从1开始编号
s = [1 1 2 2 8 8 3 9 3 3 7 4 4 6];
t = [2 8 8 3 9 7 9 7 4 6 6 6 5 5];
w = [4 8 3 8 1 6 2 6 7 4 2 14 9 10];
G = graph(s,t,w);
plot(G,'EdgeLabel',G.Edges.Weight,'LineWidth',2);
set( gca,'xtick',[],'YTick',[]);%去掉坐标轴上的数字
[P,d] = shortestpath(G,1,5)%求解由1到5的最短路径
```

# 网络最大流问题

## Ford Fulkerson算法

![b2aad9dfb244de1d9c76d05cf4f6c4d2](img/b2aad9dfb244de1d9c76d05cf4f6c4d2.png)

## 函数maxflow

### 图中的最大流

```matlab
s = [1 1 2 2 3 4 4 4 5 5];
t = [2 3 3 4 5 3 5 6 4 6];
weights = [0.77 0.44 0.67 0.75 0.89 0.90 2 0.76 1 1];
G = digraph(s,t,weights);
plot(G,'EdgeLabel',G.Edges.Weight,'Layout','layered');
```

![Figure contains an axes object. The axes object contains an object of type graphplot.](https://ww2.mathworks.cn/help/examples/matlab/win64/MaximumFlowInGraphExample_01.png)

确定从节点 1 到节点 6 的最大流。

 Get 

```matlab
mf = maxflow(G,1,6)
mf = 1.2100
```



