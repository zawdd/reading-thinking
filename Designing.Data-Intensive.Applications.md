## 1.reliable scalable and maintainable applications
data intensive applications need to :
1. databases: store data and find again
2. caches: speed up reads
3. search indexes: find by key word
4. stream processing: send message, handle asynchronously
5. batch processing: periodically crunch large data
various approaches to cacheing, searching and so on, and it hard to combine tools. applications code stitch those tools together.
### Reliability
The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or soft‐ ware faults, and even human error).
**tolerating certain types of faults, not all, and the important is know which faults need to be handled**
#### Hardware faults
1. add redundancy: RAID, dual power, hot swappable CPUs, diesel generator: word for one machine
2. multi-machine redundancy work for small applications
3. large number machines: software fault tolerance
#### Software errors
systematic faults, things may help:carefully thinking about assumptions and interactions in the system; thorough testing; process isolation; allowing processes to crash and restart; measuring, monitoring, and analyzing system behavior in production.
#### Human errors
How do we make our systems reliable, in spite of unreliable humans?
*I think: 用规则，互相check*
1. Design systems in a way that minimizes opportunities for error.
2. Decouple the places where people make the most mistakes from the places where they can cause failures.解耦最容易出错的地方，和最容易导致失败的地方。sandbox, use real data, without affecting real data.
3. Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests.
4. Allow quick and easy recovery from human errors.minimizes the impact of failures. like roll back.
5. Set up detailed and clear monitoring,
6. Implement good management practices and training.
### Scalability
As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth
两个方面：访问量扩大，或者处理的数据增大
#### Describing Load
1. 描述系统当前的负载
2. 用何种负载指标来形容负载，qps？读写速度？同时在线用户数？cache率？
#### Describing performance
1. 观察随负载增加后，现有环境下系统的性能
2. 观察需要增加多少资源，才能使得增加负载后的系统性能和以前持平
**机械震动还会导致请求同一个请求两次之间的响应时间有差异**
* p95,p99分位，提升很难，代价大，效果甚微，但是头部客户往往是那慢的百分之一，因为数据量大。
* Queueing delays often account for a large part of the response time at high percen‐ tiles.几个个头部队列的慢请求，会影响后面的快请求，并发度低时。
the right way of aggregating response time data is to add the histograms
#### Approaches for Coping with Load
An architecture that is appropriate for one level of load is unlikely to cope with 10 times that load.所以负载增大10倍后系统什么地方最容易出问题，是个好问题。
大量体现在各方面，读写存储复杂度，所以没有一个magic scaling sauce的架构解决所有问题
### Maintainability
Over time, many different people will work on the system (engineering and oper‐ ations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively
Every legacy system is unpleasant in its own way.
Three design principles for software systems:
1. Operability:Make it easy for operations teams to keep the system running smoothly.
2. Simplicity: Make it easy for new engineers to understand the system.
3. Evolvability:Make it easy for engineers to make changes to the system in the future.Also known as extensibility, modifiability, or plasticity.
#### Operability
Good operability means having good visibility into the system’s health, and having effective ways of managing it.
good operations team:
* monitoring health and restoring service
* tracking down the cause of problems
* keep update, security patches
* keep tabs on how different systems affect each other.一个问题的修改会影响其他的
* Anticipating future problems and solving them before thewhich initially had a large following but eventually faded into obscurityy occur
* establish good practices and tools for DEV and OP
* performing complex maintenance tasks, 比如迁移
* 维护系统的安全性,比如配置的更改
* 定义流程使得操作可以预期，保持生产环境的稳定
* 保留下来系统的相关知识，形成wiki
#### Simplicity
Complexity是一种accidental 它不是软件要解决的问题中的本质问题，而是指开发中由于实现而带来的一种意外，常见的解决这种复杂度的方法就是抽象。好的抽象不仅能够减少复杂度，而且有更好的性能。
#### Evolvability
Agile敏捷开发，传统敏捷开发的针对的模块规模较小的代码，如何针对大的系统进行，比如对一个重要功能进行重构。我认为需要首先完善相关测试，然后进行逐步的开发重构，对一个功能进行逐步分解，然后每个步骤都进行灰度的替换，通过测试保证重构的代码正确。
## 2.Data Models and Query Languages
对于分层，核心问题是：how is it represented in terms of the next-lower layer?把现实表述为Model把，数据表述为Json，table，graph等。数据模型data model决定了后续上层应用的功能，对整个系统有深远的影响，因此选择需要谨慎。
### Relational Model VS Document Model
面向对象的编程语言，经常需要转化对象到关系数据库的行和列（impedance mismatch)，因此有了专门做此转化的的框架，hibernate等。但是这还不够方便，后续就有了对象关系数据库，基于Document，存JSON，XML等。
存ID不存字面，便于后续的改变，由于ID是对人类无意义的，所以任何时候都是ok的，方便国际化，减少冗余。
Document databases，joins are not needed and often weak.对于上述ID的情况，是一种典型的多对一的场景，关系数据库很方便，利用join，对于Document数据库则不是。对于多对多的情况，类似。
#### Are Document Databases Repeating History?
对于上述问题，似乎又无解了。两个好的模型解决：
* relational model:which became SQL, and took over the world
采用关系数据库存，you only need to build a query optimizer once, and then all applications that use the database can benefit from it. 以优化器来解决查询优化和查询复杂的问题。
* network model:which initially had a large following but eventually faded into obscurity一开始火，后来默默无闻
思路：In the tree structure of the hierarchical model, every record has exactly one parent; in the net‐ work model, a record could have multiple parents.the link just like pointers.In the tree structure of the hierarchical model, every record has exactly one parent; in the net‐ work model, a record could have multiple parents.
缺点：更新复杂，需要在应用程序中记录这些关系，从而才能查询。
**现在document数据库一方面以网状存数据，类似于过去，但是当表达多对一，多对多的关系时，这个关系对象，会用一个唯一的标示符identifier引用，类似关系数据模型的外键，或者document model中的document reference。这个identifier用来做join活连续查询**
#### Relational Versus Document Databases Today
the document data model are schema flexibility, better performance due to locality
The relational model counters by providing better support for joins, and many-to-one and many-to-many relationships.
#### Schema flexibility in the document model
document databases are schema-on-read!so the traditional approach of relational databases are schema on write.
#### Data locality for queries
it is generally recommended that you keep documents fairly small and avoid writes that increase the size of a document.
grouping related data together for locality:column family concept.
###  Query Languages for data
SQL是declarative的，SQL 是根据关系代数的转化而来的，告诉平台你的意图，条件，但是并不说明如何达到这个目标，易于并行化，隐藏了实现细节。普通的编程语言是imperative, 告诉平台具体的操作，和顺序，不容易并行，
Css是declarative而javascript对应的dom api就是imperative.
#### MapReduce Querying
mongodb等有以JSON形式描述的SQL查询。
### Graph-Like Data Models
以图形式作为数据模型，比如social graphs，web graph，road or rail networks.图中的点和边，不一定要是相同的。many ways of structuring and querying data in graphs.
#### Property graphs
每个点和边都有属性，然后相当于两张关系表，一张是边的，一张是点的，记录他们间的关系。the cypher query Language用来操作这种模型。query的好处在于忽略细节，底层来做查询优化。SQL可以用recursive common table expressions技术来查询关系数据库模型达到上述目的，不过复杂的多。
#### Triple store
In a triple-store, all information is stored in the form of very simple three-part state‐ ments: (subject, predicate, object). For example, in the triple (Jim, likes, bananas), Jim is the subject, likes is the predicate (verb), and bananas is the object.
主谓宾的形式描述事实，主语和宾语是点，谓语就是边
网页也可以表示这种数据，一个网页可以是一个主语，也可以是一个谓语，这样就连成了一个语义网络。SPARQL query language用来查这种数据模型。
#### The Foundation:Datalog
it provides the foundation that later query languages build upon.Instead of writing a triple as (subject, predicate, object), we write it as predicate(subject, object).
## 3.Storage and Retrieval
上述的模型，在实践的时候会有些取舍。会话的处理和分析与查询的优化是两个关键。two engines: log-structured storage engines, and page-oriented storage engines such as B-trees.well-chosen indexes speed up read queries, but every index slows down writes.
### Hash Indexs
1. 一开始我们用追加的文件的形式记录数据，然后遍历全部数据查询
2. 然后我们采用hashmap，保存文件中新写入数据的偏移，然后把hashmap保存在内存中，以此作为索引
3. 当文件越来越大时，分割文件，每达到一个大小后，就开辟新的文件（segment），老的文件可以压缩（包括删除老的数据）
4. 压缩后的文件会变小，于是可以再次合并，写入新的文件。合并时查询依然查询原来的文件，完全合并后才删除老的文件，这样也减少了碎片，合并压缩的操作都是后台的。
**很多阿里，百度的开源系统其实就是继续此思想，但在实现时考虑到更多的细节，每个细节有不同的解决方案，此时需要根据业务需求做trade off**
如：文件格式（二进制最好），删除数据怎么表示（可以加特殊flag），崩溃后的恢复（内存种的hash表如何恢复：可以定时做snapshot),部分写（类似事务性），并行读写（单线程写，多线程读）
追加日志方式的优点：
* 连续写的效率高于随即写
* 并发和灾难恢复简单（可以理解为写文件写一条数据是个原子操作）
缺点：
* hash table必须要能放入内存
* 连续key的范围查询效率低，因为每个key都要走hash
### SSTables and LSM-Trees
上述文件中的key，要让其有序，并不会破会顺序写，叫做Sorted String Table，一个key在一个segment文件中只出现一次。优点：
1. 便于合并，由于有序，内存中装不下也好合并。key相同时，由于segment生成的时间有先后，可以用来决定保留那个key的值。
2. 内存中保存的不是所有的key，类似B＋树，只是部分key，由于有顺序，找到一个key后可以再顺序找具体的key，这样减少了内存中要维护的hashmap的大小
3. 两个key之间的范围的keyvalues可以压缩成一个block，这样，内存中的key指向的就是这样的block，由于压缩，也减少了IO的带宽。
#### Constructing and maintaining SSTables
how get the data sorted by key in the first place.在磁盘上采用B树，内存中采用红黑树，AVL树，都可以以任意顺序插入，然后顺序读。
先写内存中写一个树，写大一定大小，才写到文件。读的时候需要从内存中的数据开始查找，然后以此每个segment，后台再定时合并压缩segment。为了防止崩溃，内存中的数据消失，就先写一个log，当所有内存的数据都写到磁盘上时，这个log就可以清除。
#### Making an LSM-tree out of SSTables
Log Structured Merge Tree,building on Log-structured filesystems,这种基于合并和压缩排序文件的叫做LSM存储引擎。Lucene就是其中一个应用，
优化问题：
1. 当key不存在时，需要遍历所有的segment，为了解决，引入了Bloom filters，布隆过滤器
2. 两种压缩与合并的策略，size-tiered and leveled  compaction:In size-tiered com‐ paction, newer and smaller SSTables are successively merged into older and larger SSTables. In leveled compaction, the key range is split up into smaller SSTables and older data is moved into separate “levels,” which allows the compaction to proceed more incrementally and use less disk space.
### B Trees
把数据库分为固定大小的blocks或pages，每次读写一块，类比硬盘。每个page可以存别的page的位置作为索引，一个节点指向几个叶子叫做branching factor,由数据量和key的范围决定，通常是几百。大多数数据库B树就4层，(A four-level tree of 4 KB pages with a branching factor of 500 can store up to 256 TB.)，为了防止写时出错，程序崩溃，采用WAL，write ahead log/redo log。还要考虑并行写时的枷锁问题。
#### BTrees optimizations
1. Copy On Write策略，帮助并行写和crash recover
2. key可以缩写以减少空间，一个page中跟的key，必定再其上面的索引的范围内
3. 叶子的page如果能连续，性能会好，但是比较难
4. 叶子page加上其前后page的指针，帮助scanning in order
### Comparing B-Trees and LSM-Trees
B-Trees faster for read, and LSM faster for write,但需要根据特定的业务去选择合适的。
LSM后台会进行压缩合并，在高分位的写压力的请款下会有影响，因为硬件的性能有限，而且这种处理过程是无法预期的，这点不如BTree，由于BTree中一个key只存在一个地方，所以数据库多用此存储引擎，便于实现事务。
### Other indexing structures
构建secondary index，很多value有同一个key，处理方法：This can be solved in two ways: either by making each value in the index a list of matching row identifiers (like a postings list in a full-text index) or by making each key unique by appending a row identifier to it. Either way, both B-trees and log-structured indexes can be used as secondary indexes.
clustered index (storing all row data within the index) 解决读时需要根据指针找value的问题
#### Multicolumn indexes
concatenated index, which simply combines several fields into one key by appending one column to another。比如经纬度的检索，Btree和LSMtree不适合，对于此特例用RTree
#### Full-text search and fuzzy indexes
Lucene底层基于SStable，内存中，有有限状态机Levenshtein automation，支持给定一个编辑举例后的词的检索
### Transaction Processing or analytics
OLTP（低延迟少数据量的读写）和OLAP（大数据量的查询，批量倒入数据ETL，或流式倒入数据）
### Data Warehousing
专门用于OLAP，数据仓库针对数据分析对索引以及存储引擎都做了专门的优化。
#### The divergence between OLTP databases and data warehouses
SQL good for analytices, so use relational data model. drill-down and slicing and dicing.商业数据仓库Teradata, Vertica, SAP HANA, and ParAccel ，开源的：Apache Hive, Spark SQL, Cloudera Impala, Facebook Presto, Apache Tajo, and Apache Drill [52, 53]. Some of them are based on ideas from Google’s Dremel
#### Stars and Snowflakes:  Schemas for Analytics
数据残酷的数据模型比较单一，star schema (also known as dimen‐ sional modeling [55]).由许多真实的数据库表，构成一个可供查询的fact table，里面的key都是外键，其他的表围绕着这个fact table，所有叫star table
#### Column-Oriented Storage
基于OLAP每次查询需要的列只有几列，所以以列存储，查询时不需要读取所有的数据。列存储不只是关系数据库才有，非关系也可以用列存储。
#### Column Compression
基于列存储，就很容易压缩，采用bitmap encoding，除了压缩，爱便于列条件的过滤，and就是位AND，in就是位OR，同样列有利于CPU的处理，以此读取一串进入L1 cache，这叫做vectorized processing
#### Sort Order in Column Storage
列排序，底层可以按照SSTable的思想，每个列中每行的对应关系不能变。每份数据按一个顺序存，这样，各种排序时可以受益。原始数据保存在一处，其他的索引指向指针，指针找数据。
#### writing to column oriented Storage
采用LSM tree，先在内存中写，然后再和磁盘原有的数据，merge成新的文件。
#### aggregation
materialized views, 把聚合后的结果直接存储，便于查询，但是写复杂。一种特例叫做data cube。
## Encoding and Evolution
作为服务端的程序，需要考虑rolling upgrade or known as staged rollout,作为客户端程序，要考虑到客户可能不更因，即都要考虑一个兼容问题。
Backward compatibility
Newer code can read data that was written by older code.
Forward compatibility
Older code can read data that was written by newer code.
而这里既有代码的兼容，也有数据的兼容，于是不同的格式数据有不同的用途
### Formats for Encoding Data
* 内存中，各种对象，表，数组，hash，树，都是针对CPU优化的
* 为了持久化，需要编码内存的数据。
一个语言中的序列化和语言耦合太紧，而且为了能反序列化，解码程序需要能够实力化任何类，这有安全问题，可以远程代码执行，而且效率低，又无法forward和backward compatibility
### JSON,XML and Binary Variants
解决上述的同时，问题：编码的信息有歧义，比如数字和字符串，数字无法指示精度，位数类型。JSON XML对二进制字符串支持不好。所以有了Base64，但增长了33％，CSV格式，no schema。
#### Binary Encoding
把JSON等用二进制编码减少空间
#### Thrift and Protocol Buffers
Thrift from facebook and Protocol buffers from google, Thrift has two different encoding format, one is binaryProtocol other is CompactProtocol. Compact的方法，利用没个字节的高位的0个1表示这个数据是否后面还有数字。protocolbuffer和compact的类似。required和optional的配置对具体编码没有影响，是运行时的一个检查。
只要不是required的字段的变动，schema可以前向后向兼容。proto不需要类型，thrift需要存类型。
#### Avro
由于thrift not fit for hadoop's use case.严格依赖定义的schema来解析，可以有一个writer schema和一个reader schema，avro来做翻译，把写的和读的schema中的字段对应上，为了前向和后向兼容，定义的字段要有默认值，这样翻译时发现缺少了字段可以用默认值。
当用在数据库时，可以每个record维护一个版本号，一个版本号对应一个schema，这样reader就知道用正确的writer的schema了。
一个优势，Avro不含有tag number，因此更适合动态生成schema，不需要考虑哪个tag number对不对
### The Merits of Schemas
## Modes of Dataflow
为了传输数据需要对数据编码成二进制，之后考虑传输，传输有databases, service calls, asynchronous message passing这三个方式
### Dataflow through databases
前向兼容和后向兼容的编码，当其经过应用程序后，转化为对象，再序列化，会丢失新增的field。数据会活的比代码久 data outlives code
### Dataflow through services :REST and RPC
Service oriented architecture SOA就是现在所谓的微服务。A key design goal of a service-oriented/microservices architecture is to make the application easier to change and maintain by making services independently deploya‐ ble and evolvable.
RPC有种种缺陷，区别于本地调用，但是近来也有新的更新，比如采用Protocol buffer等作为RPC的协议，显示的区别local function。RPC的性能会比REST好，通常用在同一个组织的，同一个数据中心中。为了sever和client的版本兼容，请求中可以加上版本号。
### Message Passing Dataflow
RabbitMQ, ActiveMQ, Hor‐ netQ, NATS, and Apache Kafka。采用Actor model，一个actor处理一条消息，有利于多线程并发的设计。
## Distributed Data
three reasons:
1.Scalability
2.Fault tolerance/high availability
3.Latency (users around the world)
### Scaling to Higher Load
share memory architecture: limited to a single geographic location
share disk architecture: contention and the overhead of locking limit the Scalability
### Shared nothing architectures
also called horizontal scaling,
### Replication VS Partitioning
There are two common ways data is distributed across multiple nodes:
* Replication
Keeping a copy of the same data on several different nodes, potentially in differ‐ ent locations. Replication provides redundancy: if some nodes are unavailable, the data can still be served from the remaining nodes. Replication can also help improve performance.
There are two common ways data is distributed across multiple nodes:
* Partitioning
Splitting a big database into smaller subsets called partitions so that different par‐ titions can be assigned to different nodes (also known as sharding).
这两个机制经常配合使用
## Chapter 5 Replication
three popular algorithms:single-leader, multi-leader, and leaderless replication, 复制数据最大的问题就是要处理数据的变化
### Leaders and Followers
how do we ensure that all the data ends up on all the rep‐ licas?The most common solution for this is called leader-based replication (also known as active/passive or master–slave replica‐ tion)
### Synchronous Versus Asynchronous Replication
可以兼顾这两者，更新5个子节点，如果由3个返回就可以返回了，另外两个异步。纯异步的依然用的很多，当子节点够多时，失败的风险就很小了。
异步最大的缺点是learder失败时会丢数据，还有就是数据一致性的问题，确定不同的值该用哪一个。微软用了chain replication来解决这个问题，
### Setting Up New Followers
问题：同步数据给新节点时，不能通过增加锁来牺牲高可用性
解决：1. 获取数据库某一时刻的快照，2 复制快照到新节点，3，新节点向leader请求快照后的增量（生成快照也打在leader的log里，就能区分那些数据是快照后的）4. 新节点追上所有的数据后认为启动完成
### Handling Node Outages断电
1. 节点恢复
2. leader failover, 探测leader失败，选择新的leader，重新配置新系统使得使用新leader，旧的leader即使恢复也要成为节点。
* 如果采用异步复制，新leader可能没有全部数据。之后旧leader上线后，新leader数据会不一致。这里一般会放弃旧leader中的unreplicated的数据
* 放弃discard数据会有风险，有可能这部分数据已经被别的系统使用了，比如自增的mysql主键，从而会冲突
* 防止脑裂，发现两个leader自动杀掉一个，若此机制设置不好又会杀掉两个leader,**如果机器够多，恢复机制完善不如两个都杀了省事**
* 通过超时判断leader是否live的超时时间的设置
因为这些的复杂性，所以有时候即使有自动恢复的机制也用手动的
## Implementation of Replication Logs
几种不同的replication方法的实践
### Statement-based replication
leader把所有写操作的语句日志发给子节点，让其执行，其中的问题：
>执行失败怎么办？是否需要等待每个子节点都更新成功才返回？ 执行成功的才入log，后者是复制机制的问题

* 使用了非确定结果的语句结果可能不一致，比如NOW，RANDOM等函数
* 需要严格的保证执行顺序，因为语句之间可能会有依赖，这在有多个并行执行的事务时很难保证
* 语句的副作用side effects，在不同的副本上可能会不一致，比如triggers，函数等
解决：leader替换所有不确定的函数的call为固定的返回结果，不过有很多边界条件，因此该方案不是首选的。
### Write-ahead log (WAL) shipping
这里的log发的是记录到leader上的数据，然后同步发给子节点，利用只追加的日志。这里的日志就是底层数据，两者格式一样。问题在于这种日志太大了，几乎相当于存储的一倍。主从节点的软件版本要一致，不然新版本的数据，老版本就无法处理了。如果复制协议可以兼容不同的版本，就能online升级，否则只能offline升级整个系统
### Logical(row based) log replication
对于复制日志，和本地存储用不一样的log，从而复制协议的log和存储引擎解耦。把变化的数据，以行的形式记录到复制日志（logical log）然后下发给其他的节点，其实就像用中文告诉每一个节点怎么更新数据。对于事务增加一个标示，指明之后的几行是事务mysql的binlog采用这种方式。便于其他应用程序处理复制log
### Trigger-based replication
利用trigger探测数据的改变，然后交由其他应用来处理数据的复制，这种方法更灵活，可以控制那部分数据需要复制，还能加入一些其他的逻辑，但是负载高，而且容易出bug，比起利用存储引擎内置的复制机制。
## Problems with Replication Lag
复制数据不仅为了容错，提供高可用性，还有就是提供扩展能力，提供低延迟的数据访问。因此要解决复制的滞后问题。
对于读扩展的架构，可以增加节点，提升读的性能，但是需要异步复制机制，否则一个节点的同步写失败，会导致整个写不可用，节点越多越可能出问题。所以完全同步的复制机制不现实。
因此采用异步复制，但是导致短期数据主从不一致，但是最终一致。一般要做到1s以下。
当主从延迟会出的问题：
### Reading Your Own Writes
用户刚提交的数据，要给用户展示出来，要保证read after write consistency，解决方法：
1. 当读取用户会更改的数据时从leader上读
2. 当大多数数据用户都可以改时，要增加规则，比如最新更新的数据从leader上读
3. 客户端可以记录最新更新的时间，这样去子节点读时，发现没有这个时间的就去别的副本上读，否则一致等待数据。
4. 当有多个数据中心时，就要路由到包含此leader的中心上去
还要保证跨设备的一致性，
1. 跨设备不容易知道最近的数据更新时间了，需要一个集中的服务，记录这个时间
2. 不同设备可能连的不是同一个数据中心，leader都不一样，需要先路由到同一个leader
### Monotonic Reads
主从延迟会导致moving backward in time现象，先读了一个低延迟的从库，然后读了一个高延迟的从库，时光倒流了看起来。monotonic reads比强一致性弱，比最终一致性要强。如果用户的一系列请求读到了新的数据，则不再去读老的数据。做法，保证一个用户总是从一个副本读取数据，这就是通常为什么用userid或hash路由，而不是随机
### Consistent Prefix Reads
主从延迟，导致第三者观察A，B俩者的信息时会出现因果倒置。Consistent Prefix Reads保证，如果写操作是有顺序的，那么任何读这些写操作的，都需要保证顺序。分布式DB中常见，由于每个partition操作是独立的，没有全局的写顺序。解决：保证有因果关系的写在同一个partition，但是这比较难。有算法显式的跟踪因果依赖
## Solutions for Replication Lag
如果最终一致性解决不了问题，那就需要考虑强一致性。假设是同步复制考虑问题，而事实上用异步复制。应用程序应不要关注这个问题，让DB保证，DB利用事务保证强一致性
## Multi-Leader Replication
单个leader一旦失败，整个系统都无法写
### Use Cases for multi leader Replication
当多个数据中心时可以多个leader一个中心一个，否则多leader的复杂性比收益小。致命缺点可能会写冲突。还有如自增key，触发器等性质也会由于多leader而带来问题。所以还是应该尽量避免muti leader
#### Clients with offline operations
用户线下的操作需要后期同步到服务端，如果每个设备上都有一个calendar，则每一个设备都是一个local的存储，都是一个leader。于是这也是一个multi leader的问题，该问题没有很好的解决
#### Collaborative editing
实时的协作编辑，又许多utomatic conflict resolution方面的研究，这也是一个mutil leader的问题，会导致写冲突，一般就是加锁，可以更细粒度，更段时间的加锁。
### Handling Write Conlicts
#### Synchronous versus asynchronous conflict detection
把异步检测冲突变成的同步的，然后就可以提示其中一个写的用户，目前已经有冲突了，但这样又失去了multi leader多用户共同在线编辑的优势
#### Conflict avoidance
避免冲突，使得一个用户创建的数据都走一个leader，别人修改这个数据也要走同一个leader，问题是数据的leader有可能改变。
#### Converging toward a consistent state
数据最终趋于一致，解决方法：
1. 每个写操作赋予唯一ID，最后一个ID作为写的赢家，可以写，last write wins （LWW）缺点会造成数据丢失
2. 给每一个副本一个唯一ID写只写到最高ID的副本上，问题同1
3. 把修改的值merge到一起，同时披露出来（局限性太强）
4. 把冲突记录下来，并交由后来的用户处理
#### Custom conflict resolution logic
让用户来定义这种multi leader的应用应该如何处理在读／写时的冲突，冲突解决方案一般只应用在row或者document的粒度，而不是整个事务
#### What is a Conflict
冲突的种类，有的比如两个人同时写一个字段，这种比较容易发现，还有比如两个人同时预定一个会议室，这种就难以发现，类似订票之类的，在multi leader下更容易出问题，后面会讨论。
### Multi-Leader Replication Topologies
写操作在依据不同的传播规则在多个leader间传递，比如星型拓扑，树状拓扑，环状拓扑，全部点对点的toplogy等，点对点拓扑会使得消息的顺序错乱，其他的拓扑则当节点fail时需要复杂的手动恢复，为了防止点对点时写顺序错乱，采用version vectors技术。很多multi leader的数据库并不保证检测冲突，使用时需要谨慎。
## Leaderless replication
Amazon Dynamo 数据库，没有leader，每个client都可以写，不能保证写的顺序。
### Writing to the database when a node is down
无leader的数据库在读的时候也会同时并行的读每个节点，取版本最新的数据
#### Read repair and anti entropy
需要保证最终一致性，若实效节点重新上线后应该如何获取其已经错过的写操作呢？两个机制
1. Read repair，读的时候修复版本落后的数据
2. anti-entropy process,有一个后台程序发现每个副本间的不同，然后复制修改，和基于log，基于leader的架构不同，这种复制不会有顺序，也不保证延迟。
#### Quorums for reading and writing
读写要保证有规定比例的实例返回正确才人为成功，w+r>n保证读写的节点至少有一个是一样的，最新版本的数据才能被读到。这个数字需要根据读写的特征调整，当写少读多时，可以w＝n r＝1减少读的时间，请求会发到所有的节点，w，r只是等待返回的个数。
### Limitations of Quorum Consistency
设置Quorum只用读写有至少一个node是overlap的就行，并不强制要求w，r都要超过n/2，所以有时候会设置较小的w和r，这样当网络大面积不稳定时，有超过n/2的节点有问题时，读写请求依然可以返回，虽然有概率会读到旧版本的数据，但总比不可用强。
即使设置了w＋r>n也并不能一定保证是正确的，比如并发写时的冲突，读写同时进行时，部分写失败时读
所以还需要很多其他的优化，只有w r不能保证服务一定是可用的。要保证最终一致性。
#### monitoring staleness
由于写没有顺序，监控难做，但是仍要监控当前有多少节点的数据是旧的，从而知道当前系统是有网络问题，或者负载过大。
### Sloppy quorums and hinted handoff
leaderless的系统适合，读延迟低，兼容独立节点失败，能够容忍都到旧数据的应用。
当网络中断，节点数目达不到quorums时面临一个trade off
* Is it better to return errors to all requests for which we cannot reach a quorum of w or r nodes?
* Or should we accept writes anyway, and write them to some nodes that are reachable but aren’t among the n nodes on which the value usually lives?
后者就是sloppy quorums，比如当写时需要w个节点，当前没有w个了，就从其他能用的节点里（不在原来的n个中）挑选来写，等到网络恢复后再把这个临时写的给写回到原来规定的w个节点中取，这个叫做hinted handoff。这种方案就不能保证读时至少能够读到一个最新的值，但是可用性高很多，所以目前的设计中很多数据库都会采用。
#### Multi datacenter operation
leaderless also suitable for multi datacenter
### Detecting Concurrent writes
无leader和multi leader的问题一样，写的顺序会不一致，会有写失败，都导致了写冲突，为了实现最终一致性怎么办？（给每个数据增加版本号？）
* Last write wins：很难定义顺序谁先谁后，并发写时有的节点的写的结果由于顺序落后会被丢掉，但是返回给客户端的还是成功。LWW用在缓存上可以，用在数据不能丢失的冲突解决方案中就不行了。或者保证每次只写一次，即给操作定义一个UUID
* The happens before relationship and Concurrency
如何定义顺序和并发，若有后一个操作依赖前一个，那么就是有顺序的，并不依赖时间戳来判断，只有判断的两个操作的顺序类型，才能知道是要处理顺序问题还是并发问题。
1. 如何发现顺序关系？
每次操作增加版本号，读数据时除了返回所有的数据，还要返回最后的数据版本号，读的客户端根据它上次已知的版本号可以读出写之前的数据，写操作时也需要提交它上次的读的版本号，然后进行数据merge。带版本号的写就是有顺序的，如果写时不带任何版本号，那么就是和其他写是并行的
2. merging concurrently written values
保证不会丢失数据，然是需要客户端做额外的merge工作在写的时候，这个merge的工作通过好的数据结构和设计能够做到自动化，比如Riak的CRDT
3. Version vectors
上述是只有一个副本，当有多个副本时，版本号就变成了版本号向量（类似vesrion clock），Riak中用到dotted version vector，版本号用来让服务器知道是overwrite还是concurrent write。
### Summary
Single-leader replication is popular because it is fairly easy to understand and there is no conflict resolution to worry about. Multi-leader and leaderless replication can be more robust in the presence of faulty nodes, network interruptions, and latency spikes—at the cost of being harder to reason about and providing only very weak consistency guarantees.
## Chapter 6 Partitioning
真对事务处理，还是数据分析，会导致不同的设计和调优
### Partitioning and replication
这两者通常是配合的
### Partitioning of Key-Value Data
为了均匀分布用随机分配，但是随机的缺点是查询时不知道一个具体的partition在那个node上，必须要query所有的node
* Partitioning by key range
会导致热点，优点可以根据返回查询几个node不用全部
* Partitioning by hash of key
一致性hash为了balance partition，hash后排序性会丢失，而且也要query所有的node，可以把两者结合，比如userid作为hash partition，后面再跟timespan作为key range partition。
### Skewed workloads and relieving hot spots
当一个keyid是热点时，进行hash不会有所帮助。底层数据库通常不管，由上曾业务系统增加一个逻辑解决这类热点问题。但是为了分布写的压力，在读上就要进行额外的操作。
### Partitioning and secondary indexes
The problem with secondary indexes is that they don’t map neatly to partitions. There are two main approaches to partitioning a database with secondary indexes: document-based partitioning and term-based partitioning.
* Partitioning secondary Indexes by Document
每一个partition有其自己的secondary index，读时不友好，请求需要并发到所有的partition
* Partitioning secondary Indexes by term
有一个global secondary index，再把这个index做partition，也就是说secondary index在一个partition中只有一部分，但是这一部分中的每一个key都是对应了全部的数据，该方案写的时候需要有事务，通常做成异步的
### Rebalancing partitions
至少要满足三个需求，rebalancing后所有流量均衡，负载均衡时读写不能受影响，应该尽可能快，带宽占用尽可能的少，不要移动不必要的数据
#### Strategies for Rebalancing
* how not to do it: hash mod N
N一旦变化，所有的partition都要变化，代价太大，所以一版都是把hash后的key根据range分配到不同的节点上
* fixed number of partitions
设计一个远大于节点数目的partitions数目，然后把一批partitions分到一个node上，partitions不能太多也不能太少，这在数据集会变化的情况下，是不容易设计的
* dynamic Partitioning
初始化时设置一定的partition，除了基于key ranged，也可以基于hash partition。
* Partitioning proportionally to nodes
每一个节点分片不一样，如果增加数据，节点的分片就分裂，有算法避免分割的不均衡
#### Operations: Automatic or Manual Rebalancing
自动化的rebalancing，需要管理员确认。全自动的会出现不可预测性，rebalancing操作代价会很大（比如流量高峰期的时候触发均衡，就不如夜间流量低峰的时候手工触发），有一个节点坏了时候，又会触发rebalancing，系统的负载就会更大。
### Request Routing
如何知道一个key在那个节点，请求的分发，也是服务发现的问题。
1. 随机发请求到一个节点，让该节点去判断转发请求到那个节点
2. 请求发给一个router模块，然后让该模块决策发到那个节点
3. 客户端直接知道发请求到那个节点，不要中间模块
the key problem is: how does the component making the routing decision (which may be one of the nodes, or the routing tier, or the client) learn about changes in the assignment of partitions to nodes.
需要所有的节点都要满足一致性和正确性，节点rebalancing后的信息要能正确同步到所有的节点包括router，client上。比如采用zookeeper把节点信息注册到zk上，zk节点有变动时会通知到所有的订阅者。
或者采用gossip protocol，在集群中同步变化，然后请求发到任意一个节点就能被再次正确路由，每个节点实现会复杂，但是避免了一个额外的zk服务。
若没有自动化的rebalancing则设计就会简单许多，只要有一个模块保存这种分区配置就可以了。
### Parallel Query Execution
把复杂的jion filtering，group的请求经过分析成若干查询过程，其中部分就可以进行并行执行。尤其是当扫描的数据量大时。
## Transactions
前面提到的分布式中要考虑的很多问题，其实事务就是解决和保证他们不出问题的一种机制。但是事务本身是为了简化编程的模型。
### The Slippery Concept of a Transaction
很多nosql的数据库，都以分布式，可扩展性为理由，不支持事务。
#### The Meaning of ACID
一个数据库所实现的ACID和另一个的不一定相同，所以一个数据库宣称自己实现了完全的ACID，细节却不一定。BASE： Basically Available, Soft state, and Eventual consistency
* Atomicity
ACID中的原子性和多线程的不一样
* Consistency
是一个应用中的概念，对数据来说只有原子性，独立性。
* Isolation
并发执行的操作，每一个是互相独立的。经典数据库往往吧isolation转化为serializability。但是会有性能问题。所以会实现弱的isolation，如snapshot isolation
* Durability
单机上，意味着数据持久化了，多副本意味着每个副本都同步了写的操作。不存在绝对的持久化，都可能会出问题。需要多种技术配合使用，以减少每个单独技术失效的风险
#### Single Object and Multi Object operations
多个操作如何判断属于同一个事务，一般通过客户端自己写BEGIN COMMIT，同时每个事务还会有独立的ID，用另外的TCP连接传输。对于菲关系型数据库一般没这个保证
* Single-Object Writes
单个数据的更新也要保证一致性，原子性，但是这个并不叫做事务
* The need for multi-Object Transactions
不能只用single的代替multi的
* Handling errors and aborts
对于事务，失败后重试是一个简单有效的策略，但是却不完美，比如事务已经完成了，比如由于负载重导致的错误，有副作用的事务，等等
### Weak Isolation levels
数据库提供的事务独立性，使得应用屏蔽了复杂的并发问题。为了性能考虑，不能串行化，所以用Weak Isolation，尽管方案更复杂，但依然用在实践中，以下是几种若的独立性的方案
#### Read Committed
* No dirty Reads
不会度取脏数据，读的谁都是commited的，如果一个数据被修改了还没有committed，则读的是其之前的数值。一个事务committed前对其他事务不可见。
* No dirty Writes
写的数据都是被committed的，通过推迟第二个写的事务。
该方案不能防止，两个计数器修改的问题
* Implementing Read Committed
为了阻止脏写，采用行级别的锁。为了阻止脏读，同样用锁，但是如果和写用一个锁，会导致写长实践阻塞读，所以大多数方案是，对于在写的数据同时保存新值和旧值。对于读的请求都给旧值。
#### Snapshot Isolation and Repeatable Read
Reads committed会导致短暂的不一致，但是有些憧憬不能接受，比如back up等，所以采用snapshot isolation 每一个事务肚脐一个consistent snapshot，适合于long runing，read only queries，用在MYsql的InnoDB存储中
* implementing snapshot isolation
用读锁来解决脏读的问题，会阻塞写。读的时候不用锁，读不会阻塞写，写不会阻塞读。同一个对象，数据库要保存多个commited的版本，MVCC。每个数据上都会根据事务id追加版本信息，这样每行数据其实多了两列，一个是created by一个是deleted by。删除的时候不真的删，只是标记，后续垃圾回收机制再删除。
* visibility rules for observing a consistent snapshot
当读的事务请求时，根据设定的可见性规则，来判断哪个事务的数据版本是这个读可见的。比如在读之后的写事务id，中断的写事务id都是不可见的
* Indexs and snapshot isolation
传统是对于所有版本的数据建索引，只不过根据版本信息做索引时的过滤，但是有许多优化的方法。比如update时不修改原page，而创建一个新的page，然后父节点指向新的page（数据库底层时B树），这叫做append only B tree，只要没有写操作影响就不用复制。这样每个写的事务都会创建新的一棵树（其实里面很多节点都是公共的，只有新写的节点才复制，不会复制那么多数据的），每次查询时根据版本查指定的树，就不需要过滤了。需要有垃圾回收机制。
* repeatable read and namming confusion
Oracle中这个技术叫做Serializable ，PostgreSQl MYSQL中叫做 repeatable read。
#### Preventing Lost updates
并发写导致的问题，lost update ，读-修改-写的俩事务并发，就会导致有一个clobbers另一个。
* Atomic Write operations
原子的更新操作，防止了应用层的read-modify-write的模式，但是并不是所有的写操作都可以用原子修改的方式重写。如果可以原子更新的方式通常是最好的。通常用锁实现原子更新，或者所有的原子操作放在一个线程中，
* Explicit locking
应用层实现显示的锁，防止lost update。有可能会忘记在应用层加锁，并且会导致race condition
* Automatically detecting lost updates
允许事务并行，但是数据库自动检测，如果有lost update，就阻止这个事务，然后会再顺序执行read modify write的事务，Mysql不支持，好处在于应用层可以不考虑lost update，但是出现这种情况时，会有性能损失。
* Compare-and-set
不支持事务的数据库，通常支持原子的比较set操作，防止lost update。但是如果数据库实现了snapshot isolation，这个compare set也会不安全，会读到old snapshot的值。就不知道别人已经修改了当前值，还是会lost update
* Conflict resolution and replication
对于多副本的，有多leader或者无leader的数据库，加锁，compare set技术都不适用，要采用Linearizability技术。原子操作支持可交换性，多个写操作的顺序可以交换而不改变最后的结果，基于此Riak实现no update lost
### Write Skew and Phantoms
除了dirty writes和updates lost并发写还会导致其他的race condtion。
比如write skew，同时更新两个对象，但是却导致某一个条件不成立了，比如值班医生不能少于1人，上述方法对这个问题都不好，在snapshot isolation 下只有严格的顺序执行能避免这个问题，通过加锁，增加约束也可以一定的解决，但是有些情况解决不了。这种情况会很多，比如网站起名字，同时两个人起相同的名字。
* Phantoms causing write Skew
一般都会select然后判断满足条件再修改，另一个事务修改的东西，影响到了第一个事务的select的结果，这种情况叫做phantoms
* materializing conflicts
把phantoms转化成数据库具体的可以加锁的列，有时候很难做这样的转化
### Serializability
Serializable isolation is usually regarded as the strongest isolation level.相比与weak isolation.用以下三个技术来实现顺序化的隔离性。目前讨论的都是单节点，多节点也可以扩展
#### Actual Serial Execution
单线程顺序执行每个事务。可行性：RAM便宜，内存数据库。OLTP事务通常都是小数据量的读写，长时间运行的一般都是读。VoltDB/H-Store Redis Datomic采用了这种机制。避免了锁和条件竞争，性能可能会比并行还好。吞吐受限于单个CPU核。为了尽量利用单线程的性能，还需要重新组织事务的格式。
* Encapsulating transactions in stored procedures
OLTP服务中，避免事务中在不断的轮询，等待应用输入数据，和应用进行网络交互，导致大量的事务闲置，如果只有单线程处理，这就会严重阻塞，影响性能。单线程的数据库中，不支持这种多交互的事务，必须一次提交全部事务SQL。这就叫做stored procedure。避免了等待网络和IO
* pros and cons of stored procedures
不好的地方：存储过程 语言不友好，缺乏库支持，每个数据库有自己的语言。不好debug，版本控制，部署，测试，监控，因为都是在数据库中执行的，不是在应用程序中。一个复杂的存储过程会吃掉大部分性能，导致影响用此数据库的其他应用的性能。这些都可以克服。比如Redis用Lua写存储过程，VoltDB会把存储过程在每个节点都执行。
* Partitioning
单线程写会有性能问题，这就需要分表，这样每一个事务就作用在一个partition，但是跨分区的事务就会需要额外的步骤，会慢，还无法水平扩展性能。
#### Two phase locking（2PL）
**两段锁和两段提交不同** 写操作不仅会阻塞其他的写，还会阻塞其他的读，和snapshot isolation中的要求不一样了。由于两段锁提供了顺序性，所以前面的各种race condition都不存在了。
* Implementation of two-phase locking
应用在Mysql InnoDB，SQL server，对象上有锁 in shared mode or in exclusive mode。共享锁，独占锁。共享锁大家都是加，但是只要有一个独占锁，共享都不能加。要写时必须获得独占锁，读时必须获得共享锁，先读后写操作，需要升级锁。一旦持有一个锁只有事务结束了才能释放。两段的含义就是，获取锁执行，和事务结束释放锁。这会导致死锁，数据库会自己检测并且杀死其中一个事务。
* Performance of two phase locking
性能差，减少了并发度。并且有的等待输入的事务会执行很长时间，其他的事务都阻塞了。死锁也会导致性能差。
* Predicate locks
解决Phantoms问题，对query的条件加锁，防止另一个事务更改第一个事务先前query的结果，类似要预测别的事务会phantom的修改该事务query的结果，所以这个锁叫做predicate lock
* Index range locks
predicate lock不work。所以大多实现2PL的采用index range lock（next key locking ),扩大了上面预测锁的范围，对索引加锁，这样其他事务基于此索引的query就不能执行了，就不用担心被phatom修改数据了。如果找不到适当的index，就会对整个表加shared lock
#### Serializable Snapshot Isolation （SSI）
完全的顺序化，性能牺牲小，2008年提出。单节点中和分布式中都有应用，PostgreSQl9.2版本后实现了SSI
* Pessimistic versus optimistic concurrency control
2PL是悲观的并发控制机制，SSI是乐观的，一个事务提交的时候，再检查是否有错误发生。只有顺序化的事务才能提交。乐观机制，有利有弊极端情况会导致大量事务重试，从而加重负载。事务间的竞争通过原子操作的交换来减少。所有的读，都是读的一致的snapshot，在top snapshot isolation，SSI增加了一个算法，检测顺序写的冲突，然后决定那个事务会被中断。
* Decisions based on an outdated premise
query请求的结果，其他事务会修改，导致outdate，如果事务中一个写操作依赖于这种premise query，就有可能会被中断。判断一个query的结果是否会变化：
1. Detecting stale MVCC reads（uncommitted write occurred before the read）
事务提交时，检查是否有其他事务的被忽略的写操作，还没有提交，如果有则事务中断（*从检查完，到提交这中间依然会有间隙，说不定正好此时数据改了，原子化此操作，加锁？compare set机制？*）
2. Detecting writes that affect prior reads (the write occurs after the read)
采用类似index range lock的思想，对索引或表加锁，不过SSI lock不会阻塞其他事务，这个锁只有事务执行时有，所有并发事务执行完就消失了。当一个事务有写操作时，需要检查这些锁，这里没有阻塞，只是一个提醒，这个索引上别的事务读过数据，现在你在修改，先提交的事务不会失败，第二个写的事务，就会发现有冲突。（*一行数据上有写版本号，也有读版本号，写的是本来snapshot带来了，ssi增加了一个读的版本信息，若顺序是T1R，T2R，T1W，则T2W要commit时，就会发现这四个版本不成顺序了，就有问题，顺序的只能是先T1，再T2，或者相反，不能互相穿插*）
* Performance of serializable snapshot isolation
上述的SSI锁的粒度会影响性能，相比于2PL，事务不用阻塞等，like snap isolation，写不会阻塞读，读不会阻塞写，适合读多的应用。对于写的应用，也不限于单CPU核心，FoundationDB，采用SSI，应用到分布式，吞吐很高。SSI期望读写事务都比较短，但相比于2PL要求没那么高，性能上线可以预期。
## The Trouble with Distributed Systems
### Faults and Partial Failures
不确定性的部分失败导致了分布式系统的复杂性
### Cloud Computing and Supercomputing
### Detecting faults
网络出问题时，路由失败返回ICMP Destination Unreachable，或者进程crash，没有监听指定端口时，返回RST/FIN
### Timeouts and Unbounded delays
网络的拥堵有多方面，交换机有队列，cpu的处理也有队列，尤其在虚拟机环境，多个虚拟机用一个物理CPU。这些排队都会导致延迟。
### Synchronous Versus Asynchronous Networks
为什么不能在硬件上设计的使得网络有一个最大延迟，并且不会丢包呢？这样软件不久很好设计了么？（困难并没有转移吧，硬件依然有和软件相同的困难，而且有的环境还不需要这样大代价的硬件）电话网络是一个这样可信的网络，连接建立的时候就分出来了一部分给这个连接的带宽资源，这样通信的连接数目就会有限制。这种网络叫做同步网络，网络中没有队列。
#### Can we not simply make network delays predictable?
以太网IP是为了传输的数据量尽可能大而设计的，就像CPU分配给每个线程的时间片一样，是动态的，而不是固定的，都是为了处理的数据量最高，
### Unreliable Clocks
时间是不好精准测定的，两个请求到达同一台机器的顺序也是不好确定的
### Monotonic Versus Time-of-Day Clocks
* Time-of-day clocks
就是自1970.1.1开始的秒数，会变化，不同的机器会不同
* Monotonic clocks
稳定的测量一段时间，只会向前，用来统计执行时间。时间的绝对值并没有意义。可以改变该始终的计时频率
### Clock Synchronization and Accuracy
NTP服务器会有各种问题，闰秒问题，
### Relying on Synchronized Clocks
软件设计中要考虑到时间这个因素也是不可靠的
* Timestamps for ordering events
时间不同步会导致基于时间戳的操作处理顺序产生错误（比如last write win），解决方式通常是增加版本向量。采用logical clocks，自增的一个计数器，来控制时间的顺序。
* Clock readings have a confidence interval
读取的时间是有一个置信度的，GPS接收器，原子钟都是更精确的计时设备，google的spanner中采用了带有置信度的local clock，会返回最早和最晚时间，（基于这种不精确的时间，返回可以设计一个时间上可信的系统- -）
* Synchronized clocks for global snapshots
如何产生一个全局的自增事务ID？首先，如果时钟可信，可以利用时间戳，比如spanner，它在提交一个事务的时候会故意等一个时间片，从而配合上时间范围的置信区间，就可以明确两个事务的先后关系，为了让这个故意等待的时间片尽可能短，就要求返回的时间置信区间尽可能窄，每个数据中心都配置了GPS接收器或者原子钟，保证时间的同步在7ms以内
### Process Pauses
一个节点如何知道自己仍然是leader？采用lease租约(leader获得其他节点给的租约)。由于进程暂停（GC，虚拟机实例漂移，线程上下文切换，IO暂停），有可能刚验证过租约的代码通过后，后面真正执行时租约已经失效了。
* Response time guarantees
真正的实时系统要保证每一个请求有严格的响应时间，会设置一个上线，real time并不见得吞吐性能高，反而会更差，但是对于某些安全系统，嵌入式体统是必须的。
* Limiting the impact of garbage collection
把GC看成一个计划下的行为，当有节点要进行GC时，就不给他发请求，这样整个系统看起来就是不会GC的。用于要求低延迟的系统。简单的做法就是要full gc时就重启实例。
### Knowledge, Truth, and Lies
基于一定的假设，我们就能基于不稳定的系统构建一个可信的系统
### The Truth Is Defined by the Majority
一个节点是不能真实的判断自己的情况的（GC，断网），所以一个分布式系统也不能信任一个节点
#### The leader and the lock
一个leader可能不是leader了，但是他自己还相信自己是，就会出问题。对于lock，lease都有此问题。利用fencing技术可以解决。每次写操作带上token，或者说版本好，即使第一个node获取了lease后，被别的节点先写了，后续再写时由于token号比已经写入的token号小，于是就会被拒绝。
在ZK中，事务id zxid和版本id cversion可以当作这个fencing token
### Byzantine Faults
上述假设node is truth如果node会欺骗，那分布式系统的问题就更多了。这种就叫做拜占庭错误，比如航空系统中，由于辐射内存中的数据会变化。一个系统中由多个组织构成，有的想要欺骗其他人。比如P2P，bitcoin就是避免相信一个节点的数据。解决这个问题代价太大，一般不用考虑。程序中的bug导致的拜占庭错误，解决算法也帮助不了解决问题，因为一般算法大都要求有三分之二的节点是对的，而bug影响全部。
### System Model and Realityd
