### 基础概念

ElasticSearch 是一个分布式、高扩展、高实时的搜索与数据分析引擎。它能很方便的使大量数据具有搜索、分析和探索的能力。

Elasticsearch节点类型
节点分一下几类节点：主节点(master node)、数据节点(data node)、摄取节点(ingest node)、协调节点(coordinate node)、冷/热节点(hot/warm node)、Machine Learning Node

节点类型|配置参数|默认值
--|:--:|--:
master|node.master|true
data|node.data|true
ingest|node.ingest|true
coordinating only|无|每个节点默认都是coordinating节点，设置其他类型全部为false
marching learning|node.ml|true(需enable x-pack)