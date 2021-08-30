文档： https://raft.github.io/
论文： https://web.stanford.edu/~ouster/cgi-bin/papers/raft-atc14
论文中文翻译： https://www.infoq.cn/article/raft-paper
博客： https://www.cnblogs.com/xybaby/p/10124083.html


## 前言
算法分解：
    * 领导选取
    * 日志复制
    * 安全性
    * 成员变化
减少状态

## 复制状态机

a+b永远可以推导得出c

一致性算法一般有以下特性：
1. 确保安全性（从来不会返回一个错误的结果）
2. 高可用性：只有有大多数机器存活，就是可用的
3. 不依赖时序保证一致性
4. 通常情况下，一条命令 能够尽可能快的在大多数节点对一轮rpc调用作出相应时完成

## 5. raft一致性算法

### 5-2 图表
#### 5-2 状态
1. 在所有节点中都持久化状态：更新stable storage在响应rpc之前
    * currentTerm： server收到的最近的term，初始化为0
    * votedFor： 在本轮term中收到的candidateId
    * log[]: logEntries，每个entry包含以下内容
      * command：用于更新state machine
      * term： leader在收到命令时的情况 
      * index： 从1开始

2. 可变化的状态 volatile state
   * commitIndex： 
   * lastApplied： 
3. leader上可变化的状态
   * nextIndex[]: 每个server对应的下一个log entry，初始化为leader的last log index+1
   * matchIndex[]: 每个server中最高的已经replicated的log entry index




