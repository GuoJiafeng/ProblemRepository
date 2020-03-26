

**作者：写scala的老刘**

**链接：https://www.jianshu.com/p/a2f1bdcc4d2a**

**来源：简书**

**著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。**



### (1)执行模式

Spark Streaming: 以micro-batch的模式:以固定的时间间隔来划分每次处理的数据， Structed streaming: 有两种模式：1),Micro-batch模式:处理模式类似sparkStreaming的批处理，2),Continuous Processing模式:获取数据后,放入queue中，启动long-running的worker线程从queue中读取数据并实时处理。该模式下在功能上还有一些缺陷，比如对端到端的exactly-once语义的支持。

### (2)ApI

Sparkstreaming: 基于RDD开发，程序入口是StreamingContext，数据模型是Dstream，数据的转换操作通过Dstream的api完成，真正的实现依然是通过调用rdd的api完成
 Structed Streaming: 基于sql开发，入口是sparksession，使用的统一Dataset数据集，数据的操作会使用sql自带的优化策略实现

### (3)时间机制

SparkStreaming的处理逻辑是根据应用运行时的时间(ProcessingTime)进行处理,不能根据消息中自带的时间戳完成一些特殊的处理逻辑
 StructedStreaming很大的改变是它加入了EventTime,WeaterMark等概念,在处理消息时,可以考虑消息本身的时间属性,同时,也支持基于运行时间的处理方式

### (4)UI页面

SparkStreaming提供了内置的界面化的UI操作,便于观察应用运行,批处理时间,消息速率,是否延迟等信息
 StructedStreaming则没有直观的UI页面

