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

