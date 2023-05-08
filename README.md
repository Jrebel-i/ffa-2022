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

## 3，AirWallex基于 Flink 打造实时风控系统｜董大凡

文档：[董大凡Airwallex基于Flink打造实时风控系统.pdf](.\实时风控\【5】董大凡Airwallex基于Flink打造实时风控系统.pdf)

视频：https://www.bilibili.com/video/BV1aK411R72M/?spm_id_from=333.880.my_history.page.click&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：

## 4，Flink CEP 新特性进展与在实时风控场景的落地｜耿飙&胡俊涛

文档：[耿飚&胡俊涛-Flink CEP 新特性进展与在实时风控场景的落地.pdf](.\实时风控\【4】耿飚&胡俊涛-Flink CEP 新特性进展与在实时风控场景的落地.pdf)

视频：https://www.bilibili.com/video/BV1Y8411j7Fm/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：[Flink CEP 新特性进展与在实时风控场景的落地 (qq.com)](https://mp.weixin.qq.com/s/tkgQDxffAOwxLb06lqOdtw)

问题：

• [FLINK-27392](https://issues.apache.org/jira/browse/FLINK-27392)：支持在Pattern内的相邻事件之间定义时间窗口 

• [FLINK-26941](https://issues.apache.org/jira/browse/FLINK-26941)：支持在带有窗口的Patten中以notFollowedBy结尾 

• [FLINK-24865](https://issues.apache.org/jira/browse/FLINK-24865)：支持批模式下使用MATCH_RECOGNIZE

• [FLINK-23890](https://issues.apache.org/jira/browse/FLINK-23890)：优化Timer创建策略



新增接口（[FLIP-200](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=195730308)）

案例参考：https://help.aliyun.com/document_detail/459880.html
代码：https://github.com/RealtimeCompute/ververica-cep-demo.git

克隆代码，并且通过依赖可以获取到jar包的source，拷贝进项目查看

```xml
<dependency>
    <groupId>com.alibaba.ververica</groupId>
    <artifactId>flink-cep</artifactId>
    <version>1.15-vvr-6.0.2-api</version>
</dependency>
```

借此再了解一下：https://repo.maven.apache.org/maven2/com/alibaba/ververica/ 这个仓库

https://help.aliyun.com/apsara/enterprise/v_3_14_0_20210519/sc/user-guide/job-development-1.html?spm=a2c4g.14484438.10001.471

![image-20230309221300671](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230309221300671.png)

正好redis一直以来都是使用的 [bahir-flink](https://github.com/apache/bahir-flink) 但是又好久没有更新维护了，所以可以借此机会了解一下阿里是怎么实现的

但是很可惜redis source为空的，所以使用jd-gui反编译，并将class保存为java文件

![image-20230309231143168](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230309231143168.png)

但是所有文件都带有注释

![image-20230309231833478](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230309231833478.png)

然后取消勾选

![image-20230309231854254](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230309231854254.png)

看到一个flink-shaded-force-shading模块

https://blog.csdn.net/weixin_44723515/article/details/128298568

## 5，网易游戏实时 HTAP 计费风控平台建设｜林佳

文档：[林佳-网易游戏实时 HTAP 计费风控平台建设.pdf](.\实时风控\【1】林佳-网易游戏实时 HTAP 计费风控平台建设.pdf)

视频：https://www.bilibili.com/video/BV1p24y1y73n/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：[网易游戏实时 HTAP 计费风控平台建设 (qq.com)](https://mp.weixin.qq.com/s/DGsm46huEFDzDqS8aDLSHQ)

问题：

**风控业务会话** 

由一次用户行为所引发的，需要多个系统协作完成、同时触发多个请求、产生跨 越多个服务提供方调用的全过程

**业务会话情况**

多服务、多请求产生的异构结果难以直接关联 

时间跨度大、业务水位不同步 

调用顺序复杂，存在并发、异步的情况 

**业务会话目前问题**

业务会话级的问题定位，极度依赖人工处理和个人经验，重复工作多，容易错判 

这里需要注意的是，业务会话跨越了多个相互独立的请求链路，且没有统一全局的 trace-id 可以被提前置入所有的数据中。

**开源Tracing方案：** 

依赖全局trace-id 

通常需要侵入服务打点 

单次请求链路跟踪

**实时关联的数据结构**

![image-20230316235611042](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230316235611042.png)

**基准** 

需要关注的核心风控数据点 一旦出现就认定存在一个包含它的业务会话

**补充** 

非关键的、辅助判断的风控数据点 依附到相应的基准风控数据中，不单独开启业务会话 有至少一个ID可以和基准数据进行关联

![image-20230316235752775](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230316235752775.png)

**基准的生成(faster)**

![image-20230316235848476](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230316235848476.png)

**补充风控数据点的关联（1.17版本支持）**

当某一条数据来源有延迟的情况下，这笔数据会被丢失，这是 Flink 1.16 正式版之前的情况。在 Flink 1.17 版本中，社区的小伙伴已经把这个代码合并进去了

![image-20230316235924014](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230316235924014.png)

**延迟数据的补回**

![image-20230317000135175](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230317000135175.png)

**实时风控数据AP（TiDB）**

TiDB KV + TiFlash (HTAP特性)

![image-20230317000232635](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230317000232635.png)

**实时风控数据AP on TiFlash**

![image-20230317000322559](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230317000322559.png)

**数据打宽**

![image-20230317000444365](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230317000444365.png)

![image-20230317000505684](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230317000505684.png)

# 行业案例

## 1，Flink 在蔚来自动驾驶AO部门的运用｜林志浩

文档：[林志浩-Flink在蔚来自动驾驶AO部门的运用.pdf](.\行业案例\【3】林志浩-Flink在蔚来自动驾驶AO部门的运用.pdf)

视频：https://www.bilibili.com/video/BV1TG4y1G7pu/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 2，运满满实时计算实践和思考｜欧锐

文档：[欧锐-满帮实时计算实践和思考.pdf](.\行业案例\【1】欧锐-满帮实时计算实践和思考.pdf)

视频：https://www.bilibili.com/video/BV1hR4y1y7XL/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 3，Flink 在平安证券的实践｜张兴

文档：[张兴-FLINK在平安证券的实践.pdf](.\行业案例\【3】张兴-FLINK在平安证券的实践.pdf)

视频：https://www.bilibili.com/video/BV1b24y1y7fS/?spm_id_from=333.999.0.0&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：

数据去重应用场景：

1，并发数据，通过固定时间窗口来处理

2，数据时效非常长，主要使用phoenix来解决问题，将数据插入到phonenix，通过维表去关联是否存在这条数据来实现去重



## 4，集度汽车 Flink on native k8s 的应用与实践｜周磊、顾云

文档：[周磊&顾云-集度汽车 Flink on native k8s 的应用与实践.pdf](.\行业案例\【4】周磊&顾云-集度汽车 Flink on native k8s 的应用与实践.pdf)

视频：https://www.bilibili.com/video/BV1Lg411W7Gp/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：![image-20230503141021304](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230503141021304.png)



## 5，中信建投证券基于 Flink 的实时计算平台探索与实践｜王若梦、宋宇航

文档：[王若梦、宋宇航-中信建投证券基于Flink的实时计算平台探索与实践.pdf](.\行业案例\【4】王若梦、宋宇航-中信建投证券基于Flink的实时计算平台探索与实践.pdf)

视频：https://www.bilibili.com/video/BV1P8411j774/?spm_id_from=pageDriver&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 6，Apache Flink 在翼支付的应用与实践｜尹春光

文档：[尹春光-ApacheFlink 在翼支付的实践应用.pdf](.\行业案例\【3】尹春光-ApacheFlink 在翼支付的实践应用.pdf)

视频：https://www.bilibili.com/video/BV1VW4y1p7bX/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 7，电商 SaaS 全渠道实时数据中台最佳实践｜张成玉&应圣楚

文档：[张成玉、应圣楚｜电商SaaS全渠道实时数据中台最佳实践.pdf](.\行业案例\【2】张成玉、应圣楚｜电商SaaS全渠道实时数据中台最佳实践.pdf)

视频：https://www.bilibili.com/video/BV12v4y1d7h3/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 8，FlinkSQL 在米哈游的平台建设和应用实践｜张剑

文档：[张剑分论坛｜FlinkSQL在米哈游的平台建设和应用实践.pdf](.\行业案例\【2】张剑分论坛｜FlinkSQL在米哈游的平台建设和应用实践.pdf)

视频：https://www.bilibili.com/video/BV1544y1Q7Fs/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：[Flink SQL 在米哈游的平台建设和应用实践(qq.com)](https://mp.weixin.qq.com/s/9OvQ8EoFVDJGbMyHbpkMyg)

问题：

- 第一，语义表达和控制能力的建设

  ![image-20230505213101445](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505213101445.png)

问题一：算子并行度和传输方式不可控

![image-20230505213304548](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505213304548.png)

解决方法：

https://nightlies.apache.org/flink/flink-docs-release-1.13/zh/docs/dev/execution/execution_plans/

这个visualizer网站已经失效了，不过flink官方在0.9版本还在，可以将前端代码复制到本地运行，并将相应的js,css,img文件拷贝下来，直接本地运行

https://github.com/apache/flink/blob/release-0.9/flink-dist/src/main/flink-bin/tools/planVisualizer.html

https://github.com/apache/flink/blob/release-0.9/flink-clients/src/main/resources/web-docs/css/pactgraphs.css

这里是修改的streamGraph

```java
//打印执行计划
System.out.println(env.getExecutionPlan());
//通过编辑修改parallelism可以实现并行度的修改
//甚至可以修改算子之间的连接方式   ship_strategy项

{
  "nodes" : [ {
    "id" : 1,
    "type" : "Source: Custom Source",
    "pact" : "Data Source",
    "contents" : "Source: Custom Source",
    "parallelism" : 1
  }, {
    "id" : 2,
    "type" : "Timestamps/Watermarks",
    "pact" : "Operator",
    "contents" : "Timestamps/Watermarks",
    "parallelism" : 1,
    "predecessors" : [ {
      "id" : 1,
      "ship_strategy" : "FORWARD",
      "side" : "second"
    } ]
  }, {
    "id" : 4,
    "type" : "Window(GlobalWindows(), DeltaTrigger, TimeEvictor, ComparableAggregator, PassThroughWindowFunction)",
    "pact" : "Operator",
    "contents" : "Window(GlobalWindows(), DeltaTrigger, TimeEvictor, ComparableAggregator, PassThroughWindowFunction)",
    "parallelism" : 16,
    "predecessors" : [ {
      "id" : 2,
      "ship_strategy" : "HASH",
      "side" : "second"
    } ]
  }, {
    "id" : 5,
    "type" : "Sink: Print to Std. Out",
    "pact" : "Data Sink",
    "contents" : "Sink: Print to Std. Out",
    "parallelism" : 16,
    "predecessors" : [ {
      "id" : 4,
      "ship_strategy" : "FORWARD",
      "side" : "second"
    } ]
  } ]
}

```



通过修改JobGraph的方式

![image-20230505213336543](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505213336543.png)

问题二：Create View逻辑视图

![image-20230505222604793](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505222604793.png)

解决方法：

其实是在 Apache calcite 语法解析的时候，View 它只是一个逻辑辅助，在这一过程会将其丢弃。那么我们如何让 View 这一信息被底层感知到呢？

主要有两个办法:

办法一是 SQL 解析的时候不丢失 View 信息

办法二是在 RealNode 到 Optimizer Rule 能够识别到 View 的特征信息，这样就可以把 View 当成一个真正的代码去翻译了



采用了办法二，最终的方案是采用识别特定函数实现，内置了一个 breakpoint 函数。在创建 View 的时候可以同时多 select 一个 breakpoint，这样在底层翻译的时候，就可以把它当成一个真正的 RealNode 处理。



问题三：状态保存时间

![image-20230505223113259](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505223113259.png)



解决方法：

​		采用的方案是用 Flink SQL+CDC+Regular Join 的方式来实现。接入还是一样消费 Kafka，通过 CDC 来消费数据库分库分表的数据，最后通过正常的 Regular Join 来实现。

​		这里的 Regular join 底层同时依赖两个 MapState，比如 Topic A 对应 MapState 是 A，MySQL 里的数据库的数据对应的是 B。如果我们能轻易的将 MapState B 的状态设置为 0 或者不过期，那么这个状态的数据就会被永久的保存下来。即使流的数据先到达了，后面状态数据到达也能触发数据的关联，从而比较好的解决这类问题。

​		具体的解决办法是，我们可以在 Flink SQL 中指定左右流 Join 的状态时间，在 Graph 中识别有 Join 的算子，最终透传到 Join 算子做状态时间的设置。



- 第二，资源调优和弹性能力的建设

  ![image-20230505223316313](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505223316313.png)

  问题一：静态资源调优

  ![image-20230505223857871](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505223857871.png)

​		解决方法：

​		第一个环节，首先进行语法校验，然后通过语法校验及后端生成 Stream Graph，拿到 Stream Graph 的同时我们还会进行 Source/Sink 连通校验和参数初步调整。

​		第二个环节，根据当前的任务逻辑及流量合理的调整资源。首先探测 Source 的流量，然后拿这个值和用户的作业 SQL、Stream Graph 做 Optimizer。		Optimizer 部分主要包括 Restart、HighAvailable、Checkpoint、Parallelism、TaskManager、JobManager、StateBackend。

​		通过不断优化，得到一个比较好的任务资源参数，供用户作为初始任务资源使用。



​		问题二：动态资源调优及扩缩容

​		解决方法：

​		那么任务上线后是什么情况呢？比如 Flink SQL 正常的 Running，首先将指标采集 Push 到 Kafka，然后会有实时任务进行指标的清洗聚合。针对重要的指标，比如消费延迟指标、算子速率指标、JVM 进程指标，状态大小指标等。

​		这些指标作为动态资源调整服务的入参，能及时感知到当前任务的运行状况，然后动态资源调整会进行需求资源的申请，将任务重启，并给用户发送通知。如果重启失败，会进行配置回滚，然后告知用户调整失败需要手工介入。

​	针对动态资源调整，我们的场景大概有如下四个：

- 设定历史数据追数：Kafka 积压历史数据初次消费、CDC 全量到增量。
- 期望时间动态调整：特定时间扩缩容，解决活动可预知的流量高峰。
- 根据指标动态调整：延迟或反压及时调整，预测流量变化提前调整。
- 异常指标动态调整：例如 JVM GC 频繁，及时调整 TM 内存。



​		问题三：弹性资源能力的建设

​		引进 Flink Native K8S



- 第三，指标体系建设

  ![image-20230505224523085](https://jrebe-note-pic.oss-cn-shenzhen.aliyuncs.com/img/image-20230505224523085.png)

  

  调度任务依赖，是指 Kafka/MysqlCDC 数据入湖，下游有离线调度依赖，我们需要感知当前任务是否有延迟，Checkpoint 有没有做，数据在数仓里是否具有可见性，还需要保证数据完整入仓入湖后，下游任务才会启动。

  

- 第四，近实时数仓建设

第一个场景，日志场景建设。当数据量大，入仓时间多于 10 分钟的时候，下游任务相应增大，有没有办法缩短入仓时间？当 HDFS 写入流量波动较大的时候，能不能更加平稳，且数据不丢不重？

众所周知，从日志文件通过 Kafka 到 Flink SQL、写入 Iceberg 都有可能产生数据重复，这一链路能保证数据不丢，但较难保证数据不重。

对此我们的方案是基于文件日志采集 MetaData Logs，然后将 MetaData Logs 在下游复用。其中 MetaData Logs 的文件的行数起到很重要的作用，因为这一链路能保证数据不丢。

如果数据的行数等于 MetaData Logs，就代表这个数据没有重复，一旦数据行数多于 MetaData Logs，就代表这个数据有重复了，但我们只需要基于重复的某一个文件日志进行去重处理，而不需要对全量日志文件都进行去重处理。

针对 Iceberg 表我们建立了 Iceberg Manager 来做小文件合并、过期快照清理、孤儿文件清理。



第二个场景，数据库场景建设。比如数据库是 MySQL，我们想通过 Flink CDC 将数据直接写入 Iceberg V2 表。那么就会有如下几方面的考虑：

- 多个 Flink CDC 任务是否会对一个 MySQL 读取？数据库是否会有压力？已经读取的数据能否复用起来？
- Flink CDC 增量读取，支持指定读取的时间起点。
- IcebergV2 全量数据同步时，数据量较大，容易产生了较多 Delete Files，辅助链路的 Iceberg Manager 在进行表级别优化的时候，就会产生较大的压力。
- Flink CDC 同步任务太麻烦，希望配置化就生成好任务，希望有一键数据入湖的能力。



一键任务生成。辅助自动任务的调优扩缩容机制，保证 Flink CDC 全量同步和增量同步资源的切换问题，通过 Kafka 来实现对同一个数据源读取时候的压力问题，将数据写入 Kafka，Kafka 的数据会被下游的 Flink SQL 任务自动感知并同步。

为了解决 Delete Files 全量数据过多的问题。我们在进行全量同步的时候，会关闭写入 Iceberg V2 表的 upsert 功能，在增量的时候才会开启，这样就可以保证全量同步的时候数据既不丢也不重。同时，Flink SQL 任务增量数据会写入 Iceberg V1 表，方便下游链路进行复用。



同时发现应用程序分析和调试工具

https://nightlies.apache.org/flink/flink-docs-release-1.17/docs/ops/debugging/application_profiling/

## 9，Flink 在中泰证券的实践与应用｜连序全

文档：[连序全-Flink在中泰证券的实践与应用.pdf](.\行业案例\【1】连序全-Flink在中泰证券的实践与应用.pdf)

视频：https://www.bilibili.com/video/BV1YY411d7eX/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：[Flink 在中泰证券的实践与应用(qq.com)](https://mp.weixin.qq.com/s/mnuisYIaJD6UW7tnnFdjsg)

问题：

实时数据管道场景说明

1. Kafka 数据通过 Flink SQL 同步到 Kafka，实现不同 Kafka 集群间的消息复制，实现集群读写分离的场景。
2. 通过 Flink SQL 将日志数据落地到 HDFS，提供给后续审计、数据挖掘等场景使用。
3. 将监控数据实时写入 TiDB，实现监控运维大屏。
4. 将客户的流水数据、交易数据写入 Hbase，满足客户实时流水数据的查询。



性能调优

​	1，通过 Task Manager 节点的 CPU 负载、Flink 的背压状态来定位具体的 Stream Operator。通过 Arthas 评估该 Stream Operator 关键路径的耗时，最终定位到产生性能瓶颈的具体业务逻辑。

​	2，在定位到性能瓶颈点之后，利用 Flink State 存储一些中间状态，避免业务逻辑重复计算。

​	3，在数据输出方面，合理设置 TiDB 的写入参数，最大程度的提升写入效率。



数据准确性

1. Checkpoint 指定持久化的存储方式，我们选择了星环 HDFS 作为存储底座，保证了任务在发生异常后可以恢复运行。
2. 作业上线后会根据业务的需求随时更新代码，我们需要设置 RETAIN_ON_CANCELLATION 参数，在任务版本的升级后，仍然可以恢复当前的状态继续运行。
3. 当上游系统出现异常时，操作 HVR 进行数据回放，保证数据源的可回溯性。同时 Flink 作业按照事件的类型进行幂等处理，保证整体数据的准确性。
4. 通过 Queryable State 查询作业运行过程中的状态数据，在线排查客户数据的异常问题。



数据输出优化

​	1，TiDB 输出表开启 TiFlash 功能，TiDB 通过 raft 协议异步复制数据到 TiFlash。

​	2，对于不同的查询场景选择不同的存储引擎，对于单客户的点查场景，通过 SQL Hint 指示使用 TiKV 存储引擎。

​	3，对于聚合统计类的场景，比如我们要查询 Top 100 的客户，通过 SQL Hint 指示使用 TiFlash 列式存储引擎。经过实际观测，在此应用场景下，通过 TiFlash 引擎可以将查询的耗时由分钟级降低至秒级。





使用Arthas 评估Flink Stream Operator 关键路径的耗时：

https://arthas.aliyun.com/en/doc/quick-start.html

```bash
#下载arthas
wget https://github.com/alibaba/arthas/releases/download/arthas-all-3.6.8/arthas-bin.zip
unzip arthas-bin.zip -d  arthas-bin/
cd arthas-bin/
./as.sh

#启动flink任务
/usr/lib/flink/bin/flink run -t yarn-per-job examples/streaming/TopSpeedWindowing.jar
#并记录jobmaster地址
ip-10-0-23-22.ap-southeast-2.compute.internal:42451
#需要在对应的taskmanager所在的节点上安装arthas
#比如我需要查看WindowOperator算子的处理速度
trace org.apache.flink.streaming.runtime.operators.windowing.WindowOperator processElement

#打印如下
`---ts=2023-05-05 13:14:45;thread_name=Window(GlobalWindows(), DeltaTrigger, TimeEvictor, ComparableAggregator, PassThroughWindowFunction) -> Sink: Print to Std. Out (1/1)#0;id=46;is_daemon=false;priority=5;TCCL=org.apache.flink.runtime.execution.librarycache.FlinkUserCodeClassLoaders$SafetyNetWrapperClassLoader@6ad311fd
    `---[0.081702ms] org.apache.flink.streaming.runtime.operators.windowing.EvictingWindowOperator:processElement()
        +---[3.47% 0.002832ms ] org.apache.flink.streaming.runtime.streamrecord.StreamRecord:getValue() #115
        +---[2.50% 0.002041ms ] org.apache.flink.streaming.runtime.streamrecord.StreamRecord:getTimestamp() #115
        +---[3.14% 0.002567ms ] org.apache.flink.streaming.api.windowing.assigners.WindowAssigner:assignWindows() #114
        +---[3.00% 0.002453ms ] org.apache.flink.streaming.runtime.operators.windowing.EvictingWindowOperator:getKeyedStateBackend() #120
        +---[2.91% 0.002381ms ] org.apache.flink.runtime.state.KeyedStateBackend:getCurrentKey() #120
        +---[3.40% 0.002776ms ] org.apache.flink.streaming.runtime.operators.windowing.EvictingWindowOperator:isWindowLate() #230
        +---[2.98% 0.002436ms ] org.apache.flink.runtime.state.internal.InternalListState:setCurrentNamespace() #235
        +---[3.71% 0.003031ms ] org.apache.flink.runtime.state.internal.InternalListState:add() #236
        +---[8.68% 0.007091ms ] org.apache.flink.streaming.runtime.operators.windowing.WindowOperator$Context:onElement() #243
        +---[2.53% 0.002068ms ] org.apache.flink.streaming.api.windowing.triggers.TriggerResult:isFire() #245
        +---[2.72% 0.002223ms ] org.apache.flink.streaming.api.windowing.triggers.TriggerResult:isPurge() #254
        `---[3.53% 0.00288ms ] org.apache.flink.streaming.runtime.operators.windowing.EvictingWindowOperator:registerCleanupTimer() #257
```



星环 HDFS：https://www.modb.pro/db/603163

Queryable State[Flink新功能] ：https://nightlies.apache.org/flink/flink-docs-master/docs/dev/datastream/fault-tolerance/queryable_state/

https://blog.csdn.net/weixin_45366499/article/details/115442928

## 10，Flink 在新能源场站运维的应用｜姚远

文档：[姚远-Flink在新能源场站运维的应用.pdf](.\行业案例\【4】姚远-Flink在新能源场站运维的应用.pdf)

视频：https://www.bilibili.com/video/BV1eD4y1v75q/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：



## 11，菜鸟供应链实时数仓最佳实践｜张庭

文档：[张庭-菜鸟供应链实时数仓最佳实践.pdf](.\行业案例\【1】张庭-菜鸟供应链实时数仓最佳实践.pdf)

视频：https://www.bilibili.com/video/BV17K411R7rd/?spm_id_from=333.788&vd_source=1435dbab789f2dad584fcf275be722e4

文章：

问题：
