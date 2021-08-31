# MVCC(多版本并发控制)
#数据库 #待学习 #并发控制

 MVCC 英文：multi-version concurrection control 意为：多版本并发控制
 
 而所谓 **MVCC 并发版本控制**，是靠 readView (事务视图) 来实现的。多个 readView 组成 undo log（回滚日志）see: https://www.cnblogs.com/AlmostWasteTime/p/11466520.html
 
 ## 数据并发问题场景：
 详见 [[1.1为何需要并发控制]]
 1. 读读
 	 不存在并发问题
 2. 读写
 	线程安全问题, 造成事务隔离性问题 脏读 幻读 不可重复读
 3. 写写
     线程安全问题, 更新丢失问题 ABA
	 
MVCC解决读写冲突的无锁并发控制 
解决脏读幻读不可重复读等事务隔离问题， **不能解决更新丢失问题？**
 	