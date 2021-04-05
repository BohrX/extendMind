# 传统io NIO的RandomAccessFile 写速度比较
#io 

传统 io 将内容写到内核的缓存区 NIO (NIO的RandomAccessFile) 会调用 fsync命令刷到硬盘。
- 传统的快，但是可能丢失数据
- NIO的慢，但是可靠安全
![[io写文件示意图.png]]

