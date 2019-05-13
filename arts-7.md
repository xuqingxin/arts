# ARTS Week 7

## Algorithm
[Palindrome Number](https://github.com/xuqingxin/leetcode/blob/master/Algorithms/0009-Palindrome.Number.md)

## Review
### 再见了，面向对象编程
原文链接：[Goodbye, Object Oriented Programming](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53)

这篇文章依次阐述了面向对象编程的三大支柱继承，封装和多态存在的问题，最后提出了解决方案：函数式编程，并推荐了作者的Facebook小组[
Learn Elm Programming](https://www.facebook.com/groups/learnelm/)。

#### 继承：倒下的第一根柱子
##### 香蕉猴子丛林问题
作者通过亲身经历的项目，说明了为了重用某 一个类，需要把这个类的父类，父类的父类，...，直至最基础的父类都包含进项目，同时还需要把这条继承链条上所有用到的其他相关类也包含进项目，否则编译通不过。
这就像你需要一个香蕉，最后得到的是一只手握香蕉的大猩猩以及整个丛林。
解决办法是有的，那就是使用包含及委托的模式。

##### 菱形继承问题
假如有基类A，子类B，C都继承自A。现在有一个类D，需要同时继承自B和C，这样A，B，C，D这四个类就形成了一个菱形。在现实生活中，这是合理的场景，比如A是电器设备，B是扫描仪，C是打印机，D是集打印扫描于一体的机器。但是绝大多数面向对象编程语言都不支持这种情况。
解决办法同样是使用包含及委托的模式。

##### 脆弱的基类问题
作者曾经写了一个继承自其他类的子类。这个子类一直工作得好好的，直到有一天，它忽然工作不正常了。而作者没有对代码做任何改动，唯一的解释就是基类发生了变化。作者举了一个的例子说明了这个问题。

这是基类。
```Java
import java.util.ArrayList;
public class Array{
    private ArrayList<Object> a = new ArrayList<Object>(); 
    public void add(Object element)  {
        a.add(element);  
    }
    public void addAll(Object elements[])  {
        for (int i = 0; i < elements.length; ++i)    
            a.add(elements[i]); // this line is going to be changed
    }
}
```

这是作者写的子类。
```Java
public class ArrayCount extends Array {
    private int count = 0;
 
    @Override
    public void add(Object element)  {
        super.add(element);
        ++count;
    }
 
    @Override
    public void addAll(Object elements[]) {
        super.addAll(elements);
        count += elements.length;
    }
}
```
子类的作用是维护一个数值用来记录加入数值的对象个数。目前一些都很正常。但是假设某天基类做了如下改动：
```Java
public void addAll(Object elements[])  {
    for (int i = 0; i < elements.length; ++i)
        add(elements[i]); // this line was changed
}
```
仅仅修改了一行代码，子类的逻辑就马上变得不正确了。

解决办法？没有。这个巨大的问题永远都会威胁着宝贵的继承这个支柱。

##### 层级问题
假设我们要开公司，为了保存公司档案，我们是应该建一个叫”文档“的文件夹，然后在里面再建一个叫”公司“的文件夹还是先建一个叫”公司“的文件夹，然后在里面再建一个叫”文档“的文件夹？

这两个办法都可以，但是哪一个是对的？或者是最好的？

类别层级问题对于基类具有广泛性而子类具有特殊性这样情况是适用的。但是对于基类和子类相对随意或者可以互换位置的情况下，这种模型就不适用了。
解决办法也有，使用标签。它们没有层级关系，都是平级的。

#### 封装：倒下的第二根柱子
##### 引用问题
为了效率考虑，代码对对象的访问，使用引用而不是值。在带参数构造函数里，对象可以被转入构造函数。但是被传入的对象是不安全的。因为调用构造函数的代码有了被传入对象的引用。
解决办法：构造函数只能深度克隆被传入的对象。

#### 多态：倒下的第三根柱子
多态在面向对象编程中永远都是一个配角，这倒不是说多态不好，而是我们根本不需要为了多态而使用面向对象。使用接口，我们一样可以使用多态，不需要面向对象这个大包袱。

#### 怎么办？
既然面向对象编程有这么问题，怎么办呢？作者给出了解决方案：函数式编程。在文章最后，作者还给出了他在Facebook的小组链接[
Learn Elm Programming](https://www.facebook.com/groups/learnelm/)。

==================================================

作者提到的继承问题的确是事实，不过也没那么严重，作者也提到了解决办法。至于封装问题，老实说我没理解。而多态，我觉得作者没提到点子上，或者说根本就没问题。

文章结尾提到的函数式编程的确是一个编程的一大领域，且这些年有越来越流行的趋势，但是后面紧接着附上作者在Facebook的工作组链接，让人有为了宣传作者自己的工作而特意写的这篇文章的嫌疑。

## Tip
### 在Github里如何找到自己Watch的项目
对于Github里好的项目，我们可以Watch也可以Star，还可以Fork。关于这三者的区别，可以看下这篇文章 [如何用好 github 中的 watch、star、fork](https://www.jianshu.com/p/6c366b53ea41)

在Github上Star，或者Fork了某个项目，可以通过点击页面上右上角的用户头像，在弹出的菜单中选择 **"Your repositories"** 和 **"Your stars"** 。

![Popup Menu](https://github.com/xuqingxin/arts/blob/master/images/Tip7/1.png)

但是没有"Your watchings"菜单啊，怎么办？办法当然有的，只是Github藏得比较深。在上面弹出的菜单中，选择 **"Settings"** ，在新的页面中选择 **"Notifications"** 这个Tab，然后点击页面上方的 **"things you're watching"** 这个链接，就可以找到所有正在watch的项目了。

![Setting->Notification](https://github.com/xuqingxin/arts/blob/master/images/Tip7/2.png)

其实还有一个快捷的方法，那就是直接在浏览器的地址中输入这个URL：
[https://github.com/watching](
https://github.com/watching)


## Share
### 你确定你真的了解Java四种引用（强引用、弱引用、软引用、虚引用）了吗？
原文链接：[你确定你真的了解Java四种引用（强引用、弱引用、软引用、虚引用）了吗？](https://mp.weixin.qq.com/s?__biz=MzUzODQ0MDY2Nw==&mid=2247483981&idx=1&sn=e41692db5ff0aeaeeb17af0845e2f2da)

文章用比较简单的篇幅列举了Java四种引用的区别，指出它们何时会进行被GC，生存周期如何。主要内容如下表格：

|**引用类型**|**GC回收时间**|**生存时间**|
|-|-|-|
|强引用|从不|一直存活直到JVM停止运行|
|软引用|内存不足时|内存不足时终止|
|弱引用|GC时|GC后终止|
|虚引用|未知|未知|