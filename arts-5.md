# ARTS Week 5

## Algorithm
[ZigZag Conversion](https://github.com/xuqingxin/leetcode/blob/master/Algorithms/0006-ZigZag.Conversion.md)

## Review



## Tip
### MySQL中datetime与timestamp区别

#### datetime
1. 保存格式为yyyy-MM-dd HH:mm:ss.SSS（年月日时分秒毫秒），它与时区无关。MySQL 5.6.4后，可以存储小数，精确到毫秒；
2. 值范围：从1000-01-01 00:00:00.000 到 9999-12-31 23:59:59.999
3.  长度：8个字节
4.  格式：datetime(n)，n为小数位数。如果只需要精确到秒，使用datetime，或datetime(0)即可；如果需要精确到3为小数，则使用datetime(3)。

#### timestamp
1. 保存自1970-01-01午夜(格林尼治标准时间)以来的秒数，它和unix时间戳相同。它与时区有关，查询时转为相应的时区时间。比如，服务器上存储的是1970-01-01 00:00:00，客户端是北京，那么查询得到的结果会加8个时区的小时，即1970-01-01 08:00:00。
2. 值范围：1970-01-01 00:00:01 UTC 到 2038-01-19 03:14:07
3. 长度：4个字节
4. 格式：timestamp(n)，n为小数位数。如果只需要精确到秒，使用datetime，或datetime(0)即可；如果需要精确到3为小数，则使用datetime(3)。


## Share
### 架构师能力模型
原文链接：[架构师能力模型](https://mp.weixin.qq.com/s?__biz=MzI0MTczNDgyOQ==&mid=2247484195&idx=1&sn=4023a1def4da46509a481b77e297e1f7)

这篇文章归纳概括了架构师的主要能力：
* 研发流程的持续改进
* 归纳抽象和技术泛化能力
* 业务和需求的分析和理解能力
* 技术折中和持续改进能力
* 技术广度和深度
* 持续学习的能力
* 技术影响力
* 沟通表达能力
* 技术管理能力
* 坚持正确的价值观
