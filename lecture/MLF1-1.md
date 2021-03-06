---
title: 机器学习基石作业1：part1
date: 2017-02-06 16:35:57
tags: MLF&MLT
categories: ML
---
机器学习基石课后作业1-1：对应题目1～题目14
<!-- more -->

## 机器学习基石作业1

### 问题1
Q1. 下列哪些问题适合采用机器学习的方法？
① 将数分为素数和非素数
② 信用卡交易中潜在的欺诈交易
③ 物体掉落到地面的时间
④ 流量大的十字路口信号灯最优循环方案
⑤ 确定某种特定药物的建议服用年龄

A1: 判断一个问题是否适合采用机器学习方法的三个准则：
a. 存在某种可以被学习到的潜在规律
b. 潜在规律难以被简单的定义，因此直接编写潜在规律的程序是困难的
c. 存在某些与潜在规律相关的数据（即与问题本身相关的数据）
根据上述三条准则，不难选择②④⑤

### 问题2

Q2~Q5：分辨不同问题具体属于哪一类型的机器学习问题，关键在于区分不同机器学习问题的特点。
分类1：根据输出空间$\mathbb{Y}$的不同可以分为-- ①分类问题：$\mathbb{Y}={1,2,...,K}$ ②回归问题：$\mathbb{Y}=\mathbb{R}$ ③结构学习：$\mathbb{Y}=各种结构的集合$
分类2：根据标签$y_n​$的不同可以分为--①监督学习：每个训练数据都有$y_n​$ ②无监督学习：每个训练数据都无$y_n​$ ③半监督学习：部分训练数据有$y_n​$ ④强化学习：无显示的标签，可以想成控制某个特定环境下的某个个体，通过与环境的互动，来不断改进个体的行为。更详细的定义见[强化学习](https://www.zhihu.com/question/41775291)
分类3：根据学习潜在规律函数$f$方式的不同：①批量学习：将全部有的数据喂进去获得一个模型 ②在线学习：不断慢慢喂数据来更新模型（在有新的数据进来时，无需训练之前的数据就可以调整模型）③主动学习：策略性的选择数据，具有甄别数据好坏的能力

Q2：通过不同的决策方法并根据结果作为反馈来不断提高下棋水平？

A2：强化学习（reinforcement learning）

Q3：将没有任何标签的书籍进行分类？

A3：无监督学习（unsupervised learning）

Q4：通过1000张有脸的照片和10000张无脸的照片来区分其他照片中是否有脸？

A4：监督学习（supervised learning）

Q5：有选择性的安排实验，快速确定治疗癌症药物的功效？

A5：主动学习（active learning）--原因不是很清楚，可能在选择性安排实验

### 问题3

Q6~Q8：主要涉及训练样本外的数据的误差的分析。
令$\mathbb{X}={x_{1},x_2,...,x_N,x_{N+1},...,x_{N+L}}$和$\mathbb{Y}=\{-1,+1\}$。此外，我们假设训练集$D=\{(x_n,y_n)\}_{n=1}^N$，其中$y_n\in\mathbb{Y}$，测试集的输入为$\{x_{N+l}\}_{l=1}^L$，定义训练集外误差(OTS)为（其中$f$为潜在目标函数，$g$为似然函数）：
$$
E_{OTS}(g,f)=\frac{1}{L}\sum_{l=1}^L[g(x_{N+l})\neq f(x_{N+l})]
$$
Q6：假设对于全部的$x$，$f(x)=+1$，和$g(x)=+1\ (x=x_k中k为奇数)，g(x)=-1\ (其他情况)$，求$E_{OTS}(g,f)=?$？

A6：其实题目本质上可以转换为求$N+1$到$N+L$有多少个偶数。则可以简单的举特例可以得到结果，也可以进行具体的推导，得到的结果为：$(\lfloor\frac{N+L}{2}\rfloor-\lfloor\frac{N}{2}\rfloor)$。所以最终结果为$\frac{1}{L}\times(\lfloor\frac{N+L}{2}\rfloor-\lfloor\frac{N}{2}\rfloor)$

Q7：如果存在目标函数$f$对于每一个在训练集中的数据$\{(x_n,y_n)\}_{n=1}^N\in D$均有$f(x_n)=y_n$，则为无噪干扰情况。对于一切可能的$f: \mathbb{X}\to\mathbb{Y}$，存在多少种可能的$f$，使得在训练集$D$上满足无噪干扰情况。（注：如果函数$f_1=f_2\ for \forall x\in \mathbb{X}$，则认为两个函数相同）？

A7：显然，$f$的不同取决于$(x_{N+1},y_{N+L}),...,(x_{N+L},y_{N+L})$，则共有$2^L$种可能的输出$y_{N+1},...,y_{N+L}$结果。

Q8：一个确定的算法$\mathbb{A}$定义为以训练集$D$为输入，输出一个似然函数$g$。如果对于全部满足Q7条件的$f$产生的可能性是相等的，则对于两个算法$\mathbb{A}_1$和$\mathbb{A}_2$，哪条等式成立？

A8：由于不管哪种算法$\mathbb{A}​$产生的似然函数$g​$对训练集之外的数据$(x_{N+1},...,x_{N+L})​$产生的结果$(y_{N+1},...,y_{N+L})​$只可能是$2^L(\pm1的全部可能)​$中的一种，由于$E_{OTS}(g,f)​$仅和训练集$D​$之外的数据有关，因此完全可以将$g​$视为全部可能的$f​$(总共$2^L​$种)中的一种而不影响最终结果。因此，问题就转换为全部$f​$中的任意两个$f_1​$和$f_2​$关于$E_{OTS}​$的问题了。则显然有$E_f\{E_{OTS}(f_1,f)\}=E_f\{E_{OTS}(f_2,f)\}​$成立。
​	可以通过一个简单的例子来说明：$L=2$的情况，$f_1$预测的结果为$\{-1,-1\}$，$f_2$预测的结果为$\{+1,+1\}$，则$f$全部的结果有四种，代入计算下数学期望可以发现上式成立。（可以这样思考，从$f_1$出发，改变1个--对应err=1，改变2个--对应err=2和从$f_2$出发，改变1个，改变2个）

### 问题4

Q9~Q12：主要考察对容器模型的理解，考虑一个含有无限弹珠的容器(仅有橙色和绿色两种类型弹珠)，假设容器中橙色弹珠的比例为$\mu$，从容器中抽取10颗弹珠做为样本，该样本中橙子弹珠的比例为$\nu$

Q9：如果$\mu=0.5$，则使得$\nu=\mu$的概率为多少？

A9：概率论里面的知识，$C_{10}^5 0.5^50.5^5=0.246\approx 0.24$

Q10：如果$\mu=0.9$，则使得$\nu=\mu$的概率为多少？

A10：同理，$C_{10}^9 0.9^90.1^1=0.387\approx 0.39$

Q11：如果$\mu=0.9$，则使得$\nu\leq 0.1$的概率为多少？

A11：$C_{10}^1 0.9^{1}0.1^9+C_{10}^0 0.9^{0} 0.1^{10}=9.1\times 10^{-9}$

Q12：如果$\mu=0.9$，则通过Hoeffding不等式获得$\nu\leq 0.1$的上界是多少？

A12：Hoeffding不等式：
$$
P[|\nu-\mu|>\epsilon]\leq2exp(-2\epsilon^2N)
$$
上式中根据题意可知$\epsilon=0.8$，代入可知$P[|\nu-\mu|>\epsilon]\leq5.52\times10^{-6}$，可以与Q11中的结果对比可见，该概率明显大于上述值。从而也可以说明Hoeffding不等式获得的界限要远大于真实情况，从侧面反映了后面几章中对于样本估计和真实情况近似可接受度的说明（即通过Hoeffding不等式获得的$\mu$和$\nu$的接近度要远小于真实情况）。

### 问题5

Q13~Q14：一个袋子里含有无穷多的骰子(6面)，这些骰子共有四种不同类型，每种类型出现的概率相等：
a. 所有偶数面为橙色，奇数面为绿色
b. 所有偶数面为绿色，奇数面为橙色
c. 数字1-3面为橙色，数字4-6面为绿色
d. 数字1-3面为绿色，数字4-6面为橙色

Q13：如果从袋子中取出5颗骰子，则获得的5颗骰子数字1面全为橙色的概率？

A13：数字1为橙色的有(b)(c)，因此取出一个的概率为0.5，所以：$P=0.5^5=\frac{8}{256}$

Q14：如果从袋子中取出5颗骰子，存在某个面5颗骰子均为橙色的概率？

A14：全部的可能为组合{(a)(c), (a)(d), (b)(c), (b)(d)}，则对应的结果为：$P=0.5^5\times 4-0.25^5\times 4=\frac{31}{256}$（其中的0.25是指单从一种类型取出时情况---因为在组合中存在一些重复情况）

