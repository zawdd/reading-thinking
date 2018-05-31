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
## Replication
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
