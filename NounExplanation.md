# Noun Explanation  

## bps & Bps

- 比特率是指每秒传输的比特（bit）数，单位为bps（bit per second）也可表示为b/s。比特率越高，单位时间传输的数据量（位数）越大。  
- Bps：Byte per second
- Kbps：千比特每秒  
- Mbps：兆比特每秒  
- KBps：千字节每秒  
- MBps：兆字节每秒  

> 存储单位：TB、PB、EB、ZB、YB、DB、NB  

## RAID

- 独立磁盘冗余阵列：Redundant Array of Independent Disks  

## TPS & QPS

1. TPS：Transactions Per Second（每秒传输的事务处理个数），即服务器每秒处理的事务数。TPS包括一条消息入和一条消息出，加上一次用户数据库访问。（业务TPS = CAPS x 每个呼叫平均TPS）  
    - TPS是软件测试结果的测量单位。一个事务是指一个客户机向服务器发送请求然后服务器做出反应的过程。客户机在发送请求时开始计时，收到服务器响应后结束计时，一次来计算使用的时间和完成的事务个数  
    - 一般的，评价系统性能均以每秒钟完成的技术交易的数量来衡量。系统整体处理能力取决于处理能力最低模块的TPS值。  
2. QPS：Queries Per Second（每秒查询率），即一台服务器每秒能够响应的查询次数，是对一个特定的查询服务器在规定时间内所处理流量多少的衡量标准。在因特网上，作为域名系统服务器的机器性能经常用每秒查询率来衡量。
    - 对应fetches/sec，即每秒的响应请求数，也就是最大吞吐能力  
