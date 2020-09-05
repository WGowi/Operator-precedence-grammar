# Operator-precedence-grammar

C++读取文件，求解firstvt集与lastvt集，构建算符优先关系表，打印文法分析过程，实现算符优先文法

[toc]

## 概述    

算符优先分析法(Operator Precedence Parse)是仿效四则运算的计算过程而构造的一种语法分析方法。算符优先分析法的关键是比较两个相继出现的终结符的优先级而决定应采取的动作。

​    优点：简单，有效，适合表达式的分析。

​    缺点：只适合于算符优先文法，是一个不大的文法类。



## FIRSTVT集和LASTVT集

**FIRSTVT集**

**定义**：FIRSTVT(P)={a|P=>a…,或P=>Qa…,a属于VT,Q 属于VN}

**求法**：

  若P→a…或P→Qa…, 则a属于FIRSTVT(P);

  若P→Q…, 则FIRSTVT(Q)含于FIRSTVT(P);

  直至FIRSTVT(P)不再增大。

**LASTVT集**

**定义**：LASTVT(P)={a|P=>...a,或P=>…aQ,a含于VT,Q 含于VN}

**求法**：

  若P→...a或P→…aQ, 则a属于LASTVT(P);

  若P→...Q, 则LASTVT(Q)含于LASTVT(P);

  直至LASTVT(P)不再增大。



## 构造算符优先关系表

以以下文法为例：

​    E→E+T|T

​    T→T*F|F

​    F→(E)|i

 

**终结符之间的优先关系**

对算符文法G, a,b属于VT 定义

(1)a=b: G中有P→. . .ab. . .或P→. . .aQb. . .

(2)a<b: G中有P→. . .aQ. . .且Q=>b…或Q=>Rb...

(3)a>b: G中有P→. . .Qb. . . 且Q=>. ..a或Q=>…aR



**算符优先关系表的构造**

(1) 在文法中添加E→#E#。

(2) 求出FIRSTVT和LASTVT集

![](https://gowi-picgo.oss-cn-shenzhen.aliyuncs.com/20200905114909.png)



(3) 找出所有终结符，并画出关系表的结构

- 从文法中找出形为aQb（终结符+非终结符+终结符）和ab（终结符+终结符）的部分，本例中为(E)和#E#，然后在(和)与#和#相应的表格填等于号。
-  从文法中找出形为aQ（终结符+非终结符）的部分，a与Q的FIRSTVT集合中每一个元素在表格中的交叉点填小于号。
- 从文法中找出形为Qa（非终结符+终结符）的部分， Q的LASTVT集合中每一个元素与a在表格中的交叉点填大于号。

![img](https://img-blog.csdn.net/20180513191429699)



## 构计算分析过程

初始时，输入指针指向输入串的第一个符号，#入栈;然后比较栈顶终结符a和输入符号b的优先关系:
1.如a=b,且都是#，输入串合法，分析结束。
2.如a<b或a=b, b入栈，输入指针右移。
3.如a>b,寻找位于栈顶的包含a的最小的可规约串(最左素短语) ,
3.1如果找到，将该串规约。
3.2如果未找到，输入串非法，分析结束。
4.如a和b不存在优先关系，输入串非法，分析结束。

![](https://gowi-picgo.oss-cn-shenzhen.aliyuncs.com/EC58F0F92DDBA8D5D1ABAFB2D9CCE744.jpg)



## 实现过程

![](https://gowi-picgo.oss-cn-shenzhen.aliyuncs.com/Untitled.png)

## 
