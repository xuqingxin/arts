# ARTS Week 4

## Algorithm
[Longest Palindromic Substring](https://github.com/xuqingxin/leetcode/blob/master/Algorithms/0005-Longest.Palindromic.Substring.md)

## Review
### 3 Tips to Improve Development Workflow
原文链接：[3 Tips to Improve Development Workflow](
https://medium.com/@lucaspenzeymoog/3-tips-to-improve-development-workflow-384310948fa1)

虽然题目写的是开发流程，但是实际上是针对开发者个人的，跟软件开发流程没什么关系。

文章提供了日常开发工作中提高生产力的3个方法。
#### 1. Test Watchers
对于TDD开发，经常需要运行测试用例。写完代码后，即使只是打开终端，进行测试用例这样的小事，也是需要时间的。但是使用了Test Watch后，只要你保存了代码，那么测试用例就会自动执行，开发人员只要关注代码本身，而不用花时间在执行用例这种小事上了。

#### 2. 记笔记
即使对于有经验的开发者，也会遇到技术问题而需要去Google或Stack Overflow上寻找答案。如果找到了答案，可以更进一步，把答案或解决方案记录下来，便于下次查找。一个好的办法是使用Evernote。它有Chrome插件，可以把网页上的内容一键保存，而且使用Google搜索的时候，它会自动帮你搜索自己保存的相关内容，并列举在Google搜索结果的旁边。

#### 3. 便于阅读的代码
使用工具让代码更整洁，更便于阅读。根据[Eagleson法则](
https://github.com/xuqingxin/arts/blob/master/arts-3.md)，6个月前写的代码就不属于你自己了。[Linters](https://en.wikipedia.org/wiki/Lint_%28software%29)工具通过分析可以帮助我们检测代码是否违反了常见的编程范式，是否有格式错误，变量或函数命令是否符合规范等等。

通过方法让我们的开发过程越自动化，我们就能解放越多的时间专注在真正重要的事情上。

==================================================
对于作者提到的三点我都非常赞同。

如果使用TDD开发的话，第一点绝对会提高生产力。Web开发也有类似的利器，通过使用2个显示器或者一个显示器分为2部分，一边是IDE，一边是浏览器，IDE里的代码改动后，浏览器里立即显示相应的变化，工作效率要好多。

至于第二点，除了记录在类似Evernote的应用程序中，我觉得更好的方法是记录在网上的博客里，或者直接记载Github上。这有几个好处：
1. 你遇到的问题，别人也可能会遇到。放到网上，便于让大家搜索到
2. 通过整理并记录下问题和答案，可以让自己对问题的理解更加深刻
3. 持续输出，算是写作的一种，可以提高自己的写作和表达能力

第三点我是一直非常推崇的。现在相比软件的性能，软件的维护性越来越重要。使用工具，可以帮助我们极大地提高代码的可读性。在团队合作越来越重要的今天，一款软件往往是一个小组好几个人共同开发的。如果每个人写的风格都自成一体，那今后的维护成本就大了。特别是如果有人离职了，代码的可阅读性越高，那么接手维护的成本就相应地越低。

## Tip
### log4net保存日志到MySQL中的几个注意点

今天下午花2个小时，总算把日志通过log4net保存到了MySQL数据库中，以下是主要的操作步骤和几个注意事项。

#### 操作步骤
1. 使用Nuget安装log4net
2. 使用Nuget安装MySql.Data
3. log4net的配置文件中增加一个appender

```xml
<appender name="MySQLAppender" type="log4net.Appender.AdoNetAppender">
    <bufferSize value="1" />

    <connectionType value="MySql.Data.MySqlClient.MySqlConnection, MySql.Data"/>
    <connectionString value="server=localhost;database=log4app;uid=root;pwd=root;" />
    <commandText value="INSERT INTO applog (date, thread, logger, method, line, level, message, exception) VALUES (@date, @thread, @logger, @method, @line, @level, @message, @exception)" />
    <parameter>
      <parameterName value="@date"/>
      <dbType value="DateTime"/>
      <layout type="log4net.Layout.RawTimeStampLayout" />
    </parameter>
    <parameter>
      <parameterName value="@thread" />
      <dbType value="String" />
      <size value="255" />
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%thread" />
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@logger"/>
      <dbType value="String"/>
      <size value="255"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%logger"/>
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@method"/>
      <dbType value="String"/>
      <size value="50"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%method"/>
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@line"/>
      <dbType value="Int16"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%line"/>
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@level"/>
      <dbType value="String"/>
      <size value="50"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%-5level"/>
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@message"/>
      <dbType value="String"/>
      <size value="4000"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%message"/>
      </layout>
    </parameter>
    <parameter>
      <parameterName value="@exception"/>
      <dbType value="String"/>
      <size value="2000"/>
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%exception"/>
      </layout>
    </parameter>
</appender>
```

#### 注意点
1. MySQL Server可以安装最新版本8.0的，但是在配置密码加密方式的时候，要选择兼容5.X版本的传统认证模式，不要选择强默认推荐的强密码加密方式。因为很对客户端目前都只提供5.X版本的加密方式。因为我们的程序需要在.Net Framework 4.5下运行，所以MySql.Data的版本选择了6.9.12，这个版本就不支持新的强密码加密方式，会导致因为不能连接数据库而无法写日志。
![密码加密方式选择5.x兼容版本](https://github.com/xuqingxin/arts/blob/master/images/Tip4/1.png)

2. 如果配置都没问题，但是日志没有写入数据库，可以打开log4net的内部调试开关，查看哪有问题。打开log4net的内部调试开关有两个办法。
   
   1. 在配置文件App.config中设置log4net.Internal.Debug为true，注意是程序配置文件而不是log4net的配置文件（如果log4net的配置放在单独的文件中的话）。这样错误信息会在输出到控制台。
   ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="log4net.Internal.Debug" value="true"/>
        </appSettings>
    </configuration>
   ```

   2. 在代码中设置log4net.Util.LogLog.InternalDebugging为true，错误信息会输出到控制台System.Diagnostics.Trace文件中，通过在App.config中配置Trace监听器，可以把信息输入到文件中。
   ```xml
    <configuration>
    ...
    <system.diagnostics>
        <trace autoflush="true">
            <listeners>
                <add 
                    name="textWriterTraceListener" 
                    type="System.Diagnostics.TextWriterTraceListener" 
                    initializeData="C:\tmp\log4net.txt" />
            </listeners>
        </trace>
    </system.diagnostics>
    ...
    </configuration>
   ```


## Share
### 【生活现场】从诗词大会飞花令到elasticsearch原理解析

原文链接：
[【生活现场】从诗词大会飞花令到elasticsearch原理解析](
https://mp.weixin.qq.com/s/LD2VG6dRNYXOO9KE38F_Mg)

这篇文章使用漫画的形式，结合实际生活中的一个电视节目“诗词大会飞花令”，把ElasticSearch的实现原理解释得通俗易懂。

这种通过平常生活中的事情把技术讲清楚的能力，也是沟通的一个技巧。另外，只有自己真正掌握了一项技术，才能用简单的话语，通俗易懂的方式解释给别人听。

除了这篇文章，作者还有其他的一些文章，都挺不错，值得一看。
* [【生活现场】从洗袜子到hbase存储原理解析](
https://mp.weixin.qq.com/s?__biz=MzIzMTE1ODkyNQ==&mid=2649411489&idx=1&sn=cc830718ac8af0287a0f2c4a880a87c9)
* [【生活现场】从生日请客到hdfs工作原理解析](
https://mp.weixin.qq.com/s?__biz=MzIzMTE1ODkyNQ==&mid=2649411210&idx=1&sn=749f6a034d91ed3292a9f7167dee9c41)
* [【生活现场】从打牌到map-reduce工作原理解析](
https://mp.weixin.qq.com/s?__biz=MzIzMTE1ODkyNQ==&mid=2649411054&idx=1&sn=f5fc02ccfb32cbe0421f13255027ae3f)
* [【生活现场】从搬家到容器技术docker应用场景解析](
https://mp.weixin.qq.com/s?__biz=MzIzMTE1ODkyNQ==&mid=2649410963&idx=1&sn=dab123af8a39a0d7eb3d06c22b5d7ad9)