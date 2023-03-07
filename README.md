PDF下载：https://flink-forward.org.cn/#download

直播回放：https://developer.aliyun.com/special/ffa2022?spm=ffa.ffa-home.0.0.1b4943c9ctd616



# 平台建设

## 1，Flink SQL 在美团实时数仓生产中的增强与实践｜董剑辉&张彬

文档：[董剑辉&张彬-Flink+SQL在美团实时数仓中的增强与实践.pdf](.\平台建设\【2】董剑辉&张彬-Flink+SQL在美团实时数仓中的增强与实践.pdf)

视频：https://www.bilibili.com/video/BV1wD4y1Y7pB/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

SQL 作业无法细粒度配置造成资源浪费

SQL 修改逻辑无法从原先状态恢复

SQL 作业出现数据正确性问题难以排查

 丢数问题，乱序问题，SQL使用问题

Trace系统（分布式会话跟踪系统）

Flink SQL 涉及到的算子有 30+ 个，算子非常多而且有些算子是通过 codegen 代码生成技术 实现的。Flink SQL 算子都继承 AbstractStreamOperator，该类中有对 record 及 watermark 处理的方法 setKeyContextElement1/2 与 processWatermark1/2。

![image-20221218152723530](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20221218152723530.png)

数据进入算子的方法 setKeyContextElement1/2(watermark类似, processWatermark1/2), 数据流出到一下 task 的 pushToRecordWriter, 对这几个关键的方法监听, 就能控制算子的输入输出。

以简单的Map为例：调用StreamMap.processElement，然后在processElement()方法中调用output.collect()，而这个output就是RecordWriterOutput，它就会调用到pushToRecordWriter()方法



字节码增强技术动态记录数据 

优点：

1 代码改动小 

2 通过 Javaagent 方式与 Flink 解耦，方便以后升级 

缺点： 

需要单独维护及部署 Javaagent jar



## 2，Flink 在蚂蚁大规模金融场景的平台建设｜李志刚

文档：[李志刚-Flink在蚂蚁大规模金融场景的平台建设.pdf](.\平台建设\【2】李志刚-Flink在蚂蚁大规模金融场景的平台建设.pdf)

视频：https://www.bilibili.com/video/BV1x24y1y7tW/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

热启动技术

K8s集群模式

流批一体

SQL作业的调试

方案一 

1. 在所有算子入口处增加代码 trace代码 
2. 影响代码优雅，热点 

方案二 

​	字节码增强（同上面美团的类似）

![image-20221218172313776](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20221218172313776.png)

https://www.databricks.com/ 全向量化计算引擎

## 3，Flink 实时计算平台在知乎演进｜贾承昆

文档：[贾承昆-Flink 实时计算平台在知乎的演进 .pdf](.\平台建设\【4】贾承昆-Flink 实时计算平台在知乎的演进 .pdf)

视频：https://www.bilibili.com/video/BV17K411R7JH/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

统一元数据管理

本身就有schema：doris,clickhouse.mysql

不具备schema：Kafka，redis

Protobuf Format

动态 Jar 加载

资源超卖

日志采集和持久化

自动监控和报警

逻辑资源隔离和计费

## 4，Dinky 在 Flink 开发模式的开源探索实践｜亓文凯

文档：[亓元凯-Dinky在Flink开发模式的开源探索实践.pdf](.\平台建设\【5】亓元凯-Dinky在Flink开发模式的开源探索实践.pdf)

视频：https://www.bilibili.com/video/BV158411j7gU/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

Flink 整库实时入仓入湖

http://www.dlink.top/docs/next/data_integration_guide/cdcsource_statements

## 5，Apache Streampark 让 Flink 开发管理更简单｜王华杰

文档：[王华杰-Apache StreamPark 让Flink开发管理更简单最终版.pdf](.\平台建设\【5】王华杰-Apache StreamPark 让Flink开发管理更简单最终版.pdf)

视频：https://www.bilibili.com/video/BV1Lg411W7xb/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

https://github.com/apache/incubator-streampark

## 6，小米基于 Flink 的实时数仓建设实践｜周超

文档：[周超-小米基于Flink的实时数仓建设实践最终版.pdf](.\平台建设\【4】周超-小米基于Flink的实时数仓建设实践最终版.pdf)

视频：https://www.bilibili.com/video/BV1Lg411W7xb/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

![image-20221221230436321](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20221221230436321.png)

zstd压缩

## 7，联通 Flink 实时计算平台化运维实践｜穆纯进

文档：[穆纯进-联通 Flink 实时计算平台化运维实践.pdf](.\平台建设\【3】穆纯进-联通 Flink 实时计算平台化运维实践.pdf)

视频：https://www.bilibili.com/video/BV12G4y157ct/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：



## 8，货拉拉基于 Flink 计算引擎的应用与优化实践｜王世涛

文档：[货拉拉基于Flink计算引擎的应用与优化实践.pdf](.\平台建设\【1】货拉拉基于Flink计算引擎的应用与优化实践.pdf)

视频：https://www.bilibili.com/video/BV17G4y1G7fS/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：



## 9，爱奇艺统一实时计算平台建设｜李恒

文档：[李恒-爱奇艺统一实时计算平台.pdf](.\平台建设\【3】李恒-爱奇艺统一实时计算平台.pdf)

视频：https://www.bilibili.com/video/BV1qY411d7Ae/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：



## 10，阿里实时计算平台建设实践｜周凯波

文档：[周凯波-阿里实时计算平台建设实践.pdf](.\平台建设\【1】周凯波-阿里实时计算平台建设实践.pdf)

视频：https://www.bilibili.com/video/BV1jD4y1v7pr/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

# 核心技术

## 1，Flink 容错恢复 2.0 最新进展｜梅源

文档：[梅源-Flink 容错恢复最 2.0 最新进展.pdf](.\核心技术\【1】梅源-Flink 容错恢复最 2.0 最新进展.pdf)

视频：https://www.bilibili.com/video/BV1ND4y1v7zG/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 2，Flink OLAP Improvement of Resource Management and Runtime｜曹帝胄

文档：[Flink OLAP Improvement of  Resource Management and Runtime 曹帝胄.pdf](.\核心技术\【4】Flink OLAP Improvement of  Resource Management and Runtime 曹帝胄(1).pdf)

视频：https://www.bilibili.com/video/BV1nD4y1v7Lw/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 3，Flink Connector 社区新动向与开发指南｜任庆盛&罗根

文档：[任庆盛&罗根Flink Connector 社区新动向与开发指南withComments.pdf](.\核心技术\【4】任庆盛&罗根Flink Connector 社区新动向与开发指南withComments.pdf)

视频：https://www.bilibili.com/video/BV1VM41167Y2/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 4，Flink Unaligned Checkpoint 在 Shopee 的优化和实践｜范瑞

文档：[范瑞 - Flink Unaligned Checkpoint 在 Shopee 的优化和实践-11-16.pdf](.\核心技术\【2】范瑞 - Flink Unaligned Checkpoint 在 Shopee 的优化和实践-11-16(1).pdf)

视频：https://www.bilibili.com/video/BV1tR4y1y7gQ/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 5，StateBackend performance improvement with TerarkDB｜李明& 王义

文档：[李明&王义StateBackend performance improvement with TerarkDB .pdf](.\核心技术\【3】李明&王义StateBackend performance improvement with TerarkDB .pdf)

视频：https://www.bilibili.com/video/BV1bR4y1y72a/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 6，Adaptive and flexible execution management for batch jobs｜朱翥

文档：[朱翥 _ Adaptive Batch Job Execution.pdf](.\核心技术\【3】朱翥 _ Adaptive Batch Job Execution.pdf)

视频：https://www.bilibili.com/video/BV1oP411T7ay/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

同源执行实例

![image-20230108154945017](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230108154945017.png)

![image-20230108160556936](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230108160556936.png)

## 7，Flink Shuffle 3.0: Vision, Roadmap and Progress｜宋辛童

文档：[宋辛童Flink Shuffle 3.0-Vision_Roadmap and Progress.pdf](.\核心技术\【2】宋辛童Flink Shuffle 3.0-Vision_Roadmap and Progress.pdf)

视频：https://www.bilibili.com/video/BV1M44y1Q7mf/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

![image-20230108174825872](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230108174825872.png)

# ======================================================

## 8，Flink OLAP 在字节跳动的查询优化和落地实践｜何润康

文档：[何润康 Final - Flink OLAP 在字节跳动的查询优化和落地实践.pdf](.\核心技术\【3】何润康 Final - Flink OLAP 在字节跳动的查询优化和落地实践.pdf)

视频：https://www.bilibili.com/video/BV1k14y1n7fs/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

查询优化

1. Query Optimizer 优化 

   （1）Plan 缓存

   ![image-20230305150927446](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305150927446.png)

   （2）TopN 下推

   ![image-20230305151020715](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151020715.png)

   （3）跨 Union All 下推

   ![image-20230305151058497](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151058497.png)

   （4）Join Filter 传递

   ![image-20230305151126645](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151126645.png)

2. Query Executor 优化

   （1）问题：Classloader 问题分析

   ![image-20230305151213774](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151213774.png)

   解决：Classloader 复用

   ![image-20230305151256358](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151256358.png)

   （2）问题：Codegen 问题分析

   ![image-20230305151516167](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151516167.png)

   解决：Codegen 缓存优化

   ![image-20230305151637142](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151637142.png)

   解决：反序列化优化

   ![image-20230305151925795](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151925795.png)

   ![image-20230305151951779](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305151951779.png)

   其他优化：Join Probe 提前输出（probe了解：https://www.jianshu.com/p/af9b169c9a36）， 内存池化， 内存使用优化

   ![image-20230305152056202](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305152056202.png)

稳定性治理

![image-20230305152152246](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305152152246.png)

Java ClassLoader：https://blog.csdn.net/a745233700/article/details/89245847

向量化引擎：https://zhuanlan.zhihu.com/p/449878214

物化视图：

## 9，基于 Log 的通用增量 Checkpoint 在美团的进展｜王非凡

文档：[王非凡基于Log的通用增量Checkpoint在美团的进展.pdf](.\核心技术\【4】王非凡基于Log的通用增量Checkpoint在美团的进展.pdf)

视频：https://www.bilibili.com/video/BV1h8411j75R/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

Log based Checkpoint 制作方式

![image-20230305172344695](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305172344695.png)

**Log based Checkpoint 优势**

更轻量的 recovery ：checkpoint 间隔越短，recovery 时需要回放的数据 就越少。 

更低的事务化 sink 端到端延迟：事务化 sink 在 checkpoint 时进行  commit，更快的 checkpoint 意味着可以进行更频繁的 commit。 

更可预测的 checkpoint 间隔：不需要等 DB flush ，compaction 的影响 也更小，checkpoint 制作时长仅取决于需要持久化到 durable storage 上 的 changelog 数据的多少。 

更友好的资源使用：比较重的 DB 快照操作分散执行，可以避免 cpu使用  率、磁盘 IO 和 网卡流量的尖刺。

**DFS 实现 Changelog 存储的问题** 

Changelog Restore 重复下载文件问题 ：为了避免产生过多小文件，同一 文件中会包含一个 TM 内多个 operator 的 changelog，restore 时这些 operator 会重复下载 changelog 文件，导致 restore 性能差。

小文件问题严重，HDFS NN 压力巨大：以我们一个 4800 并发的作业为 例，默认配置下将会产生 130 万左右个 changelog 文件，单个作业 NN 请 求的 QPS 高达 18000 次/秒左右。 

Changelog 文件写延迟太高，影响 checkpoint 制作速度：还是以我们的 4800 并发的作业为例，写 changelog 文件 P99 延迟在 3秒左右，最大延 迟甚至达到 2 分钟。



解决 重复下载文件问题：

![image-20230305172656086](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305172656086.png)

**Changelog候选存储对比：**

![image-20230305172737682](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305172737682.png)

**BookKeeper 实现 changelog storage**：

State Changelog 相关组件

![image-20230305172849396](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305172849396.png)

## 10，PyFlink 最新进展解读及典型应用场景介绍｜付典

文档：[付典-PyFlink 最新进展解读及典型应用场景介绍.pdf](.\核心技术\【5】付典-PyFlink 最新进展解读及典型应用场景介绍.pdf)

[付典-PyFlink 最新进展解读及典型应用场景介绍.pdf](核心技术\【5】付典-PyFlink 最新进展解读及典型应用场景介绍.pdf)

视频：https://www.bilibili.com/video/BV1c8411578K/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

问题：

## 11，Apache Flink 1.16 功能解读｜黄兴勃

文档：[黄兴勃-Apache Flink 1.16 功能解读.pdf](.\核心技术\【1】黄兴勃-Apache Flink 1.16 功能解读.pdf)

视频：https://www.bilibili.com/video/BV1JK411R7ZX/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：[Apache Flink 1.16 功能解读 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzU3Mzg4OTMyNQ==&mid=2247503755&idx=1&sn=2ae04a59736b11e648699eec42328662&chksm=fd3841c9ca4fc8df8b5c71e4723f34ff762f063906c3354d6f9246521be01252cd390cd52f2f&scene=126&sessionid=1678009053#rd)

问题：

## 12，基于 Log 的通用增量 Checkpoint｜俞航翔

文档：[俞航翔-基于Log的通用增量Checkpoint.pdf](.\核心技术\【1】俞航翔-基于Log的通用增量Checkpoint.pdf)

视频：https://www.bilibili.com/video/BV1hD4y1v7Xi/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：

Changelog Incremental Checkpoint

Local Recovery



**了解Fault Tolerance2.0：**

![image-20230305200919076](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230305200919076.png)



## 13，Flink state 优化以及远程 state 的探索｜张杨

文档：[张杨_Flink_state的优化与remote_state的探索.pdf](.\核心技术\【2】张杨_Flink_state的优化与remote_state的探索.pdf)

视频：https://www.bilibili.com/video/BV1Yv4y1d77u/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：

![image-20230306232743251](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230306232743251.png)

**问题：**

业务场景 

• 模型训练，样本拼接 

• key数量庞大，分布稀疏

 • 数据ttl短，小时级

 缓存失效快反复reload/compaction频繁/cpu消耗高

**优化思考**

![image-20230306232647555](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230306232647555.png)

**State压缩优化**

优化思路 

• 开启partitoned index filter，减少缓存竞争 

• 关闭rocksdb压缩，减少缓存加载/compaction时候的cpu消耗 

• 支持接口层压缩，在数据从state读写前后进行压缩解压缩操作，减 少state大小

![image-20230306232602487](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230306232602487.png)

zstd压缩算法：https://www.baidu.com/link?url=KWYa1OoL8MkJvli46jYQEBGAs4j5M44JjwaeMIagJcgbn-h3wgUTAv4Ajt-Sc5io&wd=&eqid=927fe225000165180000000664060738



**问题**

离在线混部，降本增效

 • 大state作业重启下载state慢 

• 大state作业rescale加载state慢 

在线业务机器io能力不足/state强依赖load过程

**优化思路**

 • 实现flink state的存算分离

 • State远程化/服务化，重启/rescale直接建立连接进行读写 

• 远程state服务需要支持checkpoint完整功能依赖的接口

**整体架构**

![image-20230306233404234](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230306233404234.png)

**缓存使用**

 • 每次state的操作都要走网络 rpc，cpu消耗太高 • 网络rpc延迟高，任务吞吐低 • cache是一个自然而然的选择

**缓存难点**

写缓存

 • 内存攒批，后台定期/checkpoint刷 出去 

• 上百倍的写rpc减少 读缓存 

==》效果好，达到预期效果



读缓存

• key较少场景效果明显，命中率极高，效果好

• 稀疏key场景，大量读null，缓存命中率低 

• 周期性业导致缓存定期失效，读null，命中率暴跌 

==》支持key全量缓存配置，有效解决稀疏/缓存失效场 景性能问题，内存使用上升。 



# 实时风控



## 1，京东物流实时风控实践｜周文跃

文档：[周文跃-京东物流实时风控实践.pdf](.\实时风控\【3】周文跃-京东物流实时风控实践.pdf)

视频：https://www.bilibili.com/video/BV1bW4y1p7ir/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：

## 2，Flink CEP 在抖音电商的业务实践｜张健

文档：[张健-FlinkCEP在抖音电商的业务实践.pdf](.\实时风控\【2】张健-FlinkCEP在抖音电商的业务实践.pdf)

视频：https://www.bilibili.com/video/BV1JM41167Sh/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：
