#mybatis相关
	概念：是一个封装JDBC的持久层框架，它和Hibernate都属于ORM框架，其实不完全的ORM框架
	mybatis让程序员只关注SQL语句本身，而不用去关注创建连接、statement等操作。
	ORM：对象-关系映射   传入参数和查询结果需要对象与数据库数据间的映射

##JDBC八个步骤：
	加载数据库驱动Class.forName;通过驱动管理类获取连接;获取预处理statement;创建SQL语句；
	传入SQL参数;执行sql语句获取结果;遍历查询结果集;释放资源
##mybatis简化JDBC：
	（1）创建连接   全局配置文件
	（2）执行statement  映射文件 
	（3）频繁的开启和关闭数据库，造成性能下降   全局配置文件，数据库连接池
##工作步骤（原理）：
	1）配置文件   全局配置文件：配置数据源、事务等运行时信息      映射文件：执行sataement语句，包括sql语句、参数、结果等
	2）SqlsessionFactory  会话工厂  负责生产会话
	3）Sqlsession  会话   通过该会话对数据库进行增删改查
	4）Executor 执行器  sqlsession通过excutor来真正操作数据库
	5）mapperStatement 


##mapper映射文件
	1）xml头信息  从官方文档获取
	2）<mapper namespace=""></mapper>   namespace  id  parameterType  ResultType  Resultmap
	3）基础语法  select insert update  delete selectkey：select LAST_INSERT_ID 获取自增主键
	4）动态拼接SQL   常用：if   where  SQL   foreach

#redis相关
##redis基础介绍
	1）NOSQL：为了解决高并发、高可用、高可扩展，大数据存储等一系列问题的解决方案，即非关系型数据库。
		Not only SQL 不能取代关系型数据库，是对SQL的良好补充。
	2）NOSQL分类：①Key-Value存储数据库 如 redis ，用于内容缓存，用于处理高并发访问负载；
				  ②列存储数据库  如Hbase
				  ③文档型数据库  如MongoDB
				  ④图形数据库   
	3）redis：是使用C语言开发的高性能键值存储数据库。键值类型：String字符类型、Hash类型、List类型、Set类型、Sorted类型。
	4）redis应用：主要用于缓存、分布式集群架构中的session分离。

##redis操作
	1）单实例连接   jedis（IP,ort）  
	2）数据库连接池连接  jedispool（ip,port）  jedis = jedispool.getsource();
	3）Spring-redis配置文件整合

##redis持久化方案
	1）RDB：RDB持久化是指在指定时间间隔内将内存数据集快照写入磁盘，就是将数据集写入临时文件，写入成功后，再替换之前的文件。
		问题：非法关闭会丢失数据；当数据集过大时，持久化会影响服务器。
	2）AOF：AOF持久化以日志的形式记录服务器处理的每一个增删改操作，以文本方式记录，追加到文本。同步持久或异步持久
			每操作一次redis，就将记录存储到AOF持久化文件中。
		问题：追加方式同步或异步持久化会影响一定的性能;恢复大数据集的速度稍慢;
	
##redis主从复制
	1）原因：redis的持久化解决了服务器重启也不会丢失数据，但是服务器硬盘故障则会丢失数据，redis主从复制则会解决单点故障问题
	2）主机发生增删改查操作，从机会将数据进行同步，且从机不支持写操作
##redis集群
	1）所有的redis节点之间彼此互连（通过ping-pong机制），节点fail是通过集群中半数以上节点检测时才生效
	2）集群管理通过ruby脚本语言编写的
	3）配置集群  jedis连接集群
>
