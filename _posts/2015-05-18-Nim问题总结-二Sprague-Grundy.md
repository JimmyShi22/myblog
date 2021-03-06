---
layout: default
title: Nim问题总结-二Sprague-Grundy
comments: true
kind: OJ
---
##Sprague-Grundy 函数（转）
###声明
   笔者最近意外的发现 笔者的个人网站 http://tiankonguse.com/ 的很多文章被其它网站转载，但是转载时未声明文章来源或参考自 http://tiankonguse.com/ 网站，因此，笔者添加此条声明。
    郑重声明：这篇记录《 博弈论之Sprague-Grundy 函数》转载自 http://tiankonguse.com/ 的这条记录：http://tiankonguse.com/record/record.php?id=676

###前言

sg函数很神奇的，很多人看到它就很害怕的样子．

###正文

上一篇的文章里我们仔细研究了Nim游戏，并且了解了找出必胜策略的方法。
但如果把Nim的规则略加改变，你还能很快找出必胜策略吗？

比如说：有n堆石子， 每次可以从第1堆石子里取1颗、2颗或3颗，可以从第2堆石子里取奇数颗，可以从第3堆及以后石子里取任意颗……这时看上去问题复杂了很多，但相信你如果 掌握了本节的内容，类似的千变万化的问题都是不成问题的。

现在我们来研究一个看上去似乎更为一般的游戏：给定一个有向无环图和一个起始顶 点上的一枚棋子，两名选手交替的将这枚棋子沿有向边进行移动，无法移动者判负。
事实上，这个游戏可以认为是所有Impartial Combinatorial Games的抽象模型。
也就是说，任何一个ICG都可以通过把每个局面看成一个顶点，对每个局面和它的子局面连一条有向边来抽象成这个“有向图游戏”。

下 面我们就在有向无环图的顶点上定义Sprague-Garundy函数。

首先定义mex(minimal excludant)运算，这是施加于一个集合的运算，表示最小的不属于这个集合的非负整数。
例如mex{0,1,2,4}=3、mex{2,3,5}=0、mex{}=0。

对于一个给定的有向无环图，定义关于图的每个顶点的Sprague-Garundy函数g如下：g(x)=mex{ g(y) | y是x的后继 }。

来 看一下SG函数的性质。
首先，所有的terminal position所对应的顶点，也就是没有出边的顶点，其SG值为0，因为它的后继集合是空集。
然后对于一个g(x)=0的顶点x，它的所有后继y都满足 g(y)!=0。
对于一个g(x)!=0的顶点，必定存在一个后继y满足g(y)=0。

以上这三句话表明，顶点x所代表的postion 是P-position当且仅当g(x)=0（跟P-positioin/N-position的定义的那三句话是完全对应的）。
我们通过计算有向无环图 的每个顶点的SG值，就可以对每种局面找到必胜策略了。
但SG函数的用途远没有这样简单。
如果将有向图游戏变复杂一点，比如说，有向图上并不是只有一枚棋 子，而是有n枚棋子，每次可以任选一颗进行移动，这时，怎样找到必胜策略呢？

让我们再来考虑一下顶点的SG值的意义。
当g(x)=k时， 表明对于任意一个0<=i<k，都存在x的一个后继y满足g(y)=i。
也就是说，当某枚棋子的SG值是k时，我们可以把它变成0、变成 1、……、变成k-1，但绝对不能保持k不变。
不知道你能不能根据这个联想到Nim游戏，Nim游戏的规则就是：每次选择一堆数量为k的石子，可以把它变 成0、变成1、……、变成k-1，但绝对不能保持k不变。
这表明，如果将n枚棋子所在的顶点的SG值看作n堆相应数量的石子，那么这个Nim游戏的每个必 胜策略都对应于原来这n枚棋子的必胜策略。

对于n个棋子，设它们对应的顶点的SG值分别为(a1,a2,…,an)，再设局面 (a1,a2,…,an)时的Nim游戏的一种必胜策略是把ai变成k，那么原游戏的一种必胜策略就是把第i枚棋子移动到一个SG值为k的顶点。
这听上去 有点过于神奇——怎么绕了一圈又回到Nim游戏上了。

其实我们还是只要证明这种多棋子的有向图游戏的局面是P-position当且仅当所有棋子所在的位置的SG函数的异或为0。
这个证明与上节的Bouton’s Theorem几乎是完全相同的，只需要适当的改几个名词就行了。

刚才，我为了使问题看上去更容易一些，认为n枚棋子是在一个有向图上移动。
但如果不是在一个有向图上，而是每个棋子在一个有向图上，每次可以任选一个棋子（也就是任选一个有向图）进行移动，这样也不会给结论带来任何变化。

所 以我们可以定义有向图游戏的和(Sum of Graph Games)：设G1、G2、……、Gn是n个有向图游戏，定义游戏G是G1、G2、……、Gn的和(Sum)
游戏G的移动规则是：任选一个子游戏Gi 并移动上面的棋子。
Sprague-Grundy Theorem就是：g(G)=g(G1)^g(G2)^…^g(Gn)。
也就是说，游戏的和的SG函数值是它的所有子游戏的SG函数值的异或。

再考虑在本文一开头的一句话：任何一个ICG都可以抽象成一个有向图游戏。
所以“SG函数”和“游戏的和”的概念就不是局限于有向图游戏。
我们给每个ICG 的每个position定义SG值，也可以定义n个ICG的和。
所以说当我们面对由n个游戏组合成的一个游戏时，只需对于每个游戏找出求它的每个局面的 SG值的方法，就可以把这些SG值全部看成Nim的石子堆，然后依照找Nim的必胜策略的方法来找这个游戏的必胜策略了！

回到本文开头的 问题。
有n堆石子，每次可以从第1堆石子里取1颗、2颗或3颗，可以从第2堆石子里取奇数颗，可以从第3堆及以后石子里取任意颗……
我们可以把它看作3个 子游戏，第1个子游戏只有一堆石子，每次可以取1、2、3颗，很容易看出x颗石子的局面的SG值是x%4。
第2个子游戏也是只有一堆石子，每次可以取奇数 颗，经过简单的画图可以知道这个游戏有x颗石子时的SG值是x%2。
第3个游戏有n-2堆石子，就是一个Nim游戏。
对于原游戏的每个局面，把三个子游戏 的SG值异或一下就得到了整个游戏的SG值，然后就可以根据这个SG值判断是否有必胜策略以及做出决策了。
其实看作3个子游戏还是保守了些，干脆看作n个 子游戏，其中第1、2个子游戏如上所述，第3个及以后的子游戏都是“1堆石子，每次取几颗都可以”，称为“任取石子游戏”，这个超简单的游戏有x颗石子的 SG值显然就是x。
其实，n堆石子的Nim游戏本身不就是n个“任取石子游戏”的和吗？

所以，对于我们来说，SG函数与“游戏的和”的概念不是让我们去组合、制造稀奇古怪的游戏，而是把遇到的看上去有些复杂的游戏试图分成若干个子游戏，对于每个比原游戏简化很多的子游戏找出它的SG函数，然后全部异或起来就得到了原游戏的SG函数，就可以解决原游戏了。

##思路
由于每一个石堆都有自己的减小方式，使用Sprague-Grundy的方法，将不同的石堆中石子的数量x映射成一个统一的数值变化方式，即求出对应的g(x)。
不同的石堆有自己的减小方式，继而g(x)的求法也不同。将所有石堆的g值异或求和，得到k。对于k = 0的情况，则下一次变化一定会使得k != 0，为P局面。
若 k != 0的情况（N局面），则一定存在一种方式（减小某一个石堆的数值）使得一次move之后k = 0。所以，开局的时候，拿到k != 0（N局面）的人获胜，
此人每次都将局面转化成k = 0的情况，使得另一个人无论如何move，都只能从k = 0局面转移到k != 0的局面。


步奏如下：

1.找到每个石堆的迭代关系。

2.根据x值推导g(x)。 g(x)=mex{ g(y) | y是x的后继 }. 若一个k对应生成两个或多个值，则根据SG定理，g(X) = g(x[1]) xor g(x[2]) xor … xor g(x[n])求出g(x)。（通过找规律生成g的映射方式能够大大缩短计算时间）。

3.根据输入的每个石堆的值x，计算g(x)， 并将g(x)异或求和。若结果为 0,则为P局面，先手输，若为1，位N局面，先手赢。

相关例题：http://hihocoder.com/contest/hiho46/problem/1
代码如下：

```c++
#include <iostream>
using namespace std;

int get_sg(int k)
{
	if (k == 0)
		return 0;
	else
	{
		if (k % 4 == 0)
			return k - 1;
		else if (k % 4 == 3)
			return k + 1;
		else
			return k;
	}
}

int main()
{
	int N;
	cin >> N;

	int sum = 0;
	for (int i = 0; i < N; i++)
	{
		int a;
		cin >> a;
		sum ^= get_sg(a);
	}

	if (sum)
		cout << "Alice" << endl;
	else
		cout << "Bob" << endl;

	return 0;
}
```

