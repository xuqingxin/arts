# ARTS Week 3

## Algorithm
[Median of Two Sorted Arrays](https://github.com/xuqingxin/leetcode/blob/master/Algorithms/0004-Median.Of.Two.Sorted.Arrays.md)


## Review
### 软件开发的15个基本定律

原文链接：[
15 Fundamental Laws of Software Development](
https://exceptionnotfound.net/fundamental-laws-of-software-development/)

文章分享了15个软件开发中的定律，并对这些定律做了简单的解释。

#### 1. 奥卡姆剃刀法则(Occam's Razor)
> 在所有的竞争假设中，应该选择假设最少的那个。

这个法则和Unix中的"KISS"原则有点类似，如果一件事有多个选择的话，那就选简单的那个。

#### 2. 汉隆剃刀法则(Hanlon's Razor)
> 能解释为愚蠢的，就不要解释为恶意。

很多人会不自觉得犯错，他们并不是有意要做破坏，而是自己能力不足。因此不要假设别人有恶意，而是要假设他们是无知，并且帮忙他们克服这个无知。

#### 3. 帕累托原则(The Pareto Principle)
> 80%的问题来源于20%的原因。

最快的一次性解决很多问题的方法就是找到他们共同的根源并修复它们。

#### 4. 邓宁克鲁格效应(Dunning-Kruger Effect)
> 能力不足的人往往会错误地高估他们实际的能力。

人们在做不擅长的工作时往往会认为自己很擅长目前的工作，并且没有足够的能力认识到他们实际上并不擅长。

#### 5. 莱纳斯法则(Linus's Law)
> 如果有足够多的眼睛，所有的bug都将无所遁形。

用另外的话来讲，如果你发现不了问题，那就让其他人来帮忙。这也是为什么在某些时候，类似结对编程的概念行得通的原因。

#### 6. 鲁棒性原则或波斯托法则(Robustness Principle (AKA Postel's Law))
> 保守输出，自由输入。

John Postel最初将它作为实现TCP的一个原则。

#### 7. Eagleson法则(Eagleson's Law)
> 任何自己的代码如果6个月或更长时间没去看的话，就如同是其他人写的一样。

如果你离开了某个项目几个月之后，重新加入进来，之前你写的代码就是别人的代码了，现在你负责改善它。

#### 8. 彼得原则(Peter Principle)
> 确定一个岗位的候选人往往基于这个候选人在他当前职位上的表现，而不是基于这个岗位需要的能力。

简单来说，就是组织中员工不断迁升，最终趋向于上升到他所不能胜任的岗位（如果他能胜任目前的岗位，就会被继续提拔）。

#### 9. 呆伯特的原则(Dilbert Principle)
> 没有能力的员工将比有能力的员工更能提拔到管理岗位，从而将他们从实际工作中去除，以减少他们可能造成的危害。

#### 10. 霍夫斯塔特定律(Hofstadter's Law)
> 即使你考虑到了霍夫施塔特定律，项目的实际完成时间总是比预期的要长。

#### 11. 90-90法则(The 90-90 Rule)
> 前 90％的代码占用了10％的开发时间，其余的10％代码占用了90％的开发时间。

这也许解释了为什么那么多软件项目最后都超预算。

#### 12. 帕金森法则(Parkinson's Law)
> 工作量总是会填满其所需的时间。

我们在评估的时候，总会有理由让评估的工作量尽可能得大。

#### 13. 赛尔法则(Sayre's Law)
> 争议的强度总是和价值成反比。

也就是说：重要性越少的事情，人们越有热情去争议。

#### 14. 帕金森琐碎法则(Parkinson's Law of Triviality (AKA Bikeshedding))
> 在任何议程项目上所花费的时间与金钱之和成反比。


在讨论非常专业而且金额庞大的事情时，一般人由于缺乏专业知识，不敢随便发言，以免失言，贻笑大方，因此多半都会肯定（或逃避）该重大方案，而提些与主题无关的鸡毛蒜皮小事。相对的，对于简单的琐碎小事，由于平常大家都会接触到而且有相当的认识，反而意见特别多，帕金森称此现象为琐碎定律。

#### 15. 好辩法则(Law of Argumentative Comprehension)
> 人们越理解某事，他们就越愿意去争论，他们也越好这口。

这是作者用这个法则来简化塞尔法则和帕金森琐碎法则的结合体。


## Tip
### C#调用C++ DLL函数的PInvoke 签名问题

这周使用C#开发一个GPIO模块，在调用使用C++编写的SDK时，VS抛了一个错误，提示内容为函数的”调用导致堆栈不对称。原因可能是托管的 PInvoke 签名与非托管的目标签名不匹配。请检查 PInvoke 签名的调用约定和参数与非托管的目标签名是否匹配。“

查询了资料后，发现这是因为VS中默认有个选项是选中的，只要把它去掉就可以正常运行了。这个选项是

调试->窗口->异常设置->Managed Debugging Assistants->PInvokeStackImbalance


## Share
### 一个线程罢工的诡异事件
原文链接：[一个线程罢工的诡异事件](
https://crossoverjie.top/2019/03/12/troubleshoot/thread-gone/)

作者通过这篇文章清楚地还原了如何通过阅读源码定位并修复了线上应用的一整个过程。

看了这篇文章，我觉得作者解决问题很有方法论，不是东一榔头西一棒地胡乱猜测，而是通过一系列的，系统的方法，不断逼近问题，找到根源，然后修复它。

首先，作者理解清楚了业务的逻辑，知道它是干什么的。
然后，定位问题，发现线程都在等待。
接着，检查现有代码，结果没发现问题。不过发现原来的代码使用了一个开源组件。
因为，没有发现，所以请教同事，在同事的帮助下，通过本地模拟，重现了线上的现象。发现是一个线程抛了异常。
最后，通过加try/catch，解决问题。

一般人到了这里就结束了，既然问题解决了，那就没必要再多花时间了。但是作者没有止步于此，他进一步去阅读组件源码，弄不明白了为什么线程抛了异常，代码就不工作了。

这篇文章给了我两点启发：

1. 有了系统性解决问题的方法，即使在工作中遇到了之前没碰到过的问题，也不会茫然无措，根据方法论进行解决，一般来说都能找到问题
2.  凡事不能满足于解决问题。有时候问题解决了，但是我们并不清楚为什么这么做能解决问题。如果每次我们都能有打破沙锅问到底的精神，那么我们的水平就会快速提高，不仅知其然，而且知其所以然。今后解决问题的能力也就越来越高。