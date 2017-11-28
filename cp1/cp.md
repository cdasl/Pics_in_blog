# 编译原理书面作业解析 1

## 3. 有正则表达式 `(a|b)*abb(a|b)` 
### 3.1 使用Thompson构造法为其构造NFA，写出NFA处理符号串ababbab过程中的状态转移序列。
**Solution:** Thompson构造法的全称为<font color=#66ccff>McMaughton-Yamada-Thompson算法（龙书P100） </font>,构造过程如下：
(1). 分解题干中的正则表达式，本题中，可分为三部分,即
`a=c=(a|b)*, b=abb`。基本的构造规则见龙书p101。
(2). 画出每一部分对应的NFA，如下
![](https://github.com/cdasl/Pics_in_blog/blob/master/cp1/cp3.1.a.png?raw=true)a, c（7是终态）
![](https://github.com/cdasl/Pics_in_blog/blob/master/cp1/cp3.1.b.png?raw=true)b

(3). 拼接，得![aha](https://github.com/cdasl/Pics_in_blog/blob/master/cp1/3.1.png?raw=true)
状态转移序列就顺着NFA走就行了。
### 3.2 使用子集构造法将3.1得到的NFA转换为DFA，写出分析ababbab过程中的状态转移。
**Solution:**
(1). 计算等价类的开始状态 `A=ε-closure(0)`，计算方法就是看NFA中顺着 `0` 走能到达的所有节点，此处 `ε-closure(0)={0, 1, 2, 3, 7}`
(2). 计算 `D-trans(A, a)` ，这个的意思是求出 **A** 状态中的所有节点在输入 a 以后能到达的所有节点。而 `D-trans(A,a)=ε-closure(move(A, a))`，`move(A, a)={4, 8}`，也就是说，最后要求的是 
`ε-closure({4, 8})=ε-closure(4)∪ε-closure(8)={1, 2, 3, 4, 6, 7, 8}=B`
剩下的内容以此类推，当出现两个集合相同的时候，合并为一个状态。
求完所有的 `ε-closure(0)` 集合后，如下（图就不画了......）
State | a | b
:--:|---|----
A | B  | C
B | B  | D
C | B  | C
D | B  | E
E | F  | G
F | F  | H
G | F  | G
H | F  | I
I | F  | G

### 3.3 最小化3.2得到的DFA
**Solution:** 在上面的表格中，找到除 `State` 以外完全相同的 n 行，它们就可以合并成一个状态，最后的DFA如下:
![](https://github.com/cdasl/Pics_in_blog/blob/master/cp1/3.3.png?raw=true)

To be continued...



