### 基础概念

#1、什么是ES
ElasticSearch 是基于Lucene实现的分布式、高扩展、准实时的搜索平台，它是使用Java语言开发的并通过JSON和Java API提供其基本所有的特性。
#2、ES基本概念
* 集群（Cluster)

ES集群是一个或多个节点的集合，它们共同存储了整个数据集，并提供了联合索引以及可跨所有节点的搜索能力。多节点组成的集群拥有冗余能力，它可以在一个或几个节点出现故障时保证服务的整体可用性。
集群靠其独有的名称进行标识，默认名称为“elasticsearch”。节点靠其集群名称来决定加入哪个ES集群，一个节点只能属一个集群。

* 节点(node)

一个节点是一个逻辑上独立的服务，可以存储数据，并参与集群的索引和搜索功能, 一个节点也有唯一的名字，群集通过节点名称进行管理和通信。

一般有一下几类节点：主节点(master node)、数据节点(data node)、摄取节点(ingest node)、协调节点(coordinate node)、冷/热节点(hot/warm node)、Machine Learning Node

节点类型|配置参数|默认值
--|:--:|--:
master|node.master|true
data|node.data|true
ingest|node.ingest|true
coordinating only|无|每个节点默认都是coordinating节点，设置其他类型全部为false
marching learning|node.ml|true(需enable x-pack)


* 索引（Index)

索引是具有类似特性的文档的集合，相当于一个数据库，或者一个数据存储方案(schema)，索引由其名称(必须为全小写字符)进行标识，并通过引用此名称完成文档的创建、搜索、更新及删除操作，一个ES集群中可以按需创建任意数目的索引。

* 文档类型（Type）

文档类型是索引内部的逻辑分区(category/partition)，一个索引内部可定义一个或多个类型(type)，相当于数据库中的“表”。

* 文档（Document)

文档是Lucene索引和搜索的原子单位，相当于数据库的表“记录”。

* Mapping

用来约束文档字段的类型，相当于数据库中的“schema”。

* 分片(shard)

ES的“分片(shard)”机制可将一个索引内部的数据分布地存储于多个节点，它通过将一个索引切分为多个底层物理的Lucene索引完成索引数据的分割存储功能，这每一个物理的Lucene索引称为一个分片(shard)。
每个分片其内部都是一个全功能且独立的索引，因此可由集群中的任何主机存储。

>Shard有两种类型：主分片(primary shard)和副本分片(replica shard)
>1、主分片用于文档存储，新建一个索引需指定分片数量，一旦索引创建完成，其Primary shard的数量将不可更改。
>
>2、副本分片是Primary Shard的副本，用于冗余数据及提高搜索性能，每个Primary shard默认配置了一个Replica shard，但也可以配置多个，且其数量可动态更改。ES会根据需要自动增加或减少这些Replica shard的数量。
