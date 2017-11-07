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
## Storage and Retrieval
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
