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
3. Evolvability:Make it easy for engineers to make changes to the system in the future.
